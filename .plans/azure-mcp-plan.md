# Azure MCP in Action - Course Plan

## Course Overview

**Title**: Azure Infrastructure with AI Assistance
**Subtitle**: Master Azure Deployments Using GitHub Copilot for Azure
**Target Audience**: Developers and DevOps engineers new to AI-assisted Azure infrastructure
**Platform**: VS Code with GitHub Copilot for Azure extension
**Format**: Hands-on prompt engineering and infrastructure deployment (hybrid approach)

> **Course Model**: This course follows the same structure and teaching philosophy as [LangChain.js for Beginners](https://github.com/danwahlin/langchainjs-for-beginners) - adapted for Azure deployment and infrastructure management rather than AI application development. The repository structure, chapter organization, and hands-on learning approach are mirrored from that successful course.

> **⚠️ Important Clarification**: This course teaches AI-assisted Azure development, not fully automated deployment. GitHub Copilot for Azure generates Azure CLI commands, Bicep templates, and Terraform configurations that you validate and execute manually. This "generate → validate → execute" workflow ensures safety, learning, and control.

## Course Philosophy

GitHub Copilot for Azure is your AI pair programmer for Azure infrastructure. Instead of memorizing complex Azure CLI commands, wrestling with documentation, or writing infrastructure templates from scratch, you'll learn to leverage AI assistance to accelerate your Azure development workflow.

**What You'll Actually Learn**:

1. **Prompt Engineering for Infrastructure**
   - Craft effective prompts to generate accurate Azure CLI commands
   - Request Bicep and Terraform templates through natural language
   - Learn patterns for asking the right questions

2. **AI-Assisted Code Generation**
   - Generate deployment commands with `#azure_generate_azure_cli_command`
   - Create infrastructure-as-code templates automatically
   - Produce diagnostic and troubleshooting scripts

3. **Validation and Safety**
   - Review AI-generated code before execution
   - Use `--dry-run` flags and syntax validation
   - Estimate costs before creating resources
   - Implement security best practices

4. **Manual Execution with Confidence**
   - Execute validated commands safely
   - Troubleshoot deployment issues with AI assistance
   - Monitor resource creation and configuration
   - Clean up resources to avoid unexpected costs

5. **Documentation Discovery**
   - Query Microsoft Learn with `#azure_query_learn`
   - Find relevant examples and best practices
   - Compare Azure services and architectures
   - Stay current with Azure updates

**Teaching Approach**:
- **Generate → Validate → Execute workflow**: Every example follows this safe pattern
- **Real-world scenarios**: Each chapter solves actual deployment challenges
- **Progressive skill building**: From simple commands to complex multi-service architectures
- **Cost and security first**: Every chapter includes cost estimation and cleanup scripts
- **Hands-on learning**: You execute real deployments (with safety guardrails)
- **Prompt pattern library**: Reusable templates for common infrastructure tasks

**What This Course Is NOT**:
- ❌ **Not fully automated deployment**: You validate and execute code manually (by design)
- ❌ **Not a replacement for Azure knowledge**: You still need to understand Azure basics
- ❌ **Not hands-off infrastructure**: You're in control of every deployment decision
- ❌ **Not production-ready without review**: AI-generated code requires validation

**What This Course IS**:
- ✅ **AI-accelerated Azure development**: Generate code 10x faster than manual writing
- ✅ **Safe learning environment**: Validate before executing, cleanup after practicing
- ✅ **Prompt engineering mastery**: Learn patterns that work across Azure services
- ✅ **Infrastructure-as-code foundations**: Build reusable Bicep/Terraform templates
- ✅ **Production-ready skills**: Learn workflows used by professional Azure developers

---

## Repository Structure

```
Azure-MCP-for-Beginners/
├── 00-course-setup/                    # Safety, cost management, security baseline
├── 01-first-deployment/                # Your first AI-generated Azure CLI commands
├── 02-cli-mastery/                     # Advanced command generation patterns
├── 03-bicep-templates/                 # Infrastructure-as-Code with Bicep
├── 04-terraform-basics/                # Getting started with Terraform generation
├── 05-simple-web-app/                  # Deploy Node.js app to App Service
├── 06-containerized-app/               # Deploy containers to AKS or Container Apps
├── 07-data-storage/                    # Databases and storage solutions
├── 08-diagnostics-troubleshooting/     # Using AI for debugging and optimization
├── 09-multi-service-architecture/      # Complex applications with multiple services
├── 10-production-ready-deployment/     # Complete production deployment capstone
├── prompts/                            # Reusable prompt pattern library
│   ├── ask-mode-patterns/              # Documentation and learning prompts
│   ├── agent-mode-patterns/            # Command and template generation
│   ├── by-service/                     # Service-specific prompt templates
│   └── advanced-patterns/              # Complex multi-service scenarios
├── scripts/                            # Validation and testing scripts
│   ├── validate-prompts.ts             # Test prompt outputs
│   ├── validate-commands.ts            # Verify Azure CLI syntax
│   ├── validate-templates.ts           # Check Bicep/Terraform validity
│   ├── cost-estimator.ts               # Calculate deployment costs
│   └── cleanup-checker.ts              # Verify resource cleanup
├── data/                               # Reference materials and samples
│   ├── sample-bicep-templates/         # Pre-built templates for comparison
│   ├── sample-terraform-configs/       # Reference Terraform configurations
│   ├── architecture-diagrams/          # Visual architecture references
│   ├── cost-estimation-spreadsheets/   # Cost calculator templates
│   ├── security-checklists/            # Per-service security requirements
│   └── troubleshooting-guides/         # Common errors and solutions
├── future/                             # Advanced topics (bonus content)
│   ├── 11-multi-region-deployments/    # Global architecture patterns
│   ├── 12-azure-devops-integration/    # CI/CD pipelines with AI
│   ├── 13-advanced-kubernetes/         # AKS production patterns
│   └── 14-cost-optimization-advanced/  # Enterprise cost management
├── .env.example                        # Azure credentials template
├── .gitignore                          # Git ignore patterns
├── CODE_OF_CONDUCT.md                  # Microsoft Open Source Code of Conduct
├── SECURITY.md                         # Security vulnerability reporting
├── MAINTAINERS.md                      # Course maintenance guidelines
├── GLOSSARY.md                         # Comprehensive term definitions
└── README.md                           # Course home page
```

Each chapter contains (mirroring [LangChain.js for Beginners](https://github.com/danwahlin/langchainjs-for-beginners) structure):
- `README.md` - Concepts, prompt patterns, and workflow examples
  - Real-world scenario introduction
  - Learning objectives with success criteria
  - Step-by-step generate → validate → execute examples
  - Cost estimation and free tier guidance
  - Security best practices
  - Troubleshooting common issues
  - Key takeaways and next steps

- `assignment.md` - Hands-on challenges with clear success criteria
  - Challenge description with real-world context
  - Requirements checklist
  - Starter prompts to guide learning
  - Expected outputs and validation steps
  - Common mistakes to avoid
  - Troubleshooting tips
  - Bonus challenges for advanced learners
  - Self-assessment rubric

- `prompts/` - Reusable prompt templates for the chapter
  - Ask mode prompts (documentation and learning)
  - Agent mode prompts (command and template generation)
  - Prompt variations for different scenarios
  - Example outputs showing expected results

- `solution/` - Complete solution examples with explanations
  - Full prompt sequences that achieve objectives
  - Generated code examples (CLI, Bicep, Terraform)
  - Architecture decisions explained
  - Alternative approaches discussed
  - Cost analysis and optimization notes

- `commands/` - Generated Azure CLI command examples
  - Validated and tested command sequences
  - Commented for learning purposes
  - Cleanup scripts included
  - Cost estimation annotations

- `templates/` - Generated infrastructure-as-code templates
  - Bicep templates with annotations
  - Terraform configurations (where applicable)
  - Parameter files and examples
  - Deployment instructions

- `images/` - Visual learning aids
  - Architecture diagrams
  - GitHub Copilot for Azure screenshots
  - Workflow illustrations
  - Azure Portal verification steps

---

## Chapter Breakdown

### Chapter 0: Course Setup and Safety Fundamentals

**Title**: Setting Up for Safe, Cost-Effective Azure Learning
**Focus**: Installation, configuration, cost management, and security baseline
**Estimated Time**: 90 minutes
**Prerequisites**: Computer with VS Code, valid email for Azure account

---

**Learning Objectives**:
- ✅ Create Azure free account with $200 credit and billing protection
- ✅ Install and configure GitHub Copilot for Azure extension
- ✅ Set up cost alerts and spending limits to avoid surprises
- ✅ Establish security baseline with least-privilege principles
- ✅ Understand agent mode vs Ask mode and when to use each
- ✅ Test your setup with first AI-generated commands
- ✅ Create emergency cleanup procedures

**Why This Chapter Matters**:
> Before writing a single line of infrastructure code, you need guardrails. This chapter sets up financial protection (cost alerts), security defaults (managed identities), and emergency procedures (cleanup scripts). These aren't optional—they're essential for safe learning.

---

**Part 1: Azure Account Setup**

**Choose Your Azure Subscription**:

You have two options for this course:

**Option A: Use an Existing Azure Subscription** ✅ RECOMMENDED if you have one
- Skip to "Immediate Safety Configuration" below
- Use your existing subscription for all course exercises
- Set up course-specific resource group to keep learning resources separate
- Configure billing alerts for the course budget

**Option B: Create a Free Azure Account** ✅ RECOMMENDED if you're new to Azure
- Perfect for learning and exploration
- No charges during free trial period ($200 credit)
- Continue with setup steps below

**Free Tier Benefits** (Option B):
- $200 credit for first 30 days
- 12 months of free services (App Service, Functions, Storage, etc.)
- Always-free services (Azure Active Directory, etc.)

**Setup Steps** (Option B only):
1. Navigate to [azure.microsoft.com/free](https://azure.microsoft.com/free)
2. Create account (requires credit card for verification, but won't charge)
3. Complete phone and identity verification
4. Access Azure Portal at [portal.azure.com](https://portal.azure.com)

**Immediate Safety Configuration** (BOTH options):
```
⚠️ CRITICAL: Set up billing alerts BEFORE creating any resources

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

**Create Course Resource Group**:
```bash
# This resource group will contain all your course deployments
# Naming: azure-copilot-course-[your-initials]
# Example: azure-copilot-course-dw
# Region: Choose closest to you (e.g., eastus, westus, westeurope)
```

**Cost Commitment for Course**:
- Estimated: $50-100 if using all chapters with paid tiers
- Can be completed for $0-20 by using Free tiers only
- Cleanup scripts provided to minimize costs

---

**Part 2: GitHub Copilot for Azure Installation**

**Prerequisites**:
- VS Code installed
- GitHub Copilot subscription (required)
- Azure CLI installed (recommended)

**Installation Steps**:
1. Open VS Code
2. Go to Extensions (Cmd+Shift+X / Ctrl+Shift+X)
3. Search for "GitHub Copilot for Azure"
4. Install the extension
5. Reload VS Code
6. Sign in to Azure when prompted
7. Authorize GitHub Copilot for Azure to access your account

**Extension**: [GitHub Copilot for Azure](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azure-github-copilot)

**What You Get**:
- `#azure_generate_azure_cli_command` - Generate Azure CLI commands
- `#azure_query_learn` - Query Microsoft Learn documentation
- `#azure_diagnose_resource` - Troubleshoot resource issues
- Bicep and Terraform template generation
- Contextual Azure suggestions and completions

**Verification**:
```
Open GitHub Copilot Chat in VS Code
Try this prompt: "@azure list my subscriptions"
Expected: You should see your Azure subscription details
```

---

**Part 3: Understanding agent mode vs ask mode**

**⚠️ CRITICAL CONCEPT**: How GitHub Copilot for Azure Actually Works

GitHub Copilot for Azure **generates code** (CLI commands, Bicep, Terraform) that you execute manually. It does **NOT** directly create Azure resources. This is by design for safety and learning.

**The Workflow**:
```
You: Describe what you want (prompt)
  ↓
AI: Generates Azure CLI commands or templates
  ↓
You: Review and validate the generated code
  ↓
You: Execute commands manually (with --dry-run first)
  ↓
Azure: Creates resources based on your executed commands
```

**agent mode** - For generating infrastructure code:
```
Examples:
#azure_generate_azure_cli_command Create storage account in East US
#azure_generate_azure_cli_command Deploy web app with Node.js runtime
#azure_diagnose_resource Investigate why my App Service is slow
```
**When to use**: Generating commands, templates, diagnostics

**ask mode** - For learning and questions:
```
Examples:
@azure What's the difference between AKS and Container Apps?
@azure How do I choose the right App Service tier?
@azure What are the cost implications of using Premium storage?
```
**When to use**: Conceptual questions, comparisons, learning

**Decision Tree**:
```
Do I need executable code? → Use agent mode (#azure_generate_azure_cli_command)
Am I asking a question? → Use ask mode (@azure)
Do I need troubleshooting? → Use agent mode (#azure_diagnose_resource)
Do I need documentation? → Use agent mode (#azure_query_learn)
```

**Course Convention**:
- All hands-on examples use **agent mode** tools
- Questions and explanations use **ask mode**
- Every prompt shows which mode to use
- Practice both modes in every chapter

---

**Part 4: Understanding Model Context Protocol (MCP)**

**What is MCP?**

Model Context Protocol is an open standard for connecting AI systems to tools and data sources. Think of it like USB-C for AI—a universal connector that works across different tools and platforms.

**MCP in GitHub Copilot for Azure**:
- GitHub Copilot for Azure implements MCP under the hood
- You interact through agent mode tools (e.g., `#azure_generate_azure_cli_command`)
- MCP handles the communication between Copilot and Azure APIs
- This abstraction makes Azure expertise accessible through natural language

**Why This Matters**:
- **Portability**: Skills transfer to other MCP-enabled tools
- **Consistency**: Same patterns work across Azure services
- **Future-proof**: MCP is becoming an industry standard
- **Extensibility**: More Azure tools will support MCP over time

**What You Don't Need to Know**:
- MCP protocol details (abstracted away)
- JSON-RPC specifications (handled automatically)
- Server implementation (GitHub Copilot for Azure handles this)

---

**Part 5: Safety and Cost Management Setup**

**Cost Management Dashboard Setup**:
```
1. Navigate to: Cost Management + Billing
2. Enable: Cost Analysis (shows current spending)
3. Enable: Cost Alerts (email + SMS notifications)
4. Set up: Daily cost review habit (check every morning)
5. Download: Azure mobile app for spending alerts
```

**Resource Tagging Strategy**:
```bash
# Every resource you create should have these tags:
--tags \
  course="azure-copilot-beginner" \
  chapter="01" \
  environment="learning" \
  auto-delete="true" \
  created-by="[your-name]"

# Why tags matter:
# - Easy identification of course resources
# - Bulk cleanup operations
# - Cost attribution and tracking
# - Compliance and governance
```

**Cleanup Script Template**:
```bash
#!/bin/bash
# cleanup-chapter-01.sh
# Run this after completing Chapter 1 to delete all resources

echo "⚠️  WARNING: This will DELETE all resources with chapter='01' tag"
echo "Press Ctrl+C to cancel, or Enter to continue..."
read

# List resources to be deleted
az resource list \
  --tag chapter=01 \
  --query "[].{Name:name, Type:type, ResourceGroup:resourceGroup}" \
  --output table

# Confirm deletion
echo ""
echo "Delete these resources? (yes/no)"
read confirmation

if [ "$confirmation" == "yes" ]; then
  # Delete tagged resources
  az resource list --tag chapter=01 --query "[].id" --output tsv | \
    xargs -I {} az resource delete --ids {} --verbose
  echo "✅ Cleanup complete"
else
  echo "❌ Cleanup cancelled"
fi
```

**Emergency Cleanup Procedure**:
```bash
# If you need to delete EVERYTHING immediately:

# 1. List all resource groups
az group list --output table

# 2. Delete course resource group (DANGER: irreversible!)
az group delete \
  --name azure-copilot-course-[your-initials] \
  --yes \
  --no-wait

# 3. Verify deletion
az group list --output table
# The course resource group should not appear

# This deletes ALL resources in that group
# Use only in emergencies or after course completion
```

---

**Part 6: Security Baseline Configuration**

**Security Principles for Course**:

1. **Least Privilege**
   - Use managed identities instead of passwords
   - Grant minimum required permissions
   - Never hardcode credentials

2. **Defense in Depth**
   - Private endpoints by default
   - Network security groups for VM access
   - Azure Key Vault for secrets

3. **Audit and Monitor**
   - Enable Azure Monitor for all resources
   - Set up security alerts
   - Review activity logs regularly

**Secure Defaults Template**:
```bash
# When creating resources, always include security settings:

# Example: Storage Account with secure defaults
az storage account create \
  --name mystorageaccount \
  --resource-group my-rg \
  --location eastus \
  --sku Standard_LRS \
  --allow-blob-public-access false \          # No public access
  --https-only true \                         # HTTPS only
  --min-tls-version TLS1_2 \                  # Modern TLS
  --enable-hierarchical-namespace false

# Example: Web App with secure defaults
az webapp create \
  --name my-web-app \
  --resource-group my-rg \
  --plan my-plan \
  --runtime "NODE:18-lts" \
  --assign-identity \                         # Managed identity
  --https-only true                           # HTTPS only
```

**Security Checklist** (use for every deployment):
- [ ] No hardcoded passwords or keys
- [ ] HTTPS-only enabled
- [ ] Public access disabled unless required
- [ ] Managed identities used for authentication
- [ ] Network security groups configured
- [ ] Azure Key Vault for sensitive data
- [ ] Monitoring and alerts enabled
- [ ] Tags for resource tracking

---

**Part 7: Development Environment Setup**

**Required Tools**:
```bash
# Azure CLI (command-line interface)
# macOS:
brew install azure-cli

# Windows:
winget install Microsoft.AzureCLI

# Linux:
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

# Verify installation:
az --version
az login
```

**Recommended Tools**:
```bash
# Bicep CLI (infrastructure-as-code)
az bicep install
az bicep version

# Terraform (alternative to Bicep)
# macOS:
brew install terraform

# Windows:
choco install terraform

# Verify:
terraform version
```

**VS Code Extensions**:
- GitHub Copilot for Azure (required)
- Azure Account
- Azure CLI Tools
- Bicep (for template editing)

---

**Part 8: First Hands-On Exercise**

**Exercise: Generate Your First Azure CLI Command**

**Step 1: Use agent mode to Generate a Command**
```
Open GitHub Copilot Chat
Use this prompt:

#azure_generate_azure_cli_command
List all resource groups in my subscription in table format
```

**Expected Output**:
```bash
az group list --output table
```

**Step 2: Validate the Command**
```
Look at the generated command. Does it:
- Use valid Azure CLI syntax? ✅
- Match what you asked for? ✅
- Include the table format? ✅
- Have any dangerous flags (--force, --yes)? ❌ (good!)
```

**Step 3: Execute the Command**
```bash
# Copy the generated command and run it:
az group list --output table

# Expected: You should see at least one resource group
# (the one you created earlier for the course)
```

**Step 4: Try ask mode**
```
Switch to ask mode in GitHub Copilot Chat:

@azure What is the difference between a resource group and a subscription?
```

**Expected**: Explanation of Azure hierarchy concepts

---

**Assignment: Build Your Personal Setup Checklist**

**Requirements**:
- [ ] Azure account created with $200 credit activated
- [ ] Billing alerts configured ($10, $50, $100 thresholds)
- [ ] GitHub Copilot for Azure extension installed and authenticated
- [ ] Azure CLI installed and logged in
- [ ] Course resource group created with proper naming
- [ ] Emergency cleanup script created and tested (on empty resource group)
- [ ] Security checklist downloaded and reviewed
- [ ] Successfully generated first Azure CLI command
- [ ] Successfully executed first command
- [ ] Cost Management dashboard bookmarked

**Bonus Challenges**:
1. Set up Azure mobile app for push notifications on spending
2. Create a custom tag taxonomy for your learning projects
3. Write a script that lists all resources and their estimated monthly costs
4. Configure Azure Key Vault for storing any secrets you'll use
5. Enable Azure Advisor recommendations for your subscription

**Success Criteria**:
- ✅ Can generate Azure CLI commands using agent mode
- ✅ Can ask questions using ask mode
- ✅ Have cost protection in place (will receive alerts before overspending)
- ✅ Have security defaults configured
- ✅ Have cleanup scripts ready to use
- ✅ Understand the generate → validate → execute workflow

---

**Common Mistakes and Troubleshooting**:

**Mistake #1: Skipping billing alerts**
- **Symptom**: Unexpected charges at end of month
- **Fix**: Stop everything and set up alerts NOW (see Part 5)

**Mistake #2: Using production-like names**
- **Bad**: `--name my-app` (too generic)
- **Good**: `--name learning-app-dw-20241019` (unique, identifiable)

**Mistake #3: Forgetting to add tags**
- **Symptom**: Can't find your resources later, difficult cleanup
- **Fix**: Use the tagging template from Part 5 for EVERY resource

**Mistake #4: Not testing cleanup scripts**
- **Symptom**: Resources left running, unexpected costs
- **Fix**: Test your cleanup script on an empty resource group first

**Mistake #5: Executing commands without validation**
- **Symptom**: Wrong resources created, hard to troubleshoot
- **Fix**: Always read generated commands before executing

---

**Key Takeaways**:

1. **Safety First**: Cost alerts and cleanup scripts aren't optional
2. **Understand the Workflow**: AI generates → You validate → You execute
3. **agent mode vs ask mode**: Know when to use each
4. **Tags Are Your Friend**: Every resource needs proper tags
5. **Security by Default**: Use managed identities, private endpoints, HTTPS
6. **Test Cleanup Scripts**: Practice deleting resources safely

---

**What's Next?**

**[Chapter 1: Your First AI-Generated Deployment](../01-first-deployment/README.md)**

Now that your environment is safe and secure, you'll deploy your first Azure resource using AI-generated commands. You'll learn the complete workflow from prompt to production.



---

## This file contains the corrected versions of all chapters reflecting how GitHub Copilot for Azure actually works

### Chapter 1: Your First AI-Generated Azure Deployment

**Title**: From Prompt to Production: Your First App Service
**Focus**: Complete generate → validate → execute workflow
**Estimated Time**: 60 minutes
**Prerequisites**: Completed Chapter 0

---

**Learning Objectives**:
- ✅ Generate Azure CLI commands using `#azure_generate_azure_cli_command`
- ✅ Validate generated commands for correctness and safety
- ✅ Execute commands with `--dry-run` flag first
- ✅ Deploy your first Azure web app
- ✅ Verify deployment success in Azure Portal
- ✅ Clean up resources to avoid costs
- ✅ Understand cost implications before deployment

**Real-World Scenario**:
> Your team needs a quick demo environment for a client presentation tomorrow. Instead of spending hours reading Azure documentation and constructing commands manually, you'll use GitHub Copilot for Azure to generate deployment code in minutes. You'll deploy a simple Node.js app to Azure App Service using the Free tier.

**Why This Chapter Matters**:
This chapter teaches the fundamental workflow you'll use throughout the course: AI generates infrastructure code, you validate it for safety and correctness, then execute it manually with full control. This pattern ensures you learn Azure while leveraging AI acceleration.

---

**Part 1: Understanding What You're Building**

**Target Architecture**:
```
Azure App Service (Node.js 18)
├── Free tier (F1 SKU) - $0/month
├── Linux-based runtime
├── Sample Hello World app
└── HTTPS enabled by default
```

**Cost Estimate**: $0 (using Free tier)
**Deployment Time**: ~5 minutes
**Cleanup Time**: ~1 minute

---

**Part 2: Generating Azure CLI Commands**

**Prompt (agent mode)**:
```
#azure_generate_azure_cli_command
Create a resource group named learning-rg-[YOUR-INITIALS] in East US,
then create an App Service plan with Free tier (F1 SKU) for Linux,
then create a Node.js 18 web app named demo-app-[YOUR-INITIALS]-[DATE].
Include all prerequisite resources and use secure defaults.
```

**Expected Output** (example):
```bash
# Step 1: Create resource group
az group create \
  --name learning-rg-dw \
  --location eastus \
  --tags environment=learning course=azure-copilot chapter=01

# Step 2: Create App Service plan
az appservice plan create \
  --name demo-plan-dw \
  --resource-group learning-rg-dw \
  --sku F1 \
  --is-linux

# Step 3: Create web app
az webapp create \
  --name demo-app-dw-20241019 \
  --resource-group learning-rg-dw \
  --plan demo-plan-dw \
  --runtime "NODE:18-lts" \
  --https-only true
```

---

**Part 3: Validating Generated Commands**

**Validation Checklist**:
- [ ] All commands use valid Azure CLI syntax
- [ ] Resource names are unique (include your initials + date)
- [ ] Region is specified correctly (eastus)
- [ ] SKU is Free tier (F1)
- [ ] Runtime matches requirement (NODE:18-lts)
- [ ] Commands are in correct dependency order
- [ ] Security flags are set (--https-only true)
- [ ] Tags are included for tracking
- [ ] No dangerous flags (--force, --yes without confirmation)

**Cost Validation (ask mode)**:
```
@azure What is the monthly cost of an F1 App Service plan?
Expected answer: $0/month (Free tier)
```

---

**Part 4: Executing with --dry-run First**

**Safety Step** (not all Azure CLI commands support --dry-run, but use `--output json` for validation):
```bash
# Validate resource group creation (list existing first)
az group list --query "[?name=='learning-rg-dw']" --output table

# If it doesn't exist, safe to proceed
```

---

**Part 5: Execute Commands Step-by-Step**

```bash
# Command 1: Create resource group
az group create \
  --name learning-rg-dw \
  --location eastus \
  --tags environment=learning course=azure-copilot chapter=01

# Verify success
az group list --output table | grep learning-rg

# Command 2: Create App Service plan
az appservice plan create \
  --name demo-plan-dw \
  --resource-group learning-rg-dw \
  --sku F1 \
  --is-linux

# Verify success
az appservice plan list --output table

# Command 3: Create web app
az webapp create \
  --name demo-app-dw-20241019 \
  --resource-group learning-rg-dw \
  --plan demo-plan-dw \
  --runtime "NODE:18-lts" \
  --https-only true

# Verify success and get URL
az webapp show \
  --name demo-app-dw-20241019 \
  --resource-group learning-rg-dw \
  --query "{Name:name, URL:defaultHostName, State:state}" \
  --output table
```

---

**Part 6: Deploy Sample Application**

**Generate Deployment Command (agent mode)**:
```
#azure_generate_azure_cli_command
Deploy sample Node.js Hello World app from Azure samples GitHub repo
to my web app demo-app-dw-20241019
```

**Execute Deployment**:
```bash
az webapp deployment source config \
  --name demo-app-dw-20241019 \
  --resource-group learning-rg-dw \
  --repo-url https://github.com/Azure-Samples/nodejs-docs-hello-world \
  --branch master \
  --manual-integration

# Monitor deployment
az webapp log tail \
  --name demo-app-dw-20241019 \
  --resource-group learning-rg-dw
```

---

**Part 7: Verification in Azure Portal**

1. Open [Azure Portal](https://portal.azure.com)
2. Navigate to Resource Groups → learning-rg-dw
3. Click on your web app
4. Click "Browse" to view the running app
5. Verify you see "Hello World!"

---

**Part 8: Cleanup (CRITICAL)**

**Generate Cleanup Command (agent mode)**:
```
#azure_generate_azure_cli_command
Delete all resources in resource group learning-rg-dw
```

**Execute Cleanup**:
```bash
# List what will be deleted
az resource list \
  --resource-group learning-rg-dw \
  --output table

# Delete resource group (this deletes everything inside)
az group delete \
  --name learning-rg-dw \
  --yes \
  --no-wait

# Verify deletion
az group list --output table | grep learning-rg
# Should return nothing
```

---

**Assignment**:

1. Deploy a Python 3.11 web app using the same workflow
2. Use a different region (West US or your closest region)
3. Deploy sample Python code from Azure samples
4. Document the complete command sequence
5. Calculate total deployment time
6. Clean up all resources

**Success Criteria**:
- ✅ Generated valid Azure CLI commands
- ✅ Validated all commands before execution
- ✅ Successfully deployed web app
- ✅ App accessible via HTTPS URL
- ✅ Verified deployment in Azure Portal
- ✅ Cleaned up all resources
- ✅ Cost remained $0 (Free tier)

---

**Key Takeaways**:

1. **AI Generates, You Execute**: GitHub Copilot for Azure creates commands, you run them
2. **Validate Everything**: Never blindly execute AI-generated code
3. **Free Tiers Exist**: Many Azure services have Free tiers for learning
4. **Cleanup is Mandatory**: Always delete resources after practicing
5. **Documentation Through Prompts**: Effective prompts are documentation

---

### Chapter 2: CLI Command Mastery

**Title**: Advanced Prompt Patterns for Azure CLI Generation
**Focus**: Prompt engineering techniques for complex commands
**Estimated Time**: 75 minutes
**Prerequisites**: Chapter 0-1

**Learning Objectives**:
- ✅ Master prompt engineering patterns for Azure CLI
- ✅ Generate complex multi-step deployment commands
- ✅ Handle conditional logic and error handling in commands
- ✅ Create reusable command templates
- ✅ Debug and troubleshoot generated commands
- ✅ Optimize commands for efficiency

**Real-World Scenario**:
> Your company is onboarding 10 new developers who each need identical development environments: storage account, key vault, and container registry. Instead of manually creating each environment, you'll use GitHub Copilot for Azure to generate a reusable script that provisions all resources with one command.

---

**Part 1: Basic Prompt Patterns**

**Pattern 1: Single Resource Creation**
```
#azure_generate_azure_cli_command
Create a [RESOURCE_TYPE] named [NAME] in [REGION] using [SKU/TIER]
with [SECURITY_OPTIONS]
```

**Example**:
```
#azure_generate_azure_cli_command
Create a storage account named learnstg2024 in East US using Standard_LRS
with blob public access disabled and HTTPS-only enabled
```

**Pattern 2: Resource with Dependencies**
```
#azure_generate_azure_cli_command
Create [RESOURCE] in [REGION] with [DEPENDENCIES].
Include all prerequisite resources. Use tags: [TAG_LIST]
```

**Pattern 3: Query and Filter**
```
#azure_generate_azure_cli_command
List all [RESOURCE_TYPE] in [SCOPE] where [CONDITION]
and display as [FORMAT]
```

---

**Part 2: Advanced Patterns**

**Pattern 4: Conditional Creation**
```
#azure_generate_azure_cli_command
Check if resource group [NAME] exists.
If not, create it in [REGION].
If yes, skip creation and continue.
```

**Pattern 5: Bulk Operations**
```
#azure_generate_azure_cli_command
Create 5 storage accounts in East US named storage-dev-01 through storage-dev-05
using Standard_LRS. Use a loop for efficiency.
```

**Pattern 6: Configuration Updates**
```
#azure_generate_azure_cli_command
Update web app [NAME] to use:
- Node.js 20 runtime
- Always On enabled
- Custom domain [DOMAIN]
- SSL from Key Vault
Generate commands in order with verification steps between each.
```

---

**Part 3: Error Handling and Validation Patterns**

**Pattern 7: Pre-flight Checks**
```
#azure_generate_azure_cli_command
Before creating AKS cluster, verify:
1. Subscription has enough quota
2. Region supports AKS
3. Required providers are registered
4. Service principal exists
Generate validation commands first, then creation commands.
```

**Pattern 8: Rollback Scripts**
```
#azure_generate_azure_cli_command
Create an App Service plan and web app.
Also generate a rollback script that deletes both if deployment fails.
```

---

**Part 4: Optimization Patterns**

**Pattern 9: Parallel Creation**
```
#azure_generate_azure_cli_command
Create 3 independent resources in parallel:
- Storage account in East US
- Key Vault in West US
- Container Registry in Central US
Use --no-wait flag for parallel execution.
```

**Pattern 10: Idempotent Operations**
```
#azure_generate_azure_cli_command
Create or update resource group named prod-rg in East US.
Generate command that succeeds whether group exists or not.
```

---

**Assignment**:

1. Create a script that provisions a complete dev environment
2. Include error handling and validation
3. Make it reusable with parameters
4. Add cleanup function
5. Test with 3 different configurations
6. Document prompt patterns used

**Success Criteria**:
- ✅ Generated complex multi-step commands
- ✅ Included error handling
- ✅ Commands are idempotent (can run multiple times safely)
- ✅ Script is parameterized and reusable
- ✅ All resources tagged properly
- ✅ Cleanup script works correctly

---

**Cleanup Using Azure MCP**

**⚠️ IMPORTANT**: Complete this cleanup to avoid unexpected Azure charges

This chapter had you create multiple resources for practicing prompt patterns. Clean them all up before proceeding to Chapter 3.

**Method 1: Use Azure MCP Prompt (RECOMMENDED)**

**Generate Cleanup Commands (agent mode)**:
```
#azure_generate_azure_cli_command
Delete all resources tagged with chapter=02 in my subscription
```

**Expected Commands** (verify before executing):
```bash
# List resources to be deleted
az resource list --tag chapter=02 --output table

# Delete tagged resources
az resource list --tag chapter=02 --query "[].id" --output tsv | \
  xargs -I {} az resource delete --ids {} --verbose
```

**Method 2: Manual Cleanup Commands** (if prompt fails or for direct execution)

```bash
# Step 1: List resources with chapter=02 tag
az resource list --tag chapter=02 --output table

# Step 2: Delete by tag
az resource list --tag chapter=02 --query "[].id" --output tsv | \
  xargs -I {} az resource delete --ids {} --verbose

# OR if you used a dedicated resource group:
# List what will be deleted
az resource list --resource-group [YOUR-CHAPTER-2-RG] --output table

# Delete entire resource group
az group delete --name [YOUR-CHAPTER-2-RG] --yes --no-wait
```

**Before You Delete**:
- [ ] Verify the list shows only Chapter 2 resources
- [ ] Confirm no production or important resources are listed
- [ ] Double-check resource names match what you created in this chapter

**Verify Deletion**:
```bash
# Check that tagged resources are gone
az resource list --tag chapter=02 --output table
# Should return empty

# Check billing
az consumption usage list --start-date $(date -d "7 days ago" +%Y-%m-%d)
```

---

### Chapter 3: Infrastructure-as-Code with Bicep

**Title**: AI-Generated Bicep Templates for Reproducible Deployments
**Focus**: Bicep template generation using GitHub Copilot for Azure
**Estimated Time**: 90 minutes
**Prerequisites**: Chapters 0-2

**Learning Objectives**:
- ✅ Understand Bicep vs Azure CLI commands
- ✅ Generate Bicep templates using GitHub Copilot for Azure
- ✅ Validate Bicep syntax automatically
- ✅ Deploy resources using Bicep templates
- ✅ Parameterize templates for reusability
- ✅ Export existing resources as Bicep

**Real-World Scenario**:
> Your team needs to deploy identical staging and production environments across 3 Azure regions. Azure CLI commands would require hundreds of lines and be error-prone. Instead, you'll use GitHub Copilot for Azure to generate a Bicep template that you can deploy to any region with just parameter changes.

---

**Part 1: Understanding Bicep vs CLI**

**When to Use Azure CLI**:
- One-off deployments
- Quick prototypes
- Administrative tasks
- Learning and exploration

**When to Use Bicep**:
- Repeatable deployments
- Multi-environment setups (dev/staging/prod)
- Complex architectures with dependencies
- Version-controlled infrastructure
- Team collaboration

---

**Part 2: Generating Your First Bicep Template**

**Prompt (agent mode)**:
```
Generate a Bicep template that creates:
- App Service plan (B1 SKU)
- Web app with Node.js 18 runtime
- Application Insights for monitoring
- Connection string configured automatically

Use parameters for app name and location.
Include outputs for app URL and instrumentation key.
```

**Expected Output** (abbreviated):
```bicep
@description('Name of the web app')
param appName string

@description('Location for all resources')
param location string = resourceGroup().location

resource appServicePlan 'Microsoft.Web/serverfarms@2022-03-01' = {
  name: '${appName}-plan'
  location: location
  sku: {
    name: 'B1'
    tier: 'Basic'
  }
  kind: 'linux'
  properties: {
    reserved: true
  }
}

resource webApp 'Microsoft.Web/sites@2022-03-01' = {
  name: appName
  location: location
  properties: {
    serverFarmId: appServicePlan.id
    siteConfig: {
      linuxFxVersion: 'NODE|18-lts'
      httpsOnly: true
    }
  }
}

output webAppUrl string = webApp.properties.defaultHostName
```

---

**Part 3: Validating Bicep Templates**

```bash
# Install Bicep CLI (if not done in Chapter 0)
az bicep install

# Validate template syntax
az bicep build --file main.bicep

# Generate What-If analysis (preview changes without deploying)
az deployment group what-if \
  --resource-group my-rg \
  --template-file main.bicep \
  --parameters appName=myapp location=eastus
```

---

**Part 4: Deploying Bicep Templates**

```bash
# Create resource group
az group create --name bicep-demo-rg --location eastus

# Deploy template
az deployment group create \
  --resource-group bicep-demo-rg \
  --template-file main.bicep \
  --parameters appName=demoapp location=eastus

# Verify deployment
az deployment group list \
  --resource-group bicep-demo-rg \
  --output table
```

---

**Assignment**:

1. Generate a Bicep template for a 3-tier web app architecture
2. Include: storage account, database, app service, and CDN
3. Parameterize environment (dev/staging/prod)
4. Add conditional resources (CDN only in prod)
5. Deploy to two different environments
6. Export template from Azure Portal and compare

**Success Criteria**:
- ✅ Generated valid Bicep template
- ✅ Template passes validation
- ✅ Successfully deployed to multiple environments
- ✅ Parameters work correctly
- ✅ Outputs provide useful information
- ✅ Template is well-documented with comments

---

**Cleanup Using Azure MCP**

**⚠️ IMPORTANT**: Complete this cleanup to avoid unexpected Azure charges

This chapter had you deploy resources using Bicep templates. The resources need to be deleted, but **keep your Bicep template files** for future reference.

**Generate Cleanup Commands (agent mode)**:
```
#azure_generate_azure_cli_command
Delete all resource groups created in Chapter 3: bicep-demo-rg
and any dev/staging environments I created for the assignment
```

**Expected Commands** (verify before executing):
```bash
# List resources in all Chapter 3 resource groups
az resource list --resource-group bicep-demo-rg --output table

# Delete the demo resource group
az group delete --name bicep-demo-rg --yes --no-wait

# If you created additional environments for the assignment:
az group delete --name bicep-dev-rg --yes --no-wait
az group delete --name bicep-staging-rg --yes --no-wait
```

**Alternative: Tag-Based Cleanup**:
```bash
# If you tagged resources with chapter=03
az resource list --tag chapter=03 --output table

# Delete all tagged resources
az resource list --tag chapter=03 --query "[].id" --output tsv | \
  xargs -I {} az resource delete --ids {} --verbose
```

**Before You Delete**:
- [ ] Save your Bicep template files locally (they will NOT be deleted)
- [ ] Verify the resource groups listed are from Chapter 3 only
- [ ] Confirm no production resources are in these groups
- [ ] Check that you have copies of any templates you want to keep

**Verify Deletion**:
```bash
# Check that resource groups are gone
az group list --output table | grep bicep

# Verify no Chapter 3 resources remain
az resource list --tag chapter=03 --output table
# Should return empty
```

**Note**: The Bicep templates you created are stored locally and will NOT be deleted. You may use these templates as references in future chapters.

---

### Chapter 4: Terraform Basics with AI Assistance

**Title**: AI-Generated Terraform for Multi-Cloud Readiness
**Focus**: Terraform configuration generation
**Estimated Time**: 90 minutes
**Prerequisites**: Chapters 0-3

**Learning Objectives**:
- ✅ Understand Terraform vs Bicep trade-offs
- ✅ Generate Terraform configurations using GitHub Copilot for Azure
- ✅ Initialize and plan Terraform deployments
- ✅ Apply Terraform configurations safely
- ✅ Manage Terraform state
- ✅ Destroy resources cleanly

**Real-World Scenario**:
> Your company might migrate from Azure to AWS or GCP in the future. To maintain flexibility, you're adopting Terraform as your IaC tool. You'll use GitHub Copilot for Azure to generate Terraform configurations while learning Terraform syntax through AI assistance.

---

**Part 1: Why Terraform?**

**Bicep Advantages**:
- Azure-native
- Simpler syntax
- Better Azure integration
- Automatic state management

**Terraform Advantages**:
- Multi-cloud support
- Mature ecosystem
- Large community
- Provider marketplace
- Better for complex scenarios

---

**Part 2: Generating Terraform Configurations**

**Prompt (agent mode)**:
```
Generate Terraform configuration for Azure that creates:
- Resource group in East US
- Storage account with Standard_LRS
- Container named 'data'
- Private endpoint for secure access

Include provider configuration, variables, and outputs.
Use Terraform 1.5+ syntax with AzureRM provider 3.0+
```

**Expected Output**:
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

**Part 3: Terraform Workflow**

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

**Assignment**:

1. Generate Terraform configuration for complete dev environment
2. Use modules for reusability
3. Implement remote state in Azure Storage
4. Create workspaces for dev/staging/prod
5. Deploy to all three environments
6. Compare costs across environments

**Success Criteria**:
- ✅ Generated valid Terraform configuration
- ✅ Configuration passes validation
- ✅ Successfully deployed with `terraform apply`
- ✅ State stored remotely in Azure
- ✅ Multiple workspaces functional
- ✅ Clean destroy with no orphaned resources

---

**Cleanup Using Terraform and Azure MCP**

**⚠️ IMPORTANT**: Complete this cleanup to avoid unexpected Azure charges

This chapter had you deploy resources using Terraform. The **preferred cleanup method is using Terraform's destroy command**, as it properly manages state.

**Method 1: Terraform Destroy (RECOMMENDED)**
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

# Verify all resources are gone
az resource list --output table | grep terraform
```

**Method 2: Azure MCP Fallback** (if Terraform state is lost/corrupted)
```
#azure_generate_azure_cli_command
Delete all resource groups created in Chapter 4: terraform-demo-rg
and any dev/staging/prod environments I created
```

**Expected Commands**:
```bash
# List all Terraform-managed resource groups
az group list --query "[?tags.managed_by=='terraform']" --output table

# Delete each resource group
az group delete --name terraform-demo-rg --yes --no-wait
az group delete --name terraform-dev-rg --yes --no-wait
az group delete --name terraform-staging-rg --yes --no-wait
az group delete --name terraform-prod-rg --yes --no-wait
```

**Before You Delete**:
- [ ] Run `terraform destroy` first (preferred method)
- [ ] Verify Terraform state shows no remaining resources
- [ ] Keep your Terraform configuration files (.tf files) for reference
- [ ] Delete the remote state storage account (if you created one)

**Clean Up Remote State Storage** (if applicable):
```bash
# If you created a storage account for remote state
az storage account delete \
  --name tfstateXXXXXX \
  --resource-group terraform-state-rg \
  --yes
```

**Verify Complete Deletion**:
```bash
# Check for any remaining Terraform-managed resources
az resource list --tag managed_by=terraform --output table
# Should return empty

# Verify resource groups are gone
az group list --output table | grep terraform
# Should return empty
```

**Note**: Your Terraform configuration files (.tf) are stored locally and will NOT be deleted. You may use these as references in future projects.

---

### Chapter 5: Simple Web Application Deployment (Ghost CMS)

**Title**: End-to-End Web App Deployment with AI Assistance
**Focus**: Complete deployment workflow for production-ready app
**Estimated Time**: 120 minutes
**Prerequisites**: Chapters 0-4

**Learning Objectives**:
- ✅ Deploy a complete web application (not just Hello World)
- ✅ Configure custom domains and SSL
- ✅ Set up application settings and secrets
- ✅ Implement monitoring and logging
- ✅ Configure auto-scaling
- ✅ Set up deployment slots (staging/production)

**Real-World Scenario**:
> Your team built a Node.js e-commerce API that needs to handle 10,000 requests/day. You need to deploy it to Azure with proper monitoring, auto-scaling, and zero-downtime deployments. You'll use GitHub Copilot for Azure to generate all the infrastructure code and configuration.

---

**Part 1: Architecture Planning**

**ask mode for Architecture Guidance**:
```
@azure I need to deploy a Node.js API that:
- Handles 10,000 req/day
- Needs auto-scaling
- Requires 99.9% uptime
- Uses PostgreSQL database
- Stores files in blob storage

What Azure services should I use and why?
```

**Part 2: Generate Complete Deployment**

**Prompt (agent mode)**:
```
#azure_generate_azure_cli_command
Deploy a production-ready Node.js API with:
- App Service (B1 tier, can scale to S1)
- Azure Database for PostgreSQL Flexible Server
- Storage account for file uploads
- Application Insights for monitoring
- Key Vault for secrets
- Managed identity for secure access
- Custom domain support
- Deployment slots (staging + production)

Include all security best practices.
Use resource group: ecommerce-api-rg in East US
```

**Part 3: Deploy and Configure**

Execute generated commands step-by-step with validation between each.

**Part 4: Monitoring Setup**

```
#azure_generate_azure_cli_command
Configure Application Insights alerts for:
- Response time > 2 seconds
- Error rate > 5%
- Availability < 99%
- CPU usage > 80%

Send alerts to email: alerts@company.com
```

---

**Assignment**:

1. Deploy a complete 3-tier web application
2. Implement CI/CD with GitHub Actions
3. Configure custom domain with SSL
4. Set up comprehensive monitoring
5. Perform zero-downtime deployment to production
6. Document all costs

**Success Criteria**:
- ✅ Application deployed and accessible
- ✅ Database connected securely (no hardcoded passwords)
- ✅ Monitoring and alerts functional
- ✅ Auto-scaling configured and tested
- ✅ Deployment slots working
- ✅ SSL certificate installed
- ✅ Cost within $50/month

---

## 🚀 Real-World Project: Deploy Ghost CMS

**⏱️ Time**: 20-30 minutes | **Cost**: ~$35/month | **Hype**: ⭐⭐⭐⭐ (46k GitHub stars)

**What is Ghost?** Professional publishing platform used by Mozilla, DuckDuckGo, and 46,000+ sites. Node.js-based CMS perfect for Azure App Service.

**Portfolio Value**: "Deployed production Ghost CMS on Azure with App Service, MySQL, and Blob Storage"

### Azure Services Required

- App Service (Linux, Node.js 18)
- Azure Database for MySQL Flexible Server
- Blob Storage (for images/media)
- Application Insights (monitoring)

### Deployment Using Azure MCP

**Prompt 1: Generate Complete Ghost Infrastructure**

```
#azure_generate_azure_cli_command
Deploy Ghost CMS production environment:
- Resource group: ghost-blog-rg in East US
- App Service B1 Linux with Node.js 18 runtime named ghost-app-[MYINITIALS]
- MySQL Flexible Server B1ms tier named ghost-mysql-[MYINITIALS]
- Create MySQL database named ghost_production
- Storage account for media uploads named ghoststg[MYINITIALS]
- Configure firewall rules for App Service to MySQL access
- Tag all resources with chapter=05 project=ghost

Generate all commands in deployment order with dependencies
```

**Prompt 2: Configure Ghost Environment Variables**

```
#azure_generate_azure_cli_command
Configure Ghost app settings for ghost-app-[MYINITIALS]:
- NODE_ENV=production
- database__client=mysql2
- database__connection__host=[MYSQL-SERVER].mysql.database.azure.com
- database__connection__user=ghostadmin
- database__connection__password=[SECURE-PASSWORD]
- database__connection__database=ghost_production
- database__connection__ssl=true
- url=https://ghost-app-[MYINITIALS].azurewebsites.net
- Storage adapter for Azure Blob Storage
```

**Prompt 3: Deploy Ghost from Container**

```
#azure_generate_azure_cli_command
Deploy Ghost 5 to App Service ghost-app-[MYINITIALS] using Docker container:
- Image: ghost:5-alpine from Docker Hub
- Configure container settings for production
- Enable continuous deployment
- Set startup command if needed
```

**Prompt 4: Configure Custom Domain (Optional)**

```
#azure_generate_azure_cli_command
Add custom domain myblog.com to App Service ghost-app-[MYINITIALS]
Configure free managed SSL certificate from Azure
Set up automatic HTTPS redirect
```

**Prompt 5: Enable CDN for Media (Optional)**

```
#azure_generate_azure_cli_command
Create Azure CDN endpoint for storage account ghoststg[MYINITIALS]
Configure caching rules for images and static content
Enable HTTPS for CDN endpoint
```

### Verification

**Access Ghost**: Navigate to `https://ghost-app-[MYINITIALS].azurewebsites.net/ghost`

**Expected Result**:
```
✅ Ghost admin setup page loads
✅ Can create admin account
✅ Can publish test blog post
✅ Images upload to Azure Storage
✅ Public site displays correctly
```

### Quick Troubleshooting Prompts

**Issue: Ghost Won't Start**
```
@azure My Ghost app service ghost-app-[MYINITIALS] won't start.
Check: container logs, Node.js version, MySQL connectivity, environment variables
Provide diagnostic steps
```

**Issue: Can't Upload Images**
```
@azure Images aren't uploading in Ghost app ghost-app-[MYINITIALS]
Check: storage account connection, CORS settings, container permissions
Generate fix commands
```

### Assignment (Optional)

Use Azure MCP to:
1. Change to a custom Ghost theme
2. Configure SendGrid for email newsletters
3. Add custom domain with SSL
4. Create 3 sample blog posts

**Deliverable**: Ghost blog URL for portfolio

### Cleanup Prompt

```
#azure_generate_azure_cli_command
Delete Ghost CMS resource group ghost-blog-rg completely
List all resources first, then generate deletion commands
```

**Manual Cleanup** (if needed):
```bash
az group delete --name ghost-blog-rg --yes --no-wait
```

**Cost After Deletion**: $0/month

---

**Cleanup Using Azure MCP**

**⚠️ IMPORTANT**: Complete this cleanup to avoid unexpected Azure charges

This chapter deployed a production-ready web application with multiple services. **This is NOT free tier** - leaving resources running can cost $50+/month.

**Method 1: Use Azure MCP Prompt (RECOMMENDED)**

**Generate Cleanup Commands (agent mode)**:
```
#azure_generate_azure_cli_command
Delete all resources in resource group ecommerce-api-rg including:
- App Service and App Service Plan
- PostgreSQL Flexible Server
- Storage account
- Application Insights
- Key Vault
- All deployment slots
```

**Expected Commands** (verify before executing):
```bash
# List everything that will be deleted
az resource list --resource-group ecommerce-api-rg --output table

# WARNING: This is a complete deletion of all services
az group delete --name ecommerce-api-rg --yes --no-wait
```

**Method 2: Manual Cleanup Commands** (if prompt fails or for direct execution)

```bash
# Step 1: BACKUP DATA FIRST
# Export PostgreSQL database
pg_dump -h [SERVER].postgres.database.azure.com -U [ADMIN] [DATABASE] > ecommerce-backup.sql

# Or use Azure CLI export
az postgres flexible-server backup list --resource-group ecommerce-api-rg --name [SERVER-NAME]

# Download files from storage
az storage blob download-batch \
  --source [CONTAINER] \
  --destination ./backup \
  --account-name [STORAGE-ACCOUNT]

# Step 2: List all resources
az resource list --resource-group ecommerce-api-rg --output table

# Step 3: Delete the entire resource group
az group delete --name ecommerce-api-rg --yes --no-wait
```

**Before You Delete**:
- [ ] ✅ **CRITICAL**: Export PostgreSQL database
- [ ] ✅ **CRITICAL**: Download files from blob storage
- [ ] Save Application Insights data or metrics screenshots
- [ ] Verify this is the correct resource group
- [ ] Confirm no production data is in this environment
- [ ] Document the total cost for your records

**Alternative: Selective Cleanup** (if you want to keep some resources):
```
#azure_generate_azure_cli_command
Keep Application Insights for historical data, but delete:
- App Service
- PostgreSQL database
- Storage account
- Key Vault
from resource group ecommerce-api-rg
```

**Manual Selective Cleanup**:
```bash
# Delete App Service but keep monitoring
az webapp delete --name [WEBAPP] --resource-group ecommerce-api-rg
az appservice plan delete --name [PLAN] --resource-group ecommerce-api-rg --yes

# Delete PostgreSQL
az postgres flexible-server delete --name [SERVER] --resource-group ecommerce-api-rg --yes

# Delete Storage
az storage account delete --name [STORAGE] --resource-group ecommerce-api-rg --yes

# Delete Key Vault
az keyvault delete --name [KEYVAULT] --resource-group ecommerce-api-rg

# Keep Application Insights for historical data
# (no deletion command needed)
```

**Cost Impact**:
- Before deletion: ~$50-100/month
- After deletion: $0/month
- Keeping just Application Insights: ~$2-5/month

**Verify Deletion**:
```bash
# Verify resource group is gone
az group list --output table | grep ecommerce

# Check for any orphaned resources
az resource list --tag chapter=05 --output table
# Should return empty

# Monitor billing to confirm charges stopped
az consumption usage list --start-date $(date -d "today" +%Y-%m-%d)
```

**Note**: Once deleted, you'll need to redeploy from scratch if you want to use this environment again. Make sure you have your deployment scripts saved!

---

### Chapter 6: Containerized Applications (n8n, Apache Superset)

**Title**: Container Deployments to Azure Container Apps & AKS
**Focus**: Container orchestration without Kubernetes complexity
**Estimated Time**: 120 minutes
**Prerequisites**: Chapters 0-5

**Learning Objectives**:
- ✅ Containerize applications with Docker
- ✅ Deploy to Azure Container Registry
- ✅ Run containers on Azure Container Apps
- ✅ Configure service-to-service communication
- ✅ Implement auto-scaling for containers
- ✅ Manage secrets with Key Vault integration

**Real-World Scenario**:
> Your microservices application has 5 services that need to scale independently. Kubernetes is overkill for your team size, but you need container orchestration. Azure Container Apps provides the right balance—you'll use GitHub Copilot for Azure to deploy your entire microservices architecture.

---

**Part 1: Understanding Container Apps vs AKS**

**ask mode**:
```
@azure When should I use Azure Container Apps vs AKS?
Consider: team size, complexity, cost, and management overhead.
```

**Part 2: Generate Deployment Commands**

```
#azure_generate_azure_cli_command
Deploy a containerized Node.js API to Azure Container Apps:
1. Create Container Apps environment
2. Deploy container from Docker Hub: node:18-alpine
3. Configure ingress for HTTPS
4. Set environment variables from Key Vault
5. Enable auto-scaling (1-10 replicas based on HTTP requests)
6. Set up managed identity for Azure services access

Resource group: containerapp-demo-rg in East US
```

---

**Assignment**:

1. Containerize a multi-service application (frontend + backend + database)
2. Deploy to Azure Container Apps
3. Configure internal and external ingress
4. Implement auto-scaling policies
5. Set up monitoring with Application Insights
6. Test scaling under load

**Success Criteria**:
- ✅ All services deployed and communicating
- ✅ Auto-scaling triggers correctly
- ✅ Secrets managed securely
- ✅ Monitoring shows real-time metrics
- ✅ Cost under $30/month
- ✅ Zero-downtime rolling updates work

---

## 🚀 Real-World Project: Deploy n8n Workflow Automation

**⏱️ Time**: 15-20 minutes | **Cost**: ~$20-30/month | **Hype**: ⭐⭐⭐⭐⭐ (43k GitHub stars)

**What is n8n?** Self-hosted workflow automation platform (Zapier alternative) with 400+ integrations. Perfect for Container Apps deployment.

**Portfolio Value**: "Deployed self-hosted n8n automation platform on Azure Container Apps with persistent storage"

### Azure Services Required

- Container Apps Environment
- Container App (n8n)
- PostgreSQL (workflow storage)
- Azure Files (persistent data)

### Deployment Using Azure MCP

**Prompt 1: Create Container Apps Environment**

```
#azure_generate_azure_cli_command
Create Container Apps environment for n8n:
- Resource group: n8n-automation-rg in East US
- Container Apps environment named n8n-env
- Log Analytics workspace for monitoring
- Tag resources with chapter=06 project=n8n
```

**Prompt 2: Deploy PostgreSQL Database**

```
#azure_generate_azure_cli_command
Create PostgreSQL Flexible Server for n8n workflows:
- Server name: n8n-postgres-[MYINITIALS]
- Resource group: n8n-automation-rg
- Tier: Burstable B1ms (cost-effective)
- Database name: n8n_db
- Configure firewall to allow Container Apps access
- Enable SSL
```

**Prompt 3: Deploy n8n Container**

```
#azure_generate_azure_cli_command
Deploy n8n to Container Apps:
- Container App name: n8n-app
- Environment: n8n-env
- Image: docker.n8n.io/n8nio/n8n:latest
- CPU: 0.5 cores, Memory: 1.0 GB
- Ingress: External, port 5678, allow HTTPS
- Scale rules: min 1, max 3 replicas
- Environment variables:
  - N8N_HOST=n8n-app.[CONTAINERAPP-DOMAIN]
  - N8N_PORT=5678
  - N8N_PROTOCOL=https
  - DB_TYPE=postgresdb
  - DB_POSTGRESDB_HOST=[POSTGRES-SERVER].postgres.database.azure.com
  - DB_POSTGRESDB_DATABASE=n8n_db
  - DB_POSTGRESDB_USER=[ADMIN-USER]
  - DB_POSTGRESDB_PASSWORD=[SECURE-PASSWORD]
```

**Prompt 4: Configure Persistent Storage (Optional)**

```
#azure_generate_azure_cli_command
Add Azure Files persistent volume to n8n-app:
- Storage account name: n8nstorage[MYINITIALS]
- File share name: n8n-data
- Mount path: /home/node/.n8n
This persists custom nodes and workflow data
```

### Verification

**Access n8n**: Navigate to the Container App's URL from `az containerapp show --name n8n-app --resource-group n8n-automation-rg --query properties.configuration.ingress.fqdn`

**Expected Result**:
```
✅ n8n welcome screen loads
✅ Can create owner account
✅ Can create a test workflow
✅ Workflows save to PostgreSQL
✅ Can trigger workflow manually
```

### Quick Troubleshooting Prompts

**Issue: n8n Won't Start**
```
@azure n8n container app n8n-app in n8n-automation-rg won't start
Check: container logs, database connectivity, environment variables
Provide diagnostic commands
```

**Issue: Workflows Don't Save**
```
#azure_generate_azure_cli_command
Check PostgreSQL connection for n8n-app
Verify database credentials and network access
Generate connection test commands
```

### Assignment (Optional)

Use Azure MCP to:
1. Create 3 different n8n workflows (HTTP request, schedule, webhook)
2. Configure custom domain
3. Add email notifications integration
4. Set up workflow backups

**Deliverable**: n8n URL + screenshot of workflows

### Cleanup Prompt

```
#azure_generate_azure_cli_command
Delete n8n resource group n8n-automation-rg completely
List all resources first, then generate deletion commands
```

**Manual Cleanup** (if needed):
```bash
az group delete --name n8n-automation-rg --yes --no-wait
```

**Cost After Deletion**: $0/month

---

## 🚀 BONUS: Apache Superset on AKS

**⏱️ Time**: 60-90 minutes | **Cost**: ~$70-100/month | **Hype**: ⭐⭐⭐⭐⭐ (59k GitHub stars)

> ⚠️ **ADVANCED BONUS CONTENT**: This introduces Azure Kubernetes Service (AKS). AKS is industry-standard for production container deployments. **Skip if you're not ready for Kubernetes.**

**What is Superset?** Modern data visualization platform used by Airbnb, Netflix, Twitter. Open-source alternative to Tableau.

**Portfolio Value**: "Deployed Apache Superset on Azure Kubernetes Service" - **THIS IS YOUR KUBERNETES CREDENTIAL**

### Azure Services Required

- Azure Kubernetes Service (AKS cluster)
- NGINX Ingress Controller
- PostgreSQL (Helm chart)
- Redis (Helm chart)
- LoadBalancer (automatic)

### Prerequisites

Install tools:
```bash
# Install Helm
# macOS: brew install helm
# Windows: choco install kubernetes-helm
# Linux: snap install helm --classic

# Install kubectl
az aks install-cli
```

### Deployment Using Azure MCP

**Prompt 1: Create AKS Cluster**

```
#azure_generate_azure_cli_command
Create Azure Kubernetes Service cluster for Superset:
- Resource group: superset-aks-rg in East US
- Cluster name: superset-aks
- Node count: 2 nodes
- Node size: Standard_D2s_v3 (2 vCPU, 8GB RAM each)
- Enable Azure Monitor for containers
- Enable RBAC
- Network plugin: Azure CNI
- Generate SSH keys
- Tag with chapter=06 project=superset
```

**Prompt 2: Get Cluster Credentials**

```
#azure_generate_azure_cli_command
Get AKS credentials for superset-aks cluster
Configure kubectl to connect to cluster
Verify nodes are ready
```

**Prompt 3: Install NGINX Ingress**

```bash
# These are standard Helm commands (Azure MCP doesn't generate Helm yet)
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update

helm install ingress-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx \
  --create-namespace \
  --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz
```

**Prompt 4: Deploy PostgreSQL for Superset**

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami

helm install superset-postgres bitnami/postgresql \
  --namespace superset \
  --create-namespace \
  --set auth.username=superset \
  --set auth.password=SupersetPassword123! \
  --set auth.database=superset \
  --set primary.persistence.size=10Gi
```

**Prompt 5: Deploy Redis for Caching**

```bash
helm install superset-redis bitnami/redis \
  --namespace superset \
  --set auth.enabled=false \
  --set master.persistence.size=5Gi
```

**Prompt 6: Deploy Apache Superset**

```bash
helm repo add superset https://apache.github.io/superset

# Create values file
cat <<EOF > superset-values.yaml
supersetNode:
  replicaCount: 2
postgresql:
  enabled: false
externalDatabase:
  host: superset-postgres-postgresql.superset.svc.cluster.local
  port: 5432
  database: superset
  user: superset
  password: SupersetPassword123!
redis:
  enabled: false
externalRedis:
  host: superset-redis-master.superset.svc.cluster.local
ingress:
  enabled: true
  ingressClassName: nginx
init:
  adminUser:
    username: admin
    password: AdminPassword123!
EOF

helm install superset superset/superset \
  --namespace superset \
  --values superset-values.yaml \
  --timeout 10m
```

### Verification

**Get Superset URL**:
```bash
# Get LoadBalancer IP
kubectl get svc -n ingress-nginx

# Access Superset at: http://[EXTERNAL-IP]
# Login: admin / AdminPassword123!
```

**Expected Result**:
```
✅ Superset login page loads
✅ Can login with admin credentials
✅ Can navigate SQL Lab
✅ Can create database connections
✅ Can build visualizations
```

### Quick Troubleshooting Prompts

**Issue: Pods Not Starting**
```
@azure My Superset pods in AKS cluster superset-aks are stuck in Pending
Check: node resources, persistent volume claims, pod events
Provide kubectl diagnostic commands
```

**Issue: No External IP for Ingress**
```
@azure NGINX Ingress Controller in superset-aks has no external IP after 10 minutes
Check: LoadBalancer provisioning, service configuration, Azure networking
Provide troubleshooting steps
```

### Assignment (Optional)

Use kubectl and Azure MCP to:
1. Connect Superset to a sample database
2. Create 3 different chart types
3. Build a dashboard with visualizations
4. Configure custom domain with SSL (cert-manager)
5. Scale to 3 Superset replicas

**Deliverable**: Superset dashboard URL + Kubernetes manifests

### Cleanup Prompt

```
#azure_generate_azure_cli_command
Delete complete AKS cluster and Superset deployment:
- Delete all Helm releases
- Delete AKS cluster superset-aks
- Delete resource group superset-aks-rg
- Verify all Azure resources are removed
```

**Manual Cleanup**:
```bash
# Delete Helm releases
helm uninstall superset -n superset
helm uninstall superset-postgres -n superset
helm uninstall superset-redis -n superset
helm uninstall ingress-nginx -n ingress-nginx

# Delete AKS cluster
az aks delete --resource-group superset-aks-rg --name superset-aks --yes --no-wait

# Delete resource group
az group delete --name superset-aks-rg --yes --no-wait
```

**Cost After Deletion**: $0/month

**⚠️ IMPORTANT**: AKS costs $70-100/month. Delete immediately after practice!

**Portfolio Impact**: Adding "Deployed applications to AKS" to your resume is HUGE. Very few junior developers have Kubernetes experience.

---

**Cleanup Using Azure MCP**

**⚠️ IMPORTANT**: Complete this cleanup to avoid unexpected Azure charges

Container Apps environments can cost $30+/month if left running. Clean up immediately after completing the chapter.

**Method 1: Use Azure MCP Prompt (RECOMMENDED)**

**Generate Cleanup Commands (agent mode)**:
```
#azure_generate_azure_cli_command
Delete all resources in resource group containerapp-demo-rg including:
- Container Apps environment
- All container apps
- Log Analytics workspace
- Any associated networking resources
```

**Expected Commands** (validate these are generated correctly):
```bash
# List all resources that will be deleted
az resource list --resource-group containerapp-demo-rg --output table

# Delete the entire resource group
az group delete --name containerapp-demo-rg --yes --no-wait
```

**Method 2: Manual Cleanup Commands** (if prompt fails or for direct execution)

```bash
# Step 1: List all resources to verify
az resource list --resource-group containerapp-demo-rg --output table

# Step 2: Delete all container apps first (graceful shutdown)
az containerapp list --resource-group containerapp-demo-rg --query "[].name" -o tsv | \
  xargs -I {} az containerapp delete --name {} --resource-group containerapp-demo-rg --yes

# Step 3: Delete container apps environment
az containerapp env list --resource-group containerapp-demo-rg --query "[].name" -o tsv | \
  xargs -I {} az containerapp env delete --name {} --resource-group containerapp-demo-rg --yes

# Step 4: Delete the entire resource group (catches any remaining resources)
az group delete --name containerapp-demo-rg --yes --no-wait

# Step 5: If you created additional resource groups for the assignment
az group delete --name containerapp-frontend-rg --yes --no-wait
az group delete --name containerapp-backend-rg --yes --no-wait
```

**Before You Delete**:
- [ ] Export any logs from Log Analytics you want to keep
- [ ] Document container configurations for future reference
- [ ] Verify the resource group names match what you created
- [ ] Confirm no production workloads are running

**Verify Complete Deletion**:
```bash
# Verify resource group is gone
az group list --output table | grep containerapp
# Should return empty

# Check for any orphaned Container Apps resources
az containerapp list --query "[].name" -o table
# Should return empty or not include your demo apps

# Verify billing impact
az consumption usage list --start-date $(date -d "today" +%Y-%m-%d)
```

**Cost Impact**:
- Before deletion: ~$30-50/month (Container Apps environment + apps)
- After deletion: $0/month

**Note**: Your Docker images remain in Azure Container Registry or Docker Hub and are NOT deleted. You can redeploy using these images anytime.

---

### Chapter 7: Data Storage Solutions (Metabase)

**Title**: Databases, Blob Storage, and Data Management with BI Platform
**Focus**: Choosing and deploying Azure data services
**Estimated Time**: 120 minutes
**Prerequisites**: Chapters 0-6

**Learning Objectives**:
- ✅ Choose appropriate Azure storage service for use case
- ✅ Deploy and configure Azure SQL Database
- ✅ Set up Cosmos DB for NoSQL needs
- ✅ Configure Blob Storage with lifecycle policies
- ✅ Implement backup and disaster recovery
- ✅ Optimize storage costs

**Real-World Scenario**:
> Your application needs three types of storage: relational data (user accounts), document data (product catalog), and file storage (user uploads). You'll use GitHub Copilot for Azure to set up all three storage types with proper security and cost optimization.

---

**Part 1: Storage Decision Matrix**

**ask mode**:
```
@azure Help me choose Azure storage for:
1. User accounts (ACID transactions required)
2. Product catalog (flexible schema, 10M documents)
3. User-uploaded images (5TB expected)
4. Application logs (time-series data)

For each, recommend service, tier, and reasoning.
```

**Part 2: Deploy Multi-Storage Architecture**

```
#azure_generate_azure_cli_command
Create a complete storage architecture:
- Azure SQL Database (Standard S0 tier) for user accounts
- Cosmos DB (SQL API, serverless) for product catalog
- Storage account (Hot tier) for image uploads
- Storage account (Cool tier) for application logs
- Lifecycle policies to move old data to Archive tier
- Backup enabled for all databases
- Private endpoints for security
- Managed identities for access

Resource group: storage-demo-rg in East US
```

---

**Assignment**:

1. Design storage architecture for a social media app
2. Include user data, posts, media files, and analytics
3. Implement proper security (private endpoints, encryption)
4. Set up backup and disaster recovery
5. Create cost optimization policies
6. Document expected monthly costs

**Success Criteria**:
- ✅ All storage types deployed correctly
- ✅ Data encrypted at rest and in transit
- ✅ Backup policies configured
- ✅ Lifecycle policies reduce costs
- ✅ Private endpoints secure access
- ✅ Cost under $100/month for expected load

---

## 🚀 Real-World Project: Deploy Metabase BI Platform

**⏱️ Time**: 25-35 minutes | **Cost**: ~$40-50/month | **Hype**: ⭐⭐⭐⭐ (37k GitHub stars)

**What is Metabase?** Open-source business intelligence platform. Easy-to-use alternative to Tableau. Perfect for visualizing data from Chapter 7's databases!

**Portfolio Value**: "Deployed Metabase BI platform on Azure connecting multiple data sources (SQL, Cosmos DB, Storage)"

### Azure Services Required

- App Service (Java runtime)
- PostgreSQL (Metabase application database)
- Connections to Chapter 7 databases (optional)

### Deployment Using Azure MCP

**Prompt 1: Deploy Metabase Infrastructure**

```
#azure_generate_azure_cli_command
Deploy Metabase BI platform:
- Resource group: metabase-bi-rg in East US
- App Service B2 Linux with Java 17 runtime named metabase-app-[MYINITIALS]
- PostgreSQL Flexible Server B1ms named metabase-postgres-[MYINITIALS]
- Create database named metabase_app_db
- Configure firewall for App Service access
- Tag resources with chapter=07 project=metabase
```

**Prompt 2: Deploy Metabase from Container**

```
#azure_generate_azure_cli_command
Configure App Service metabase-app-[MYINITIALS] for Metabase:
- Use Docker container: metabase/metabase:latest
- Configure environment variables:
  - MB_DB_TYPE=postgres
  - MB_DB_DBNAME=metabase_app_db
  - MB_DB_PORT=5432
  - MB_DB_USER=[ADMIN-USER]
  - MB_DB_PASS=[SECURE-PASSWORD]
  - MB_DB_HOST=[POSTGRES-SERVER].postgres.database.azure.com
  - MB_JETTY_PORT=3000
- Enable container port 3000
- Enable HTTPS only
```

**Prompt 3: Connect to Chapter 7 Databases (Optional)**

```
@azure How do I connect Metabase to:
1. Azure SQL Database from Chapter 7
2. Cosmos DB with SQL API
3. Blob Storage data

Provide connection strings and configuration steps
```

### Verification

**Access Metabase**: Navigate to `https://metabase-app-[MYINITIALS].azurewebsites.net`

**Expected Result**:
```
✅ Metabase welcome screen loads
✅ Can complete initial setup
✅ Can add data source connections
✅ Can run SQL queries
✅ Can create visualizations
✅ Can build dashboards
```

### Quick Setup Guide

**First-Time Setup**:
1. **Language**: English
2. **Create Account**: Admin user
3. **Add Database**: Connect to your Chapter 7 SQL/Cosmos DB
4. **Usage Data**: Your preference

**Create Your First Dashboard**:
1. Click "Ask a question"
2. Select database from Chapter 7
3. Write SQL query or use visual builder
4. Create chart (bar, line, pie, etc.)
5. Save to dashboard

### Quick Troubleshooting Prompts

**Issue: Metabase Won't Start**
```
@azure Metabase app service metabase-app-[MYINITIALS] won't start
Check: Java version, container logs, PostgreSQL connection, memory settings
Provide diagnostic steps
```

**Issue: Can't Connect to Database**
```
#azure_generate_azure_cli_command
Verify network connectivity from metabase-app-[MYINITIALS] to databases
Check: firewall rules, connection strings, SSL requirements
Generate test commands
```

### Assignment (Optional)

Use Azure MCP and Metabase to:
1. Connect to all 3 Chapter 7 data sources (SQL, Cosmos, Storage)
2. Create 5 different visualization types
3. Build a comprehensive dashboard with 6+ cards
4. Set up email alerts for data changes
5. Create a SQL question with parameters

**Deliverable**: Metabase dashboard URL (with public link)

### Cleanup Prompt

```
#azure_generate_azure_cli_command
Delete Metabase resource group metabase-bi-rg completely
List all resources first, then generate deletion commands
```

**Manual Cleanup** (if needed):
```bash
az group delete --name metabase-bi-rg --yes --no-wait
```

**Cost After Deletion**: $0/month

**Note**: If you want to keep Metabase as a portfolio project, scale down to B1 App Service (~$13/month)

---

**Cleanup Using Azure MCP**

**⚠️ CRITICAL**: Complete this cleanup to avoid unexpected Azure charges

**DATABASES AND STORAGE ARE THE MOST EXPENSIVE RESOURCES.** Leaving an Azure SQL Database and Cosmos DB running can cost $100+/month.

**⚠️ DATA LOSS WARNING**: Once you delete these resources, **ALL DATA IS PERMANENTLY GONE**. Backup first!

**BEFORE YOU DELETE ANYTHING**:
1. **Export databases** if you want to keep data
2. **Download files** from blob storage
3. **Document configurations** for future reference

**Method 1: Use Azure MCP Prompt (RECOMMENDED)**

**Generate Cleanup Commands (agent mode)**:
```
#azure_generate_azure_cli_command
Delete all resources in resource group storage-demo-rg including:
- Azure SQL Database and SQL Server
- Cosmos DB account
- All storage accounts (hot and cool tier)
- Private endpoints
- Any backup vaults
BUT FIRST generate commands to export/backup data before deletion
```

**Expected Commands** (validate these are generated correctly):
```bash
# Step 1: Backup data first (CRITICAL!)
# SQL Database backup
az sql db export \
  --resource-group storage-demo-rg \
  --server [SQL-SERVER-NAME] \
  --name [DATABASE-NAME] \
  --admin-user [ADMIN] \
  --admin-password [PASSWORD] \
  --storage-key-type StorageAccessKey \
  --storage-key [KEY] \
  --storage-uri https://[STORAGE].blob.core.windows.net/backups/db-backup.bacpac

# Download blobs
az storage blob download-batch \
  --source [CONTAINER] \
  --destination ./backup \
  --account-name [STORAGE-ACCOUNT]

# Step 2: List all resources to be deleted
az resource list --resource-group storage-demo-rg --output table

# Step 3: Delete resource group
az group delete --name storage-demo-rg --yes --no-wait
```

**Method 2: Manual Cleanup Commands** (if prompt fails or for direct execution)

```bash
# Step 1: BACKUP DATA FIRST (CRITICAL!)
# Create a backup storage account if needed
az storage account create \
  --name backupstg$(date +%s) \
  --resource-group storage-demo-rg \
  --sku Standard_LRS

# Export SQL Database
az sql db export \
  --resource-group storage-demo-rg \
  --server [YOUR-SQL-SERVER] \
  --name [YOUR-DATABASE] \
  --admin-user [ADMIN-USER] \
  --admin-password [ADMIN-PASSWORD] \
  --storage-uri [BACKUP-BLOB-URI]

# Download all blobs from storage accounts
az storage blob download-batch \
  --source [CONTAINER-NAME] \
  --destination ./local-backup \
  --account-name [STORAGE-ACCOUNT-NAME]

# Step 2: List all resources
az resource list --resource-group storage-demo-rg --output table

# Step 3: Delete Cosmos DB (most expensive)
az cosmosdb delete \
  --name [COSMOS-ACCOUNT-NAME] \
  --resource-group storage-demo-rg \
  --yes

# Step 4: Delete SQL Database and Server
az sql db delete \
  --name [DATABASE-NAME] \
  --resource-group storage-demo-rg \
  --server [SERVER-NAME] \
  --yes

az sql server delete \
  --name [SERVER-NAME] \
  --resource-group storage-demo-rg \
  --yes

# Step 5: Delete storage accounts
az storage account delete \
  --name [HOT-STORAGE-ACCOUNT] \
  --resource-group storage-demo-rg \
  --yes

az storage account delete \
  --name [COOL-STORAGE-ACCOUNT] \
  --resource-group storage-demo-rg \
  --yes

# Step 6: Delete entire resource group (catches any remaining resources)
az group delete --name storage-demo-rg --yes --no-wait
```

**Before You Delete**:
- [ ] ✅ **CRITICAL**: Exported SQL Database to .bacpac file
- [ ] ✅ **CRITICAL**: Downloaded all blobs from storage accounts
- [ ] ✅ **CRITICAL**: Exported Cosmos DB data (if needed)
- [ ] Saved backup files to local machine or separate storage
- [ ] Documented connection strings and configurations
- [ ] Verified the resource group name is correct
- [ ] Confirmed no production data exists in these resources

**Verify Complete Deletion**:
```bash
# Verify resource group is gone
az group list --output table | grep storage-demo

# Check for orphaned storage accounts
az storage account list --query "[].name" -o table | grep storage

# Check for orphaned SQL servers
az sql server list --query "[].name" -o table

# Check for orphaned Cosmos DB accounts
az cosmosdb list --query "[].name" -o table

# Verify billing impact (may take 24-48 hours to reflect)
az consumption usage list --start-date $(date -d "today" +%Y-%m-%d)
```

**Cost Impact**:
- Before deletion: ~$100-200/month (SQL Database + Cosmos DB + Storage)
- After deletion: $0/month
- **IMPORTANT**: You may still see charges for the current billing period

**Note**:
- Your backup files are stored locally or in a separate storage account (if you created one)
- To restore data later, you'll need to recreate resources and import the backups
- Consider keeping one small storage account (~$1/month) for long-term backup storage

---

### Chapter 8: Diagnostics and Troubleshooting

**Title**: AI-Assisted Azure Troubleshooting
**Focus**: Using GitHub Copilot for Azure to diagnose and fix issues
**Estimated Time**: 90 minutes
**Prerequisites**: Chapters 0-7

**Learning Objectives**:
- ✅ Use `#azure_diagnose_resource` for troubleshooting
- ✅ Query Azure Monitor logs effectively
- ✅ Analyze Application Insights telemetry
- ✅ Identify performance bottlenecks
- ✅ Resolve common deployment failures
- ✅ Optimize resource performance

**Real-World Scenario**:
> Your production App Service is experiencing high response times and occasional 500 errors. Users are complaining. You need to diagnose and fix the issue quickly. You'll use GitHub Copilot for Azure's diagnostic tools to identify the root cause and generate fixes.

---

**Part 1: Common Issues and Diagnostics**

**Issue: Slow Response Times**

```
#azure_diagnose_resource
Investigate why my App Service 'slowapp' has response times > 5 seconds.
Check: CPU usage, memory, database queries, external API calls, and network latency.
Generate diagnostic commands and analysis.
```

**Issue: Intermittent 500 Errors**

```
#azure_diagnose_resource
My web app returns 500 errors randomly. Analyze:
- Application logs for exceptions
- App Service metrics
- Database connection pool
- Memory leaks
Provide diagnostic commands and probable causes.
```

**Part 2: Performance Optimization**

```
#azure_generate_azure_cli_command
Based on diagnostics showing high CPU usage,
generate commands to:
1. Scale up App Service to next tier
2. Enable auto-scaling rules
3. Configure CDN for static content
4. Enable caching with Azure Cache for Redis
```

---

**Assignment**:

1. Deploy a problematic application (provided with known issues)
2. Use AI diagnostic tools to identify all problems
3. Generate and execute fix commands
4. Verify performance improvements
5. Document troubleshooting process
6. Create monitoring alerts to prevent recurrence

**Success Criteria**:
- ✅ Identified root causes using AI diagnostics
- ✅ Generated appropriate fix commands
- ✅ Performance improved measurably
- ✅ Monitoring configured to prevent recurrence
- ✅ Documented troubleshooting methodology
- ✅ Response time under 500ms, 99.9% uptime achieved

---

**Cleanup Using Azure MCP**

**⚠️ IMPORTANT**: Complete this cleanup to avoid unexpected Azure charges

This chapter had you create test resources for diagnostics practice. Clean them up promptly.

**Method 1: Use Azure MCP Prompt (RECOMMENDED)**

**Generate Cleanup Commands (agent mode)**:
```
#azure_generate_azure_cli_command
Delete all resources created in Chapter 8 for diagnostics testing:
- Test App Service 'slowapp' and its plan
- Application Insights instances
- Log Analytics workspaces
- Any Redis cache instances created for optimization
- All test resource groups
```

**Expected Commands** (validate these are generated correctly):
```bash
# List all Chapter 8 resources
az resource list --tag chapter=08 --output table

# Delete tagged resources
az resource list --tag chapter=08 --query "[].id" --output tsv | \
  xargs -I {} az resource delete --ids {} --verbose

# Or delete entire resource group if dedicated
az group delete --name diagnostics-demo-rg --yes --no-wait
```

**Method 2: Manual Cleanup Commands** (if prompt fails or for direct execution)

```bash
# Step 1: List all resources
az resource list --tag chapter=08 --output table

# Step 2: Delete App Service and plan
az webapp delete \
  --name slowapp \
  --resource-group diagnostics-demo-rg

az appservice plan delete \
  --name slowapp-plan \
  --resource-group diagnostics-demo-rg \
  --yes

# Step 3: Delete Redis cache if created
az redis delete \
  --name diagnostics-cache \
  --resource-group diagnostics-demo-rg \
  --yes

# Step 4: Delete Application Insights
az monitor app-insights component delete \
  --app slowapp-insights \
  --resource-group diagnostics-demo-rg

# Step 5: Delete Log Analytics workspace
az monitor log-analytics workspace delete \
  --workspace-name diagnostics-logs \
  --resource-group diagnostics-demo-rg \
  --yes

# Step 6: Delete resource group
az group delete --name diagnostics-demo-rg --yes --no-wait
```

**Before You Delete**:
- [ ] Export any diagnostic logs or insights you want to keep
- [ ] Save screenshots of diagnostics dashboards for documentation
- [ ] Document the troubleshooting methodology you learned
- [ ] Verify resource group names match what you created

**Verify Complete Deletion**:
```bash
# Verify resource group is gone
az group list --output table | grep diagnostics

# Check for orphaned resources
az resource list --tag chapter=08 --output table
# Should return empty

# Check for orphaned App Services
az webapp list --query "[?name=='slowapp']" -o table
# Should return empty
```

**Cost Impact**:
- Before deletion: ~$30-60/month (App Service + Redis + monitoring)
- After deletion: $0/month

**Note**: Diagnostic data and logs are deleted with resources. Make sure to export important findings before cleanup!

---

### Chapter 9: Multi-Service Architecture (Supabase, Strapi)

**Title**: Complex Application with Multiple Azure Services
**Focus**: Integrating multiple services into cohesive architecture
**Estimated Time**: 180 minutes
**Prerequisites**: Chapters 0-8

**Learning Objectives**:
- ✅ Design multi-tier application architecture
- ✅ Deploy 5+ interconnected Azure services
- ✅ Configure service-to-service authentication
- ✅ Implement event-driven communication
- ✅ Set up centralized logging and monitoring
- ✅ Create disaster recovery plan

**Real-World Scenario**:
> Your company is building a video streaming platform that requires: web frontend (Static Web Apps), API backend (Container Apps), video processing (Functions), storage (Blob + CDN), database (Cosmos DB), search (Cognitive Search), and caching (Redis). You'll use GitHub Copilot for Azure to architect and deploy this complex system.

---

**Part 1: Architecture Planning**

**ask mode**:
```
@azure Help me design architecture for video streaming platform with:
- Frontend: React SPA (1M users/month)
- API: Node.js (100K req/day)
- Video processing: Transcoding on upload
- Storage: 10TB videos
- Database: User data + video metadata
- Search: Full-text search on videos
- Caching: Reduce database load

Recommend specific Azure services, tiers, and reasoning.
Include cost estimate.
```

**Part 2: Deploy Complete Architecture**

```
#azure_generate_azure_cli_command
Create complete video streaming infrastructure:

Frontend:
- Azure Static Web Apps (Free tier)
- Custom domain with SSL
- GitHub Actions deployment

Backend:
- Container Apps (API service)
- Consumption-based scaling
- Managed identity for Azure services

Video Processing:
- Function App (consumption plan)
- Triggered by blob uploads
- Output to CDN

Storage:
- Storage account (Hot tier + CDN)
- Cosmos DB (serverless)
- Azure Cache for Redis (Basic tier)

Monitoring:
- Application Insights for all services
- Log Analytics workspace
- Unified dashboards

Security:
- Key Vault for secrets
- Private endpoints where possible
- Managed identities throughout

Resource group: streaming-platform-rg in East US
Generate in deployment order with dependencies.
```

---

**Part 3: Service Integration**

Configure services to communicate securely using managed identities.

**Part 4: Monitoring and Alerting**

```
#azure_generate_azure_cli_command
Set up comprehensive monitoring:
- Application Map showing service dependencies
- Alerts for failures in any service
- Performance metrics dashboard
- Cost analysis for each service
- Availability tests for all public endpoints
```

---

**Assignment**:

1. Design and deploy an e-commerce platform with:
   - Frontend (React)
   - API (Node.js)
   - Product search (Cognitive Search)
   - Order processing (Functions)
   - Database (SQL + Cosmos DB)
   - Caching (Redis)
   - Storage (Blob)
   - Email (Communication Services)

2. Implement disaster recovery
3. Create comprehensive monitoring
4. Load test and optimize
5. Document architecture decisions
6. Calculate monthly costs

**Success Criteria**:
- ✅ All services deployed and integrated
- ✅ Authentication works end-to-end
- ✅ Monitoring shows health of all components
- ✅ Disaster recovery plan tested
- ✅ Performance meets requirements
- ✅ Cost within budget
- ✅ Architecture documented with diagrams

---

## 🚀 Real-World Project: Deploy Supabase (Firebase Alternative)

**⏱️ Time**: 45-60 minutes | **Cost**: ~$60-80/month | **Hype**: ⭐⭐⭐⭐⭐ (68k GitHub stars - MASSIVE!)

**What is Supabase?** Open-source Firebase alternative. Complete BaaS (Backend-as-a-Service) with database, auth, storage, and realtime APIs. Uses PostgreSQL!

**Portfolio Value**: "Deployed complete Supabase BaaS platform on Azure - PostgreSQL, Auth, Storage, Realtime, REST API"

### Azure Services Required

- PostgreSQL Flexible Server (Supabase database)
- Container Apps (Supabase services: Auth, Storage, Realtime, REST API)
- Blob Storage (file uploads)
- Redis Cache (realtime subscriptions)
- Application Gateway (optional, for custom domain)

### Architecture Overview

```
Supabase consists of multiple microservices:
- Kong (API Gateway) - Routes requests
- GoTrue (Auth service) - User authentication
- PostgREST (REST API) - Auto-generated REST API from PostgreSQL
- Realtime (WebSocket) - Realtime subscriptions
- Storage (S3-compatible) - File uploads
- PostgreSQL (Database) - Core data storage
```

### Deployment Using Azure MCP

**Prompt 1: Deploy PostgreSQL for Supabase**

```
#azure_generate_azure_cli_command
Deploy PostgreSQL for Supabase backend:
- Resource group: supabase-rg in East US
- PostgreSQL Flexible Server D2s_v3 named supabase-db-[MYINITIALS]
- PostgreSQL 15
- Database named postgres (default)
- Enable extensions: uuid-ossp, pgcrypto, pgjwt
- Configure high availability
- Tag with chapter=09 project=supabase
```

**Prompt 2: Deploy Container Apps Environment**

```
#azure_generate_azure_cli_command
Create Container Apps environment for Supabase microservices:
- Environment: supabase-env
- Resource group: supabase-rg
- Log Analytics workspace
- Internal network isolation
```

**Prompt 3: Deploy Supabase Kong (API Gateway)**

```
#azure_generate_azure_cli_command
Deploy Kong API Gateway to Container Apps:
- Container App: supabase-kong
- Image: kong:latest
- External ingress on port 8000
- CPU: 1.0, Memory: 2Gi
- Environment variables for PostgreSQL connection
- Scale: 2-4 replicas
```

**Prompt 4: Deploy Supabase Auth Service**

```
#azure_generate_azure_cli_command
Deploy Supabase GoTrue auth service:
- Container App: supabase-auth
- Image: supabase/gotrue:latest
- Internal ingress only
- Connect to PostgreSQL
- Configure JWT secrets
- Enable email auth provider
```

**Prompt 5: Deploy PostgREST API**

```
#azure_generate_azure_cli_command
Deploy PostgREST for auto-generated REST API:
- Container App: supabase-rest
- Image: postgrest/postgrest:latest
- Connect to PostgreSQL
- Configure database schema
- Enable JWT validation
```

**Prompt 6: Deploy Realtime Service**

```
#azure_generate_azure_cli_command
Deploy Supabase Realtime for WebSocket subscriptions:
- Container App: supabase-realtime
- Image: supabase/realtime:latest
- WebSocket support enabled
- Redis for pub/sub
- Connect to PostgreSQL for change data capture
```

**Prompt 7: Deploy Storage Service**

```
#azure_generate_azure_cli_command
Deploy Supabase Storage with Azure Blob backend:
- Container App: supabase-storage
- Image: supabase/storage-api:latest
- Mount Azure Blob Storage
- Configure file upload limits
- Enable image transformations
```

**Prompt 8: Configure Redis for Realtime**

```
#azure_generate_azure_cli_command
Deploy Azure Cache for Redis for Supabase:
- Name: supabase-redis-[MYINITIALS]
- SKU: Basic C0 (cost-effective for learning)
- Connect to Realtime service
```

### Verification

**Access Supabase**:
1. Kong API Gateway URL: `https://supabase-kong.[CONTAINERAPP-DOMAIN]`
2. Test endpoints:
   - `/auth/v1/health` (Auth service)
   - `/rest/v1/` (PostgREST API)
   - `/realtime/v1/websocket` (Realtime)
   - `/storage/v1/health` (Storage)

**Expected Result**:
```
✅ All services return HTTP 200
✅ Can register new user via Auth API
✅ Can query database via REST API
✅ Can upload file to Storage
✅ Can subscribe to realtime changes
```

### Quick Troubleshooting Prompts

**Issue: Services Can't Connect to PostgreSQL**
```
@azure Supabase services in supabase-rg can't connect to PostgreSQL
Check: connection strings, firewall rules, PostgreSQL extensions, network policies
Provide diagnostic commands
```

**Issue: Kong Gateway Returns 502**
```
#azure_generate_azure_cli_command
Debug Supabase Kong gateway connectivity
Check: backend service health, routing configuration, container logs
Generate troubleshooting commands
```

### Assignment (Optional)

Use Azure MCP and Supabase to:
1. Create a simple todo app using Supabase client library
2. Implement user registration and login
3. Create database tables via REST API
4. Upload images to Storage
5. Subscribe to realtime table changes
6. Configure row-level security (RLS)

**Deliverable**: Working app + Supabase API URL

### Cleanup Prompt

```
#azure_generate_azure_cli_command
Delete Supabase deployment completely:
- All Container Apps in supabase-env
- PostgreSQL database
- Redis cache
- Storage accounts
- Resource group supabase-rg
```

**Manual Cleanup**:
```bash
az group delete --name supabase-rg --yes --no-wait
```

**Cost After Deletion**: $0/month

**Note**: Supabase is complex but EXTREMELY valuable on a resume. "Deployed full BaaS platform" is impressive!

---

## 🚀 Alternative Project: Deploy Strapi Headless CMS

**⏱️ Time**: 30-40 minutes | **Cost**: ~$40-55/month | **Hype**: ⭐⭐⭐⭐ (61k GitHub stars)

**What is Strapi?** Leading open-source headless CMS. Build APIs fast. Perfect for content-driven apps.

**Portfolio Value**: "Deployed Strapi headless CMS on Azure with PostgreSQL and media storage"

### Azure Services Required

- App Service (Node.js 18)
- PostgreSQL Flexible Server
- Blob Storage (media library)
- CDN (optional, for media delivery)

### Deployment Using Azure MCP

**Prompt 1: Deploy Strapi Infrastructure**

```
#azure_generate_azure_cli_command
Deploy Strapi CMS:
- Resource group: strapi-cms-rg in East US
- App Service B2 Linux with Node.js 18 named strapi-app-[MYINITIALS]
- PostgreSQL Flexible Server B1ms named strapi-db-[MYINITIALS]
- Database: strapi_cms
- Storage account for media: strapistorage[MYINITIALS]
- Tag with chapter=09 project=strapi
```

**Prompt 2: Configure Strapi Environment**

```
#azure_generate_azure_cli_command
Configure App Service strapi-app-[MYINITIALS] for Strapi:
- NODE_ENV=production
- DATABASE_CLIENT=postgres
- DATABASE_HOST=[POSTGRES-SERVER].postgres.database.azure.com
- DATABASE_PORT=5432
- DATABASE_NAME=strapi_cms
- DATABASE_USERNAME=[ADMIN]
- DATABASE_PASSWORD=[SECURE-PASSWORD]
- DATABASE_SSL=true
- ADMIN_JWT_SECRET=[GENERATE-RANDOM]
- API_TOKEN_SALT=[GENERATE-RANDOM]
- APP_KEYS=[GENERATE-RANDOM-KEYS]
- Enable Azure Blob Storage provider
```

**Prompt 3: Deploy Strapi Application**

```
#azure_generate_azure_cli_command
Deploy Strapi to App Service:
- Use Docker image: strapi/strapi:latest
- Or deploy from Git repository
- Configure startup command if needed
- Enable continuous deployment
```

**Prompt 4: Configure Media Storage**

```
#azure_generate_azure_cli_command
Configure Strapi Azure Blob Storage provider:
- Storage account: strapistorage[MYINITIALS]
- Container: strapi-media
- Configure CORS for uploads
- Get connection string
```

### Verification

**Access Strapi**: Navigate to `https://strapi-app-[MYINITIALS].azurewebsites.net/admin`

**Expected Result**:
```
✅ Strapi admin panel loads
✅ Can create admin account
✅ Can create content types
✅ Can add collection entries
✅ Can upload media to Azure Storage
✅ REST API endpoints work
✅ GraphQL endpoint works (if enabled)
```

### Quick Setup

**First-Time Setup**:
1. Create admin account
2. Create content type (e.g., "Article")
3. Add fields (title, content, image)
4. Create entry
5. Make API public
6. Test API: `/api/articles`

### Quick Troubleshooting Prompts

**Issue: Strapi Won't Start**
```
@azure Strapi app strapi-app-[MYINITIALS] won't start
Check: Node.js version, database connection, environment variables, memory limits
Provide diagnostic steps
```

**Issue: Media Uploads Fail**
```
#azure_generate_azure_cli_command
Debug Azure Storage integration for Strapi
Check: storage connection, CORS, container permissions, provider configuration
Generate fix commands
```

### Assignment (Optional)

Use Azure MCP and Strapi to:
1. Create 3 different content types
2. Add media uploads with image resizing
3. Configure REST API permissions
4. Enable GraphQL plugin
5. Create webhook to external service
6. Add custom API endpoint

**Deliverable**: Strapi admin URL + API documentation

### Cleanup Prompt

```
#azure_generate_azure_cli_command
Delete Strapi deployment:
- Resource group strapi-cms-rg
- All App Services, PostgreSQL, Storage
```

**Manual Cleanup**:
```bash
az group delete --name strapi-cms-rg --yes --no-wait
```

**Cost After Deletion**: $0/month

**Note**: Strapi is simpler than Supabase but still impressive. "Deployed headless CMS for enterprise" is great for portfolio!

---

**Cleanup Using Azure MCP**

**⚠️ CRITICAL**: Complete this cleanup to avoid unexpected Azure charges

**THIS IS THE MOST EXPENSIVE CHAPTER** - deploying 8+ services can cost $200+/month if left running!

**📌 IMPORTANT NOTE**: If you plan to complete Chapter 10 (Capstone Project) immediately, you may want to **reuse some of these resources**. Read the "Optional: Selective Cleanup" section below.

**Option A: Complete Cleanup** (if not doing Chapter 10 immediately)

**Method 1: Use Azure MCP Prompt (RECOMMENDED)**

**Generate Cleanup Commands (agent mode)**:
```
#azure_generate_azure_cli_command
Delete all resources in resource group streaming-platform-rg including:
- Static Web App (frontend)
- Container Apps environment and API service
- Function App and hosting plan
- Storage accounts (videos + CDN)
- Cosmos DB account
- Azure Cache for Redis
- Cognitive Search service
- Application Insights and Log Analytics
- Key Vault
- All networking resources
```

**Expected Commands** (validate these are generated correctly):
```bash
# List everything that will be deleted
az resource list --resource-group streaming-platform-rg --output table

# Delete entire resource group (most efficient)
az group delete --name streaming-platform-rg --yes --no-wait
```

**Method 2: Manual Cleanup Commands** (if prompt fails or for direct execution)

```bash
# Step 1: BACKUP DATA FIRST
# Export Cosmos DB data if needed
az cosmosdb sql database list --account-name [COSMOS-ACCOUNT] --resource-group streaming-platform-rg

# Download any important files from blob storage
az storage blob download-batch \
  --source videos \
  --destination ./backup \
  --account-name [STORAGE-ACCOUNT]

# Step 2: List all resources
az resource list --resource-group streaming-platform-rg --output table

# Step 3: Delete most expensive services first (to stop charges immediately)
# Delete Cosmos DB (most expensive)
az cosmosdb delete --name [COSMOS-ACCOUNT] --resource-group streaming-platform-rg --yes

# Delete Redis Cache
az redis delete --name [REDIS-NAME] --resource-group streaming-platform-rg --yes

# Delete Cognitive Search
az search service delete --name [SEARCH-NAME] --resource-group streaming-platform-rg --yes

# Delete Container Apps
az containerapp delete --name api-service --resource-group streaming-platform-rg --yes
az containerapp env delete --name [ENV-NAME] --resource-group streaming-platform-rg --yes

# Delete Function App
az functionapp delete --name [FUNCTION-NAME] --resource-group streaming-platform-rg

# Delete Static Web App
az staticwebapp delete --name [STATICWEBAPP-NAME] --yes

# Delete storage accounts
az storage account delete --name [STORAGE1] --resource-group streaming-platform-rg --yes
az storage account delete --name [STORAGE2] --resource-group streaming-platform-rg --yes

# Step 4: Delete entire resource group (catches everything)
az group delete --name streaming-platform-rg --yes --no-wait

# Step 5: Delete e-commerce assignment resources if created
az group delete --name ecommerce-platform-rg --yes --no-wait
```

**Option B: Selective Cleanup** (if continuing to Chapter 10 immediately)

Some resources from Chapter 9 can be reused in Chapter 10 to save deployment time:
- **Keep**: Key Vault, Application Insights, Log Analytics workspace
- **Delete**: All application-specific services

```
#azure_generate_azure_cli_command
Delete all Chapter 9 services EXCEPT Key Vault, Application Insights, and Log Analytics.
Delete: Static Web App, Container Apps, Functions, Cosmos DB, Redis, Search, Storage accounts
Keep: Key Vault (streaming-kv), Application Insights, Log Analytics workspace
Tag kept resources with chapter=09-reused-in-10
```

**Manual Selective Cleanup**:
```bash
# Delete application services but keep infrastructure
az cosmosdb delete --name [COSMOS] --resource-group streaming-platform-rg --yes
az redis delete --name [REDIS] --resource-group streaming-platform-rg --yes
az search service delete --name [SEARCH] --resource-group streaming-platform-rg --yes
az containerapp delete --name api-service --resource-group streaming-platform-rg --yes
az functionapp delete --name [FUNCTION] --resource-group streaming-platform-rg

# Keep these for Chapter 10:
# - Key Vault
# - Application Insights
# - Log Analytics workspace

# Verify what remains
az resource list --resource-group streaming-platform-rg --output table
```

**Before You Delete**:
- [ ] ✅ **CRITICAL**: Backup Cosmos DB data if you want to keep it
- [ ] ✅ **CRITICAL**: Download videos/files from blob storage
- [ ] Save Application Insights metrics or screenshots
- [ ] Export architecture diagrams and documentation
- [ ] Document all connection strings and configurations
- [ ] If doing Chapter 10 next, decide which resources to keep

**Verify Complete Deletion** (Option A):
```bash
# Verify resource group is gone
az group list --output table | grep streaming

# Check for orphaned expensive resources
az cosmosdb list --query "[].name" -o table
az redis list --query "[].name" -o table
az search service list --query "[].name" -o table
# All should return empty or not include your resources

# Verify billing impact (may take 24-48 hours)
az consumption usage list --start-date $(date -d "today" +%Y-%m-%d)
```

**Cost Impact**:
- Before deletion: ~$150-250/month (all 8+ services)
- After complete deletion: $0/month
- After selective deletion (keeping 3 resources): ~$5-10/month

**Recovery Note**:
If you delete everything and want to rebuild later:
- Saved architecture diagrams will guide redeployment
- Backup data can be restored to new instances
- GitHub Copilot for Azure can regenerate deployment commands
- Consider keeping architecture documentation in GitHub repository

---

### Chapter 10: Production-Ready Deployment (Capstone)

**Title**: Complete Production Deployment with All Best Practices
**Focus**: Combining all course knowledge into production system
**Estimated Time**: 240 minutes (4 hours)
**Prerequisites**: Chapters 0-9

**Learning Objectives**:
- ✅ Deploy production-ready multi-tier application
- ✅ Implement all security best practices
- ✅ Configure comprehensive monitoring and alerting
- ✅ Set up CI/CD pipelines
- ✅ Implement disaster recovery and high availability
- ✅ Optimize costs without sacrificing reliability
- ✅ Document everything for team handoff

**Capstone Project: Full-Stack SaaS Application**

Deploy a complete SaaS application with:
- Multi-tenant architecture
- User authentication and authorization
- Payment processing integration
- Admin dashboard
- Customer portal
- API for third-party integrations
- Real-time notifications
- Analytics and reporting
- Automated backups
- 99.9% uptime guarantee

---

**Part 1: Requirements Analysis**

**ask mode - Architecture Planning**:
```
@azure Help me architect a SaaS application with these requirements:

Users: 10,000 monthly active users
Growth: 20% month-over-month
Traffic: 500K API requests/day
Storage: 100GB data, 1TB files
Database: Multi-tenant SQL data
Availability: 99.9% uptime required
Security: SOC 2 compliance needed
Budget: $500/month initially, scale with revenue

Recommend complete architecture with:
- Compute services
- Data storage
- Networking
- Security
- Monitoring
- Cost optimization strategies
- Scaling plan for growth
```

---

**Part 2: Phased Deployment**

**Phase 1: Core Infrastructure**
```
#azure_generate_azure_cli_command
Deploy core infrastructure for SaaS app:

Networking:
- Virtual Network with subnets
- Private endpoints for all services
- Application Gateway for load balancing
- DDoS protection

Compute:
- Container Apps for API (B1, scale to B2)
- Static Web Apps for frontend
- Function Apps for background jobs

Data:
- Azure SQL Database (S1, read replicas in 2 regions)
- Blob Storage (Hot + lifecycle to Cool)
- Redis Cache (Basic C1)

Security:
- Key Vault for secrets
- Managed identities for all services
- Azure AD B2C for user auth

Resource group: saas-app-prod-rg in East US 2
Include all networking and security from the start.
```

**Phase 2: Monitoring and Observability**
```
#azure_generate_azure_cli_command
Set up production monitoring:

Application Insights:
- Distributed tracing across all services
- Custom metrics for business KPIs
- Availability tests from 5 global locations

Log Analytics:
- Centralized logging for all services
- Custom queries for troubleshooting
- Security audit logs

Alerts:
- Response time > 1 second
- Error rate > 1%
- Database CPU > 80%
- Storage capacity > 80%
- Failed deployments
- Security anomalies

Dashboards:
- Executive dashboard (uptime, users, revenue)
- Operations dashboard (performance, errors, health)
- Cost dashboard (spend by service, trends)

Send alerts to: PagerDuty integration
```

**Phase 3: Disaster Recovery**
```
#azure_generate_azure_cli_command
Implement disaster recovery:

Backups:
- SQL Database: Point-in-time restore (7 days)
- Blob Storage: Geo-redundant (GRS)
- Configuration: Export to Azure DevOps Git

Failover:
- Traffic Manager for multi-region failover
- Standby region in West US 2
- Automated failover testing monthly

Recovery:
- RTO: 4 hours
- RPO: 1 hour
- Documented recovery procedures
```

**Phase 4: CI/CD Pipeline**
```
Generate GitHub Actions workflow for:
- Automated testing (unit, integration, e2e)
- Security scanning (secrets, dependencies)
- Infrastructure deployment (Bicep templates)
- Application deployment (blue-green)
- Smoke tests after deployment
- Automatic rollback on failure
```

---

**Part 3: Cost Optimization**

```
#azure_generate_azure_cli_command
Analyze current costs and generate optimization plan:

1. Identify underutilized resources
2. Recommend reserved instances for stable workloads
3. Configure auto-shutdown for dev/test resources
4. Implement storage lifecycle policies
5. Set up budgets and alerts
6. Generate monthly cost reports

Target: Reduce costs by 30% without impacting performance
```

---

**Part 4: Security Hardening**

```
#azure_generate_azure_cli_command
Harden security for production:

1. Enable Azure Security Center recommendations
2. Implement network security groups (least privilege)
3. Configure Web Application Firewall (WAF)
4. Enable DDoS protection
5. Set up Azure Sentinel for threat detection
6. Configure audit logging for compliance
7. Implement secret rotation policies
8. Enable vulnerability scanning

Generate commands to implement all recommendations.
```

---

**Part 5: Documentation and Handoff**

Create comprehensive documentation:
1. Architecture diagrams (network, application, data flow)
2. Deployment runbooks
3. Troubleshooting guides
4. Cost analysis and optimization recommendations
5. Disaster recovery procedures
6. Monitoring and alerting documentation
7. Security compliance checklist
8. Knowledge transfer materials for operations team

---

**Capstone Assignment Success Criteria**:

**Functional Requirements**:
- ✅ Application deployed and accessible
- ✅ All features working end-to-end
- ✅ Multi-tenant isolation verified
- ✅ Payment processing functional
- ✅ Real-time notifications working

**Non-Functional Requirements**:
- ✅ 99.9% uptime achieved (tested)
- ✅ Response time < 500ms (p95)
- ✅ Can handle 2x expected load
- ✅ Disaster recovery tested successfully
- ✅ Security scan shows no critical issues

**Operational Requirements**:
- ✅ Monitoring comprehensive and alerting works
- ✅ CI/CD pipeline fully automated
- ✅ Documentation complete and accurate
- ✅ Cost within budget ($500/month)
- ✅ Team trained on operations

**Deliverables**:
- ✅ Running production application
- ✅ Complete source code and infrastructure code
- ✅ Architecture documentation with diagrams
- ✅ Operations runbooks
- ✅ Cost analysis and optimization report
- ✅ Security compliance documentation
- ✅ 30-minute presentation to stakeholders

---

**Cleanup Using Azure MCP**

**🎉 CONGRATULATIONS ON COMPLETING THE CAPSTONE!**

**⚠️ CRITICAL FINAL CLEANUP**: This capstone project is running production-grade services that can cost $500+/month

**IMPORTANT DECISION**: Decide whether to keep this as a portfolio project or delete everything.

---

**Option A: Keep as Portfolio Project** (Recommended for job hunting)

If you want to showcase this in interviews:

1. **Reduce to Free/Minimal Tier**:
```
#azure_generate_azure_cli_command
Scale down all services in saas-production-rg to free or lowest tier:
- App Service: Scale to Free (F1)
- Database: Scale to Basic tier
- Disable auto-scaling
- Remove premium features
Keep application running but minimize costs to $0-20/month
```

2. **Take Screenshots First**:
   - Architecture diagrams
   - Monitoring dashboards showing uptime
   - Performance metrics
   - Security compliance reports
   - Cost optimization results

3. **Document for Portfolio**:
   - GitHub repository with all code
   - Architecture documentation
   - README with live demo link
   - Case study writeup

**Cost after scaling down**: ~$10-30/month (worth it for portfolio!)

---

**Option B: Complete Cleanup** (if you want $0 cost)

**⚠️ WARNING**: This will permanently delete your capstone project. Backup everything first!

**BEFORE DELETING - BACKUP CHECKLIST**:
- [ ] ✅ **CRITICAL**: Push all code to GitHub (public or private repo)
- [ ] ✅ **CRITICAL**: Export all databases (SQL + Cosmos + any others)
- [ ] ✅ **CRITICAL**: Download all user-uploaded files from storage
- [ ] ✅ **CRITICAL**: Export Application Insights data and screenshots
- [ ] ✅ **CRITICAL**: Save architecture diagrams and documentation
- [ ] ✅ Take screenshots of working application
- [ ] Document all architecture decisions
- [ ] Export monitoring dashboards and metrics
- [ ] Save security scan reports
- [ ] Document cost analysis findings
- [ ] Create presentation slides about the project

**Method 1: Use Azure MCP Prompt (RECOMMENDED)**

**Generate Cleanup Commands (agent mode)**:
```
#azure_generate_azure_cli_command
Delete all resources in resource group saas-production-rg including:
- All App Services and plans
- All databases (SQL, Cosmos DB, Redis)
- Storage accounts and CDN
- Function Apps
- API Management
- Application Gateway
- All networking resources
- Key Vault
- Application Insights and Log Analytics
- All security resources
- Payment processing integrations
- Communication services
BUT FIRST generate commands to backup all data
```

**Expected Commands** (validate these are generated correctly):
```bash
# Step 1: COMPREHENSIVE BACKUP (RUN THESE FIRST!)
# Export SQL Database
az sql db export \
  --resource-group saas-production-rg \
  --server [SQL-SERVER] \
  --name [DATABASE] \
  --admin-user [ADMIN] \
  --admin-password [PASSWORD] \
  --storage-uri [BACKUP-URI]

# Export Cosmos DB
az cosmosdb sql database list --account-name [COSMOS] --resource-group saas-production-rg

# Download all blobs
az storage blob download-batch \
  --source [CONTAINER] \
  --destination ./backup \
  --account-name [STORAGE-ACCOUNT]

# Step 2: List everything
az resource list --resource-group saas-production-rg --output table

# Step 3: Delete everything
az group delete --name saas-production-rg --yes --no-wait
```

**Method 2: Manual Cleanup Commands** (if prompt fails or for direct execution)

```bash
# ============================================
# STEP 1: COMPREHENSIVE BACKUP (DO THIS FIRST!)
# ============================================

# Create backup directory
mkdir -p ./capstone-backup
cd ./capstone-backup

# Export SQL Database
az sql db export \
  --resource-group saas-production-rg \
  --server [YOUR-SQL-SERVER] \
  --name [YOUR-DATABASE] \
  --admin-user [ADMIN-USER] \
  --admin-password [ADMIN-PASSWORD] \
  --storage-key-type StorageAccessKey \
  --storage-key [STORAGE-KEY] \
  --storage-uri https://[STORAGE].blob.core.windows.net/backups/saas-db.bacpac

# Download Cosmos DB data (if applicable)
# Use Azure Data Studio or Cosmos DB export feature

# Download all files from storage accounts
az storage blob download-batch \
  --source [CONTAINER-NAME] \
  --destination ./storage-backup \
  --account-name [STORAGE-ACCOUNT]

# Export Key Vault secrets (for documentation only - store securely!)
az keyvault secret list --vault-name [KEYVAULT-NAME] --query "[].name" -o tsv > keyvault-secrets-list.txt

# ============================================
# STEP 2: VERIFY BACKUPS COMPLETED
# ============================================
ls -lh ./capstone-backup
# Verify all files are present

# ============================================
# STEP 3: DELETE SERVICES (MOST TO LEAST EXPENSIVE)
# ============================================

# List all resources
az resource list --resource-group saas-production-rg --output table

# Delete API Management (if used - most expensive)
az apim delete --name [APIM-NAME] --resource-group saas-production-rg --yes

# Delete Application Gateway (if used)
az network application-gateway delete --name [APPGW-NAME] --resource-group saas-production-rg

# Delete Cosmos DB
az cosmosdb delete --name [COSMOS-NAME] --resource-group saas-production-rg --yes

# Delete Azure SQL
az sql db delete --name [DB-NAME] --resource-group saas-production-rg --server [SERVER-NAME] --yes
az sql server delete --name [SERVER-NAME] --resource-group saas-production-rg --yes

# Delete Redis Cache
az redis delete --name [REDIS-NAME] --resource-group saas-production-rg --yes

# Delete Function Apps
az functionapp delete --name [FUNCTION-NAME] --resource-group saas-production-rg

# Delete App Services
az webapp delete --name [WEBAPP-NAME] --resource-group saas-production-rg

# Delete App Service Plans
az appservice plan delete --name [PLAN-NAME] --resource-group saas-production-rg --yes

# Delete Storage Accounts
az storage account delete --name [STORAGE1] --resource-group saas-production-rg --yes
az storage account delete --name [STORAGE2] --resource-group saas-production-rg --yes

# Delete CDN profile (if used)
az cdn profile delete --name [CDN-NAME] --resource-group saas-production-rg

# Delete Communication Services (if used)
az communication delete --name [COMM-NAME] --resource-group saas-production-rg --yes

# ============================================
# STEP 4: DELETE ENTIRE RESOURCE GROUP
# ============================================
az group delete --name saas-production-rg --yes --no-wait

# If you created additional resource groups
az group delete --name saas-staging-rg --yes --no-wait
az group delete --name saas-dev-rg --yes --no-wait
```

**Verify Complete Deletion**:
```bash
# Verify resource group is completely gone
az group list --output table | grep saas

# Check for any orphaned expensive resources
az cosmosdb list --query "[].name" -o table
az sql server list --query "[].name" -o table
az redis list --query "[].name" -o table
az apim list --query "[].name" -o table
# All should return empty or not include your resources

# Final billing check (may take 24-48 hours to reflect)
az consumption usage list --start-date $(date -d "7 days ago" +%Y-%m-%d)
```

**Cost Impact**:
- Before deletion: ~$300-600/month (production-grade SaaS)
- After complete deletion: $0/month
- After scaling to minimal tier: ~$10-30/month (portfolio-worthy)

---

**📊 Final Course Statistics**

If you completed all chapters with cleanups:
- **Total Azure resources deployed**: 100+ across 10 chapters
- **Services used**: 15+ different Azure services
- **AI-generated commands**: 500+ CLI commands and templates
- **Cost if left running**: $1,000+/month
- **Cost with proper cleanup**: $0/month
- **Skills gained**: Production-ready Azure + AI expertise
- **Time saved by AI**: ~100+ hours of manual documentation reading
- **Career value**: Significant competitive advantage

---

**🎯 Portfolio Recommendations**

Keep Chapter 10 capstone scaled down for 3-6 months:
- Use it in job applications
- Show it in technical interviews
- Reference it on LinkedIn
- Blog about your architecture decisions
- Present at local meetups

After job search:
- Delete resources or
- Convert to a real side project with paying users

---

**🙏 Thank You!**

You've completed an intensive, hands-on course in AI-assisted Azure infrastructure. This is just the beginning of your journey.

**Share Your Success**:
- Tweet about completing the course with #AzureMCP
- Star the GitHub repository
- Share feedback for improvements
- Help other students in discussions
- Consider becoming a course contributor

**Final Cleanup Verification**:
Run this one-time script to verify EVERYTHING is cleaned up:

```bash
#!/bin/bash
echo "🔍 Checking for remaining Azure resources..."

echo "\n📦 Resource Groups:"
az group list --output table

echo "\n💰 Recent Costs (last 7 days):"
az consumption usage list --start-date $(date -d "7 days ago" +%Y-%m-%d) --query "[].{Cost:pretaxCost, Service:instanceName}" -o table

echo "\n🏷️  Tagged Resources (should be empty):"
for chapter in {01..10}; do
  echo "Chapter $chapter:"
  az resource list --tag chapter=$chapter --output table
done

echo "\n✅ If all sections show empty/minimal results, cleanup is complete!"
echo "💰 Monitor your Azure billing portal for the next 48 hours to confirm $0 charges"
```

---

**Key Takeaways from Course**:

1. **AI Accelerates, You Control**: GitHub Copilot for Azure generates infrastructure code 10x faster, but you validate and execute with full control

2. **Generate → Validate → Execute**: This workflow ensures safety while leveraging AI acceleration

3. **Prompt Engineering is a Skill**: Effective prompts are precise, include context, and specify requirements clearly

4. **Cost Management is Critical**: Always estimate costs, use free tiers for learning, and clean up resources

5. **Security from the Start**: Use managed identities, private endpoints, Key Vault, and HTTPS by default

6. **Infrastructure-as-Code Wins**: Bicep and Terraform enable repeatable, version-controlled deployments

7. **Monitoring is Non-Negotiable**: You can't manage what you don't measure—comprehensive monitoring is essential

8. **Documentation Matters**: Your future self and your team will thank you for thorough documentation

9. **Azure is Vast**: This course covered ~15 services; Azure has 200+. The skills you learned (prompt engineering, IaC, monitoring) apply to all of them.

10. **Keep Learning**: Azure and AI tools evolve rapidly. Stay current with Microsoft Learn, Azure updates, and GitHub Copilot for Azure improvements.

---

**Congratulations!**

You've completed the Azure Infrastructure with AI Assistance course. You now have production-ready skills in:
- Prompt engineering for infrastructure
- Azure CLI, Bicep, and Terraform
- Multi-service architecture design
- Security and compliance best practices
- Cost optimization strategies
- Monitoring and troubleshooting
- CI/CD and automation

**Next Steps**:
1. Deploy a personal project using what you learned
2. Contribute to the course (PRs welcome!)
3. Join Azure community forums
4. Explore advanced topics in the `future/` folder
5. Get Azure certifications (your course knowledge accelerates this)

**Stay Connected**:
- Course GitHub: [link]
- Discord Community: [link]
- Monthly office hours: [calendar link]
## Additional Course Materials

> **Note**: These materials mirror the supplementary files in [LangChain.js for Beginners](https://github.com/danwahlin/langchainjs-for-beginners) (e.g., GLOSSARY.md, scripts/, data/), adapted for Azure infrastructure and GitHub Copilot for Azure content.

---

### 1. Glossary (`GLOSSARY.md`)

**Purpose**: Comprehensive reference for all technical terms used throughout the course

**Specification** (following LangChainJS GLOSSARY.md format - 21KB file with 514 lines):

**Required Sections**:

1. **GitHub Copilot for Azure Terms** (25+ entries)
   - agent mode
   - ask mode
   - `#azure_generate_azure_cli_command`
   - `#azure_query_learn`
   - `#azure_diagnose_resource`
   - Model Context Protocol (MCP)
   - Prompt engineering
   - Generate → Validate → Execute workflow

2. **Azure Core Concepts** (40+ entries)
   - Resource Group
   - Subscription
   - Azure Resource Manager (ARM)
   - Managed Identity
   - Service Principal
   - Virtual Network (VNet)
   - Azure Active Directory
   - Role-Based Access Control (RBAC)

3. **Compute Services** (15+ entries)
   - App Service
   - Container Apps
   - Azure Kubernetes Service (AKS)
   - Azure Functions
   - Virtual Machines
   - VM Scale Sets
   - Static Web Apps

4. **Data Services** (15+ entries)
   - Azure SQL Database
   - Cosmos DB
   - Blob Storage
   - Azure Cache for Redis
   - Azure Database for PostgreSQL/MySQL
   - Storage tiers (Hot, Cool, Archive)

5. **Networking** (10+ entries)
   - Private Endpoint
   - Virtual Network
   - Application Gateway
   - Load Balancer
   - Traffic Manager
   - DDoS Protection

6. **Security** (15+ entries)
   - Key Vault
   - Managed Identity
   - Private Endpoint
   - Network Security Group (NSG)
   - Azure Security Center
   - Web Application Firewall (WAF)

7. **Infrastructure-as-Code** (10+ entries)
   - Bicep
   - Terraform
   - ARM Templates
   - Infrastructure as Code (IaC)
   - Template
   - Parameter file

8. **Prompt Engineering Patterns** (20+ entries)
   - Single resource creation pattern
   - Multi-resource dependency pattern
   - Conditional creation pattern
   - Bulk operations pattern
   - Configuration update pattern
   - Validation pattern
   - Error handling pattern

9. **Deployment & Operations** (15+ entries)
   - Deployment slot
   - Blue-green deployment
   - Canary deployment
   - CI/CD
   - GitHub Actions
   - Zero-downtime deployment

10. **Cost & Governance** (10+ entries)
    - SKU/Tier
    - Free tier
    - Reserved instances
    - Azure Cost Management
    - Resource tags
    - Budget alerts

**Entry Format** (follow LangChainJS pattern):
```markdown
### Term Name

**Definition**: Clear, concise explanation in 1-2 sentences

**Why it matters**: Real-world context explaining importance

**Example**:
<code example or usage>

**Related concepts**: [Link to related glossary entries]

**Used in**: Chapter X: Section Y

**Common mistakes**:
- ❌ Mistake 1: Description
- ✅ Correct approach: Description
```

**Example Entry**:
```markdown
### agent mode

**Definition**: A mode in GitHub Copilot for Azure where specialized tools automatically assist with Azure-related tasks by generating executable code, querying documentation, or diagnosing resources.

**Why it matters**: Agent mode is how you generate Azure CLI commands, Bicep templates, and Terraform configurations. Understanding when to use agent mode vs ask mode is fundamental to the course workflow.

**Tools in agent mode**:
- `#azure_generate_azure_cli_command` - Generate Azure CLI commands
- `#azure_query_learn` - Query Microsoft Learn documentation
- `#azure_diagnose_resource` - Troubleshoot Azure resources

**Example**:
#azure_generate_azure_cli_command
Create a storage account named mystorageacct in East US using Standard_LRS
with blob public access disabled and HTTPS-only enabled


**Related concepts**: [ask mode](#ask-mode), [MCP](#model-context-protocol), [Prompt Engineering](#prompt-engineering)

**Used in**:
- Chapter 0: Part 3 - Understanding agent mode vs ask mode
- Chapter 1: Generating Your First Azure CLI Command
- All subsequent chapters for code generation

**Common mistakes**:
- ❌ Using agent mode for general questions ("What is Azure?")
- ✅ Use agent mode for generating code (#azure_generate_azure_cli_command)
- ❌ Expecting direct resource creation (AI doesn't create resources, you execute generated commands)
- ✅ Follow generate → validate → execute workflow
```

---

### 2. Validation Infrastructure (`scripts/`)

**Purpose**: Automated testing to ensure all prompt examples generate correct, functional code

**Required Scripts** (following LangChainJS validation pattern):

#### `scripts/validate-prompts.ts`
**Function**: Test that all prompt examples generate syntactically valid output

```typescript
/**
 * Validate Prompt Outputs
 *
 * Tests:
 * 1. Read all prompt examples from chapter README files
 * 2. Execute prompts against GitHub Copilot for Azure API (simulated)
 * 3. Validate generated Azure CLI commands have correct syntax
 * 4. Validate Bicep templates compile
 * 5. Validate Terraform configurations pass terraform validate
 * 6. Report any prompts that generate invalid code
 */

interface PromptTest {
  chapter: string;
  promptText: string;
  expectedOutputType: 'cli' | 'bicep' | 'terraform';
  requiredElements: string[]; // e.g., ['az group create', '--name', '--location']
}

async function validatePrompt(test: PromptTest): Promise<TestResult> {
  // Extract expected output patterns
  // Validate syntax
  // Check required elements present
  // Return pass/fail with details
}
```

#### `scripts/validate-commands.ts`
**Function**: Verify Azure CLI commands are syntactically correct

```typescript
/**
 * Validate Azure CLI Commands
 *
 * Tests:
 * 1. Read all CLI command examples from chapters
 * 2. Check syntax against Azure CLI spec
 * 3. Verify required parameters present
 * 4. Check for dangerous flags (--force, --yes without context)
 * 5. Validate resource naming conventions
 * 6. Ensure security flags present (--https-only, etc.)
 */

function validateAzureCLICommand(command: string): ValidationResult {
  // Parse command
  // Check syntax
  // Validate parameters
  // Check security flags
  // Return detailed validation result
}
```

#### `scripts/validate-templates.ts`
**Function**: Verify Bicep and Terraform templates are valid

```typescript
/**
 * Validate Infrastructure Templates
 *
 * Tests:
 * 1. Find all .bicep files in chapters
 * 2. Run: az bicep build --file <file>
 * 3. Find all .tf files in chapters
 * 4. Run: terraform validate
 * 5. Report compilation errors
 */
```

#### `scripts/cost-estimator.ts`
**Function**: Calculate estimated monthly costs for each chapter's resources

```typescript
/**
 * Cost Estimation Tool
 *
 * Reads chapter resource specifications and calculates:
 * - Monthly cost estimate
 * - Free tier eligibility
 * - Cost breakdown by service
 * - Warnings if cost exceeds chapter budget
 */

interface ResourceCost {
  service: string;
  sku: string;
  region: string;
  estimatedMonthlyCost: number;
  freeTierEligible: boolean;
}

function estimateChapterCost(chapter: string): CostReport {
  // Parse chapter resources
  // Calculate costs
  // Generate report
}
```

#### `scripts/cleanup-checker.ts`
**Function**: Verify all chapters have proper cleanup scripts

```typescript
/**
 * Cleanup Verification
 *
 * Ensures:
 * 1. Every chapter has cleanup instructions
 * 2. Cleanup scripts reference correct resource tags
 * 3. No orphaned resources after cleanup
 * 4. Cleanup scripts are tested and functional
 */
```

#### `scripts/validate-all-parallel.ts`
**Function**: Run all validations in parallel (like LangChainJS validate-examples-parallel.ts)

```typescript
/**
 * Parallel Validation Runner
 *
 * Runs all validation scripts concurrently:
 * - validate-prompts (10 concurrent)
 * - validate-commands (10 concurrent)
 * - validate-templates (5 concurrent)
 * - cost-estimator (sequential)
 * - cleanup-checker (sequential)
 *
 * Total estimated runtime: 5-10 minutes for all chapters
 */
```

---

### 3. Prompt Pattern Library (`prompts/`)

**Purpose**: Reusable, tested prompt templates for common Azure operations

**Structure**:
```
prompts/
├── README.md                    # How to use the library
├── ask-mode-patterns/           # Learning and questions
│   ├── service-comparison.md
│   ├── cost-estimation.md
│   ├── architecture-guidance.md
│   ├── troubleshooting-questions.md
│   └── best-practices.md
├── agent-mode-patterns/         # Code generation
│   ├── cli-command-generation.md
│   ├── bicep-template-generation.md
│   ├── terraform-generation.md
│   ├── diagnostics.md
│   └── resource-queries.md
├── by-service/                  # Service-specific templates
│   ├── app-service/
│   │   ├── create-web-app.md
│   │   ├── configure-scaling.md
│   │   └── setup-deployment-slots.md
│   ├── storage/
│   │   ├── create-storage-account.md
│   │   ├── configure-lifecycle.md
│   │   └── setup-cdn.md
│   ├── databases/
│   ├── networking/
│   └── security/
└── advanced-patterns/           # Complex scenarios
    ├── multi-region-deployment.md
    ├── disaster-recovery.md
    ├── cost-optimization.md
    └── security-hardening.md
```

**Template Format**:
```markdown
# Pattern Name

## Use Case
When to use this prompt pattern

## Pattern Template
<prompt template with {VARIABLES}>


## Variables
- {VARIABLE_NAME}: Description, examples, constraints

## Example
Concrete example with filled variables

## Expected Output
What AI should generate

## Validation Checklist
- [ ] Check 1
- [ ] Check 2

## Common Mistakes
❌ Mistake → ✅ Fix

## Related Patterns
Links to similar patterns
```

---

### 4. Data & Reference Materials (`data/`)

**Purpose**: Sample files, templates, and reference materials for learning

**Structure**:
```
data/
├── sample-bicep-templates/
│   ├── web-app-basic.bicep
│   ├── web-app-with-database.bicep
│   ├── container-app.bicep
│   ├── storage-with-cdn.bicep
│   └── multi-tier-architecture.bicep
├── sample-terraform-configs/
│   ├── web-app-basic.tf
│   ├── aks-cluster.tf
│   ├── storage-account.tf
│   └── multi-region-setup.tf
├── architecture-diagrams/
│   ├── chapter-01-simple-web-app.png
│   ├── chapter-05-simple-web-app-architecture.png
│   ├── chapter-06-container-app-architecture.png
│   ├── chapter-09-multi-service-architecture.png
│   └── chapter-10-production-architecture.png
├── cost-estimation-spreadsheets/
│   ├── azure-pricing-calculator.xlsx
│   ├── chapter-cost-estimates.xlsx
│   └── free-tier-tracker.xlsx
├── security-checklists/
│   ├── app-service-security.md
│   ├── storage-security.md
│   ├── database-security.md
│   ├── networking-security.md
│   └── master-security-checklist.md
├── troubleshooting-guides/
│   ├── deployment-failures.md
│   ├── permission-errors.md
│   ├── networking-issues.md
│   ├── cost-overruns.md
│   └── common-errors-solutions.md
└── sample-applications/
    ├── node-api/
    ├── react-frontend/
    ├── python-api/
    └── dotnet-web-app/
```

---

### 5. Supplementary Files

#### `CODE_OF_CONDUCT.md`
**Source**: Copy from [LangChain.js for Beginners](https://github.com/danwahlin/langchainjs-for-beginners/blob/main/CODE_OF_CONDUCT.md)
**Content**: Microsoft Open Source Code of Conduct
**Purpose**: Community standards and behavior expectations

#### `SECURITY.md`
**Source**: Copy from [LangChain.js for Beginners](https://github.com/danwahlin/langchainjs-for-beginners/blob/main/SECURITY.md)
**Content**: Security vulnerability reporting process
**Purpose**: How to report security issues responsibly

#### `MAINTAINERS.md`
**Purpose**: Guide for course maintainers and contributors
**Content**:
```markdown
# Maintainers Guide

## Course Maintenance

### Testing Prompt Examples
1. Run validation scripts before each release
2. Test on fresh Azure subscription
3. Verify cost estimates are accurate
4. Check all cleanup scripts work

### Updating for Azure Changes
- Monitor Azure CLI changelog
- Track GitHub Copilot for Azure updates
- Update pricing when Azure prices change
- Revise examples when services deprecated

### Reviewing Contributions
- Ensure PRs include validation tests
- Check cost implications
- Verify security best practices followed
- Test on multiple platforms

### Release Process
1. Run full validation suite
2. Update CHANGELOG.md
3. Tag release
4. Update documentation links
5. Announce in community channels
```

#### `CHANGELOG.md`
**Purpose**: Track course updates and changes

#### `CONTRIBUTING.md`
**Purpose**: Guide for community contributions

---

### 6. GitHub Actions Workflows (`.github/workflows/`)

#### `validate-prompts.yml`
```yaml
name: Validate Prompt Examples

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm install
      - run: npm run validate:prompts
      - run: npm run validate:commands
      - run: npm run validate:templates
```

#### `cost-check.yml`
```yaml
name: Cost Estimation Check

on:
  pull_request:
    branches: [main]

jobs:
  cost-check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm run cost:estimate
      - name: Check cost increase
        run: |
          # Fail if PR increases costs by >20%
```

---

## Course Learning Path

### Beginner Track (Chapters 0-3)
- Setup and basics
- First deployment
- Container orchestration
- Platform-as-a-Service

### Intermediate Track (Chapters 4-7)
- Serverless architectures
- Container Apps
- Monitoring and observability
- High availability

### Advanced Track (Chapters 8-10)
- Storage integration
- Database optimization
- Cost management
- Security hardening

---

## Key Differentiators

This course differs from typical Azure tutorials:

1. **MCP-First Approach**: Uses Azure MCP tools via GitHub Copilot instead of manual Azure Portal or CLI
2. **Prompt Engineering**: Teaches effective prompting patterns for infrastructure
3. **Real OSS Projects**: Every chapter deploys actual production-ready applications
4. **Hands-on Practice**: Students learn by doing, not just reading
5. **Progressive Complexity**: From simple App Service to multi-zone HA deployments
6. **Cross-Cutting Concerns**: Final chapter ties everything together with cost and security

---

## Success Metrics

Students who complete this course will be able to:

- ✅ Use Azure MCP tools effectively in GitHub Copilot
- ✅ Deploy 9 different OSS projects to Azure
- ✅ Understand Azure service trade-offs (AKS vs App Service vs Container Apps)
- ✅ Optimize costs across multiple deployments
- ✅ Implement security best practices
- ✅ Monitor and troubleshoot Azure resources
- ✅ Write effective prompts for infrastructure operations

---

## Example Chapter Structure (Detailed)

Each chapter follows this format (based on [LangChain.js for Beginners](https://github.com/danwahlin/langchainjs-for-beginners) chapter structure):

**README.md**:
1. Introduction and project overview
2. Learning objectives
3. Prerequisites
4. Key concepts
5. Azure MCP tools for this chapter
6. Architecture diagram
7. Step-by-step walkthrough with prompts
8. Expected outputs and verification
9. Troubleshooting common issues
10. Best practices and tips
11. Additional resources

**assignment.md**:
1. Challenge description
2. Requirements checklist
3. Prompts to get started
4. Bonus challenges
5. Success criteria

**prompts/**:
1. Template prompts for common operations
2. Variations for different scenarios
3. Troubleshooting prompts

**solution/**:
1. Complete prompt sequences
2. Architecture decisions explained
3. Alternative approaches

---

## Technical Stack

**Required**:
- Azure subscription (free tier works for most chapters)
- VS Code with GitHub Copilot
- GitHub Copilot for Azure extension
- Azure CLI (for verification)

**Optional**:
- Git and GitHub account (for Chapter 4)
- Docker Desktop (for local testing)

---

## Pedagogical Approach

**Mirrors [LangChain.js for Beginners](https://github.com/danwahlin/langchainjs-for-beginners)** (located at `/Users/danwahlin/Desktop/demos/LangChainJS-for-Beginners`):
- Concept → Scenario → Problem → Solution → Prompts (same pattern as LangChainJS course)
- Each example includes "Why this matters" (following LangChainJS format)
- Hands-on assignments after each chapter (same structure: assignment.md with challenges)
- Progressive complexity (beginner → intermediate → advanced tracks)
- Real-world applications (deployable projects, not toy examples)
- Same repository structure (README.md, assignment.md, code/, samples/, solution/ folders)
- Same supplementary materials (GLOSSARY.md, scripts/, data/ folders)

**Prompt-First Learning**:
- Show the prompt
- Explain what it does
- Show the output
- Explain the results
- Variations to try

**Scenario-Driven**:
Every chapter starts with: "You're deploying [PROJECT] to Azure and need to..."

---

## Future Expansion Ideas

**Potential additional chapters**:
- Multi-region deployments
- Azure DevOps integration
- Infrastructure as Code (Bicep/Terraform)
- Kubernetes advanced topics
- Microservices architectures
- AI/ML model deployment

---

## Notes

- All chapters are standalone (can be completed in any order after Chapter 0-1)
- Each deployment is production-ready (not toy examples)
- Emphasis on cost-effectiveness (using free tiers where possible)
- Security is introduced early and reinforced throughout
- Real-world trade-offs discussed (when to use which Azure service)

---

## Implementation Timeline and Priority Rankings

### Overview

Based on comprehensive analysis of the course plan against the LangChainJS for Beginners reference implementation and GitHub Copilot for Azure capabilities, this section outlines the priorities and timeline for implementing the course.

---

### Priority Levels Defined

**🔴 CRITICAL** (Must fix before any course launch)
- Blocking issues that prevent course execution
- Technical inaccuracies that would damage course credibility
- Safety/cost issues that could harm students financially

**🟡 HIGH** (Essential for course quality)
- Features needed for professional-quality course
- Missing elements that significantly impact learning outcomes
- Components that enable course maintenance and validation

**🟢 MEDIUM** (Enhances course significantly)
- Nice-to-have features that improve student experience
- Additional materials that accelerate learning
- Supplementary content that adds value

**🔵 LOW** (Polish and optimization)
- Optional enhancements
- Future-proofing elements
- Community-building features

---

### 🔴 CRITICAL PRIORITY (Complete Before Launch)

**Estimated Effort**: 120-180 hours (3-4.5 weeks full-time)

#### 1. Complete Chapter 0 with Safety Baseline (16-24 hours)
**Status**: ✅ COMPLETE (in this plan)
**Includes**:
- Billing alerts setup
- Cost management dashboard
- Security baseline configuration
- Emergency cleanup procedures
- MCP explanation and workflow understanding

**Why Critical**: Students need financial protection before deploying anything

#### 2. Create At Least 3 Complete Sample Chapters (48-72 hours)
**Status**: ✅ Chapters 1-2 detailed in plan
**Remaining**: Finish Chapter 3 (Bicep) with same level of detail

**Requirements**:
- Chapter 1: First deployment (60 minutes, every step documented)
- Chapter 2: CLI mastery (75 minutes, all prompt patterns)
- Chapter 3: Bicep templates (90 minutes, complete IaC workflow)

**Format** (for each):
- Real-world scenario
- Step-by-step instructions
- Actual commands to execute
- Expected outputs
- Cost estimates
- Cleanup scripts
- Assignment with success criteria

**Why Critical**: These chapters serve as templates for all others. Get these right, rest follows the pattern.

#### 3. Build Core Validation Infrastructure (24-32 hours)
**Status**: 📋 Specifications complete, implementation pending

**Required Scripts**:
- `validate-commands.ts` - Test Azure CLI syntax
- `cost-estimator.ts` - Calculate chapter costs
- `cleanup-checker.ts` - Verify cleanup scripts exist

**Why Critical**: Can't verify course quality without automated testing

#### 4. Create GLOSSARY.md (16-24 hours)
**Status**: 📋 Specifications complete, content pending

**Requirements**:
- 150+ entries (following LangChainJS format)
- 10 major categories
- Code examples for each entry
- Cross-references between terms
- "Used in Chapter X" for each term

**Why Critical**: Students get lost without comprehensive terminology reference

#### 5. Document Correct GitHub Copilot for Azure Capabilities (8-12 hours)
**Status**: ✅ COMPLETE (in course philosophy and chapters)

**Documented**:
- `#azure_generate_azure_cli_command` generates code, doesn't deploy
- `#azure_query_learn` for documentation
- `#azure_diagnose_resource` for troubleshooting
- Generate → Validate → Execute workflow
- Agent mode vs Ask mode usage

**Why Critical**: Prevents student confusion about how tool actually works

**Total Critical Priority**: 112-164 hours

---

### 🟡 HIGH PRIORITY (Essential for Quality)

**Estimated Effort**: 80-120 hours (2-3 weeks full-time)

#### 1. Complete Remaining Chapters (48-72 hours)
**Status**: Chapters 4-10 outlined, need full detail

**Requirements for each chapter**:
- 60-180 minute estimated completion time
- Real-world scenario introduction
- Step-by-step instructions
- Cost estimation
- Security checklist
- Assignment with rubric
- Cleanup scripts

**Chapters to Complete**:
- Chapter 4: Terraform (90 min)
- Chapter 5: Web Application (120 min)
- Chapter 6: Containers (120 min)
- Chapter 7: Data Storage (120 min)
- Chapter 8: Diagnostics (90 min)
- Chapter 9: Multi-Service (180 min)
- Chapter 10: Production Capstone (240 min)

#### 2. Create Prompt Pattern Library (16-24 hours)
**Status**: 📋 Structure defined, content pending

**Required Content**:
- 30+ reusable prompt templates
- Ask mode patterns (10+)
- Agent mode patterns (15+)
- Service-specific patterns (15+ by Azure service)
- Advanced patterns (5+)

**Format for each pattern**:
- Use case description
- Template with variables
- Concrete example
- Expected output
- Validation checklist

**Why High**: Dramatically accelerates student prompt engineering skills

#### 3. Populate data/ Folder (12-16 hours)
**Status**: 📋 Structure defined, files pending

**Required Files**:
- 5+ sample Bicep templates (tested and validated)
- 5+ sample Terraform configs (tested and validated)
- 10+ architecture diagrams (Chapters 1, 5, 6, 9, 10)
- Cost estimation spreadsheet (with formulas)
- 5+ security checklists (per Azure service)
- 5+ troubleshooting guides (common issues)

**Why High**: Provides reference materials students compare against AI-generated output

#### 4. Create Supplementary Files (4-8 hours)
**Status**: 📋 Specifications complete

**Required Files**:
- CODE_OF_CONDUCT.md (copy from LangChainJS)
- SECURITY.md (copy from LangChainJS)
- MAINTAINERS.md (create new)
- CONTRIBUTING.md (create new)
- CHANGELOG.md (create new)

**Why High**: Professionalism, community standards, maintenance procedures

**Total High Priority**: 80-120 hours

---

### 🟢 MEDIUM PRIORITY (Significant Enhancement)

**Estimated Effort**: 48-72 hours (1-2 weeks full-time)

#### 1. Advanced Validation Scripts (16-24 hours)
- `validate-prompts.ts` - Test prompt outputs
- `validate-templates.ts` - Verify Bicep/Terraform
- `validate-all-parallel.ts` - Run all tests concurrently

#### 2. GitHub Actions Workflows (8-12 hours)
- `validate-prompts.yml` - CI validation
- `cost-check.yml` - PR cost impact check
- `security-scan.yml` - Security validation

#### 3. Enhanced Chapter Content (16-24 hours)
- Real-world scenarios for all chapters
- Architecture diagrams for all chapters
- Video walkthroughs (optional)
- Interactive exercises beyond assignments

#### 4. Future/ Folder Content (8-12 hours)
- 11-multi-region-deployments/
- 12-azure-devops-integration/
- 13-advanced-kubernetes/
- 14-cost-optimization-advanced/

**Total Medium Priority**: 48-72 hours

---

### 🔵 LOW PRIORITY (Polish)

**Estimated Effort**: 40-60 hours

#### 1. Community Building (16-24 hours)
- Discord server setup
- Monthly office hours schedule
- FAQ from beta testers
- Community contribution guidelines

#### 2. Marketing Materials (12-16 hours)
- Course promotional graphics
- Social media templates
- Sample chapter previews
- Testimonials from beta testers

#### 3. Accessibility Improvements (12-20 hours)
- Screen reader compatibility
- Keyboard navigation
- High-contrast themes
- Multi-language support (future)

**Total Low Priority**: 40-60 hours

---

### Total Estimated Effort

**Course Implementation**: 280-416 hours
- Critical: 112-164 hours
- High: 80-120 hours
- Medium: 48-72 hours
- Low: 40-60 hours

**Timeline**:
- Full-time (40 hrs/week): 7-10 weeks
- Part-time (20 hrs/week): 14-21 weeks
- With team of 2-3: 5-7 weeks

---

### Phased Implementation Plan

#### Phase 1: Foundation (Weeks 1-3)
**Goal**: Minimum viable course for beta testing

**Deliverables**:
- ✅ Chapter 0 complete (safety baseline)
- ✅ Chapters 1-3 fully detailed
- ✅ Core validation scripts working
- ✅ GLOSSARY.md complete
- ✅ Basic prompt pattern library

**Success Criteria**:
- 5 beta testers can complete Chapters 0-3
- Zero critical bugs reported
- Students feel safe regarding costs
- All examples execute successfully

#### Phase 2: Expansion (Weeks 4-6)
**Goal**: Complete core course content

**Deliverables**:
- Chapters 4-7 fully detailed
- All validation scripts complete
- data/ folder populated
- Supplementary files added
- GitHub Actions configured

**Success Criteria**:
- Beta testers can complete through Chapter 7
- Automated validation passes
- Cost estimates proven accurate
- Security checklists validated

#### Phase 3: Capstone & Polish (Weeks 7-9)
**Goal**: Production-ready course

**Deliverables**:
- Chapters 8-10 complete
- Future/ folder content
- Community infrastructure
- All documentation finalized
- Marketing materials

**Success Criteria**:
- 10+ beta testers complete full course
- 90%+ satisfaction rating
- Zero critical issues
- Course ready for public launch

#### Phase 4: Launch & Iterate (Week 10+)
**Goal**: Public launch and continuous improvement

**Activities**:
- Public course launch
- Community building
- Gather feedback
- Monthly updates
- New chapter development

---

### Quality Gates

**Before Beta Testing**:
- [ ] Chapters 0-3 complete and tested
- [ ] Validation scripts pass all tests
- [ ] GLOSSARY.md has 150+ entries
- [ ] All costs verified under $50/chapter
- [ ] Cleanup scripts tested (no orphaned resources)

**Before Public Launch**:
- [ ] All 11 chapters complete
- [ ] 10+ beta testers completed successfully
- [ ] All validation scripts passing
- [ ] Zero critical security issues
- [ ] Cost estimates accurate within 10%
- [ ] All supplementary files present
- [ ] GitHub Actions configured and working

**Post-Launch Maintenance**:
- [ ] Monthly validation script runs
- [ ] Quarterly cost estimate updates
- [ ] Immediate fixes for Azure breaking changes
- [ ] Community feedback incorporated monthly

---

## Course Quality Assurance and Validation Criteria

### Overview

This section defines the quality standards and validation processes to ensure this course meets professional educational standards and provides real value to students.

---

### Quality Standards

#### 1. Technical Accuracy (CRITICAL)

**Standard**: All technical content must be factually correct and reflect current Azure and GitHub Copilot for Azure capabilities.

**Validation Methods**:
- ✅ Every prompt example tested against actual GitHub Copilot for Azure
- ✅ Every Azure CLI command validated with `az --help` or execution
- ✅ Every Bicep template validated with `az bicep build`
- ✅ Every Terraform configuration validated with `terraform validate`
- ✅ Cost estimates verified against Azure pricing calculator
- ✅ All generated code tested in real Azure environment

**Pass Criteria**:
- 100% of examples execute successfully
- 0 technical errors or inaccuracies
- All links resolve correctly
- All costs accurate within 10%

**Testing Frequency**:
- Before every release
- Monthly for existing content
- Immediately after Azure/Copilot updates

---

#### 2. Educational Quality (CRITICAL)

**Standard**: Course must follow proven pedagogical principles and be accessible to target audience.

**Validation Methods**:
- ✅ Each chapter follows Concept → Scenario → Problem → Solution pattern
- ✅ Learning objectives are measurable and achievable
- ✅ Assignments have clear success criteria
- ✅ Progressive complexity (beginner → advanced)
- ✅ Real-world scenarios motivate learning
- ✅ "Why this matters" sections provide context

**Pass Criteria**:
- Beta testers with target skill level can complete independently
- 90%+ of students achieve stated learning objectives
- Average chapter completion time within 20% of estimate
- Student satisfaction rating ≥ 4.5/5.0

**Testing Frequency**:
- Beta testing before launch
- Student surveys after each cohort
- Quarterly review of completion rates

---

#### 3. Safety & Cost Protection (CRITICAL)

**Standard**: Students must be protected from unexpected Azure costs and security vulnerabilities.

**Validation Methods**:
- ✅ Chapter 0 completed before any Azure deployments
- ✅ Billing alerts configured before first resource creation
- ✅ Cost estimates provided for every chapter
- ✅ Free tier options highlighted where available
- ✅ Cleanup scripts tested and confirmed working
- ✅ No hardcoded secrets or credentials
- ✅ Security best practices followed throughout

**Pass Criteria**:
- Zero students surprised by Azure bills
- 100% of resources cleaned up successfully with provided scripts
- Zero security vulnerabilities in examples
- All deployments follow security baseline from Chapter 0

**Testing Frequency**:
- Before every release
- After each beta tester cohort
- Monthly audit of cleanup procedures

---

#### 4. Generate → Validate → Execute Workflow (CRITICAL)

**Standard**: Course must consistently teach the correct GitHub Copilot for Azure workflow.

**Validation Methods**:
- ✅ Every example shows AI generating code
- ✅ Every example shows validation step
- ✅ Every example shows manual execution
- ✅ Students never expect direct resource creation
- ✅ Prompts use correct tool names (#azure_generate_azure_cli_command, etc.)

**Pass Criteria**:
- 100% of chapters follow workflow consistently
- Zero confusion about how GitHub Copilot for Azure works
- Beta testers can explain workflow in their own words
- Students develop prompt engineering skills progressively

**Testing Frequency**:
- Review every chapter before release
- Beta tester interviews
- Student surveys on understanding

---

#### 5. Code Quality & Best Practices (HIGH)

**Standard**: All generated code and examples follow Azure and IaC best practices.

**Validation Methods**:
- ✅ Resource naming follows Azure conventions
- ✅ Tagging used consistently for tracking
- ✅ Security flags present (--https-only, etc.)
- ✅ No deprecated Azure CLI commands
- ✅ Bicep/Terraform follows official style guides
- ✅ Comments explain non-obvious choices

**Pass Criteria**:
- Automated linting passes for all templates
- Security scanning shows zero high/critical issues
- Code follows Azure Well-Architected Framework
- Professional developers approve code quality

**Testing Frequency**:
- Before every release
- Automated on every commit (GitHub Actions)
- Quarterly code quality audit

---

### Validation Process

#### Pre-Release Validation

**1. Automated Testing** (runs on every commit)
```bash
npm run validate:all-parallel
# Runs:
# - validate-prompts.ts (10 concurrent)
# - validate-commands.ts (10 concurrent)
# - validate-templates.ts (5 concurrent)
# - cost-estimator.ts (sequential)
# - cleanup-checker.ts (sequential)
# - security-scan.ts (sequential)
#
# Pass Criteria: 0 failures, 0 warnings
```

**2. Manual Review Checklist**
- [ ] New content follows course structure
- [ ] Prompt examples tested in actual GitHub Copilot for Azure
- [ ] Cost estimates calculated and reasonable
- [ ] Cleanup scripts tested (no orphaned resources)
- [ ] Security checklist completed
- [ ] Links verified working
- [ ] Spelling and grammar checked
- [ ] Code formatted consistently

**3. Beta Testing** (before public release)
- Recruit 10-15 beta testers from target audience
- Provide clear feedback mechanism
- Track completion rates and time spent
- Conduct exit interviews
- Iterate based on feedback

---

#### Post-Release Monitoring

**1. Student Metrics**
- Chapter completion rates
- Time spent per chapter
- Common points of confusion (support tickets)
- Assignment success rates
- Course completion rate
- Student satisfaction scores

**Target Metrics**:
- Chapter completion rate ≥ 85%
- Course completion rate ≥ 70%
- Average satisfaction ≥ 4.5/5.0
- Would recommend ≥ 90%

**2. Technical Monitoring**
- GitHub Issues for bugs
- Validation script failure rates
- Azure CLI breaking changes
- GitHub Copilot for Azure updates
- Cost calculation accuracy

**Alert Thresholds**:
- Any critical bug → Immediate fix required
- Validation failure rate > 5% → Investigate within 24 hours
- Student cost complaint → Review cost estimates within 48 hours

**3. Community Engagement**
- Discord activity level
- GitHub contribution rate
- Office hours attendance
- Community-created content

---

### Continuous Improvement Process

**Monthly**:
- Review student feedback and support tickets
- Run full validation suite
- Update cost estimates for Azure pricing changes
- Check for Azure CLI/Copilot updates
- Review and address GitHub Issues

**Quarterly**:
- Comprehensive course review
- Beta test any major changes
- Update architecture diagrams if Azure UX changed
- Review and update GLOSSARY.md
- Audit security practices

**Annually**:
- Major course refresh if needed
- Add new chapters for new Azure services
- Deprecate outdated content
- Review and update all examples
- Solicit community input on direction

---

### Success Metrics (6 Months Post-Launch)

**Enrollment & Completion**:
- Target: 500+ students enrolled
- Target: 70%+ completion rate
- Target: 85%+ chapter completion rate

**Quality Metrics**:
- Target: 4.5/5.0 average rating
- Target: 90%+ would recommend
- Target: <5% negative feedback on costs
- Target: <2% support tickets per student

**Technical Metrics**:
- Target: 99%+ validation success rate
- Target: Zero critical security issues
- Target: <1% student cost complaints
- Target: All cleanup scripts 100% successful

**Community Metrics**:
- Target: 50+ community contributions
- Target: 100+ Discord members
- Target: 10+ community-created examples
- Target: 5+ translated versions (future)

---

## Course Development Reference

This plan provides a comprehensive learning path for Azure MCP beginners while maintaining the quality and structure of the LangChainJS course!

**Reference Implementation**: [LangChain.js for Beginners](https://github.com/danwahlin/langchainjs-for-beginners)
- **Local Path**: `/Users/danwahlin/Desktop/demos/LangChainJS-for-Beginners`
- **Use as Template**: Review chapter structure, README patterns, assignment format, and supplementary materials
- **Key Files to Reference**:
  - `README.md` - Main course introduction and structure
  - `GLOSSARY.md` - Comprehensive term definitions (21KB file)
  - `scripts/validate-examples.ts` - Validation script pattern
  - `scripts/validate-examples-parallel.ts` - Parallel testing approach
  - Any chapter's `README.md` - Example scenario-based lead-ins to code/prompts
  - Any chapter's `assignment.md` - Assignment format and structure

**Teaching Philosophy**: Both courses use the same pattern:
1. Concept introduction with real-world context
2. Scenario-based learning (problem → solution)
3. Hands-on examples students can run/try
4. Assignments that reinforce learning
5. Progressive complexity (beginner → advanced)
6. Production-ready, deployable solutions
