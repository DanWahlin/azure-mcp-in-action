# Chapter 4: Terraform Basics with AI Assistance

Master AI-generated [Terraform](../GLOSSARY.md#terraform) configurations for multi-cloud [infrastructure-as-code](../GLOSSARY.md#infrastructure-as-code-iac) deployments. In this chapter, you'll learn how to use [agent mode](../GLOSSARY.md#agent-mode) to generate Terraform code, understand when to use Terraform versus [Bicep](../GLOSSARY.md#bicep), and manage infrastructure state across different cloud providers.

## Prerequisites

- Completed [Course Setup](../00-course-setup/README.md)
- Completed [Chapter 1: First Deployment](../01-first-deployment/README.md)
- Completed [Chapter 2: Advanced Prompt Patterns](../02-cli-mastery/README.md)
- Completed [Chapter 3: Infrastructure-as-Code with Bicep](../03-bicep-templates/README.md)

## 🎯 Learning Objectives

- ✅ Understand [Terraform](../GLOSSARY.md#terraform) vs [Bicep](../GLOSSARY.md#bicep) vs [Azure CLI](../GLOSSARY.md#azure-cli)
- ✅ Generate Terraform configurations using [Azure MCP](../GLOSSARY.md#azure-mcp)
- ✅ Initialize and validate Terraform projects
- ✅ Plan Terraform deployments
- ✅ Apply Terraform configurations safely
- ✅ Manage Terraform state
- ✅ Destroy resources cleanly

## Real-World Scenario

> Your company might migrate from Azure to AWS or GCP in the future. To maintain flexibility, you're adopting Terraform as your IaC tool. You'll use Azure MCP to generate Terraform configurations while learning Terraform syntax through AI assistance.

---

## Part 1: Why Terraform?

### Bicep Advantages

- Azure-native
- Simpler syntax
- Better Azure integration
- Automatic state management

### Terraform Advantages

- Multi-cloud support
- Mature ecosystem
- Large community
- Provider marketplace
- Better for complex scenarios

---

## Part 2: Generating Terraform Configurations

**Prompt to Azure MCP**:

```
Generate Terraform configuration for Azure that creates:
- Resource group in East US
- Storage account with Standard_LRS
- Container named 'data'
- Private endpoint for secure access

Include provider configuration, variables, and outputs.
Use Terraform 1.5+ syntax with AzureRM provider 3.0+
```

**Note**: A [resource group](../GLOSSARY.md#resource-group) holds related resources. A [private endpoint](../GLOSSARY.md#private-endpoint) provides secure network access.

### Expected Output

```hcl
terraform {
  required_version = ">= 1.5.0"
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.0"
    }
  }
}

provider "azurerm" {
  features {}
}

variable "resource_group_name" {
  description = "Name of the resource group"
  type        = string
  default     = "terraform-demo-rg"
}

variable "location" {
  description = "Azure region"
  type        = string
  default     = "eastus"
}

resource "azurerm_resource_group" "main" {
  name     = var.resource_group_name
  location = var.location
}

resource "azurerm_storage_account" "main" {
  name                     = "terraformstg${random_string.unique.result}"
  resource_group_name      = azurerm_resource_group.main.name
  location                = azurerm_resource_group.main.location
  account_tier            = "Standard"
  account_replication_type = "LRS"

  tags = {
    environment = "learning"
    managed_by  = "terraform"
  }
}

output "storage_account_name" {
  value = azurerm_storage_account.main.name
}
```

---

## Part 3: Terraform Workflow

```bash
# Initialize Terraform
terraform init

# Validate configuration
terraform validate

# Plan changes (preview)
terraform plan

# Apply changes (execute)
terraform apply

# Show current state
terraform show

# Destroy resources
terraform destroy
```

---

## Assignment

1. Generate Terraform configuration for complete dev environment
2. Use modules for reusability
3. Implement remote state in Azure Storage
4. Create workspaces for dev/staging/prod
5. Deploy to all three environments
6. Compare costs across environments

### Success Criteria

- ✅ Generated valid Terraform configuration
- ✅ Configuration passes validation
- ✅ Successfully deployed with `terraform apply`
- ✅ State stored remotely in Azure
- ✅ Multiple workspaces functional
- ✅ Clean destroy with no orphaned resources

---

## Cleanup Using Terraform and Azure MCP

> [!IMPORTANT]
> Complete this cleanup to avoid unexpected Azure charges. This chapter had you deploy resources using Terraform. The **preferred cleanup method is using Terraform's destroy command**, as it properly manages state.

### Method 1: Terraform Destroy (RECOMMENDED)

```bash
# Destroy resources in current workspace
terraform destroy

# For multiple workspaces (if you created them):
terraform workspace select dev
terraform destroy

terraform workspace select staging
terraform destroy

terraform workspace select prod
terraform destroy
```

**Verify all resources are gone (Bash/macOS/Linux):**
```bash
az resource list --output table | grep terraform
```

**Verify all resources are gone (PowerShell/Windows):**
```powershell
az resource list --output table | Select-String "terraform"
```

### Method 2: Azure MCP Fallback (if Terraform state is lost/corrupted)

**Prompt to Azure MCP**:
```
Delete all resource groups with tag managed_by=terraform
List them first, then delete: terraform-demo-rg, terraform-dev-rg, terraform-staging-rg, terraform-prod-rg
```

**Agent mode will**:
1. Generate deletion commands → Show "Continue?" → Execute after approval
2. List all Terraform-managed resource groups
3. Delete each resource group
4. Confirm deletion completion

**Manual Azure CLI alternative**:
```bash
# List all Terraform-managed resource groups
az group list --query "[?tags.managed_by=='terraform']" --output table

# Delete each resource group
az group delete --name terraform-demo-rg --yes --no-wait
az group delete --name terraform-dev-rg --yes --no-wait
az group delete --name terraform-staging-rg --yes --no-wait
az group delete --name terraform-prod-rg --yes --no-wait
```

### Before You Delete

- [ ] Run `terraform destroy` first (preferred method)
- [ ] Verify Terraform state shows no remaining resources
- [ ] Keep your Terraform configuration files (.tf files) for reference
- [ ] Delete the remote state storage account (if you created one)

### Clean Up Remote State Storage (if applicable)

```bash
# If you created a storage account for remote state
az storage account delete \
  --name tfstateXXXXXX \
  --resource-group terraform-state-rg \
  --yes
```

### Verify Complete Deletion

**Verify resource groups are gone (Bash/macOS/Linux):**
```bash
az group list --output table | grep terraform
# Should return empty
```

**Verify resource groups are gone (PowerShell/Windows):**
```powershell
az group list --output table | Select-String "terraform"
# Should return empty
```

**Note**: Your Terraform configuration files (.tf) are stored locally and will NOT be deleted. You may use these as references in future projects.

---

## Key Takeaways

1. **Terraform for Multi-Cloud**: Use Terraform when you need flexibility across cloud providers
2. **State Management**: Terraform state tracks infrastructure; store it remotely for teams
3. **Plan Before Apply**: Always review the plan to understand changes
4. **Workspaces for Environments**: Use workspaces to manage multiple environments
5. **Destroy Cleanly**: Use `terraform destroy` to remove resources properly
6. **Modules for Reusability**: Create modules for common infrastructure patterns

---

## What's Next?

**[Chapter 5: Simple Web Application Deployment (Ghost CMS)](../05-simple-web-app/README.md)**

Now that you've mastered both Bicep and Terraform, you'll deploy a complete production-ready web application with a real-world project: Ghost CMS.
