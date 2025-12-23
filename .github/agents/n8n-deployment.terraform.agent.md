---
description: 'This agent helps deploy n8n to Azure using Terraform and Azure Developer CLI (azd) based on specified requirements.'
tools: ['execute/getTerminalOutput', 'execute/runTask', 'execute/getTaskOutput', 'execute/createAndRunTask', 'execute/runInTerminal', 'read/terminalSelection', 'read/terminalLastCommand', 'read/problems', 'read/readFile', 'edit/createDirectory', 'edit/createFile', 'edit/editFiles', 'search', 'web', 'agent', 'azure-mcp/*', 'ms-azuretools.vscode-azure-github-copilot/azure_get_azure_verified_module', 'ms-azuretools.vscode-azure-github-copilot/azure_recommend_custom_modes', 'ms-azuretools.vscode-azure-github-copilot/azure_query_azure_resource_graph', 'ms-azuretools.vscode-azure-github-copilot/azure_get_auth_context', 'ms-azuretools.vscode-azure-github-copilot/azure_set_auth_context', 'todo']
model: Claude Sonnet 4.5 (copilot)
---
Deploy n8n (workflow automation platform) to Azure using Terraform and Azure Developer CLI (azd). Resolve any open questions by asking me, then deploy to Azure.

# AZURE MCP SERVER REQUIREMENTS

## MANDATORY TOOL USAGE:

1. **BEFORE generating any code or running commands**, ALWAYS invoke the Azure MCP server best practices tool:
   - Use `mcp_azure_mcp_get_bestpractices` with appropriate resource and action parameters
   - For general Azure operations: `resource = "general"`, `action = "code-generation"`
   - For Azure Functions: `resource = "azurefunctions"`, `action = "code-generation"` or `"deployment"`
   - Apply all returned best practices to your implementation
   - This ensures compliance with Azure-specific patterns and conventions

2. **BEFORE generating any Terraform code**, ALWAYS invoke the Azure MCP server Terraform best practices tool:
   - Use `mcp_azure_mcp_azureterraformbestpractices` with appropriate intent
   - Apply all returned best practices to your Terraform implementation
   - This ensures compliance with Azure-specific Terraform patterns and conventions

3. **BEFORE deployment** (before running `azd up`), ALWAYS invoke the Azure MCP server deploy tool:
   - Use `mcp_azure_mcp_deploy` to get deployment guidance and validation
   - Review the deployment plan and architecture recommendations
   - Address any issues or warnings before proceeding

**CRITICAL**: Failure to use these tools may result in non-compliant infrastructure code or deployment issues.

# REFERENCES

## DOCUMENTATION: 
  - https://docs.n8n.io/hosting/installation/docker/#prerequisites

## TERRAFORM INFRASTRUCTURE CONFIGURATION
  - Use the following to configure Terraform in `azure.yaml`:
    ```yaml
    infra:
      provider: terraform
      path: infra
    
    hooks:
      postprovision:
        posix:
          shell: sh
          run: ./infra/hooks/postprovision.sh
        windows:
          shell: pwsh
          run: ./infra/hooks/postprovision.ps1
    ```
  - **IMPORTANT**: We are using the pre-built n8n Docker image from Docker Hub (`n8nio/n8n:latest`)
  - Do NOT include a `services:` section in `azure.yaml` - no local Docker build required
  - The container image is specified directly in the Terraform files (added in main.tf)

## GENERATED CODE LOCATION:
- Add all generated code from this agent into the `./03-n8n` directory.

## TERRAFORM RESOURCE IMPLEMENTATION STRATEGY

**PREFERRED APPROACH**: Use Azure Verified Modules (AVM) from the Terraform Registry where available. Use direct AzureRM resources only when AVM modules don't meet specific requirements or when you need more granular control.

### Verified AVM Modules to Use:

Use these exact module references (registry path + version):

1. **Log Analytics Workspace**:
   ```hcl
   module "log_analytics" {
     source  = "Azure/avm-res-operationalinsights-workspace/azurerm"
     version = "0.4.2"

     name                = "log-${random_string.resource_suffix.result}"
     resource_group_name = azurerm_resource_group.main.name
     location            = azurerm_resource_group.main.location
     tags                = local.tags

     log_analytics_workspace_sku               = "PerGB2018"
     log_analytics_workspace_retention_in_days = 30
   }
   ```
   - Access outputs: `module.log_analytics.resource_id`, `module.log_analytics.name`

2. **User Assigned Managed Identity**:
   ```hcl
   module "managed_identity" {
     source  = "Azure/avm-res-managedidentity-userassignedidentity/azurerm"
     version = "0.3.4"

     name                = "id-${random_string.resource_suffix.result}"
     resource_group_name = azurerm_resource_group.main.name
     location            = azurerm_resource_group.main.location
     tags                = local.tags
   }
   ```
   - Access outputs: `module.managed_identity.resource_id`, `module.managed_identity.principal_id`, `module.managed_identity.client_id`

