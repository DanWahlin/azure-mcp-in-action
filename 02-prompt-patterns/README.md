# Chapter 2: Prompt Patterns with Agent mode

Learn [agent mode](../GLOSSARY.md#agent-mode) prompt patterns for complex multi-step deployments, conditional resource creation, and bulk operations.

## Prerequisites

- Completed [Course Setup](../00-course-setup/README.md)
- Completed [Chapter 1: First Deployment](../01-first-deployment/README.md)

## 🎯 Learning Objectives

- ✅ Learn prompt engineering patterns for [Azure MCP](../GLOSSARY.md#azure-mcp) resource creation
- ✅ Use Azure MCP for complex multi-step deployments
- ✅ Handle conditional logic and bulk operations
- ✅ Query and update existing resources
- ✅ Verify complex deployments across multiple resources

## Real-World Scenario

Your company is onboarding 10 new developers who each need identical development environments: [storage account](../GLOSSARY.md#storage-account), [key vault](../GLOSSARY.md#key-vault), and container registry. Instead of manually creating each environment or writing scripts, you'll use [Azure MCP](../GLOSSARY.md#azure-mcp) to provision all resources with natural language prompts.

---

## How Patterns Work

All patterns in this chapter follow the same workflow:

1. **You**: Write natural language prompt in Agent mode
2. **Agent**: Generates [infrastructure code](../GLOSSARY.md#infrastructure-as-code-iac) ([Bicep](../GLOSSARY.md#bicep)/CLI) and shows "Allow?"
3. **You**: Review and approve
4. **Agent**: Executes commands to create/modify Azure resources

**Reminder**: Use [agent mode](../GLOSSARY.md#agent-mode) for creating/modifying resources. Use [ask mode](../GLOSSARY.md#ask-mode) with `@azure` for questions.

---

## Prompt Patterns

### Pattern 1: Single Resource Creation

```
Create a storage account named learnstg in East US using Standard_LRS with blob public access disabled and HTTPS-only enabled.
```

**Verify**: `az storage account show --name learnstg`

### Pattern 2: Resource with Dependencies

```
Create an Azure Key Vault named learn-kv-[YOUR-INITIALS] in West US. Include resource group learn-kv-rg if it doesn't exist. Configure for soft-delete and purge protection.
```

**Note**: Agent automatically creates prerequisite resources ([resource groups](../GLOSSARY.md#resource-group)) before the main resource.

### Pattern 3: Query and Filter

```
List all storage accounts in my subscription where location is East US and show the name, SKU, and tags
```

### Pattern 4: Conditional Creation

```
Check if resource group dev-team-rg exists in my subscription.
If it doesn't exist, create it in East US.
If it exists, tell me its current configuration.
```

**Note**: Agent handles conditional logic automatically.

### Pattern 5: Bulk Operations

```
Create 5 storage accounts for our development team:
- Names: devstg01, devstg02, devstg03, devstg04, devstg05
- Location: East US
- SKU: Standard_LRS
- Resource group: dev-storage-rg (create if doesn't exist)
```

**Verify**: `az storage account list --resource-group dev-storage-rg --output table`

### Pattern 6: Configuration Updates

```
Update my existing web app demo-app-[YOUR-INITIALS] with:
- Node.js 20 runtime
- Always On enabled
- Minimum TLS version 1.2
- HTTPS only enforced
```

### Pattern 7: Pre-creation Validation

```
Before creating an AKS cluster in East US, verify:
1. My subscription has enough quota for Standard_DS2_v2 VMs
2. The region supports AKS
3. The Microsoft.ContainerService provider is registered

If any check fails, tell me how to fix it.
```

### Pattern 8: Resource Dependency Mapping

```
Show me all resources in resource group dev-team-rg and their dependencies on each other. Which resources depend on the storage account devstg01?
```

---

## Hands-On: Create Developer Environments

Now you'll apply these patterns to create complete development environments for multiple developers.

### Step 1: Create First Environment

**Prompt**:
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

**Verify**: Navigate to [Azure Portal](../GLOSSARY.md#azure-portal) → Resource Groups → john-dev-rg

### Step 2: Replicate Environment

**Prompt**:
```
I just created a dev environment for John (john-dev-rg).
Create an identical environment for Jane Doe:
- Replace "john" with "jane" in all resource names
- Same region, SKUs, and configuration
- Update developer tag to jane
```

### Assignment

Use the patterns above to complete these tasks:

1. Create complete dev environments for 3 developers (Alice, Bob, Carol)
2. Each environment should include: resource group, storage, [Key Vault](../GLOSSARY.md#key-vault), Container Registry
3. Use consistent naming and tagging
4. Verify all resources were created correctly using Portal and [Azure CLI](../GLOSSARY.md#azure-cli)
5. Use Azure MCP to query and list all resources across the 3 environments
6. Clean up all resources when complete

**Success Criteria**:
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

**Delete using Agent mode**:
```
Delete resource groups: john-dev-rg, jane-dev-rg, dev-storage-rg, dev-team-rg, learn-kv-rg, alice-dev-rg, bob-dev-rg, carol-dev-rg
```

**Agent mode will**:
1. Generate deletion commands → Show "Continue?" → Execute after approval
2. Delete all specified resource groups
3. Remove all contained resources
4. Confirm deletion completion

### Method 2: Manual Cleanup with Azure CLI

```bash
# Delete all Chapter 2 resource groups
az group delete --name john-dev-rg --yes --no-wait
az group delete --name jane-dev-rg --yes --no-wait
az group delete --name alice-dev-rg --yes --no-wait
az group delete --name bob-dev-rg --yes --no-wait
az group delete --name carol-dev-rg --yes --no-wait
az group delete --name dev-storage-rg --yes --no-wait
az group delete --name dev-team-rg --yes --no-wait
az group delete --name learn-kv-rg --yes --no-wait
```

**Verify Deletion**:
```
List all resource groups in my subscription
# Verify Chapter 2 resource groups are gone
```

---

## Key Takeaways

1. **Natural Language Works**: Complex multi-resource environments created with simple prompts
2. **Patterns Are Reusable**: Adapt successful prompts for similar deployments
3. **Agent Handles Complexity**: Dependencies, conditional logic, and bulk operations work automatically
4. **Always Verify**: Check Portal, CLI, or Agent queries after deployment
5. **Prompts Are Documentation**: Well-written prompts serve as infrastructure documentation

---

## What's Next?

**[Chapter 3: Infrastructure-as-Code with Bicep](../03-bicep-templates/README.md)**

Now that you've learned Azure MCP for direct resource creation, you'll learn how to generate Bicep templates for repeatable, version-controlled infrastructure deployments.
