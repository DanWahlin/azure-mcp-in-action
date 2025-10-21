# AI Agent Guide for Azure MCP in Action

> **Purpose**: This course teaches Azure infrastructure deployment through AI-assisted workflows. This guide helps AI agents understand the project's architecture, conventions, and workflows to assist effectively.

## Project Type

Educational course repository teaching Azure deployment via Azure MCP and AI-first infrastructure patterns.

## Core Principles

1. **Generate → Approve → Execute → Verify**: GitHub Copilot agent mode generates infrastructure code, gets approval, executes commands, then students verify
2. **Cost-Aware**: Every deployment includes cost estimates and mandatory cleanup instructions
3. **Real-World Projects**: Deploy production OSS apps (Ghost, n8n, Superset, Metabase, Supabase, Strapi), not toy examples
4. **AI-First Interface**: Students use agent mode in GitHub Copilot for Azure to generate and execute deployment commands with approval gates
5. **Portfolio-Driven**: Each chapter provides resume-worthy credentials

## Repository Structure

```
azure-mcp-in-action/
├── 00-course-setup/          # MANDATORY: Billing protection & safety setup
├── 01-04/                    # Foundation: CLI, Bicep, Terraform
├── 05-09/                    # Real OSS deployments with progressive complexity
├── 10-production-deployment/ # Capstone combining all skills
├── prompts/                  # Reusable AI prompt patterns (currently empty, to be populated)
├── data/                     # Reference materials (diagrams, checklists, templates)
└── scripts/                  # Validation and cleanup helpers (currently empty, to be populated)
```

### Chapter Structure Pattern
```
XX-chapter-name/
├── README.md          # Objectives, prompts, assignments (primary content)
├── code/              # Starter code (often empty - students generate with AI)
├── samples/           # Reference examples (often empty initially)
└── solution/          # Solution files for validation
```

## Agent Capabilities

### When Assisting with Chapter Content

**DO:**
- Start every chapter with a real-world scenario ("Your team needs...")
- Include cost estimates upfront (`$0` with cleanup vs `$35/month` if running)
- Provide examples of both modes: agent mode (for actions), ask mode with `@azure` (for learning)
- Add mandatory cleanup section with explicit agent mode prompts
- Use three verification methods (Portal, CLI, Agent queries) after resource creation
- Reference specific OSS projects when applicable (chapters 5-9)
- Include instructions for activating agent mode (select from dropdown)
- Emphasize the approval workflow (review code before clicking "Continue")

**DON'T:**
- Suggest deployments without cleanup instructions
- Use generic placeholders instead of specific examples (use `demo-app-dw-20241019` not `<app-name>`)
- Assume deep Azure knowledge (explain service choices)
- Skip cost transparency
- Use tool-specific commands like `#azure_generate_azure_cli_command` in agent mode examples

### When Generating Azure Commands

**Naming Conventions:**
- Resource groups: `[purpose]-rg-[initials]` → `learning-rg-dw`
- App Services: `[app]-[initials]-[date]` → `demo-app-dw-20241019`
- Always include student initials for uniqueness

**Required Elements:**
```bash
# Every command must include:
--tags environment=learning course=azure-copilot chapter=XX

# Security defaults:
--https-only true              # For web apps
# Use managed identities        # Instead of connection strings
# Store secrets in Key Vault    # Never hardcode
```

**Standard Verification Checklist:**
```
✓ agent mode showed approval prompt before executing
✓ Student reviewed code before clicking "Continue"
✓ Unique resource names (initials + date)
✓ Correct region specified
✓ Appropriate SKU/tier for scenario
✓ Security settings applied (HTTPS, private access, etc.)
✓ Resources created in correct dependency order
✓ Tags included for tracking
✓ Verified in Azure Portal AND Azure CLI
```

## GitHub Copilot Prompt Patterns

### agent mode (Primary - 80% of use)

**Activation**: Select "Agent" from the mode dropdown in GitHub Copilot Chat

**Basic Pattern (Chapters 1-2)**:
```
Create [resource] named [name] in [region] using [tier/sku]
with [security options]
```

**Advanced Pattern (Chapters 5+)**:
```
Deploy production-ready [application] with:
- [Service 1] ([tier])
- [Service 2] with [specific config]
- Managed identity for secure access
- Application Insights for monitoring
- Include all security best practices
Use resource group: [name] in [region]
```

**What happens**:
1. Agent generates infrastructure code (Bicep, CLI commands, etc.)
2. Agent shows "Continue?" button
3. Student reviews code and clicks "Continue"
4. Agent executes commands in terminal
5. Commands create Azure resources
6. Agent reports success

**Important**: Always include "Azure" in your prompt so the agent selects Azure tools.

### ask mode (For Learning & Planning)

