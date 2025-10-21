# Chapter 0: Course Setup and Safety Fundamentals

**Title**: Setting Up for Safe, Cost-Effective Azure Learning
**Focus**: Installation, configuration, cost management, and security baseline
**Prerequisites**: Computer with VS Code, valid email for Azure account

---

## Learning Objectives

- ✅ Create an Azure free account with $200 credit and billing protection
- ✅ Install and configure GitHub Copilot for Azure extension (provides Azure MCP and more)
- ✅ Set up cost alerts and spending limits
- ✅ Establish security baseline with least-privilege principles
- ✅ Understand Azure MCP interaction modes and when to use each
- ✅ Test your setup with first AI-generated commands
- ✅ Create emergency cleanup procedures

## Why This Chapter Matters

> Before writing a single line of infrastructure code, you need guardrails. This chapter sets up financial protection (cost alerts), security defaults (managed identities), and emergency procedures (cleanup scripts).

## Real-World Scenario

> You've been asked to explore Azure for your company's upcoming cloud migration. Management has approved a $100 learning budget, but they're concerned about surprise bills and security issues. You need to set up a safe learning environment where you can experiment with Azure MCP to create resources, but with strict cost controls and the ability to quickly clean up everything if needed.

---

## Part 1: Azure Account Setup

### Choose Your Azure Subscription

You have two options for this course:

#### Option A: Use an Existing Azure Subscription ✅ RECOMMENDED if you have one

- Skip to "Cost Management Configuration" below
- Use your existing subscription for all course exercises
- Set up course-specific resource group to keep learning resources separate
- Configure billing alerts for the course budget

#### Option B: Create a Free Azure Account ✅ RECOMMENDED if you're new to Azure

- Perfect for learning and exploration
- No charges during free trial period ($200 credit)
- Continue with setup steps below

### Free Tier Benefits (Option B)

- $200 credit for first 30 days
- 12 months of free services (App Service, Functions, Storage, etc.)
- Always-free services (Azure Active Directory, etc.)

### Setup Steps (Option B only)