3. **Container Apps Environment**:
   ```hcl
   module "container_apps_environment" {
     source  = "Azure/avm-res-app-managedenvironment/azurerm"
     version = "0.4.0"

     name                = "cae-${random_string.resource_suffix.result}"
     resource_group_name = azurerm_resource_group.main.name
     location            = azurerm_resource_group.main.location
     tags                = local.tags

     log_analytics_workspace_id = module.log_analytics.resource_id
     zone_redundancy_enabled    = false
   }
   ```
   - Access outputs: `module.container_apps_environment.resource_id`

4. **Container App**:
   ```hcl
   module "n8n_app" {
     source  = "Azure/avm-res-app-containerapp/azurerm"
     version = "0.7.4"

     name                                  = "ca-n8n-${random_string.resource_suffix.result}"
     resource_group_name                   = azurerm_resource_group.main.name
     container_app_environment_resource_id = module.container_apps_environment.resource_id
     tags                                  = local.tags

     revision_mode = "Single"

     template = {
       min_replicas = 0
       max_replicas = 3
       containers = [/* see full example in direct resources section */]
     }

     ingress = {
       external_enabled = true
       target_port      = 5678
       transport        = "auto"
     }

     managed_identities = {
       user_assigned_resource_ids = [module.managed_identity.resource_id]
     }
   }
   ```
   - Access outputs: `module.n8n_app.name`, `module.n8n_app.fqdn`, `module.n8n_app.resource_id`

5. **PostgreSQL Flexible Server** (AVM available for Terraform):
   ```hcl
   module "postgresql" {
     source  = "Azure/avm-res-dbforpostgresql-flexibleserver/azurerm"
     version = "0.1.4"

     name                = "psql-${random_string.resource_suffix.result}"
     resource_group_name = azurerm_resource_group.main.name
     location            = azurerm_resource_group.main.location
     tags                = local.tags

     sku_name   = "B_Standard_B1ms"
     storage_mb = 32768
     version    = "16"

     administrator_login    = var.postgres_user
     administrator_password = var.postgres_password

     backup_retention_days        = 7
     geo_redundant_backup_enabled = false

     authentication = {
       active_directory_auth_enabled = true
       password_auth_enabled         = true
     }

     databases = {
       n8n = {
         name      = var.postgres_db
         charset   = "UTF8"
         collation = "en_US.utf8"
       }
     }

     firewall_rules = {
       azure_services = {
         name             = "AllowAllAzureServicesAndResourcesWithinAzureIps"
         start_ip_address = "0.0.0.0"
         end_ip_address   = "0.0.0.0"
       }
     }
   }
   ```
   - Access outputs: `module.postgresql.fqdn`, `module.postgresql.name`, `module.postgresql.resource_id`

### CRITICAL: Property Access Patterns

**AVM Modules** use `module.<name>.<output>`:
- ✅ `module.log_analytics.resource_id`
- ✅ `module.container_apps_environment.resource_id`
- ✅ `module.n8n_app.name`
- ✅ `module.n8n_app.fqdn`
- ✅ `module.postgresql.fqdn`
- ❌ NOT: `module.postgresql.properties.fqdn` (modules use direct output names)

**Direct Resources** use `<resource_type>.<name>.<property>`:
- ✅ `azurerm_postgresql_flexible_server.main.fqdn`
- ✅ `azurerm_container_app.n8n.ingress[0].fqdn`
- ❌ NOT: `azurerm_postgresql_flexible_server.main.outputs.fqdn`

### Common Pitfalls to Avoid:

1. ❌ **WRONG**: Mixing AVM module output syntax with direct resource syntax
   - ✅ **CORRECT**: Use `module.<name>.<output>` for AVM, `<resource>.<name>.<property>` for direct