**Activation**: Select "Ask" from the mode dropdown in GitHub Copilot Chat

**Architecture Guidance**:
```
@azure When should I use Azure Container Apps vs AKS?
Consider: team size, complexity, cost, and management overhead.
```

**Service Selection**:
```
@azure I need to store 10TB of files with occasional access.
Which Azure storage service should I use and what tier?
```

**Important**: Use `@azure` prefix in ask mode to scope questions to Azure.

### Troubleshooting in agent mode

**Pattern**:
```
Why is my [resource] experiencing [problem]?
Investigate [specific symptoms]
```

**What happens**: Agent analyzes logs, metrics, and provides diagnostic information and solutions.

### Cleanup Pattern (Every Chapter)

**Direct Cleanup (Recommended)**:
```
Delete all resources from Chapter X:
- [Specific resource 1]
- [Specific resource 2]
- Resource group [name]
```

**Or tag-based cleanup**:
```
Delete all resource groups tagged with chapter=XX
```

## Azure Service Deployment Patterns

### App Service (Chapters 1, 5)
```bash
# Standard flow: Resource Group → App Service Plan → Web App
az group create --name [rg-name] --location [region] --tags [tags]
az appservice plan create --name [plan] --resource-group [rg] --sku F1 --is-linux
az webapp create --name [app] --resource-group [rg] --plan [plan] \
  --runtime "NODE|LTS" --https-only true
```

### Container Apps (Chapter 6 - n8n)
```bash
# Container Apps Environment → Container App → Configure ingress
# Always include: auto-scaling, managed identity, Key Vault integration
```

### AKS (Chapter 6 - Apache Superset)
```bash
# ACR → AKS cluster → Deploy workload
# Complex scenario, emphasize Kubernetes credential value
```

### Multi-Service Architecture (Chapter 9 - Supabase, Strapi)
```bash
# PostgreSQL → Container Apps → Redis → Blob Storage → App Insights
# Service-to-service auth via managed identities
```

## Content Creation Guidelines

### Chapter README Template
```markdown
# Chapter X: [Title]

**Title**: [One-line description]
**Focus**: [Key skill being taught]
**Estimated Time**: X minutes
**Prerequisites**: Chapters [list]

## Learning Objectives
- ✅ [Specific, measurable objective]
- ✅ [Specific, measurable objective]

## Real-World Scenario
> Your team needs to [concrete business requirement]...

## Part 1: [Section Name]
[Instructions with AI prompts]

## Assignment
[Hands-on task]

### Success Criteria
- ✅ [Specific deliverable]
- ✅ [Measurable outcome]

## Cleanup
**⚠️ CRITICAL**: [Explicit cleanup instructions]
```

### When Explaining Architecture
Always include:
- **Why** this service over alternatives (cost, complexity, features)
- **Cost implications** (running vs cleaned up)
- **Trade-offs** (Container Apps vs AKS, SQL vs Cosmos DB)
- **Portfolio value** ("Deployed Superset on AKS" is interview-worthy)

### When Adding OSS Projects (Chapters 5-9)
Include:
- Project description and GitHub stars (credibility)
- Azure services required
- Cost estimate (monthly if running)
- Time to deploy
- Portfolio value statement
- Step-by-step prompts using agent mode with natural language

## Two GitHub Copilot Interaction Modes

### agent mode (Primary - 80% of interactions)
**Purpose**: Create, update, delete Azure resources; troubleshoot issues
**Activation**: Select "Agent" from mode dropdown in Copilot Chat
**How to use**: Natural language prompts with "Azure" in the text

**Example**:
```
Create a storage account named mystorageacct in East US using Standard_LRS
with blob public access disabled and HTTPS-only enabled
```

**What happens**:
- Agent generates infrastructure code
- Shows "Continue?" approval button
- After approval, executes terminal commands
- Commands create actual Azure resources

### ask mode (For Learning)
**Purpose**: Architecture questions, service selection, guidance, learning
**Activation**: Select "Ask" from mode dropdown in Copilot Chat
**How to use**: Use `@azure` prefix for Azure-scoped questions

**Example**:
```
@azure When should I use Azure Container Apps vs AKS?
Consider: team size, complexity, cost, and management overhead.
```

**What happens**:
- Provides explanations and guidance
- No code generation or execution
- Pure learning and planning

## Common Workflows

### Workflow 1: New Deployment
1. ask mode (`@azure`): Get architecture advice and service selection guidance
2. agent mode: Prompt with natural language to create resources
3. Review: Check generated code when "Continue?" appears
4. Approve: Click "Continue" to execute commands
5. Execute: Agent runs terminal commands that create resources
6. Verify: Confirm in Azure Portal, Azure CLI, and Agent queries
7. Document: Note what was created and cleanup prompts

