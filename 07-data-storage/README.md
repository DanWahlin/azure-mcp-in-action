# Chapter 7: Data Storage Solutions (Metabase)

Master Azure data storage by deploying Metabase, a business intelligence platform that requires multiple storage types. In this chapter, you'll learn to choose and configure the right Azure storage services (SQL Database, Cosmos DB, Blob Storage) for different data needs, implementing backup strategies and cost optimization.

## Prerequisites

- Completed [Course Setup](../00-course-setup/README.md)
- Completed [Chapter 1: First Deployment](../01-first-deployment/README.md)
- Completed [Chapter 2: Advanced Prompt Patterns](../02-cli-mastery/README.md)
- Completed [Chapter 3: Infrastructure-as-Code with Bicep](../03-bicep-templates/README.md)
- Completed [Chapter 4: Terraform Basics](../04-terraform-basics/README.md)
- Completed [Chapter 5: Production Web Application](../05-simple-web-app/README.md)
- Completed [Chapter 6: Containerized Applications](../06-containerized-apps/README.md)

## 🎯 Learning Objectives

- ✅ Choose appropriate Azure storage service for use case
- ✅ Deploy and configure Azure SQL Database
- ✅ Set up Cosmos DB for NoSQL needs
- ✅ Configure Blob Storage with lifecycle policies
- ✅ Implement backup and disaster recovery
- ✅ Optimize storage costs

## Real-World Scenario

> Your application needs three types of storage: relational data (user accounts), document data (product catalog), and file storage (user uploads). You'll use Azure MCP to set up all three storage types with proper security and cost optimization.

---

## Part 1: Storage Decision Matrix

**Ask Azure MCP**:

```
@azure Help me choose Azure storage for:
1. User accounts (ACID transactions required)
2. Product catalog (flexible schema, 10M documents)
3. User-uploaded images (5TB expected)
4. Application logs (time-series data)

For each, recommend service, tier, and reasoning.
```

---

## Part 2: Deploy Multi-Storage Architecture

**Prompt to Azure MCP**:
```
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
Tags: chapter=07, project=storage-demo
```

**agent mode will**:
1. Generate infrastructure code → Show "Continue?" → Execute after approval
2. Create all storage resources in the correct order
3. Configure backup policies for databases
4. Set up lifecycle management for storage accounts
5. Create private endpoints for secure access
6. Enable managed identities and return connection strings

**Verify**:
- Azure Portal: Check storage-demo-rg for all resources
- Azure CLI: `az resource list --resource-group storage-demo-rg --output table`

---

## Assignment

1. Design storage architecture for a social media app
2. Include user data, posts, media files, and analytics
3. Implement proper security (private endpoints, encryption)
4. Set up backup and disaster recovery
5. Create cost optimization policies
6. Document expected monthly costs

### Success Criteria

- ✅ All storage types deployed correctly
- ✅ Data encrypted at rest and in transit
- ✅ Backup policies configured
- ✅ Lifecycle policies reduce costs
- ✅ Private endpoints secure access
- ✅ Cost under $100/month for expected load

---

## 🚀 Real-World Project: Deploy Metabase BI Platform

**⏱️ Time**: 25-35 minutes | **Cost**: ~$40-50/month | **Hype**: ⭐⭐⭐⭐ (37k GitHub stars)

### What is Metabase?

Open-source business intelligence platform. Easy-to-use alternative to Tableau. Perfect for visualizing data from Chapter 7's databases!

### Portfolio Value

"Deployed Metabase BI platform on Azure connecting multiple data sources (SQL, Cosmos DB, Storage)"

### Azure Services Required

- App Service (Java runtime)
- PostgreSQL (Metabase application database)
- Connections to Chapter 7 databases (optional)

---

### Deployment Using Azure MCP

#### Step 1: Deploy Metabase Infrastructure

**Prompt to Azure MCP**:
```
Deploy Metabase BI platform:
- Resource group: metabase-bi-rg in East US
- App Service B2 Linux with Java 17 runtime named metabase-app-[MYINITIALS]
- PostgreSQL Flexible Server B1ms named metabase-postgres-[MYINITIALS]
- Create database named metabase_app_db
- Configure firewall for App Service access
- Tag resources with chapter=07 project=metabase
```

**agent mode will**:
1. Generate infrastructure code → Show "Continue?" → Execute after approval
2. Create App Service and App Service Plan
3. Create PostgreSQL Flexible Server with database
4. Configure firewall rules for App Service
5. Apply tags to all resources and return connection details

#### Step 2: Deploy Metabase Container

**Prompt to Azure MCP**:
```
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

**agent mode will**:
1. Generate configuration code → Show "Continue?" → Execute after approval
2. Configure App Service to run Metabase container
3. Set all environment variables
4. Enable HTTPS and proper ports, then restart the app service

#### Prompt 3: Connect to Chapter 7 Databases (Optional)

```
@azure How do I connect Metabase to:
1. Azure SQL Database from Chapter 7
2. Cosmos DB with SQL API
3. Blob Storage data

Provide connection strings and configuration steps
```

---

### Verification

**Access Metabase**: Navigate to `https://metabase-app-[MYINITIALS].azurewebsites.net`