1. Navigate to [azure.microsoft.com/free](https://azure.microsoft.com/free)
2. Create account (requires credit card for verification, but won't charge)
3. Complete phone and identity verification
4. Access Azure Portal at [portal.azure.com](https://portal.azure.com)

### Cost Management Configuration (BOTH options)

```
⚠️ Set up billing alerts BEFORE creating any resources

1. Navigate to: Cost Management + Billing
2. Create budget: $10 (alert at 50%, 80%, 100%)
3. Create budget: $50 (alert at 80%, 100%)
4. Create budget: $100 (alert at 90%, 100%)
5. Set up email + SMS alerts (dual notification)

Why this matters:
- Protects you from unexpected charges
- Alerts you if you accidentally leave resources running
- Helps track course spending vs other Azure usage
```

### Create Course Resource Group

Create a dedicated resource group to keep all your course resources organized and easy to clean up.

**Naming Convention**: `azure-copilot-course-[your-initials]`
**Region**: Choose closest to you (e.g., eastus, westus, westeurope)

#### Method 1: Azure Portal

1. Go to [portal.azure.com](https://portal.azure.com)
2. Click **Resource groups** in the left menu (or search for it)
3. Click **+ Create** at the top
4. Fill in the form:
   - **Subscription**: Select your subscription
   - **Resource group name**: `azure-copilot-course-[your-initials]` (e.g., `azure-copilot-course-dw`)
   - **Region**: Select your closest region (e.g., East US, West Europe)
5. Click **Review + create**
6. Click **Create**

#### Method 2: Azure CLI (Command Line)

```bash
# Login to Azure (if not already logged in)
az login

# Create the resource group
az group create \
  --name azure-copilot-course-[your-initials] \
  --location eastus

# Verify it was created
az group show --name azure-copilot-course-[your-initials]
```

**Tip**: Use the same region throughout the course for better performance and lower data transfer costs.

---

## Part 2: GitHub Copilot for Azure Installation

### Prerequisites

- VS Code installed
- [GitHub Copilot](https://github.com/features/copilot) subscription (free or paid)
- [GitHub Copilot for Azure](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azure-github-copilot) extension
- [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) installed (recommended)

### Installation Steps

1. Open VS Code
2. Go to Extensions (Cmd+Shift+X / Ctrl+Shift+X)
3. Search for "GitHub Copilot for Azure"
4. Install the extension
5. Sign in to Azure when prompted
6. Authorize GitHub Copilot for Azure to access your account

### What You Get

The GitHub Copilot for Azure extension provides:

**Agent Mode Capabilities:**
- Create and manage Azure resources with natural language
- Deploy applications and infrastructure
- Configure security and networking
- Troubleshoot issues and optimize resources
- Automatic tool selection based on your prompts
- Generate and execute Azure CLI commands, Bicep, and Terraform templates

**Ask Mode Capabilities:**
- Query Microsoft Learn documentation with `@azure`
- Get architectural guidance and best practices
- Compare Azure services and pricing
- Learn Azure concepts and terminology

**Behind the Scenes:**
- Azure MCP (Model Context Protocol) tools automatically selected by GitHub Copilot agent mode
- No need to memorize specific tool commands
- Use natural language with "Azure" in your prompts

### Verification

```
Open GitHub Copilot in "Ask" mode (change the drop-down to "Ask" at the bottom of the chat panel if needed)
Try this prompt: "@azure list my subscriptions"
Expected: You should see your Azure subscription details
```

### How to Access Azure MCP

Throughout this course, you'll interact with Azure MCP through **GitHub Copilot Chat** in VS Code:

**Opening GitHub Copilot Chat**:
- **Keyboard shortcut**: `Cmd+Shift+I` (macOS) or `Ctrl+Shift+I` (Windows/Linux)
- **Or**: Click the Copilot icon in the Activity Bar → Open Chat

---

## Part 2a: How to Use GitHub Copilot for Azure - Two Interaction Modes

GitHub Copilot for Azure supports two modes, each optimized for different tasks:

### Agent Mode (Primary)

**When to use**: Creating, deploying, managing, or troubleshooting Azure resources

**How to activate**:
1. Open GitHub Copilot Chat in VS Code (`Cmd+Shift+I` or `Ctrl+Shift+I`)
2. Click the mode dropdown at the bottom of the chat panel
3. Select **Agent**

**How to use**: Type natural language prompts with "Azure" somewhere in the prompt. GitHub Copilot automatically selects the right Azure tools.

**Example**:
```
Create a storage account named mystorageacct in East US using Standard_LRS
with blob public access disabled and HTTPS-only enabled
```

**What happens**:
1. Agent generates infrastructure-as-code (Bicep templates, Azure CLI commands, etc.)
2. Agent asks for your approval with a "Continue" button
3. After approval, agent automatically executes terminal commands
4. Commands create/modify Azure resources in your subscription
5. Agent reports success and shows what was created

**Important**: You'll see "Continue" buttons before major actions. Always review what the agent plans to do before clicking Continue.

---

### Ask Mode (For Learning)

**When to use**: Getting Azure guidance, comparing services, learning best practices

**How to activate**:
1. Open GitHub Copilot Chat in VS Code
2. Click the mode dropdown at the bottom of the chat panel
3. Select **Ask**

**How to use**: Start prompts with `@azure` to scope questions to Azure

**Example**:
```
@azure What's the difference between Azure Container Apps and Azure Kubernetes Service?
@azure What App Service tier should I use for 10,000 requests/day?
@azure How do I choose between SQL Database and Cosmos DB?
```

**What happens**: Copilot provides explanations, comparisons, and recommendations. No code generation or resource creation.

---

### Quick Reference: When to Use Each Mode

| Task | Mode | How to Use |
|------|------|------------|
| Create resources | Agent | Natural language prompt with "Azure" |
| Deploy applications | Agent | Natural language prompt with "Azure" |
| Update resources | Agent | Natural language prompt with "Azure" |
| Delete resources | Agent | Natural language prompt with "Azure" |
| Troubleshoot issues | Agent | Natural language prompt with "Azure" |
| Get Azure advice | Ask | `@azure What's the difference between...?` |
| Compare services | Ask | `@azure Should I use X or Y for...?` |
| Learn best practices | Ask | `@azure What are best practices for...?` |

---

### Understanding the Agent Mode Workflow

**The complete workflow looks like this**:

```
You: "Create an Azure storage account in East US"
  ↓
Agent: Analyzes request, generates Bicep template
  ↓
Agent: Shows preview and asks "Continue?"
  ↓
You: Review and click "Continue"
  ↓
Agent: Executes `az deployment create...` in terminal
  ↓
Terminal: Creates actual Azure resources
  ↓
Agent: Reports success, shows resource details
```

**Key Points**:
- Agent mode generates code AND executes it (with your approval)
- You control when actions happen via "Continue" buttons
- Agent automatically selects the right Azure tools based on your prompt

---

## Part 3: Understanding How GitHub Copilot for Azure Works

### ⚠️ CRITICAL CONCEPT: How Agent Mode Creates Resources

GitHub Copilot for Azure in **Agent Mode** creates Azure resources through a **Generate → Approve → Execute** workflow. Here's what actually happens:

1. **Generate**: Agent creates infrastructure-as-code (Bicep, Terraform, CLI commands)
2. **Approve**: You review and click "Continue" buttons to approve actions
3. **Execute**: Agent runs terminal commands that create resources in Azure
4. **Verify**: You confirm resources were created correctly

**This is powerful and requires understanding the approval workflow.**

### The Agent Mode Workflow

```
You: "Create an Azure storage account named mystorageacct in East US"
  ↓
Agent (in Agent Mode): Analyzes request, generates Bicep template
  ↓
Agent: Shows you the template and asks "Continue?"
  ↓
You: Review the code and click "Continue"
  ↓
Agent: Executes `az deployment create...` in your terminal
  ↓
Terminal Commands: Create actual Azure resources
  ↓
You: Verify in Azure Portal and Azure CLI
  ↓
Resources: Live and running in your subscription
```

### What Agent Mode Can Do

When you're in Agent Mode with "Azure" in your prompt, the agent can:

**Resource Management**
```
Create a storage account named mystorageacct in East US
Deploy a Node.js web app with B1 tier
Update my app service to use Node 22
Delete resource group my-test-rg
```

**Querying and Information**
```
List all AKS clusters in my subscription
Show me all storage accounts in East US
What resources are in my resource group?
```

**Troubleshooting**
```
Why is my app service slow?
My web app returns 500 errors - help me troubleshoot
Investigate high costs in my subscription
```

**Learning and Questions** (Switch to Ask Mode with `@azure` for better results)
```
@azure What's the difference between AKS and Container Apps?
@azure How do I choose the right App Service tier?
@azure What are best practices for securing storage accounts?
```

### Verification Methods

After agent mode creates resources, always verify:

**Method 1: Azure Portal** (Visual Confirmation)
```
1. Open the [Azure Portal](https://portal.azure.com)
2. Navigate to Resource Group
3. Verify resource exists and is running
4. Check configuration settings
```

**Method 2: Azure CLI** (Programmatic Verification)
```bash
# Verify resource group
az group show --name my-resource-group

# Verify storage account
az storage account show --name mystorageacct

# List all resources in a group
az resource list --resource-group my-resource-group --output table
```

**Method 3: Agent Mode Query** (Quick Check)
```
List all resources in resource group my-resource-group
Show details of storage account mystorageacct
```

### Course Convention

- **All Chapters**: Use Agent Mode for creating and managing resources
- **All Chapters**: Use Ask Mode (with `@azure`) for learning and questions
- Always verify resources after creation (Portal, CLI, or Agent queries)
- Always review what an Azure MCP tool will do before clicking "Continue" in agent mode
- Practice safe approval habits in every chapter

---

## Part 4: Understanding Model Context Protocol (MCP)

### What is MCP?

Model Context Protocol is an open standard for connecting AI systems to tools and data sources. Think of it like USB-C for AI—a universal connector that works across different tools and platforms.

### MCP in GitHub Copilot for Azure

- GitHub Copilot for Azure implements MCP under the hood
- You interact primarily through **direct natural language prompts** (Mode 1: Direct Resource Creation)
- You can also use @azure for questions (Mode 2) or #azure_generate_azure_cli_command for learning CLI syntax (Mode 3)
- MCP handles the communication between Copilot and Azure APIs
- This abstraction makes Azure expertise accessible through natural language

### Why This Matters

- **Portability**: Skills transfer to other MCP-enabled tools
- **Consistency**: Same patterns work across Azure services
- **Future-proof**: MCP is becoming an industry standard
- **Extensibility**: More Azure tools will support MCP over time

### What You Don't Need to Know

- MCP protocol details (abstracted away)
- JSON-RPC specifications (handled automatically)
- Server implementation (GitHub Copilot for Azure handles this)

---

## Part 5: First Hands-On Exercise

### Exercise 1: Practice Agent Mode with Queries

Let's start with safe query operations that don't create any resources.

#### Step 1: Activate Agent Mode

```
1. Open GitHub Copilot Chat (`Cmd+Shift+I` or `Ctrl+Shift+I`)
2. Click the mode dropdown at the bottom of the chat panel
3. Select "Agent"
```

#### Step 2: Query Your Subscription

```
Use this prompt in Agent Mode:

List all resource groups in my Azure subscription
```

**What happens**: Agent mode will query your Azure subscription and return the results.

**Tool limit exceeded error?**: If you see a message about tool limits, select the `tools` icon at the bottom of the chat panel and deselect any unnecessary tools.

#### Step 3: Review the Results

The agent will show you:
- Resource group names
- Locations
- Tags (if any)
- Subscription information

#### Step 4: Verify with Azure CLI

```bash
az group list --output table
```

Both methods should show the same resources!

**Key Learning**: Agent mode can query Azure resources without needing `#azure_generate_azure_cli_command` or other tool prefixes.

---

### Exercise 2: Practice Additional Agent Mode Queries

Try these safe query prompts in Agent Mode:

```
List all storage accounts in my subscription

Show details of resource group [YOUR-RG-NAME]

What App Services are running in East US?

Show me all resources tagged with environment=learning
```

**These queries don't create or modify anything - perfect for learning!**

**What to notice**:
- Agent automatically selects the right Azure tools
- You just use natural language with "Azure" context
- No need for `#` or `@` prefixes in Agent mode

---

### Exercise 3: Practice Ask Mode

Now let's try Ask Mode for learning and guidance.

#### Step 1: Switch to Ask Mode

```
1. In GitHub Copilot Chat, click the mode dropdown
2. Select "Ask"
```

#### Step 2: Ask Questions with @azure

```
@azure What is the difference between a resource group and a subscription?

@azure What's the cost of Azure App Service B1 tier?

@azure Should I use AKS or Container Apps for microservices?

@azure What are best practices for securing storage accounts?
```

**Expected**: Detailed explanations and architectural guidance with no code generation or execution.

**Key Learning**: Ask mode with `@azure` is for learning, not for creating resources.

---

### Exercise 4: Understanding the Difference

Practice switching between modes to understand when to use each:

**Agent Mode** (for actions):
```
Mode: Agent
Prompt: List all resource groups in my subscription
Result: Executes query and returns results
```

**Ask Mode** (for learning):
```
Mode: Ask
Prompt: @azure What is a resource group?
Result: Explanation only, no execution
```

---

## Assignment: Build Your Personal Setup Checklist

### Requirements

- [ ] Azure account created with $200 credit activated
- [ ] Billing alerts configured ($10, $50, $100 thresholds)
- [ ] GitHub Copilot for Azure extension installed and authenticated
- [ ] Azure CLI installed and logged in
- [ ] Course resource group created with proper naming
- [ ] Emergency cleanup script created and tested (on empty resource group)
- [ ] Security checklist downloaded and reviewed
- [ ] Successfully used Agent Mode to query Azure resources
- [ ] Successfully used Ask Mode with @azure to get guidance
- [ ] Understand how to switch between Agent and Ask modes
- [ ] Cost Management dashboard bookmarked

### Bonus Challenges

1. Set up Azure mobile app for push notifications on spending
2. Create a custom tag taxonomy for your learning projects
3. Use Agent Mode to generate a list of all resources and their estimated costs
4. Configure Azure Key Vault for storing any secrets you'll use
5. Enable Azure Advisor recommendations for your subscription

### Success Criteria

- ✅ Can use Agent Mode to query and manage Azure resources
- ✅ Can use Ask Mode with @azure to get guidance and learn
- ✅ Understand the difference between Agent Mode and Ask Mode
- ✅ Know how to activate each mode in GitHub Copilot Chat
- ✅ Have cost protection in place (will receive alerts before overspending)
- ✅ Have security defaults configured
- ✅ Have cleanup scripts ready to use
- ✅ Understand the Generate → Approve → Execute → Verify workflow

---

## Common Mistakes and Troubleshooting

### Mistake #1: Skipping billing alerts

- **Symptom**: Unexpected charges at end of month
- **Fix**: Stop everything and set up alerts NOW (see Part 5)

### Mistake #2: Using production-like names

- **Bad**: `--name my-app` (too generic)
- **Good**: `--name learning-app-dw-20241019` (unique, identifiable)

### Mistake #3: Forgetting to add tags

- **Symptom**: Can't find your resources later, difficult cleanup
- **Fix**: Use the tagging template from Part 5 for EVERY resource

### Mistake #4: Not testing cleanup scripts

- **Symptom**: Resources left running, unexpected costs
- **Fix**: Test your cleanup script on an empty resource group first

### Mistake #5: Not verifying resource creation

- **Symptom**: Unsure if resources were created correctly, hard to troubleshoot
- **Fix**: Always verify in Azure Portal and Azure CLI after agent mode creates resources

### Mistake #6: Clicking "Continue" without reviewing

- **Symptom**: Resources created that you didn't intend, unexpected configurations
- **Fix**: Always read what the agent plans to do before clicking "Continue"

### Mistake #7: Using the wrong mode

- **Symptom**: Getting explanations when you wanted actions, or vice versa
- **Fix**: Use Agent Mode for actions, Ask Mode (with @azure) for learning

---

## Key Takeaways

1. **Safety First**: Cost alerts and cleanup scripts aren't optional
2. **Two Modes**: Agent Mode for actions, Ask Mode for learning
3. **Understand the Workflow**: Generate → Approve ("Continue") → Execute → Verify
4. **Agent Mode Auto-Selects Tools**: Just use natural language with "Azure" context
5. **Tags Are Your Friend**: Every resource needs proper tags
6. **Security by Default**: Use managed identities, private endpoints, HTTPS
7. **Test Cleanup Scripts**: Practice deleting resources safely
8. **Review Before Approving**: Always read what the agent will do before clicking "Continue"

---

## What's Next?

**[Chapter 1: Your First AI-Generated Deployment](../01-first-deployment/README.md)**

Now that your environment is safe and secure, you'll deploy your first Azure resource using Agent Mode. You'll learn the complete Generate → Approve → Execute → Verify workflow.
