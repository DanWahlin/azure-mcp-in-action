# Chapter 2: Advanced Prompt Patterns with agent mode

Mastering agent mode for complex multi-step deployments, conditional resource creation, and bulk operations. In this chapter, you'll learn advanced prompt engineering patterns that let you efficiently create multiple resources with dependencies, handle conditional logic, and perform bulk operations - all using natural language prompts with GitHub Copilot agent mode.

## Prerequisites

- Completed [Course Setup](../00-course-setup/README.md)
- Completed [Chapter 1: First Deployment](../01-first-deployment/README.md)

## 🎯 Learning Objectives

- ✅ Master prompt engineering patterns for Azure MCP resource creation
- ✅ Use Azure MCP for complex multi-step deployments
- ✅ Handle conditional logic and error handling with Azure MCP
- ✅ Create bulk resources efficiently
- ✅ Query and update existing resources
- ✅ Verify complex deployments across multiple resources

## Real-World Scenario

> Your company is onboarding 10 new developers who each need identical development environments: storage account, key vault, and container registry. Instead of manually creating each environment or writing scripts, you'll use Azure MCP to directly provision all resources with natural language prompts.

---

## Part 1: Choosing the Right Mode

Before diving into patterns, let's clarify when to use agent mode versus ask mode.

### Mode Selection Decision Tree

```
Do you need to CREATE, UPDATE, or DELETE Azure resources?
  └─> YES → Use agent mode (80% of use)
      Example: "Create a storage account named mystorageacct..."
      What happens: Generates code → Shows "Continue?" → Executes after approval

Do you need ADVICE on architecture, service selection, or best practices?
  └─> YES → Use ask mode with @azure
      Example: "@azure Which database should I use for..."
      What happens: Provides guidance and recommendations
```

### Quick Reference Table

| Task | Mode | You Say | What Happens |
|------|------|---------|--------------|
| Create storage account | agent mode | "Create storage account..." | Generates code → Approve → Executes |
| Which database to use? | ask mode | "@azure Which database..." | Provides guidance |
| Update existing resource | agent mode | "Update app service plan..." | Generates code → Approve → Executes |
| Learn best practices | ask mode | "@azure What are best practices..." | Provides recommendations |

**This chapter focuses on agent mode** - the primary way you'll create and manage Azure resources.

---

## Part 2: Basic Prompt Patterns for Azure MCP

### Pattern 1: Single Resource Creation

**Prompt to Azure MCP**:
```
Create a [RESOURCE_TYPE] named [NAME] in [REGION] using [SKU/TIER]
with [SECURITY_OPTIONS]
```

#### Example

**Activate agent mode**, then use this prompt:
```
Create a storage account named learnstg2024 in East US using Standard_LRS
with blob public access disabled and HTTPS-only enabled.
```

**What happens in agent mode**:
1. Generates infrastructure code (Bicep or CLI commands)
2. Shows "Continue?" button for you to review
3. After approval, executes commands in terminal
4. Commands create the storage account with your settings
5. Returns confirmation with account details

**Verify**: Check Azure Portal or use `az storage account show --name learnstg2024`

### Pattern 2: Resource with Dependencies

**Prompt to Azure MCP**:
```
Create [RESOURCE] in [REGION] with [DEPENDENCIES].
Include all prerequisite resources.
```

#### Example

```
Create an Azure Key Vault named learn-kv-[YOUR-INITIALS] in West US.
Include resource group learn-kv-rg if it doesn't exist.
Configure for soft-delete and purge protection.
```

**agent mode will**:
1. Generate code → Show "Continue?" → Execute after approval
2. Create resource group if needed
3. Create Key Vault with specified configuration
4. Apply security settings and tag all resources

### Pattern 3: Query and Filter

**Prompt to Azure MCP**:
```
List all [RESOURCE_TYPE] in [SCOPE] where [CONDITION]
```

#### Example

```
List all storage accounts in my subscription where location is East US
and show the name, SKU, and tags
```

**agent mode will** query and return filtered results.

---

## Part 3: Advanced Patterns for Azure MCP

### Pattern 4: Conditional Creation

**Prompt to Azure MCP**:
```
Check if resource group dev-team-rg exists in my subscription.
If it doesn't exist, create it in East US.
If it exists, tell me its current configuration.
```

**agent mode will**:
1. Generate code → Show "Continue?" → Execute after approval
2. Query for the resource group
3. Create it if missing, or return details if it exists
4. Handle the conditional logic automatically

### Pattern 5: Bulk Operations

**Prompt to Azure MCP**:
```
Create 5 storage accounts for our development team:
- Names: devstg01, devstg02, devstg03, devstg04, devstg05
- Location: East US
- SKU: Standard_LRS
- Resource group: dev-storage-rg (create if doesn't exist)
```

**agent mode will**:
1. Generate code → Show "Continue?" → Execute after approval
2. Create the resource group if needed
3. Create all 5 storage accounts
4. Apply consistent configuration
5. Return summary of created resources

**Verify**: `az storage account list --resource-group dev-storage-rg --output table`

### Pattern 6: Configuration Updates

**Prompt to Azure MCP**:
```
Update my existing web app demo-app-[YOUR-INITIALS] with:
- Node.js 20 runtime
- Always On enabled
- Minimum TLS version 1.2
- HTTPS only enforced
```