#### Expected Result

```
✅ Metabase welcome screen loads
✅ Can complete initial setup
✅ Can add data source connections
✅ Can run SQL queries
✅ Can create visualizations
✅ Can build dashboards
```

---

### Quick Setup Guide

#### First-Time Setup

1. **Language**: English
2. **Create Account**: Admin user
3. **Add Database**: Connect to your Chapter 7 SQL/Cosmos DB
4. **Usage Data**: Your preference

#### Create Your First Dashboard

1. Click "Ask a question"
2. Select database from Chapter 7
3. Write SQL query or use visual builder
4. Create chart (bar, line, pie, etc.)
5. Save to dashboard

---

### Quick Troubleshooting Prompts

#### Issue: Metabase Won't Start

```
@azure Metabase app service metabase-app-[MYINITIALS] won't start
Check: Java version, container logs, PostgreSQL connection, memory settings
Provide diagnostic steps
```

#### Issue: Can't Connect to Database

**Prompt to Azure MCP**:
```
Verify network connectivity from metabase-app-[MYINITIALS] to databases
Check: firewall rules, connection strings, SSL requirements
Diagnose connectivity issues
```

**agent mode will** generate diagnostic queries → ask "Continue?" → analyze firewall rules, connection strings, and provide diagnostic steps.

---

### Assignment (Optional)

Use Azure MCP and Metabase to:
1. Connect to all 3 Chapter 7 data sources (SQL, Cosmos, Storage)
2. Create 5 different visualization types
3. Build a comprehensive dashboard with 6+ cards
4. Set up email alerts for data changes
5. Create a SQL question with parameters

**Deliverable**: Metabase dashboard URL (with public link)

---

### Cleanup Using Azure MCP

**Prompt to Azure MCP**:
```
Delete resource group metabase-bi-rg and all resources inside it
```

**agent mode will** generate deletion commands → ask "Continue?" → delete Metabase App Service, PostgreSQL, and all related resources.

**Manual alternative**:
```bash
az group delete --name metabase-bi-rg --yes --no-wait
```

**Cost After Deletion**: $0/month

**Note**: If you want to keep Metabase as a portfolio project, scale down to B1 App Service (~$13/month)

---

## Cleanup Using Azure MCP

> [!CAUTION]
> Complete this cleanup to avoid unexpected Azure charges. **DATABASES AND STORAGE ARE THE MOST EXPENSIVE RESOURCES.** Leaving an Azure SQL Database and Cosmos DB running can cost $100+/month.

> [!CAUTION]
> **DATA LOSS WARNING**: Once you delete these resources, **ALL DATA IS PERMANENTLY GONE**. Backup first!

### BEFORE YOU DELETE ANYTHING

1. **Export databases** if you want to keep data
2. **Download files** from blob storage
3. **Document configurations** for future reference

---

### Method 1: Use Azure MCP Prompt (RECOMMENDED)

```
Delete all resources in resource group storage-demo-rg including:
- Azure SQL Database and SQL Server
- Cosmos DB account
- All storage accounts (hot and cool tier)
- Private endpoints
- Any backup vaults
BUT FIRST generate commands to export/backup data before deletion
```

### Method 2: Manual Cleanup Commands

```bash
# Step 1: BACKUP DATA FIRST (CRITICAL!)
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

# Step 2: List all resources
az resource list --resource-group storage-demo-rg --output table

# Step 3: Delete resource group
az group delete --name storage-demo-rg --yes --no-wait
```

---

### Before You Delete

- [ ] ✅ **CRITICAL**: Exported SQL Database to .bacpac file
- [ ] ✅ **CRITICAL**: Downloaded all blobs from storage accounts
- [ ] ✅ **CRITICAL**: Exported Cosmos DB data (if needed)
- [ ] Saved backup files to local machine or separate storage
- [ ] Documented connection strings and configurations
- [ ] Verified the resource group name is correct
- [ ] Confirmed no production data exists in these resources

---

### Verify Complete Deletion

```bash
# Verify resource group is gone
az group list --output table | grep storage-demo

# Check for orphaned storage accounts
az storage account list --query "[].name" -o table | grep storage

# Check for orphaned SQL servers
az sql server list --query "[].name" -o table

# Check for orphaned Cosmos DB accounts
az cosmosdb list --query "[].name" -o table
```

**Cost Impact**:
- Before deletion: ~$100-200/month
- After deletion: $0/month

---

## Key Takeaways

1. **Right Tool for Job**: Choose storage service based on data type and access patterns
2. **Backup is Critical**: Always implement backup before production use
3. **Lifecycle Policies**: Use lifecycle management to reduce storage costs
4. **Security First**: Private endpoints and encryption are non-negotiable
5. **BI Tools Add Value**: Metabase makes your data accessible to non-technical users
6. **Cost Awareness**: Data services are expensive - monitor and optimize regularly

---

## What's Next?

**[Chapter 8: Diagnostics and Troubleshooting](../08-diagnostics-troubleshooting/README.md)**

Now that you've deployed various storage services, you'll learn how to diagnose and fix common Azure issues using AI-assisted troubleshooting.
