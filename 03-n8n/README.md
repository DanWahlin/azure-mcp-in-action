# Chapter 3: Automating n8n Deployments with GitHub Copilot Agents

In this chapter, you'll learn how to deploy production-ready infrastructure using specialized GitHub Copilot agents. You'll deploy n8n (a workflow automation platform) to Azure using either Bicep or Terraform, while GitHub Copilot agents handle the complexity of infrastructure-as-code generation, best practice validation, and automated deployment. This hands-on chapter demonstrates how AI agents can transform deployment workflows from hours to minutes.

**Prerequisites**: [Chapter 0: Course Setup](../00-course-setup/README.md), [Chapter 1: First Deployment](../01-first-deployment/README.md)

## Quick Navigation
- [Part 1: Meet the Specialized Agents](#part-1-meet-the-specialized-agents)
- [Part 2: Bicep Agent Deployment](#part-2-bicep-agent-deployment)
- [Part 3: Terraform Agent Deployment](#part-3-terraform-agent-deployment)
- [Part 4: Troubleshooting](#part-4-troubleshooting-common-issues)
- [Part 5: Assignment](#part-5-assignment)

## 🎯 Learning Objectives
- ✅ Understand when to choose the Bicep or Terraform GitHub Copilot agent for Azure work
- ✅ Practice selecting specialized agents inside GitHub Copilot Chat → [agent mode](../GLOSSARY.md#agent-mode)
- ✅ Use Azure MCP tooling (best practices, schema, deploy plans) before letting an agent create resources
- ✅ Deploy n8n into [Azure Container Apps](../GLOSSARY.md#azure-container-apps) with [PostgreSQL Flexible Server](../GLOSSARY.md#postgresql) and Log Analytics
- ✅ Verify deployments via Portal, CLI, and agent-mode queries
- ✅ Clean up all resources immediately after completing exercises

## Real-World Scenario

Your automation team wants a managed n8n instance in Azure so business users can design workflows without touching production systems. They expect AI-assisted deployments that minimize costs and must see the full [Generate → Approve → Execute → Verify workflow](../GLOSSARY.md#generate--approve--execute-workflow) using GitHub Copilot agents.

## Resource Plan

**Required tags**: `--tags environment=learning course=azure-copilot chapter=03`
**Region**: `westus` (aligns with both agent specs)
**SKUs**: [Container Apps](../GLOSSARY.md#azure-container-apps) consumption, [PostgreSQL](../GLOSSARY.md#postgresql) B_Standard_B1ms, Log Analytics PerGB2018

> **Cost Note**: This chapter deploys paid services. Clean up resources immediately after completing the exercises to minimize costs.

---

## Part 1: Meet the Specialized Agents

| Agent | File | Best Use Case |
| --- | --- | --- |
| Bicep Agent | [`../.github/agents/n8n-deployment.bicep.agent.md`](../.github/agents/n8n-deployment.bicep.agent.md) | When your org prefers Azure-native IaC and wants azd + Bicep
| Terraform Agent | [`../.github/agents/n8n.deployment.terraform.agent.md`](../.github/agents/n8n.deployment.terraform.agent.md) | When you need multi-cloud portability or existing Terraform workflows

**How to select an agent in GitHub Copilot Chat**
1. Open GitHub Copilot Chat (`Cmd+Shift+I` / `Ctrl+Shift+I`).
2. Set mode to **Agent** (use the dropdown at the bottom of the chat panel).
3. From the same dropdown, select `n8n-deployment.bicep.agent.md` or `n8n.deployment.terraform.agent.md`).
4. Verify the selected agent name appears in your chat input area.


### What Makes These Agents Special?

These specialized agents handle:

**Pre-deployment Validation**
- Automatically call `mcp_azure_mcp_get_bestpractices` for general Azure guidance
- Call `mcp_azure_mcp_bicepschema` (Bicep agent) or `mcp_azure_mcp_azureterraformbestpractices` (Terraform agent) for IaC-specific best practices
- Validate deployment plan with `mcp_azure_mcp_deploy` before execution

**Smart Scaffolding**
- Generate complete project structure: `azure.yaml`, [IaC](../GLOSSARY.md#infrastructure-as-code-iac) files, post-provision hooks, `.gitignore`
- Create example parameter/variable files with secure defaults
- Configure [Azure Developer CLI](../GLOSSARY.md#azure-developer-cli) (azd) integration automatically

**Resource Provider Management**
- Automatically register `Microsoft.App`, `Microsoft.DBforPostgreSQL`, and `Microsoft.OperationalInsights`
- Prevent 409 conflict errors during deployment
- Run `azd up` after you approve the plan

**Post-Provision Automation**
- Execute hooks to configure `WEBHOOK_URL` without manual intervention
- Update environment variables after [Container Apps](../GLOSSARY.md#azure-container-apps) FQDN is available
- Handle circular dependencies automatically

**Built-in Expertise**
- Embed critical configurations: health probe timeouts (60s initial delay), [PostgreSQL](../GLOSSARY.md#postgresql) SSL settings
- Apply security best practices: [Managed Identity](../GLOSSARY.md#managed-identity), HTTPS-only, secure secrets
- Generate production-ready infrastructure from day one

> ⚠️ **Safety Reminder**: The agents will actually run deployments after you click **Continue**. Always review the generated [Bicep](../GLOSSARY.md#bicep)/[Terraform](../GLOSSARY.md#terraform) code and azd commands first.

### Bicep vs Terraform: Quick Comparison

| Aspect | Bicep Agent | Terraform Agent |
| --- | --- | --- |
| **Best For** | Azure-native teams, ARM/Bicep standardization | Multi-cloud, existing Terraform workflows |
| **State Management** | azd manages locally | azd manages locally (`.azure/<env>/infra`) |
| **Syntax** | Declarative, Azure-focused | HCL, provider-agnostic |
| **Key Function** | `newGuid()` for encryption key | `random_password` resource |
| **Provider Setup** | Native Azure Resource Manager | `resource_provider_registrations = "none"` |
| **Parameter Files** | `main.parameters.json` | `main.tfvars.json` (NOT `terraform.tfvars.json`) |
| **Post-Provision** | Uses `azd env get-value` | Uses `terraform output -raw` |
| **Learning Curve** | Lower if Azure-focused | Steeper but transferable skills |

---

## Part 2: Bicep Agent Deployment

### 2.1 Why Choose This Path
- Native Azure experience with first-class [Bicep](../GLOSSARY.md#bicep) tooling.
- Excellent for teams standardizing on ARM/Bicep and Azure RBAC policies.
- Leverages the post-provision hooks already documented in the agent file.
- Simpler syntax for Azure-only deployments.

### 2.2 Critical Technical Details (Bicep)

**Health Probes (MOST IMPORTANT - Common Failure Point)**
- **Liveness probe**: `initialDelaySeconds: 60` - n8n requires at least 60 seconds to initialize
- **Startup probe**: `failureThreshold: 30` - allows up to 5 minutes for first startup
- **Why critical**: Without these settings, [Azure Container Apps](../GLOSSARY.md#azure-container-apps) will kill the container before n8n finishes starting, causing "CrashLoopBackOff" errors

**Database Connection Requirements**
- MUST use [PostgreSQL](../GLOSSARY.md#postgresql) server FQDN (fully qualified domain name), not short name
- MUST enable SSL: `DB_POSTGRESDB_SSL_ENABLED=true` (required for Azure PostgreSQL)
- MUST set SSL certificate validation: `DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED=false` (Azure PostgreSQL certificates)
- Connection timeout: 60 seconds (`DB_POSTGRESDB_CONNECTION_TIMEOUT=60000`) to handle cold starts
- Firewall: Allow Azure services (`0.0.0.0` to `0.0.0.0`)

**Bicep-Specific Requirements**
- Encryption key: MUST use `param n8nEncryptionKey string = newGuid()` (parameter default only)
- **NEVER** use `newGuid()` in variable declarations or expressions (will cause Bicep errors)
- Post-provision hook uses `azd env get-value` to retrieve deployment outputs

**WEBHOOK_URL Configuration**
- Cannot be set during initial creation (circular dependency with Container App FQDN)
- Post-provision hook runs **automatically** after `azd up` completes
- Hook retrieves FQDN and updates environment variable without manual steps

### 2.3 Kickoff Prompt
With the **n8n Bicep** agent selected in GitHub Copilot, run the following prompt:
```
Create a deployment for n8n to Azure using Bicep and azd
- Region westus, environment name n8n
- Show generated Bicep code and azd commands for approval
- Include required tags: environment=learning course=azure-copilot chapter=03
```

**Behind the scenes** the agent will:
- Call `mcp_azure_mcp_get_bestpractices` (general/code-generation) and summarize guidance.
- Fetch Bicep schema tips via `mcp_azure_mcp_bicepschema`.
- Generate `infra/main.bicep`, parameters, `azure.yaml`, `infra/hooks/postprovision.*`, and `.gitignore` entries.

### 2.4 Approve the Plan
- GitHub Copilot posts a diff + command list (resource group, azd init, az provider register, etc.).
- Review naming: expect `n8n-<suffix>` resources and required tags.
- Click **Continue** only when the plan matches the requirements.

### 2.5 Execution & Monitoring
- `azd up` provisions Resource Group → Log Analytics → Container Apps Environment → Managed Identity → PostgreSQL Flexible Server → n8n Container App.
- The post-provision hook updates `WEBHOOK_URL` once the Container App FQDN exists.
- Watch terminal output for health probe configuration confirmation (startup/liveness/readiness).

### 2.6 Verification (choose at least two)
1. **Portal**: Resource group `learning-rg-[initials]` (or agent-proposed name) should contain Container App, PostgreSQL server/database, Log Analytics workspace.
2. **Azure CLI**:
   ```bash
   az containerapp show \
     --name <app-name> \
     --resource-group <rg> \
     --query "{State:properties.latestRevisionName, Url:properties.configuration.ingress.fqdn}" --output table
   az postgres flexible-server show --name <server> --resource-group <rg>
   ```
3. **Agent Query**: "List all resources tagged chapter=03" or "Show outputs from the latest azd deployment".

### 2.7 Access n8n
- URL: `https://<container-app-fqdn>`.
- Default auth user from parameters (usually `admin`).
- Password stored in `infra/main.parameters.json` (you set this before deployment).

### 2.8 Cleanup (Bicep)
After testing flows:
```
Delete the Chapter 3 n8n resource group and all dependent resources
```
- The agent calls `azd down` or `az group delete` (confirm in plan).  
- Verify deletion via `az group list --tag chapter=03`.  
- Ensure `.azure/` artifacts remain locally so you can redeploy later.

---

## Part 3: Terraform Agent Deployment

### 3.1 Why Choose This Path
- Mirrors multi-cloud InfraOps processes with [Terraform](../GLOSSARY.md#terraform) state managed by [azd](../GLOSSARY.md#azure-developer-cli).
- Demonstrates how GitHub Copilot agents comply with Terraform best practices before code generation.
- Useful if your team already stores Terraform modules in a registry.
- Skills transfer to other cloud providers (AWS, GCP).

### 3.2 Critical Technical Details (Terraform)

**Health Probes (MOST IMPORTANT - Common Failure Point)**
- **Liveness probe**: `initial_delay = 60` - n8n requires at least 60 seconds to initialize
- **Startup probe**: `failure_count_threshold = 30` - allows up to 5 minutes for first startup
- **Why critical**: Without these settings, [Azure Container Apps](../GLOSSARY.md#azure-container-apps) will kill the container before n8n finishes starting, causing "CrashLoopBackOff" errors

**Database Connection Requirements**
- MUST use [PostgreSQL](../GLOSSARY.md#postgresql) server FQDN (fully qualified domain name), not short name
- MUST enable SSL: `DB_POSTGRESDB_SSL_ENABLED=true` (required for Azure PostgreSQL)
- MUST set SSL certificate validation: `DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED=false` (Azure PostgreSQL certificates)
- Connection timeout: 60 seconds (`DB_POSTGRESDB_CONNECTION_TIMEOUT=60000`) to handle cold starts
- Firewall: Allow Azure services (`0.0.0.0` to `0.0.0.0`)

**Terraform-Specific Requirements**
- Provider configuration: `resource_provider_registrations = "none"` in `providers.tf` (prevents 409 conflicts)
- Encryption key: Use `random_password` resource (NOT `random_string`)
- Variable files: azd uses `main.tfvars.json` (NOT `terraform.tfvars.json`)
- Post-provision hook: Navigate to `.azure/${AZURE_ENV_NAME}/infra` and use `terraform output -raw`

**WEBHOOK_URL Configuration**
- Cannot be set during initial creation (circular dependency with Container App FQDN)
- Post-provision hook runs **automatically** after `azd up` completes
- Hook retrieves FQDN from Terraform outputs and updates environment variable without manual steps

### 3.3 Kickoff Prompt
Select the **n8n Terraform** agent, then run:
```
Deploy the Chapter 3 n8n stack with Terraform and azd
- Region westus, environment name n8n
- Show Terraform plan and azd commands for approval
- Follow the repository conventions for tags and cleanup guidance
```

**Agent workflow**:
- Retrieves Azure + Terraform best practices via MCP tools.
- Generates `infra/main.tf`, `variables.tf`, `providers.tf`, `outputs.tf`, `main.tfvars.json.example`, hooks, and `.gitignore` entries.
- Ensures `resource_provider_registrations = "none"` in the azurerm provider block.

### 3.4 Approve the Plan
- Expect to see `azd init`, `az provider register`, and `azd up` steps.
- Review Terraform plan snippet: verifies Container App, PostgreSQL Flexible Server, Log Analytics workspace, and random suffix resources.
- Confirm secrets are flagged as sensitive outputs before clicking **Continue**.

### 3.5 Execution & State
- `azd up` runs `terraform init/plan/apply` inside `.azure/<env>/infra`.
- Post-provision hooks open Terraform outputs to retrieve the Container App FQDN and update `WEBHOOK_URL` automatically.
- Encryption key produced by `random_password` is stored as a sensitive Terraform output—save it securely.

### 3.6 Verification Options
1. **Portal**: Same as the Bicep path; ensure Container App replica count shows scale-to-zero capability (min 0, max 3).
2. **Azure CLI**:
   ```bash
   az containerapp revision list --name <app> --resource-group <rg> --output table
   az postgres flexible-server db list --server-name <server> --resource-group <rg>
   ```
3. **Terraform Outputs**:
   ```bash
   cd .azure/n8n/infra
   terraform output
   ```
4. **Agent Query**: "Show Terraform outputs for the n8n environment".

### 3.7 Cleanup (Terraform)
Use the same agent:
```
Run azd down for the n8n Terraform environment and confirm all Chapter 3 resources are gone
```
- Agent preview should show `azd down --purge` plus resource-group validation.
- Verify: `az group list --tag chapter=03 --output table` returns nothing.

---

## Part 4: Troubleshooting Common Issues

### Issue 1: Container Keeps Restarting (CrashLoopBackOff)

**Symptoms**:
- [Container App](../GLOSSARY.md#azure-container-apps) shows "Provisioning" state indefinitely
- Container restarts repeatedly
- [Azure Portal](../GLOSSARY.md#azure-portal) shows replica count cycling 0 → 1 → 0

**Root Causes**:
- Health probes killing container before n8n initialization completes
- Missing or incorrect health probe timeouts

**Solutions**:
1. **Verify health probe configuration** in generated IaC:
   - **Bicep**: Check `infra/main.bicep` for `livenessProbe.initialDelaySeconds: 60` and `startupProbe.failureThreshold: 30`
   - **Terraform**: Check `infra/main.tf` for `initial_delay = 60` and `failure_count_threshold = 30`

2. **Check container logs**:
   ```bash
   az containerapp logs show \
     --name <app-name> \
     --resource-group <rg-name> \
     --follow
   ```

3. **Review container app health**:
   ```bash
   az containerapp show \
     --name <app-name> \
     --resource-group <rg-name> \
     --query "properties.{provisioningState:provisioningState, runningStatus:runningStatus, latestRevision:latestRevisionName}"
   ```

### Issue 2: Database Connection Failures

**Symptoms**:
- n8n logs show "ECONNREFUSED" or "connection timeout" errors
- Container starts but cannot connect to [PostgreSQL](../GLOSSARY.md#postgresql)
- Error: "SSL connection required"

**Root Causes**:
- Using PostgreSQL short name instead of FQDN
- SSL not enabled or incorrectly configured
- Firewall rules blocking Azure services

**Solutions**:
1. **Verify database connection settings** in container environment variables:
   ```bash
   az containerapp show \
     --name <app-name> \
     --resource-group <rg-name> \
     --query "properties.template.containers[0].env[?name=='DB_POSTGRESDB_HOST'].value"
   ```
   Should return FQDN like `n8n-pg-abc123.postgres.database.azure.com` (NOT just `n8n-pg-abc123`)

2. **Confirm SSL is enabled**:
   ```bash
   az containerapp show \
     --name <app-name> \
     --resource-group <rg-name> \
     --query "properties.template.containers[0].env[?name=='DB_POSTGRESDB_SSL_ENABLED'].value"
   ```
   Should return `["true"]`

3. **Check PostgreSQL firewall rules**:
   ```bash
   az postgres flexible-server firewall-rule list \
     --server-name <server-name> \
     --resource-group <rg-name> \
     --output table
   ```
   Should include rule allowing Azure services (`0.0.0.0` to `0.0.0.0`)

### Issue 3: WEBHOOK_URL Not Configured

**Symptoms**:
- n8n loads but static assets (CSS/JS) fail to load
- n8n interface appears broken or unstyled
- Webhook URLs incorrect in n8n workflows

**Root Causes**:
- Post-provision hook did not run
- Hook script not executable (Bash)
- Incorrect FQDN in WEBHOOK_URL

**Solutions**:
1. **Verify WEBHOOK_URL is set**:
   ```bash
   az containerapp show \
     --name <app-name> \
     --resource-group <rg-name> \
     --query "properties.template.containers[0].env[?name=='WEBHOOK_URL'].value"
   ```

2. **Manually run post-provision hook**:
   - **Bicep**: `./infra/hooks/postprovision.sh` (macOS/Linux) or `./infra/hooks/postprovision.ps1` (Windows)
   - **Terraform**: Same scripts, but they navigate to `.azure/n8n/infra` first

3. **Make script executable** (macOS/Linux):
   ```bash
   chmod +x infra/hooks/postprovision.sh
   ```

### Issue 4: 409 Conflict Errors (Terraform Only)

**Symptoms**:
- `azd up` fails with "409 Conflict" errors
- Error mentions resource provider registration
- Terraform apply fails with provider registration issues

**Root Causes**:
- `resource_provider_registrations` not set to `"none"` in providers.tf
- Resource providers not registered manually before deployment

**Solutions**:
1. **Verify providers.tf configuration**:
   ```hcl
   provider "azurerm" {
     resource_provider_registrations = "none"
     features {}
   }
   ```

2. **Manually register providers** (run before `azd up`):
   ```bash
   az provider register --namespace Microsoft.App
   az provider register --namespace Microsoft.DBforPostgreSQL
   az provider register --namespace Microsoft.OperationalInsights
   ```

3. **Check registration status**:
   ```bash
   az provider show --namespace Microsoft.App --query "registrationState"
   az provider show --namespace Microsoft.DBforPostgreSQL --query "registrationState"
   az provider show --namespace Microsoft.OperationalInsights --query "registrationState"
   ```
   All should return `"Registered"`

### Issue 5: Bicep `newGuid()` Errors

**Symptoms**:
- Bicep deployment fails with `newGuid()` validation errors
- Error: "newGuid() can only be used as parameter default value"

**Root Cause**:
- `newGuid()` used in variable declaration or expression (not allowed)

**Solution**:
Ensure encryption key uses `newGuid()` **only** as parameter default in `main.bicep`:
```bicep
@secure()
@description('n8n encryption key (auto-generated if not provided)')
param n8nEncryptionKey string = newGuid()  // ✅ Correct location

// ❌ WRONG - Do NOT use in variables:
// var encryptionKey = newGuid()
```

### Getting Additional Help

If issues persist:
1. **Check agent-generated code**: Review `infra/main.bicep` or `infra/main.tf` against agent file specifications
2. **Review azd logs**: `azd up --debug` provides detailed deployment logs
3. **Consult agent files**: [Bicep agent](../.github/agents/n8n-deployment.bicep.agent.md) and [Terraform agent](../.github/agents/n8n.deployment.terraform.agent.md) contain complete specifications
4. **Use GitHub Copilot in Ask mode**: Switch to Ask mode and query "Why is my n8n container failing to start?" with relevant error logs

---

## Part 5: Assignment
1. Pick the IaC path you did *not* follow during the walkthrough and complete it solo.
2. Document the prompts you used, the approval decisions you made, and any adjustments.
3. Capture screenshots or CLI output of the verification steps (Portal + CLI + agent query).
4. Submit a short write-up: cost estimate, pain points, and how the agent workflow improved speed.

### Success Criteria
- ✅ Correct agent selected and acknowledged the MCP safety prompts.
- ✅ Best-practice tool output reviewed before code generation.
- ✅ `azd up` completed without manual edits to generated IaC.
- ✅ n8n reachable over HTTPS with basic auth enabled.
- ✅ Three verification methods recorded.
- ✅ `azd down` or RG deletion performed; all resources cleaned up.

---

## Cleanup Checklist (Applies to Both Paths)
- [ ] `azd down` (or agent-proposed RG deletion) completed.
- [ ] `az group list --tag chapter=03 --output table` shows no rows.
- [ ] Portal confirms the resource group no longer exists.
- [ ] `.azure/` configuration retained locally for future redeployments.
- [ ] Secrets removed from shell history or stored securely (passwords, encryption keys).

---

## Key Takeaways
1. Specialized GitHub Copilot agents bring domain knowledge (Bicep vs Terraform) so you can focus on intent.
2. Every run follows Generate → Approve → Execute → Verify—never skip an approval gate.
3. Azure MCP tools (best practices, schema, deploy planner) are invoked automatically to enforce governance.
4. Post-provision hooks matter: they finalize settings (like `WEBHOOK_URL`) that depend on runtime values.
5. Cleanup immediately after learning reinforces responsible Azure resource management.

---

## What's Next?

**Upcoming Chapters (Currently Being Refreshed)**

The next chapters are being updated to align with the agent mode workflow. Until they're ready, you can:

1. **Explore archived chapters** in the [`old/`](../old) directory for additional Azure scenarios
2. **Practice the patterns** from Chapters 0-3 with your own projects
3. **Experiment with** the Bicep and Terraform agents from Chapter 3 on other OSS applications

**Stay tuned** for Chapter 4 and beyond, which will continue building on the Generate → Approve → Execute workflow you've mastered!