**agent mode will**:
1. Generate code → Show "Continue?" → Execute after approval
2. Update the web app configuration
3. Apply all settings and restart the app if needed
4. Return updated configuration details

**Verify**: `az webapp config show --name demo-app-[YOUR-INITIALS] --resource-group learning-rg-[YOUR-INITIALS]`

---

## Part 4: Verification and Troubleshooting Patterns

### Pattern 7: Pre-creation Validation

**Prompt to Azure MCP**:
```
Before creating an AKS cluster in East US, verify:
1. My subscription has enough quota for Standard_DS2_v2 VMs
2. The region supports AKS
3. The Microsoft.ContainerService provider is registered

If any check fails, tell me how to fix it.
```

**agent mode will**:
1. Generate diagnostic queries → Show "Continue?" → Execute after approval
2. Run all validation checks
3. Report on quota availability and verify provider registration
4. Provide remediation steps if needed

### Pattern 8: Resource Dependency Mapping

**Prompt to Azure MCP**:
```
Show me all resources in resource group dev-team-rg
and their dependencies on each other.
Which resources depend on the storage account devstg01?
```

**agent mode will**:
1. Generate analysis queries → Show "Continue?" → Execute after approval
2. List all resources in the group
3. Identify dependencies and help you understand deletion order

---

## Part 5: Complete Environment Patterns

### Pattern 9: Multi-Resource Environment

**Prompt to Azure MCP**:
```
Create a complete development environment for developer John Doe:
1. Resource group: john-dev-rg in West US
2. Storage account: johndstg2024 (Standard_LRS, private)
3. Key Vault: john-kv-2024 (soft-delete enabled)
4. Container Registry: johnacr2024 (Basic SKU)

Configure with:
- All resources in same region
- Secure defaults (HTTPS, private access where possible)
```

**agent mode will**:
1. Generate infrastructure code → Show "Continue?" → Execute after approval
2. Create all 4 resources in correct order
3. Configure security settings
4. Return summary with connection strings

**Verify**: Navigate to Azure Portal → Resource Groups → john-dev-rg

### Pattern 10: Template-Based Replication

**Prompt to Azure MCP**:
```
I just created a dev environment for John (john-dev-rg).
Create an identical environment for Jane Doe:
- Replace "john" with "jane" in all resource names
- Same region, SKUs, and configuration
- Update developer tag to jane
```

**agent mode will**:
1. Generate replication code → Show "Continue?" → Execute after approval
2. Replicate the environment structure
3. Update names and tags appropriately
4. Maintain same configuration and create parallel environment

---

## Assignment

Use Azure MCP to complete these tasks:

1. Create complete dev environments for 3 developers (Alice, Bob, Carol)
2. Each environment should include: resource group, storage, Key Vault, Container Registry
3. Use consistent naming and tagging
4. Verify all resources were created correctly using Azure Portal and Azure CLI
5. Use Azure MCP to query and list all resources across the 3 environments
6. Clean up all resources when complete

### Success Criteria

- ✅ Used Azure MCP to create 3 complete environments
- ✅ All resources have consistent configuration
- ✅ All resources properly tagged (developer name, environment, chapter)
- ✅ Verified creation using Portal, CLI, and Azure MCP queries
- ✅ Successfully replicated environment structure for each developer
- ✅ Cleaned up all resources using Azure MCP

---

## Cleanup Using Azure MCP

> [!IMPORTANT]
> Complete this cleanup to avoid unexpected Azure charges. This chapter had you create multiple resource groups and resources. Clean them all up before proceeding to Chapter 3.

### Method 1: Use Azure MCP (RECOMMENDED)

**List resources first**:
```
List all resource groups in my subscription
```

**Delete using agent mode**:
```
Delete resource groups: john-dev-rg, jane-dev-rg, dev-storage-rg, dev-team-rg, learn-kv-rg
```

**agent mode will**:
1. Generate deletion commands → Show "Continue?" → Execute after approval
2. Delete all specified resource groups
3. Remove all contained resources
4. Confirm deletion completion

### Method 2: Manual Cleanup with Azure CLI

```bash
# Delete resource groups manually
az group delete --name john-dev-rg --yes --no-wait
az group delete --name jane-dev-rg --yes --no-wait
az group delete --name dev-storage-rg --yes --no-wait
az group delete --name dev-team-rg --yes --no-wait
az group delete --name learn-kv-rg --yes --no-wait
```

### Verify Deletion

```
List all resource groups in my subscription
# Verify Chapter 2 resource groups are gone
```

---

## Key Takeaways

1. **Azure MCP Handles Complexity**: Natural language prompts create complex multi-resource environments
2. **Patterns Are Reusable**: Successful prompts can be adapted for similar deployments
3. **Verification is Essential**: Always verify resources using Portal, CLI, and Azure MCP queries
4. **Conditional Logic Works**: Azure MCP handles "if exists, skip" and similar logic automatically
5. **Bulk Operations Are Easy**: Create multiple similar resources with one prompt
6. **Your Prompts Are Documentation**: Well-written prompts serve as infrastructure documentation

---

## What's Next?

**[Chapter 3: Infrastructure-as-Code with Bicep](../03-bicep-templates/README.md)**

Now that you've mastered Azure MCP for direct resource creation, you'll learn how to generate Bicep templates for repeatable, version-controlled infrastructure deployments.