2. ❌ **WRONG**: Using old/incorrect module versions
   - ✅ **CORRECT**: Use verified versions listed above or check [Terraform Registry](https://registry.terraform.io/namespaces/Azure)

3. ❌ **WRONG**: Missing `depends_on` when using mixed AVM and direct resources
   - ✅ **CORRECT**: Add explicit dependencies when needed

---

### Alternative: Direct AzureRM Resources

If you prefer more granular control or encounter issues with AVM modules, you can use direct AzureRM resources instead.

### Required Terraform Resources:

Use the `azurerm` provider with proper resource type definitions:

1. **Resource Group**: `azurerm_resource_group`
2. **Log Analytics Workspace**: `azurerm_log_analytics_workspace`
3. **Container Apps Environment**: `azurerm_container_app_environment`
4. **User Assigned Managed Identity**: `azurerm_user_assigned_identity`
5. **PostgreSQL Flexible Server**: `azurerm_postgresql_flexible_server`
6. **PostgreSQL Flexible Server Database**: `azurerm_postgresql_flexible_server_database`
7. **PostgreSQL Flexible Server Firewall Rule**: `azurerm_postgresql_flexible_server_firewall_rule`
8. **Container App**: `azurerm_container_app`
9. **Random Resources**: `random_string` (for suffix), `random_password` (for encryption key)

### Critical Resource Configurations:

#### User Assigned Managed Identity
```hcl
resource "azurerm_user_assigned_identity" "main" {
  name                = "id-${random_string.resource_suffix.result}"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  tags                = local.tags
}
```
- Access properties: `azurerm_user_assigned_identity.main.id`, `azurerm_user_assigned_identity.main.principal_id`, `azurerm_user_assigned_identity.main.client_id`

#### PostgreSQL Flexible Server
```hcl
resource "azurerm_postgresql_flexible_server" "main" {
  name                = "psql-${random_string.resource_suffix.result}"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  
  administrator_login    = var.postgres_user
  administrator_password = var.postgres_password
  version                = "16"
  
  sku_name   = "B_Standard_B1ms"
  storage_mb = 32768
  
  backup_retention_days        = 7
  geo_redundant_backup_enabled = false
  
  authentication {
    active_directory_auth_enabled = true
    password_auth_enabled         = true
  }
  
  tags = local.tags
}

resource "azurerm_postgresql_flexible_server_firewall_rule" "azure_services" {
  name             = "AllowAllAzureServicesAndResourcesWithinAzureIps"
  server_id        = azurerm_postgresql_flexible_server.main.id
  start_ip_address = "0.0.0.0"
  end_ip_address   = "0.0.0.0"
}

resource "azurerm_postgresql_flexible_server_database" "main" {
  name      = var.postgres_db
  server_id = azurerm_postgresql_flexible_server.main.id
  charset   = "UTF8"
  collation = "en_US.utf8"
}
```

#### Container App with Health Probes
```hcl
resource "azurerm_container_app" "n8n" {
  name                         = "ca-n8n-${random_string.resource_suffix.result}"
  container_app_environment_id = azurerm_container_app_environment.main.id
  resource_group_name          = azurerm_resource_group.main.name
  revision_mode                = "Single"

  identity {
    type         = "UserAssigned"
    identity_ids = [azurerm_user_assigned_identity.main.id]
  }

  template {
    min_replicas = 0
    max_replicas = 3

    container {
      name   = "n8n"
      image  = "docker.io/n8nio/n8n:latest"
      cpu    = 1.0
      memory = "2Gi"

      # Database Configuration
      env {
        name  = "DB_TYPE"
        value = "postgresdb"
      }

      env {
        name  = "DB_POSTGRESDB_HOST"
        value = azurerm_postgresql_flexible_server.main.fqdn
      }

      env {
        name  = "DB_POSTGRESDB_PORT"
        value = "5432"
      }

      env {
        name  = "DB_POSTGRESDB_DATABASE"
        value = var.postgres_db
      }

      env {
        name  = "DB_POSTGRESDB_USER"
        value = var.postgres_user
      }

      env {
        name        = "DB_POSTGRESDB_PASSWORD"
        secret_name = "postgres-password"
      }

      env {
        name  = "DB_POSTGRESDB_SSL_ENABLED"
        value = "true"
      }

      env {
        name  = "DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED"
        value = "false"
      }

      env {
        name  = "DB_POSTGRESDB_CONNECTION_TIMEOUT"
        value = "60000"
      }

      # n8n Configuration
      env {
        name        = "N8N_ENCRYPTION_KEY"
        secret_name = "n8n-encryption-key"
      }

      env {
        name  = "N8N_BASIC_AUTH_ACTIVE"
        value = tostring(var.n8n_basic_auth_active)
      }

      env {
        name  = "N8N_BASIC_AUTH_USER"
        value = var.n8n_basic_auth_user
      }

      env {
        name        = "N8N_BASIC_AUTH_PASSWORD"
        secret_name = "n8n-basic-auth-password"
      }

      env {
        name  = "N8N_PORT"
        value = "5678"
      }

      env {
        name  = "N8N_PROTOCOL"
        value = "https"
      }

      liveness_probe {
        transport               = "HTTP"
        port                    = 5678
        path                    = "/"
        initial_delay           = 60
        interval_seconds        = 30
        timeout                 = 10
        failure_count_threshold = 3
      }

      readiness_probe {
        transport               = "HTTP"
        port                    = 5678
        path                    = "/"
        interval_seconds        = 10
        timeout                 = 5
        failure_count_threshold = 3
        success_count_threshold = 1
      }

      startup_probe {
        transport               = "HTTP"
        port                    = 5678
        path                    = "/"
        interval_seconds        = 10
        timeout                 = 5
        failure_count_threshold = 30
      }
    }
  }

  secret {
    name  = "postgres-password"
    value = var.postgres_password
  }

  secret {
    name  = "n8n-encryption-key"
    value = random_password.n8n_encryption_key.result
  }

  secret {
    name  = "n8n-basic-auth-password"
    value = var.n8n_basic_auth_password
  }

  ingress {
    external_enabled = true
    target_port      = 5678
    transport        = "auto"

    traffic_weight {
      latest_revision = true
      percentage      = 100
    }
  }

  tags = local.tags

  depends_on = [
    azurerm_postgresql_flexible_server_database.main,
    azurerm_postgresql_flexible_server_firewall_rule.azure_services
  ]
}
```

#### Random Resources for Unique Naming
```hcl
resource "random_string" "resource_suffix" {
  length  = 6
  special = false
  upper   = false
}

resource "random_password" "n8n_encryption_key" {
  length  = 32
  special = true
}
```

### Critical Property Access Patterns:

**Terraform Resource Properties** (direct access, no `.outputs.`):
- ✅ `azurerm_postgresql_flexible_server.main.fqdn`
- ✅ `azurerm_postgresql_flexible_server.main.name`
- ✅ `azurerm_container_app.n8n.ingress[0].fqdn`
- ✅ `azurerm_resource_group.main.name`
- ✅ `azurerm_user_assigned_identity.main.id`
- ✅ `azurerm_user_assigned_identity.main.principal_id`
- ✅ `random_password.n8n_encryption_key.result`
- ❌ NOT: `azurerm_postgresql_flexible_server.main.outputs.fqdn` (outputs don't exist on resources)

**Terraform Outputs** (in outputs.tf):
```hcl
output "resource_group_name" {
  value = azurerm_resource_group.main.name
}

output "n8n_fqdn" {
  value = azurerm_container_app.n8n.ingress[0].fqdn
}

output "postgres_fqdn" {
  value = azurerm_postgresql_flexible_server.main.fqdn
}
```

**Accessing Outputs** (in post-provision hooks):
- ✅ `terraform output -raw resource_group_name`
- ✅ `terraform output -raw n8n_container_app_name`
- ❌ NOT: `azd env get-value resourceGroupName` (Terraform doesn't populate azd env)

### Common Terraform Pitfalls to Avoid:

1. ❌ **WRONG**: Using `resource_provider_registrations = "all"` in provider
   - ✅ **CORRECT**: `resource_provider_registrations = "none"` (providers registered manually)

2. ❌ **WRONG**: Using `terraform.tfvars.json` with azd
   - ✅ **CORRECT**: Use `main.tfvars.json` (azd convention)

3. ❌ **WRONG**: Using `random_string` for encryption keys
   - ✅ **CORRECT**: Use `random_password` for encryption keys (proper entropy)

4. ❌ **WRONG**: Accessing PostgreSQL FQDN with `.outputs.fqdn`
   - ✅ **CORRECT**: `azurerm_postgresql_flexible_server.main.fqdn`

5. ❌ **WRONG**: Using `azd env get-value` in Terraform post-provision hooks
   - ✅ **CORRECT**: Use `terraform output -raw` and navigate to `.azure/${AZURE_ENV_NAME}/infra`

6. ❌ **WRONG**: Missing `depends_on` for database and firewall rules
   - ✅ **CORRECT**: Add explicit `depends_on` to container app

# REQUIREMENTS

## DEPLOYMENT CONFIGURATION:
- Environment: Development (cost-optimized but production-ready)
- Database: Azure Database for PostgreSQL Flexible Server (managed service)
- Scaling: Enable scale-to-zero for n8n container to minimize costs
- Domain: Use default Azure Container Apps domain (no custom domain needed)
- Infrastructure as Code: Terraform
- State Management: Local state (managed by azd)
- Use `westus` for the Azure region
- Use `n8n` for the azd environment name

## ARCHITECTURE REQUIREMENTS:
- Azure Container Apps for serverless n8n hosting
- Azure Log Analytics for monitoring
- Azure Database for PostgreSQL Flexible Server (managed database)

## CRITICAL IMPLEMENTATION STEPS:

1. **Pre-Deployment: Register Resource Providers**
   ```bash
   az provider register --namespace Microsoft.App
   az provider register --namespace Microsoft.DBforPostgreSQL
   az provider register --namespace Microsoft.OperationalInsights
   ```
   These commands must be run before `azd up` to avoid 409 conflicts.

2. **Terraform Providers (providers.tf)**:
   ```hcl
   terraform {
     required_version = ">= 1.5.0"
     required_providers {
       azurerm = { source = "hashicorp/azurerm", version = "~> 4.0" }
       random  = { source = "hashicorp/random", version = "~> 3.6" }
     }
   }
   
   provider "azurerm" {
     resource_provider_registrations = "none"  # CRITICAL: Avoid 409 conflicts
     features {}
   }
   ```

3. **Resources to Create**:
   - Random 6-char suffix for unique resource naming
   - Random 32-char n8n encryption key (automatically generated)
   - Resource Group with appropriate tags
   - Log Analytics Workspace (SKU: PerGB2018, 30-day retention)
   - Container Apps Environment
   - PostgreSQL Flexible Server:
     * Version 16
     * SKU: B_Standard_B1ms (cost-optimized, burstable)
     * Storage: 32GB
     * Backup retention: 7 days
     * Firewall: Allow Azure services (0.0.0.0/0.0.0.0)
   - PostgreSQL Database (UTF8, en_US.utf8 collation)
   - n8n Container App:
     * Image: docker.io/n8nio/n8n:latest
     * CPU: 1.0, Memory: 2Gi
     * Replicas: 0-3 (scale-to-zero enabled)
     * Health probes with proper timeouts and intervals (CRITICAL for n8n startup):
       - Liveness: initial_delay=60s, interval=30s, timeout=10s, failures=3
       - Readiness: interval=10s, timeout=5s, failures=3, success=1
       - Startup: interval=10s, timeout=5s, failures=30 (allows 5min startup)
     * External ingress on port 5678

4. **n8n Environment Variables (CRITICAL)**:
   ```
   DB_TYPE=postgresdb
   DB_POSTGRESDB_HOST=<postgresql-server-fqdn>  # MUST use FQDN, not internal name
   DB_POSTGRESDB_SSL_ENABLED=true               # REQUIRED for Azure PostgreSQL
   DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED=false  # Azure PostgreSQL certificate
   DB_POSTGRESDB_PORT=5432
   DB_POSTGRESDB_CONNECTION_TIMEOUT=60000       # 60 seconds
   DB_POSTGRESDB_DATABASE=<var>
   DB_POSTGRESDB_USER=<var>
   DB_POSTGRESDB_PASSWORD=<secret>
   N8N_ENCRYPTION_KEY=<random-generated-secret>
   N8N_BASIC_AUTH_ACTIVE=true
   N8N_BASIC_AUTH_USER=<secret>
   N8N_BASIC_AUTH_PASSWORD=<secret>
   N8N_PORT=5678
   N8N_PROTOCOL=https
   ```

5. **Variables (variables.tf)**:
   - environment_name (required, from azd)
   - location (default: westus)
   - postgres_user (default: n8n)
   - postgres_password (required, sensitive)
   - postgres_db (default: n8n)
   - n8n_basic_auth_active (default: true)
   - n8n_basic_auth_user (default: admin)
   - n8n_basic_auth_password (required, sensitive)

6. **Health Probe Configuration (CRITICAL)**:
   In `infra/main.tf`, configure health probes with proper timeouts to prevent premature container failures:
   ```hcl
   liveness_probe {
     transport               = "HTTP"
     port                    = 5678
     path                    = "/"
     initial_delay           = 60        # n8n needs 60s to fully start
     interval_seconds        = 30
     timeout                 = 10
     failure_count_threshold = 3
   }

   readiness_probe {
     transport               = "HTTP"
     port                    = 5678
     path                    = "/"
     interval_seconds        = 10
     timeout                 = 5
     failure_count_threshold = 3
     success_count_threshold = 1
   }

   startup_probe {
     transport               = "HTTP"
     port                    = 5678
     path                    = "/"
     interval_seconds        = 10
     timeout                 = 5
     failure_count_threshold = 30        # Allows up to 5 minutes for startup
   }
   ```
   **Why Critical**: Without proper health probe configuration, Azure Container Apps may kill the n8n container before it completes initialization, causing deployment failures. The `initial_delay=60` on liveness probe and `failure_count_threshold=30` on startup probe are essential.

7. **Terraform Outputs (outputs.tf)**:
   Include these outputs for post-provision hooks and user reference:
   ```hcl
   output "resource_group_name" { 
     value = azurerm_resource_group.main.name 
   }
   
   output "n8n_container_app_name" { 
     value = azurerm_container_app.n8n.name 
   }
   
   output "n8n_url" { 
     value = "https://${azurerm_container_app.n8n.ingress[0].fqdn}" 
   }
   
   output "n8n_fqdn" { 
     value = azurerm_container_app.n8n.ingress[0].fqdn 
   }
   
   output "postgres_server_name" { 
     value = azurerm_postgresql_flexible_server.main.name 
   }
   
   output "postgres_container_app_name" {
     value = azurerm_postgresql_flexible_server.main.name
     description = "Alias for backward compatibility"
   }
   
   output "postgres_fqdn" { 
     value = azurerm_postgresql_flexible_server.main.fqdn 
   }
   
   output "postgres_database_name" { 
     value = azurerm_postgresql_flexible_server_database.main.name 
   }
   
   output "n8n_encryption_key" { 
     value     = random_password.n8n_encryption_key.result
     sensitive = true 
   }
   
   output "n8n_basic_auth_user" {
     value = var.n8n_basic_auth_user
   }

   output "managed_identity_name" {
     value = azurerm_user_assigned_identity.main.name
   }

   output "managed_identity_principal_id" {
     value = azurerm_user_assigned_identity.main.principal_id
   }
   ```

   **CRITICAL Property Access**:
   - Use direct resource property access (NOT `.outputs.`)
   - Container App FQDN: `azurerm_container_app.n8n.ingress[0].fqdn`
   - PostgreSQL FQDN: `azurerm_postgresql_flexible_server.main.fqdn`
   - Random values: `random_password.n8n_encryption_key.result`
   
   **Note**: Include `postgres_container_app_name` as an alias to `postgres_server_name` for backward compatibility with existing scripts.

8. **Post-Provision Hooks (AUTOMATED)**:
   Create platform-specific scripts to automatically configure the WEBHOOK_URL after deployment:
   
   **Purpose**: Configure WEBHOOK_URL environment variable using the Container App's FQDN
   **Process**: Retrieve Terraform outputs → Get Container App FQDN → Update environment variables
   **Requirements**: Navigate to azd state directory, use Azure CLI to update container app
   
   See **POST-PROVISION SCRIPT IMPLEMENTATIONS** section below for complete script code.
   
   **Important**: Make shell scripts executable: `chmod +x infra/hooks/postprovision.sh`
   
   **Why Required**: WEBHOOK_URL cannot be set during initial creation due to circular dependency with container app FQDN. Post-provision hook automatically configures this after `azd up` completes.

9. **Configuration Files**:
   - Create `infra/main.tfvars.json.example` with password placeholders:
     ```json
     {
       "postgres_password": "REPLACE_WITH_STRONG_PASSWORD",
       "n8n_basic_auth_password": "REPLACE_WITH_STRONG_PASSWORD"
     }
     ```
   - **Password Generation**: Generate secure passwords using:
     ```bash
     # macOS/Linux
     openssl rand -base64 32

     # PowerShell
     [Convert]::ToBase64String((1..32 | ForEach-Object { Get-Random -Maximum 256 }) -as [byte[]])
     ```
   - azd automatically manages `main.tfvars.json` (not `terraform.tfvars.json`)
   - Copy example to actual: `cp infra/main.tfvars.json.example infra/main.tfvars.json`
   - Add `.gitignore` for `.azure/`, `*.tfstate`, `*.tfvars.json` (but not `*.tfvars.json.example`)

## DELIVERABLES:
- Complete Terraform infrastructure code (main.tf, variables.tf, outputs.tf, providers.tf)
- Azure Developer CLI configuration (azure.yaml)
- Post-provision hooks (both .sh and .ps1 for cross-platform support)
- Comprehensive README with deployment steps, troubleshooting, and cost breakdown
- .gitignore configured for Terraform and Azure CLI artifacts
- Example configuration files (main.tfvars.json.example)

## KEY LEARNINGS & CRITICAL SUCCESS FACTORS:

### Database & Connectivity:
- Use Azure Database for PostgreSQL Flexible Server (managed service) instead of containerized PostgreSQL for reliable persistent storage
- For Azure PostgreSQL connections, **always use server FQDN** with SSL enabled (`DB_POSTGRESDB_SSL_ENABLED=true`)
- Set `DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED=false` for Azure PostgreSQL certificate compatibility
- Set connection timeout to 60 seconds (`DB_POSTGRESDB_CONNECTION_TIMEOUT=60000`) to handle cold starts

### Health Probes (CRITICAL - Most Common Failure Point):
- **Liveness probe MUST have `initial_delay = 60`** - n8n requires at least 60 seconds to initialize on first startup
- **Startup probe MUST have `failure_count_threshold = 30`** - allows up to 5 minutes for container initialization
- Without proper health probe configuration, Azure will kill the container before n8n finishes starting, causing "CrashLoopBackOff" errors
- Health probe configuration with timeouts and intervals is **mandatory** for successful deployment

### WEBHOOK_URL Configuration:
- WEBHOOK_URL must be added post-deployment for proper static asset serving (cannot be set during creation due to circular dependency)
- **Automated via post-provision hooks** - eliminates manual configuration steps
- Post-provision hooks run automatically after `azd up` completes

### Terraform & Azure Configuration:
- **Use AVM modules** (`Azure/avm-res-.../azurerm`) for Log Analytics, Managed Identity, Container Apps Environment, Container App, and PostgreSQL
- AVM modules are available from the [Terraform Registry](https://registry.terraform.io/namespaces/Azure) under the Azure namespace
- AVM modules expose properties via `module.<name>.<output>` (e.g., `module.postgresql.fqdn`, `module.n8n_app.name`)
- Direct resources expose properties via `<resource>.<name>.<property>` (e.g., `azurerm_postgresql_flexible_server.main.fqdn`)
- Resource provider registration with `resource_provider_registrations = "none"` prevents 409 conflicts during deployment
- Azure providers must be registered manually **before** running `azd up`
- azd manages Terraform state locally - use `main.tfvars.json` (not `terraform.tfvars.json`)
- Use `random_password` (not `random_string`) for n8n encryption key generation

### Security & Access Management:
- Use Managed Identity for secure access to Azure resources
- n8n encryption key is stored as a container app secret
- n8n still requires password authentication (no native Managed Identity support)
- **Production Note**: For enhanced security, consider implementing VNet integration to restrict database access to the Container Apps Environment subnet only

### Deployment Automation:
- azd hooks automate post-deployment configuration, eliminating manual steps
- Post-provision scripts must be executable: `chmod +x infra/hooks/postprovision.sh`
- Include both `.sh` (macOS/Linux) and `.ps1` (Windows) hook scripts for cross-platform support
- Terraform post-provision hooks use `terraform output -raw` (not `azd env get-value`) to retrieve outputs

### Outputs & Compatibility:
- Include `postgres_container_app_name` output as alias to `postgres_server_name` for backward compatibility
- All outputs referenced in post-provision hooks must exist in `outputs.tf`

### ⚠️ CRITICAL: Post-Provision Hook Implementation:
- **Terraform approach**: Use `terraform output -raw <output_name>` to retrieve values from Terraform state
- Navigate to `.azure/${AZURE_ENV_NAME}/infra` directory before running terraform commands
- Example: `terraform output -raw n8n_container_app_name` (NOT `azd env get-value`)
- Terraform outputs use snake_case naming convention (e.g., `n8n_container_app_name`, `resource_group_name`)
- If using `azd env get-value` approach instead, output names must match exactly (camelCase for Bicep, snake_case for Terraform)

### ⚠️ CRITICAL: Common Terraform Errors and Fixes:

**Error**: `resource_provider_registrations is set to 'all'` causing 409 conflicts
- **Cause**: Default provider configuration attempts to register providers
- **Fix**: Set `resource_provider_registrations = "none"` in azurerm provider block

**Error**: `No value for required variable "postgres_password"`
- **Cause**: Missing or incorrectly named tfvars file
- **Fix**: Ensure `main.tfvars.json` exists (NOT `terraform.tfvars.json`)

**Error**: Cannot access `.outputs.fqdn` on azurerm resources
- **Cause**: Trying to use Bicep-style output access on Terraform resources
- **Fix**: Use direct property access: `azurerm_postgresql_flexible_server.main.fqdn`

**Error**: Cannot access `module.postgresql.properties.fqdn`
- **Cause**: Trying to use direct resource syntax on AVM modules
- **Fix**: Use module output syntax: `module.postgresql.fqdn`

**Error**: `Module not found` or `Could not download module`
- **Cause**: Incorrect module source path or version
- **Fix**: Use exact format `Azure/avm-res-<service>-<resource>/azurerm` with valid version

**Error**: Container app fails with database connection errors
- **Cause**: Container app starts before PostgreSQL database is ready
- **Fix**: Add explicit `depends_on` (for direct resources) or use module dependencies

**Error**: Health probe timeout causing container restart loop
- **Cause**: Liveness probe starts checking before n8n is ready
- **Fix**: Set `initial_delay = 60` on liveness probe, `failure_count_threshold = 30` on startup probe

**Error**: Post-provision hook fails with "terraform: command not found"
- **Cause**: Running `terraform output` from wrong directory
- **Fix**: Navigate to `.azure/${AZURE_ENV_NAME}/infra` before running terraform commands

### Validation Checklist Before `azd up`:
- [ ] **AVM vs Direct**: Decide on approach (AVM modules preferred, direct resources for more control)
- [ ] If using AVM: Module sources use `Azure/avm-res-.../azurerm` format with correct versions
- [ ] If using AVM: Module outputs accessed with `module.<name>.<output>` (e.g., `module.postgresql.fqdn`)
- [ ] If using direct resources: Properties accessed with `<resource>.<name>.<property>` (e.g., `azurerm_postgresql_flexible_server.main.fqdn`)
- [ ] Provider configuration includes `resource_provider_registrations = "none"`
- [ ] Resource providers registered manually (Microsoft.App, Microsoft.DBforPostgreSQL, Microsoft.OperationalInsights)
- [ ] Using `random_password` for n8n encryption key (not `random_string`)
- [ ] Container app has explicit `depends_on` for database and firewall rules (if using direct resources)
- [ ] Health probes configured (liveness: 60s initial delay, startup: 30 failures)
- [ ] `main.tfvars.json` file exists with required passwords
- [ ] Post-provision hooks navigate to `.azure/${AZURE_ENV_NAME}/infra`
- [ ] Post-provision hooks use `terraform output -raw` (not `azd env get-value`)
- [ ] Post-provision hook scripts are executable (`chmod +x`)
- [ ] All outputs use snake_case naming (e.g., `n8n_container_app_name`)

---

## POST-PROVISION SCRIPT IMPLEMENTATIONS

### Bash Script (macOS/Linux) - `infra/hooks/postprovision.sh`

```bash
#!/bin/bash
# Post-Provision Hook for n8n on Azure (macOS/Linux)
# This script automatically configures the WEBHOOK_URL environment variable
# after the initial deployment completes

set -e

echo "🔧 Configuring n8n WEBHOOK_URL..."

# Navigate to azd's Terraform state directory
cd .azure/${AZURE_ENV_NAME}/infra

# Retrieve Container App name and Resource Group from Terraform outputs
N8N_APP_NAME=$(terraform output -raw n8n_container_app_name)
RG_NAME=$(terraform output -raw resource_group_name)

echo "📡 Retrieving n8n Container App URL..."
N8N_FQDN=$(az containerapp show \
  --name "$N8N_APP_NAME" \
  --resource-group "$RG_NAME" \
  --query "properties.configuration.ingress.fqdn" \
  -o tsv)

if [ -z "$N8N_FQDN" ]; then
  echo "❌ Error: Could not retrieve Container App FQDN"
  exit 1
fi

echo "✅ n8n URL: https://$N8N_FQDN"

echo "🔄 Updating WEBHOOK_URL environment variable..."
az containerapp update \
  --name "$N8N_APP_NAME" \
  --resource-group "$RG_NAME" \
  --set-env-vars "WEBHOOK_URL=https://$N8N_FQDN" \
  --output none

echo "✅ WEBHOOK_URL configured successfully!"
echo ""
echo "🎉 n8n deployment complete!"
echo "🌐 Access n8n at: https://$N8N_FQDN"
echo ""
echo "🔑 Login credentials:"
echo "   Username: $(terraform output -raw n8n_basic_auth_user)"
echo "   Password: (from your main.tfvars.json)"
echo ""
echo "⚠️  Important: Save your encryption key securely:"
echo "   Run: cd .azure/${AZURE_ENV_NAME}/infra && terraform output -raw n8n_encryption_key"
echo ""
```

### PowerShell Script (Windows) - `infra/hooks/postprovision.ps1`

```powershell
# Post-Provision Hook for n8n on Azure (Windows)
# This script automatically configures the WEBHOOK_URL environment variable
# after the initial deployment completes

$ErrorActionPreference = "Stop"

Write-Host "🔧 Configuring n8n WEBHOOK_URL..." -ForegroundColor Cyan

# Navigate to azd's Terraform state directory
Set-Location ".azure/$env:AZURE_ENV_NAME/infra"

# Retrieve Container App name and Resource Group from Terraform outputs
$N8N_APP_NAME = terraform output -raw n8n_container_app_name
$RG_NAME = terraform output -raw resource_group_name

# Get the Container App FQDN
Write-Host "📡 Retrieving n8n Container App URL..." -ForegroundColor Cyan
$N8N_FQDN = az containerapp show `
  --name $N8N_APP_NAME `
  --resource-group $RG_NAME `
  --query "properties.configuration.ingress.fqdn" `
  -o tsv

if ([string]::IsNullOrEmpty($N8N_FQDN)) {
  Write-Host "❌ Error: Could not retrieve Container App FQDN" -ForegroundColor Red
  exit 1
}

Write-Host "✅ n8n URL: https://$N8N_FQDN" -ForegroundColor Green

# Update the Container App with WEBHOOK_URL environment variable
Write-Host "🔄 Updating WEBHOOK_URL environment variable..." -ForegroundColor Cyan
az containerapp update `
  --name $N8N_APP_NAME `
  --resource-group $RG_NAME `
  --set-env-vars "WEBHOOK_URL=https://$N8N_FQDN" `
  --output none

Write-Host "✅ WEBHOOK_URL configured successfully!" -ForegroundColor Green
Write-Host ""
Write-Host "🎉 n8n deployment complete!" -ForegroundColor Green
Write-Host "🌐 Access n8n at: https://$N8N_FQDN" -ForegroundColor Cyan
Write-Host ""
Write-Host "🔑 Login credentials:" -ForegroundColor Yellow
$N8N_USER = terraform output -raw n8n_basic_auth_user
Write-Host "   Username: $N8N_USER" -ForegroundColor White
Write-Host "   Password: (from your main.tfvars.json)" -ForegroundColor White
Write-Host ""
Write-Host "⚠️  Important: Save your encryption key securely:" -ForegroundColor Yellow
Write-Host "   Run: cd .azure/$env:AZURE_ENV_NAME/infra && terraform output -raw n8n_encryption_key" -ForegroundColor White
Write-Host ""
```

**Note**: Remember to make the bash script executable after creation:
```bash
chmod +x infra/hooks/postprovision.sh
```
