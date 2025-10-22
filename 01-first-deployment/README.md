# Chapter 1: Your First AI-Generated Azure Deployment

Welcome to your first hands-on Azure deployment using GitHub Copilot [agent mode](../GLOSSARY.md#agent-mode)! In this chapter, you'll learn the fundamental **[Generate → Approve → Execute → Verify workflow](../GLOSSARY.md#generate--approve--execute-workflow)** that you'll use throughout the course. You'll start by querying your Azure subscription, then deploy a simple Node.js web app to [Azure App Service](../GLOSSARY.md#app-service) using natural language prompts. Agent mode will generate the [infrastructure code](../GLOSSARY.md#infrastructure-as-code-iac), ask for your approval with "Allow" buttons, execute the deployment commands, and you'll verify the results in both the [Azure Portal](../GLOSSARY.md#azure-portal) and [Azure CLI](../GLOSSARY.md#azure-cli). This practical introduction shows how AI can accelerate your Azure development while maintaining full control through approval gates.

## Prerequisites

- Completed [Course Setup](../00-course-setup/README.md)

## 🎯 Learning Objectives

By the end of this chapter, you'll be able to:

- ✅ Practice querying Azure resources with agent mode
- ✅ Understand the Generate → Approve → Execute workflow
- ✅ Create your first Azure web app with agent mode
- ✅ Verify deployment success in Azure Portal and Azure CLI
- ✅ Review generated code before approving execution
- ✅ Clean up resources using agent mode
- ✅ Understand cost implications before deployment

---

## Part 1: Understanding What You're Building

### Target Architecture

```
Azure App Service (Node.js LTS)
├── Free tier (F1 SKU) - $0/month
├── Linux-based runtime
├── Sample Hello World app
└── HTTPS enabled by default
```

**Cost Estimate**: $0 (using [Free tier](../GLOSSARY.md#free-tier-f1))

---

## Part 2: Practice Querying Azure Resources

Before creating resources, let's practice querying your Azure subscription:

### Exercise: Query Existing Resources

**Step 1: Activate agent mode**

1. Open GitHub Copilot Chat (Cmd+Shift+I or Ctrl+Shift+I)
2. Select "Agent" from the mode dropdown at the bottom

**Step 2: Query Your Subscription**

Use these prompts in agent mode:

```
Show all App Services in East US region
What storage accounts exist in my Azure subscription?
```

**What happens**: Agent mode queries your subscription and returns results - no resources are created. Verify the results match what you see in Azure Portal.

### Cost Validation (Ask Questions)

**Step 1: Switch to [ask mode](../GLOSSARY.md#ask-mode)**

In GitHub Copilot Chat, select "Ask" from the mode dropdown

**Step 2: Ask Questions with @azure**

```
@azure What is the monthly cost of an F1 App Service plan?
@azure How many free App Services can I have per subscription?
@azure What's included in the Azure Free tier?
```

**Expected**: Detailed answers about pricing and limits (F1 is $0/month)

---

## Part 3: Create Resources with agent mode

Now let's use agent mode to generate and execute deployment commands:

### Activate agent mode

In GitHub Copilot Chat, select "Agent" from the mode dropdown

### Prompt to Agent

```
Create the following Azure resources:
1. Resource group named learning-rg-[YOUR-INITIALS] in East US
2. App Service plan with Free tier (F1 SKU) for Linux
3. Node.js LTS web app named demo-app-[YOUR-INITIALS]-[DATE]

Requirements:
- Use secure defaults (HTTPS-only)
- Ensure all prerequisites are created in correct order
```

**Note**: A [resource group](../GLOSSARY.md#resource-group) is a container that holds related Azure resources. An [App Service plan](../GLOSSARY.md#app-service-plan) defines the compute resources for your app.

### What Happens in agent mode

The workflow will be:
1. **Generate**: Agent generates infrastructure code (Bicep templates or Azure CLI commands)
2. **Approve**: Agent shows "Continue?" button - review the code before clicking
3. **Execute**: Agent runs commands in your terminal
4. **Confirm**: Commands create the actual Azure resources
5. **Report**: Agent confirms what was created
6. Return confirmation with resource details

---

## Part 4: Verify Resource Creation

> **Note**: Always verify resources were created correctly!

### Method 1: Azure Portal Verification

You can use the Azure Portal to visually confirm resources:

1. Open [Azure Portal](https://portal.azure.com)
2. Navigate to **Resource Groups**
3. Find `learning-rg-[YOUR-INITIALS]`
4. Verify you see:
   - App Service plan (Free tier F1)
   - Web App (Node.js LTS runtime)

### Method 2: Azure CLI Verification

You can also verify using Azure CLI commands:

```bash
# Verify resource group
az group show --name learning-rg-[YOUR-INITIALS] --output table

# Verify App Service plan
az appservice plan show \
  --name demo-plan-[YOUR-INITIALS] \
  --resource-group learning-rg-[YOUR-INITIALS] \
  --query "{Name:name, SKU:sku.name, Location:location}" \
  --output table

# Verify web app
az webapp show \
  --name demo-app-[YOUR-INITIALS] \
  --resource-group learning-rg-[YOUR-INITIALS] \
  --query "{Name:name, URL:defaultHostName, State:state, Runtime:siteConfig.linuxFxVersion}" \
  --output table
```

### Method 3: Agent mode Query

```
Show details of web app demo-app-[YOUR-INITIALS]
List all resources in resource group learning-rg-[YOUR-INITIALS]
What's the status of my App Service plan demo-plan-[YOUR-INITIALS]?
```

---

## Part 5: Deploy Sample Application

Now let's deploy a sample Node.js application to the web app:

### Prompt to Azure MCP

```
Deploy the sample Node.js Hello World app from Azure samples
- https://github.com/Azure-Samples/nodejs-docs-hello-world
to my web app demo-app-[YOUR-INITIALS] in resource group learning-rg-[YOUR-INITIALS]
```

**Azure MCP will configure the deployment source and trigger the deployment.**

### Verify Deployment

1. **Azure Portal**: Navigate to your web app → Click "Browse" button
2. **Direct URL**: Visit `https://demo-app-[YOUR-INITIALS]-[DATE].azurewebsites.net`
3. **Expected**: You should see "Hello World!" displayed

### Monitor Deployment (Optional)

```bash
# Watch deployment logs in real-time
az webapp log tail \
  --name demo-app-[YOUR-INITIALS] \
  --resource-group learning-rg-[YOUR-INITIALS]
```

---

## Part 7: Cleanup (CRITICAL)

> [!IMPORTANT]
> Complete this cleanup to avoid unexpected Azure charges (even though F1 is free, it's good practice!)

### Cleanup Using Azure MCP

```
Delete resource group learning-rg-[YOUR-INITIALS] and all resources inside it
```

**Azure MCP will directly delete the resource group and all contained resources.**

### Verify Deletion

After Azure MCP completes the deletion, verify:

**Using Azure CLI (Bash/macOS/Linux):**
```bash
az group list --output table | grep learning-rg
# Should return nothing
```

**Using Azure CLI (PowerShell/Windows):**
```powershell
az group list --output table | Select-String "learning-rg"
# Should return nothing
```

**Or use agent mode:**
```
List all resource groups in my Azure subscription
# learning-rg-[YOUR-INITIALS] should not appear
```

### Alternative: Manual Cleanup with Azure CLI

If needed, you can also delete manually:

```bash
# List what will be deleted
az resource list --resource-group learning-rg-[YOUR-INITIALS] --output table

# Delete resource group
az group delete --name learning-rg-[YOUR-INITIALS] --yes --no-wait
```

**Verify deletion (Bash/macOS/Linux):**
```bash
az group list --output table | grep learning-rg
```

**Verify deletion (PowerShell/Windows):**
```powershell
az group list --output table | Select-String "learning-rg"
```

---

## Assignment

Use Azure MCP to complete these tasks:

1. Create a Python 3.14 web app using the same workflow
2. Use a different region (West US or your closest region)
3. Deploy sample Python code from Azure samples
4. Verify the deployment using all three methods (Portal, CLI, agent mode query)
5. Calculate total deployment time
6. Clean up all resources using agent mode

### Success Criteria

- ✅ Activated agent mode in GitHub Copilot Chat
- ✅ Used agent mode to generate and execute deployment commands
- ✅ Reviewed code before clicking "Continue" buttons
- ✅ Successfully deployed Python web app
- ✅ App accessible via HTTPS URL
- ✅ Verified deployment using Portal, CLI, and agent mode queries
- ✅ Cleaned up all resources using agent mode
- ✅ Cost remained $0 (Free tier)
- ✅ Understand the Generate → Approve → Execute → Verify workflow

---

## Key Takeaways

1. **Agent mode workflow**: Generate code → Approve with "Continue" → Execute commands → Verify results
2. **Verification is Critical**: Always verify resources using Portal, Azure CLI, and agent mode queries
3. **Review Before Approving**: Always read what the agent will do before clicking "Continue"
4. **Two Modes for Different Tasks**: agent mode for actions, ask mode for learning
5. **Free Tiers Exist**: Many Azure services have Free tiers for learning (F1 App Service is $0/month)
6. **Cleanup is Mandatory**: Always delete resources after practicing to avoid charges

---

## What's Next?

**[Chapter 2: Advanced Prompt Patterns](../02-cli-mastery/README.md)**

Now that you understand the basic workflow, you'll learn advanced prompt patterns to generate complex multi-step deployments efficiently.
