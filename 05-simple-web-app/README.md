# Chapter 5: Production Web Application Deployment (Ghost CMS)

Deploy a complete production-ready web application with custom domains, SSL, monitoring, and auto-scaling. In this chapter, you'll move beyond Hello World and deploy Ghost CMS (a real-world Node.js application) with all the infrastructure needed for production use, including database, storage, and deployment slots.

## Prerequisites

- Completed [Course Setup](../00-course-setup/README.md)
- Completed [Chapter 1: First Deployment](../01-first-deployment/README.md)
- Completed [Chapter 2: Advanced Prompt Patterns](../02-cli-mastery/README.md)
- Completed [Chapter 3: Infrastructure-as-Code with Bicep](../03-bicep-templates/README.md)
- Completed [Chapter 4: Terraform Basics](../04-terraform-basics/README.md)

## 🎯 Learning Objectives

- ✅ Deploy a complete web application (not just Hello World)
- ✅ Configure custom domains and SSL
- ✅ Set up application settings and secrets
- ✅ Implement monitoring and logging
- ✅ Configure auto-scaling
- ✅ Set up deployment slots (staging/production)

## Real-World Scenario

> Your team built a Node.js e-commerce API that needs to handle 10,000 requests/day. You need to deploy it to Azure with proper monitoring, auto-scaling, and zero-downtime deployments. You'll use GitHub Copilot agent mode to generate and execute deployment commands for all the necessary infrastructure.

---

## Part 1: Architecture Planning

### Ask for Guidance with ask mode

**Step 1: Switch to ask mode**

In GitHub Copilot Chat, select "Ask" from the mode dropdown

**Step 2: Ask with @azure**
```
@azure I need to deploy a Node.js API that:
- Handles 10,000 req/day
- Needs auto-scaling
- Requires 99.9% uptime
- Uses PostgreSQL database
- Stores files in blob storage

What Azure services should I use and why?
```

**What happens**: ask mode provides architectural recommendations with reasoning - no code generation or execution.

---

## Part 2: Deploy Complete Infrastructure with Azure MCP

### Prompt to Azure MCP

```
Create a production-ready Node.js API deployment with:
- App Service (B1 tier, can scale to S1)
- Azure Database for PostgreSQL Flexible Server
- Storage account for file uploads
- Application Insights for monitoring
- Key Vault for secrets
- Managed identity for secure access
- Deployment slots (staging + production)

Include all security best practices.
Resource group: ecommerce-api-rg in East US
```

**agent mode will**:
1. Generate infrastructure code → Show "Continue?" → Execute after approval
2. Create all resources in the correct order
3. Configure dependencies automatically
4. Apply security best practices and set up managed identities
5. Return connection details

### Verify Deployment

**Azure Portal**: Navigate to ecommerce-api-rg and verify all resources
**Azure CLI**:
```bash
az resource list --resource-group ecommerce-api-rg --output table
az webapp show --name [APP-NAME] --resource-group ecommerce-api-rg
```

---

## Part 3: Configure Monitoring with Azure MCP

```
Configure Application Insights alerts for my App Service [APP-NAME]:
- Alert if response time > 2 seconds
- Alert if error rate > 5%
- Alert if availability < 99%
- Alert if CPU usage > 80%

Send alerts to: alerts@company.com
```

**agent mode will**:
1. Generate configuration code → Show "Continue?" → Execute after approval
2. Create alert rules in Application Insights
3. Configure action groups for email notifications
4. Set up metric thresholds and enable alert notifications

---

## Assignment

1. Deploy a complete 3-tier web application
2. Implement CI/CD with GitHub Actions
3. Configure custom domain with SSL
4. Set up comprehensive monitoring
5. Perform zero-downtime deployment to production
6. Document all costs

### Success Criteria

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

### What is Ghost?

Professional publishing platform used by Mozilla, DuckDuckGo, and 46,000+ sites. Node.js-based CMS perfect for Azure App Service.

### Portfolio Value

"Deployed production Ghost CMS on Azure with App Service, MySQL, and Blob Storage"

### Azure Services Required

### Azure Services Required

- App Service (Linux, Node.js LTS)
- Azure Database for MySQL Flexible Server
- Blob Storage (Ghost content/images)
- CDN (optional, for performance)

---

### Deployment Using Azure MCP

#### Step 1: Create Complete Ghost Infrastructure

**Prompt to Azure MCP**:
```
Deploy Ghost CMS to Azure with:
- Resource group: ghost-rg-[MYINITIALS] in East US
- App Service B1 Linux with Node.js LTS runtime named ghost-app-[MYINITIALS]
- Azure Database for MySQL Flexible Server (Burstable B1ms) named ghost-mysql-[MYINITIALS]
- Storage account for Ghost content named ghoststorage[MYINITIALS]
- Configure all environment variables for Ghost
- Use managed identity for secure connections
- Enable Application Insights
```

