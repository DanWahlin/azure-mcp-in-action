# Chapter 3: Infrastructure-as-Code with Bicep

Learn how to use agent mode to generate Bicep templates for reproducible, multi-environment Azure deployments. In this chapter, you'll master AI-generated infrastructure-as-code, creating reusable templates that can deploy identical environments across multiple regions with just parameter changes.

## Prerequisites

- Completed [Course Setup](../00-course-setup/README.md)
- Completed [Chapter 1: First Deployment](../01-first-deployment/README.md)
- Completed [Chapter 2: Advanced Prompt Patterns](../02-cli-mastery/README.md)

## 🎯 Learning Objectives

- ✅ Understand Bicep vs Azure CLI commands
- ✅ Generate Bicep templates using Azure MCP
- ✅ Validate Bicep syntax automatically
- ✅ Deploy resources using Bicep templates
- ✅ Parameterize templates for reusability
- ✅ Export existing resources as Bicep

## Real-World Scenario

> Your team needs to deploy identical staging and production environments across 3 Azure regions. Azure CLI commands would require hundreds of lines and be error-prone. Instead, you'll use Azure MCP to generate a Bicep template that you can deploy to any region with just parameter changes.

---

## Part 1: Understanding Bicep vs CLI

### When to Use Azure CLI

- One-off deployments
- Quick prototypes
- Administrative tasks
- Learning and exploration

### When to Use Bicep

- Repeatable deployments
- Multi-environment setups (dev/staging/prod)
- Complex architectures with dependencies
- Version-controlled infrastructure
- Team collaboration

---

## Part 2: Generating Your First Bicep Template

**Prompt to Azure MCP**:

```
Generate a Bicep template that creates:
- App Service plan (B1 SKU)
- Web app with Node.js LTS runtime
- Application Insights for monitoring
- Connection string configured automatically

Use parameters for app name and location.
Include outputs for app URL and instrumentation key.
```

### Expected Output (abbreviated)

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

## Part 3: Validating Bicep Templates

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

## Part 4: Deploying Bicep Templates

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

## Assignment

1. Generate a Bicep template for a 3-tier web app architecture
2. Include: storage account, database, app service, and CDN
3. Parameterize environment (dev/staging/prod)
4. Add conditional resources (CDN only in prod)
5. Deploy to two different environments
6. Export template from Azure Portal and compare

### Success Criteria

- ✅ Generated valid Bicep template
- ✅ Template passes validation
- ✅ Successfully deployed to multiple environments
- ✅ Parameters work correctly
- ✅ Outputs provide useful information
- ✅ Template is well-documented with comments

---

## Cleanup Using Azure MCP

**⚠️ IMPORTANT**: Complete this cleanup to avoid unexpected Azure charges

This chapter had you deploy resources using Bicep templates. The resources need to be deleted, but **keep your Bicep template files** for future reference.

### Method 1: Use Azure MCP (RECOMMENDED)

```
Delete resource groups: bicep-demo-rg, bicep-dev-rg, bicep-staging-rg
```

OR if you tagged resources:
```
List all resources tagged with chapter=03
Delete all resources tagged with chapter=03
```

**agent mode will**:
1. Generate deletion commands → Show "Continue?" → Execute after approval
2. Delete all specified resource groups
3. Remove all contained resources
4. Confirm deletion completion

### Method 2: Manual Cleanup with Azure CLI

```bash
# List resources in all Chapter 3 resource groups
az resource list --resource-group bicep-demo-rg --output table

# Delete the demo resource group
az group delete --name bicep-demo-rg --yes --no-wait

# If you created additional environments for the assignment:
az group delete --name bicep-dev-rg --yes --no-wait
az group delete --name bicep-staging-rg --yes --no-wait
```

### Before You Delete

- [ ] Save your Bicep template files locally (they will NOT be deleted)
- [ ] Verify the resource groups listed are from Chapter 3 only
- [ ] Confirm no production resources are in these groups
- [ ] Check that you have copies of any templates you want to keep

### Verify Deletion

```bash
# Check that resource groups are gone
az group list --output table | grep bicep

# Verify no Chapter 3 resources remain
az resource list --tag chapter=03 --output table
# Should return empty
```

**Note**: The Bicep templates you created are stored locally and will NOT be deleted. You may use these templates as references in future chapters.

---

## Key Takeaways

1. **Bicep for Repeatability**: Use Bicep when you need to deploy the same infrastructure multiple times
2. **Parameters Enable Reusability**: Parameterize environment-specific values
3. **What-If Prevents Mistakes**: Always preview changes before deploying
4. **Version Control Templates**: Store Bicep files in Git alongside application code
5. **Outputs Provide Information**: Use outputs to get deployment information
6. **Comments Are Documentation**: Well-commented templates are self-documenting

---

## What's Next?

**[Chapter 4: Terraform Basics with AI Assistance](../04-terraform-basics/README.md)**

Now that you've learned Bicep (Azure-native IaC), you'll explore Terraform for multi-cloud infrastructure deployments.
