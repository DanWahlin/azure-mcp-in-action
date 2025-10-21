# Chapter 1: Your First AI-Generated Azure Deployment

**Title**: From Prompt to Production: Your First App Service
**Focus**: Azure MCP direct resource creation with verification workflow
**Prerequisites**: Completed [Course Setup](../00-course-setup/README.md)

---

## Learning Objectives

- ✅ Use Azure MCP to query existing resources (read-only practice)
- ✅ Understand Azure MCP's direct resource creation capabilities
- ✅ Use Azure MCP to create your first Azure web app
- ✅ Verify deployment success in Azure Portal and Azure CLI
- ✅ Learn command generation for educational purposes
- ✅ Clean up resources using Azure MCP
- ✅ Understand cost implications before deployment

## Real-World Scenario

> Your team needs a quick demo environment for a client presentation tomorrow. Instead of spending hours reading Azure documentation, you'll use GitHub Copilot Agent Mode to generate and execute deployment commands through natural language prompts. You'll deploy a simple Node.js app to Azure App Service using the Free tier.

## Why This Chapter Matters

This chapter teaches the fundamental workflow you'll use throughout the course: **Generate → Approve → Execute → Verify**. You'll see how Agent Mode generates infrastructure code, asks for your approval, executes deployment commands, and then you verify the results in Azure Portal and Azure CLI. This pattern ensures you understand what's being created while leveraging AI to accelerate deployment.

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

**Cost Estimate**: $0 (using Free tier)
**Deployment Time**: ~5 minutes
**Cleanup Time**: ~1 minute

---

## Part 2: Practice Read-Only Queries (Safe Learning)

Before creating resources, let's practice querying Azure safely:

### Exercise: Query Existing Resources

**Step 1: Activate Agent Mode**
```
1. Open GitHub Copilot Chat (Cmd+Shift+I or Ctrl+Shift+I)
2. Select "Agent" from the mode dropdown at the bottom
```

**Step 2: Query Your Subscription**
```
Use these prompts in Agent Mode:

List all resource groups in my subscription
Show all App Services in East US region
What storage accounts exist in my subscription?
```

**What happens**: Agent Mode queries your subscription and returns results - no resources are created. Verify the results match what you see in Azure Portal.

### Cost Validation (Ask Questions)

**Step 1: Switch to Ask Mode**
```
1. In GitHub Copilot Chat, select "Ask" from the mode dropdown
```

**Step 2: Ask Questions with @azure**
```
@azure What is the monthly cost of an F1 App Service plan?
@azure How many free App Services can I have per subscription?
@azure What's included in the Azure Free tier?
```

**Expected**: Detailed answers about pricing and limits (F1 is $0/month)

---

## Part 3: Create Resources with Agent Mode

Now let's use Agent Mode to generate and execute deployment commands:

### Activate Agent Mode

```
1. In GitHub Copilot Chat, select "Agent" from the mode dropdown
```

### Prompt to Agent

```
Create the following Azure resources:
1. Resource group named learning-rg-[YOUR-INITIALS] in East US
2. App Service plan with Free tier (F1 SKU) for Linux
3. Node.js LTS web app named demo-app-[YOUR-INITIALS]-[DATE]

Requirements:
- Use secure defaults (HTTPS only)
- Add tags: environment=learning, course=azure-copilot, chapter=01
- Ensure all prerequisites are created in correct order
```

### What Happens in Agent Mode

The workflow will be:
1. **Generate**: Agent generates infrastructure code (Bicep templates or Azure CLI commands)
2. **Approve**: Agent shows "Continue?" button - review the code before clicking
3. **Execute**: Agent runs commands in your terminal
4. **Confirm**: Commands create the actual Azure resources
5. **Report**: Agent confirms what was created
6. Return confirmation with resource details

---

## Part 4: Verify Resource Creation

**CRITICAL**: Always verify resources were created correctly!

### Method 1: Azure Portal Verification