### Workflow 2: Troubleshooting
1. agent mode: Describe the problem with natural language
2. Review: Agent analyzes and provides diagnostic findings
3. agent mode: Prompt to apply fixes
4. Review: Check fix code when "Continue?" appears
5. Approve: Click "Continue" to implement fixes
6. Verify: Confirm resolution in Portal/CLI
7. agent mode: Set up monitoring alerts to prevent recurrence

### Workflow 3: Cleanup (CRITICAL)
1. agent mode: Prompt to delete chapter resources
2. Review: Check deletion commands when "Continue?" appears
3. Approve: Click "Continue" to execute deletions
4. Verify: Check Azure Portal and CLI (all resources gone)
5. Confirm: No lingering costs

## Cost Management (First-Class Concern)

### Chapter 0 Setup (MANDATORY)
```
Billing alerts at: $10 (50%, 80%, 100%), $50 (80%, 100%), $100 (90%, 100%)
Dual notifications: Email + SMS
```

### Per-Chapter Cost Pattern
| Chapter | If Running | With Cleanup |
|---------|-----------|--------------|
| 0-4 | $0-20/month | $0 |
| 5 (Ghost) | $35/month | $0 |
| 6 (n8n) | $20-30/month | $0 |
| 6 (Superset/AKS) | $70-100/month | $0 |
| 9 (Supabase) | $60-80/month | $0 |

**Total if left running**: $265-370/month
**Total with cleanup**: **$0**

### Required Tags
```bash
--tags environment=learning course=azure-copilot chapter=XX
```

## Key Concepts to Reinforce

1. **AI Acceleration**: agent mode generates and executes deployment code - learn 10x faster than manual work
2. **Generate → Approve → Execute → Verify**: Agent creates code, you approve, agent executes, you verify
3. **Approval Gates**: Always review code before clicking "Continue" - you control what gets executed
4. **Progressive Complexity**: Chapters 0-4 foundation → 5-9 real deployments → 10 capstone
5. **Production-Grade**: Deploy actual OSS platforms used by Netflix, Airbnb, Mozilla
6. **Portfolio Building**: Each deployment is interview-worthy

## Files to Reference

- `README.md`: Course overview, prerequisites, quick start
- `00-course-setup/README.md`: **Start here** - billing protection critical
- `01-first-deployment/README.md`: Core Generate→Approve→Execute→Verify pattern with agent mode
- `02-cli-mastery/README.md`: agent mode prompt engineering techniques catalog
- `05-09/README.md`: Real OSS deployments (Ghost, n8n, Superset, Metabase, Supabase, Strapi)

## When Students Ask For Help

### "How do I deploy X?"
1. Determine chapter relevance (which OSS app or Azure service?)
2. Guide to relevant chapter README
3. Show appropriate agent mode prompt pattern
4. Remind to activate agent mode (select from dropdown)
5. Emphasize reviewing code before clicking "Continue"
6. Remind about cleanup

### "My deployment failed"
1. Use agent mode with natural language to diagnose the problem
2. Check common issues: naming conflicts, quota limits, region availability
3. Review verification checklist (was Azure Portal/CLI verification done?)
4. Use agent mode to apply fixes (review code before approving)
5. Document issue for future students

### "How much will this cost?"
1. Reference chapter cost table
2. Emphasize cleanup = $0
3. Show billing alert setup (Chapter 0)
4. Explain SKU/tier options (Free vs paid)
5. Provide cleanup prompt immediately

## Agent Anti-Patterns (Avoid)

❌ Generic advice ("write tests", "handle errors") - be specific to Azure and this course
❌ Placeholders (`<app-name>`) instead of examples (`demo-app-dw-20241019`)
❌ Deployments without cleanup instructions
❌ Assuming Azure expertise (explain service choices)
❌ Skipping cost transparency
❌ Using outdated Azure CLI syntax
❌ Hardcoding secrets instead of Key Vault
❌ Forgetting tags for resource tracking

## Success Metrics

Students should be able to:
- ✅ Use agent mode to create and manage complex Azure infrastructure
- ✅ Understand the Generate → Approve → Execute → Verify workflow
- ✅ Review generated code before approving execution
- ✅ Switch between agent mode and ask mode as needed
- ✅ Verify resources using three methods (Portal, CLI, Agent queries)
- ✅ Deploy 6+ production OSS applications to Azure
- ✅ Troubleshoot issues using agent mode with natural language
- ✅ Create portfolio-worthy infrastructure projects
- ✅ Keep total course cost under $50 (with proper cleanup)

---

**Remember**: This course teaches Azure through GitHub Copilot agent mode. agent mode **generates code and executes commands with approval gates** - it's not fully autonomous. Keep the "Generate → Approve → Execute → Verify" workflow central to all guidance, emphasizing that students review code before approving. Never sacrifice safety or cost awareness for speed.
