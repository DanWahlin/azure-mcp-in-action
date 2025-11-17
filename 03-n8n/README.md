# Chapter 3: Automating n8n Deployments with Copilot Agents

**Title**: Deploy n8n to Azure with IaC-focused Copilot agents  
**Focus**: End-to-end n8n rollout using GitHub Copilot agent mode, Azure MCP tools, and either Bicep or Terraform  
**Estimated Time**: 60-90 minutes (each path ~30-40 minutes)  
**Prerequisites**: [Chapter 0](../00-course-setup/README.md), [Chapter 1](../01-first-deployment/README.md)

## Quick Navigation
- [Part 2: Bicep Agent Deployment](#part-2-bicep-agent-deployment)
- [Part 3: Terraform Agent Deployment](#part-3-terraform-agent-deployment)

## 🎯 Learning Objectives
- ✅ Understand when to choose the Bicep or Terraform Copilot agent for Azure work
- ✅ Practice selecting specialized agents inside Copilot Chat → agent mode
- ✅ Use Azure MCP tooling (best practices, schema, deploy plans) before letting an agent create resources
- ✅ Deploy n8n into Azure Container Apps with PostgreSQL Flexible Server and Log Analytics
- ✅ Verify deployments via Portal, CLI, and agent-mode queries
- ✅ Clean up all resources to return spend to $0

## Real-World Scenario
> Your automation team wants a managed n8n instance in Azure so business users can design workflows without touching production systems. They expect AI-assisted deployments that keep costs below $30/month and must see the full Generate → Approve → Execute → Verify workflow using GitHub Copilot agents.

## Cost & Resource Plan
| State | Estimated Monthly Cost |
| --- | --- |
| Running n8n Container Apps + PostgreSQL Flexible Server + Log Analytics | $20–30 |
| After cleanup (resource group deleted) | **$0** |

**Required tags**: `--tags environment=learning course=azure-copilot chapter=03`  
**Region**: `westus` (aligns with both agent specs)  
**SKUs**: Container Apps consumption, PostgreSQL B_Standard_B1ms, Log Analytics PerGB2018

---

## Part 1: Meet the Specialized Agents

| Agent | File | Best Use Case |
| --- | --- | --- |
| Bicep Agent | [`../.github/agents/n8n-deployment.bicep.agent.md`](../.github/agents/n8n-deployment.bicep.agent.md) | When your org prefers Azure-native IaC and wants azd + Bicep
| Terraform Agent | [`../.github/agents/n8n.deployment.terraform.agent.md`](../.github/agents/n8n.deployment.terraform.agent.md) | When you need multi-cloud portability or existing Terraform workflows

**How to select an agent in GitHub Copilot Chat**
1. Open Copilot Chat (`Cmd+Shift+I` / `Ctrl+Shift+I`).
2. Set mode to **Agent**.
3. Click the agent picker (spark icon) → choose `n8n Bicep` *or* `n8n Terraform` (names come from the files above).
4. Confirm "Azure" appears in your prompt so Copilot routes to Azure MCP tools.

**What these agents do for you**
- Call Azure best-practice MCP tools before generating IaC.
- Scaffold `azure.yaml`, IaC files, post-provision hooks, and example parameter files.
- Register required resource providers and run `azd up` (after you approve).
- Surface "Continue?" approval cards before any command executes.

> ⚠️ **Safety Reminder**: The agents will actually run deployments after you click **Continue**. Always review the generated Bicep/Terraform code and azd commands first.

---

## Part 2: Bicep Agent Deployment

### 2.1 Why Choose This Path
- Native Azure experience with first-class Bicep tooling.
- Excellent for teams standardizing on ARM/Bicep and Azure RBAC policies.
- Leverages the post-provision hooks already documented in the agent file.

### 2.2 Kickoff Prompt
With the **n8n Bicep** agent selected, run:
```
Create the Chapter 3 n8n environment in westus using Bicep and azd
- Use environment name n8n
- Follow the repository instructions for Chapter 3
- Show me the plan before executing anything
```

**Behind the scenes** the agent will:
- Call `mcp_azure_mcp_get_bestpractices` (general/code-generation) and summarize guidance.
- Fetch Bicep schema tips via `mcp_azure_mcp_bicepschema`.
- Generate `infra/main.bicep`, parameters, `azure.yaml`, `infra/hooks/postprovision.*`, and `.gitignore` entries.

### 2.3 Approve the Plan
- Copilot posts a diff + command list (resource group, azd init, az provider register, etc.).
- Review naming: expect `n8n-<suffix>` resources and required tags.
- Click **Continue** only when the plan matches the requirements.

### 2.4 Execution & Monitoring
- `azd up` provisions Resource Group → Log Analytics → Container Apps Environment → Managed Identity → PostgreSQL Flexible Server → n8n Container App.
- The post-provision hook updates `WEBHOOK_URL` once the Container App FQDN exists.
- Watch terminal output for health probe configuration confirmation (startup/liveness/readiness).

### 2.5 Verification (choose at least two)
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

### 2.6 Access n8n
- URL: `https://<container-app-fqdn>`.
- Default auth user from parameters (usually `admin`).
- Password stored in `infra/main.parameters.json` (you set this before deployment).

### 2.7 Cleanup (Bicep)
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
- Mirrors multi-cloud InfraOps processes with Terraform state managed by azd.
- Demonstrates how Copilot agents comply with Terraform best practices before code generation.
- Useful if your team already stores Terraform modules in a registry.

### 3.2 Kickoff Prompt
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

### 3.3 Approve the Plan
- Expect to see `azd init`, `az provider register`, and `azd up` steps.
- Review Terraform plan snippet: verifies Container App, PostgreSQL Flexible Server, Log Analytics workspace, and random suffix resources.
- Confirm secrets are flagged as sensitive outputs before clicking **Continue**.

### 3.4 Execution & State
- `azd up` runs `terraform init/plan/apply` inside `.azure/<env>/infra`.
- Post-provision hooks open Terraform outputs to retrieve the Container App FQDN and update `WEBHOOK_URL` automatically.
- Encryption key produced by `random_password` is stored as a sensitive Terraform output—save it securely.

### 3.5 Verification Options
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

### 3.6 Cleanup (Terraform)
Use the same agent:
```
Run azd down for the n8n Terraform environment and confirm all Chapter 3 resources are gone
```
- Agent preview should show `azd down --purge` plus resource-group validation.
- Verify: `az group list --tag chapter=03 --output table` returns nothing.

---

## Part 4: Assignment
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
- ✅ `azd down` or RG deletion performed; subscription back to $0 spend.

---

## Cleanup Checklist (Applies to Both Paths)
- [ ] `azd down` (or agent-proposed RG deletion) completed.
- [ ] `az group list --tag chapter=03 --output table` shows no rows.
- [ ] Portal confirms the resource group no longer exists.
- [ ] `.azure/` configuration retained locally for future redeployments.
- [ ] Secrets removed from shell history or stored securely (passwords, encryption keys).

---

## Key Takeaways
1. Specialized Copilot agents bring domain knowledge (Bicep vs Terraform) so you can focus on intent.
2. Every run follows Generate → Approve → Execute → Verify—never skip an approval gate.
3. Azure MCP tools (best practices, schema, deploy planner) are invoked automatically to enforce governance.
4. Post-provision hooks matter: they finalize settings (like `WEBHOOK_URL`) that depend on runtime values.
5. Cleanup keeps monthly spend at $0 and reinforces responsible Azure usage.