1. Open [Azure Portal](https://portal.azure.com)
2. Navigate to **Resource Groups**
3. Find `learning-rg-[YOUR-INITIALS]`
4. Verify you see:
   - App Service plan (Free tier F1)
   - Web App (Node.js LTS runtime)
   - Tags are applied correctly

### Method 2: Azure CLI Verification

```bash
# Verify resource group
az group show --name learning-rg-dw --output table

# Verify App Service plan
az appservice plan show \
  --name demo-plan-dw \
  --resource-group learning-rg-dw \
  --query "{Name:name, SKU:sku.name, Location:location}" \
  --output table

# Verify web app
az webapp show \
  --name demo-app-dw-20241019 \
  --resource-group learning-rg-dw \
  --query "{Name:name, URL:defaultHostName, State:state, Runtime:siteConfig.linuxFxVersion}" \
  --output table
```

### Method 3: Azure MCP Query

```
Show details of web app demo-app-dw-20241019
List all resources in resource group learning-rg-dw
What's the status of my App Service plan demo-plan-dw?
```

---

## Part 5: Deploy Sample Application

Now let's deploy a sample Node.js application to the web app:

### Prompt to Azure MCP

```
Deploy the sample Node.js Hello World app from Azure samples
(https://github.com/Azure-Samples/nodejs-docs-hello-world)
to my web app demo-app-dw-20241019 in resource group learning-rg-dw
```

**Azure MCP will configure the deployment source and trigger the deployment.**

### Verify Deployment

1. **Azure Portal**: Navigate to your web app → Click "Browse" button
2. **Direct URL**: Visit `https://demo-app-dw-20241019.azurewebsites.net`
3. **Expected**: You should see "Hello World!" displayed

### Monitor Deployment (Optional)

```bash
# Watch deployment logs in real-time
az webapp log tail \
  --name demo-app-dw-20241019 \
  --resource-group learning-rg-dw
```

---

## Part 6: Learning Exercise - Command Generation

**Optional**: See how Azure MCP can generate commands for learning purposes:

### Prompt

```
#azure_generate_azure_cli_command
Generate the Azure CLI commands to create:
1. Resource group in East US
2. Free tier App Service plan for Linux
3. Node.js web app

Show me the commands I would run manually.
```

### Why This Is Useful

- **Learning CLI syntax**: Understand Azure CLI structure
- **Creating scripts**: Build automation scripts
- **Documentation**: Document infrastructure as code
- **Troubleshooting**: See exact commands for manual execution

**Note**: In this course, we primarily use Azure MCP's direct creation capability. Command generation is a secondary learning tool.

---

## Part 7: Cleanup (CRITICAL)

**⚠️ IMPORTANT**: Complete this cleanup to avoid unexpected Azure charges (even though F1 is free, it's good practice!)

### Cleanup Using Azure MCP

```
Delete resource group learning-rg-dw and all resources inside it
```

**Azure MCP will directly delete the resource group and all contained resources.**

### Verify Deletion

After Azure MCP completes the deletion, verify using Azure CLI:

```bash
# Verify resource group is gone
az group list --output table | grep learning-rg
# Should return nothing

# Or use Azure MCP to verify
List all resource groups in my subscription
# learning-rg-dw should not appear
```

### Alternative: Manual Cleanup with Azure CLI

If needed, you can also delete manually:

```bash
# List what will be deleted
az resource list --resource-group learning-rg-dw --output table

# Delete resource group
az group delete --name learning-rg-dw --yes --no-wait

# Verify deletion
az group list --output table | grep learning-rg
```

---

## Assignment

Use Azure MCP to complete these tasks:

1. Create a Python 3.11 web app using the same workflow
2. Use a different region (West US or your closest region)
3. Deploy sample Python code from Azure samples
4. Verify the deployment using all three methods (Portal, CLI, MCP query)
5. Calculate total deployment time
6. Clean up all resources using Azure MCP

### Success Criteria

- ✅ Activated Agent Mode in GitHub Copilot Chat
- ✅ Used Agent Mode to generate and execute deployment commands
- ✅ Reviewed code before clicking "Continue" buttons
- ✅ Successfully deployed Python web app
- ✅ App accessible via HTTPS URL
- ✅ Verified deployment using Portal, CLI, and Agent queries
- ✅ Cleaned up all resources using Agent Mode
- ✅ Cost remained $0 (Free tier)
- ✅ Understand the Generate → Approve → Execute → Verify workflow

---

## Key Takeaways

1. **Agent Mode Workflow**: Generate code → Approve with "Continue" → Execute commands → Verify results
2. **Verification is Critical**: Always verify resources using Portal, Azure CLI, and Agent queries
3. **Review Before Approving**: Always read what the agent will do before clicking "Continue"
4. **Two Modes for Different Tasks**: Agent Mode for actions, Ask Mode for learning
5. **Free Tiers Exist**: Many Azure services have Free tiers for learning (F1 App Service is $0/month)
6. **Cleanup is Mandatory**: Always delete resources after practicing to avoid charges

---

## What's Next?

**[Chapter 2: CLI Command Mastery](../02-cli-mastery/README.md)**

Now that you understand the basic workflow, you'll learn advanced prompt patterns to generate complex multi-step deployments efficiently.