**agent mode will**:
1. Generate infrastructure code → Show "Continue?" → Execute after approval
2. Create all infrastructure resources
3. Configure MySQL database with Ghost schema
4. Set up storage account with proper permissions
5. Enable Application Insights and return connection strings

#### Step 2: Configure Ghost Environment

**Prompt to Azure MCP**:
```
Configure app settings for ghost-app-[MYINITIALS]:
- NODE_ENV=production
- database__client=mysql2
- database__connection__host=[MYSQL-SERVER].mysql.database.azure.com
- database__connection__user=ghostadmin
- database__connection__password=[SECURE-PASSWORD]
- database__connection__database=ghost_production
- database__connection__ssl=true
- url=https://ghost-app-[MYINITIALS].azurewebsites.net
```

**agent mode will** generate config updates → ask "Continue?" → execute to update the App Service configuration with all Ghost settings.

#### Step 3: Deploy Ghost Container

**Prompt to Azure MCP**:
```
Deploy Ghost 5 to App Service ghost-app-[MYINITIALS]:
- Use Docker container: ghost:5-alpine from Docker Hub
- Configure for production use
- Enable continuous deployment
```

**agent mode will** generate deployment config → ask "Continue?" → execute to configure the App Service to run the Ghost container.

#### Step 4: Configure Custom Domain (Optional)

**Prompt to Azure MCP**:
```
Add custom domain myblog.com to App Service ghost-app-[MYINITIALS]
Configure free managed SSL certificate
Enable automatic HTTPS redirect
```

#### Step 5: Enable CDN (Optional)

**Prompt to Azure MCP**:
```
Create Azure CDN endpoint for storage account ghoststorage[MYINITIALS]
Configure caching for images and static content
Enable HTTPS
```

---

### Verification

**Access Ghost**: Navigate to `https://ghost-app-[MYINITIALS].azurewebsites.net/ghost`

#### Expected Result

```
✅ Ghost admin setup page loads
✅ Can create admin account
✅ Can publish test blog post
✅ Images upload to Azure Storage
✅ Public site displays correctly
```

---

### Quick Troubleshooting Prompts

#### Issue: Ghost Won't Start

```
@azure My Ghost app service ghost-app-[MYINITIALS] won't start.
Check: container logs, Node.js version, MySQL connectivity, environment variables
Provide diagnostic steps
```

#### Issue: Can't Upload Images

```
@azure Images aren't uploading in Ghost app ghost-app-[MYINITIALS]
Check: storage account connection, CORS settings, container permissions
Generate fix commands
```

---

### Assignment (Optional)

Use Azure MCP to:
1. Change to a custom Ghost theme
2. Configure SendGrid for email newsletters
3. Add custom domain with SSL
4. Create 3 sample blog posts

**Deliverable**: Ghost blog URL for portfolio

---

### Cleanup Using Azure MCP

> [!IMPORTANT]
> Complete this cleanup to avoid unexpected Azure charges. This chapter deployed production web applications with databases. **This is NOT free tier** - leaving resources running can cost $50+/month.

### Method 1: Use Azure MCP (RECOMMENDED)

**List resources first**:
```
List all resources in ghost-rg-[MYINITIALS]
Show all resources in ecommerce-api-rg
```

**Delete using Azure MCP**:
```
Delete resource groups: ghost-rg-[MYINITIALS], ecommerce-api-rg
```

**agent mode will**:
1. Generate deletion commands → Show "Continue?" → Execute after approval
2. Delete all resource groups
3. Remove all contained resources (App Service, databases, storage)
4. Confirm deletion completion

**Cost After Deletion**: $0/month

### Method 2: Manual Cleanup with Azure CLI

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

### Before You Delete

- [ ] ✅ **CRITICAL**: Export PostgreSQL database
- [ ] ✅ **CRITICAL**: Download files from blob storage
- [ ] Save Application Insights data or metrics screenshots
- [ ] Verify this is the correct resource group
- [ ] Confirm no production data is in this environment
- [ ] Document the total cost for your records

### Verify Deletion

**Verify resource group is gone (Bash/macOS/Linux):**
```bash
az group list --output table | grep ecommerce
```

**Verify resource group is gone (PowerShell/Windows):**
```powershell
az group list --output table | Select-String "ecommerce"
```


**Cost Impact**:
- Before deletion: ~$50-100/month
- After deletion: $0/month

---

## Key Takeaways

1. **Production Deployments**: Real applications require database, storage, monitoring, and secrets management
2. **Security First**: Use managed identities and Key Vault instead of hardcoded credentials
3. **Monitoring is Critical**: Set up alerts before problems occur
4. **Deployment Slots**: Enable zero-downtime deployments
5. **OSS Experience**: Deploying Ghost CMS demonstrates real-world Azure skills
6. **Cost Management**: Production services cost money - plan and monitor carefully

---

## What's Next?

**[Chapter 6: Containerized Applications (n8n, Apache Superset)](../06-containerized-apps/README.md)**

Now that you've deployed a traditional web app, you'll learn container orchestration with Azure Container Apps and Kubernetes (AKS) through two impressive OSS projects.
