# Chapter 9: Multi-Service Architecture (Supabase, Strapi)

Deploy complex applications with multiple interconnected Azure services by setting up Supabase and Strapi. In this chapter, you'll learn to architect and deploy multi-tier applications that integrate 5+ Azure services including [Container Apps](../GLOSSARY.md#azure-container-apps), Functions, [Blob Storage](../GLOSSARY.md#blob-storage), [Cosmos DB](../GLOSSARY.md#cosmos-db), and [Redis](../GLOSSARY.md#redis-cache), with proper service-to-service authentication and centralized monitoring.

## Prerequisites

- Completed [Course Setup](../00-course-setup/README.md)
- Completed [Chapter 1: First Deployment](../01-first-deployment/README.md)
- Completed [Chapter 2: Advanced Prompt Patterns](../02-prompt-patterns/README.md)
- Completed [Chapter 3: Infrastructure-as-Code with Bicep](../03-bicep-templates/README.md)
- Completed [Chapter 4: Terraform Basics](../04-terraform-basics/README.md)
- Completed [Chapter 5: Production Web Application](../05-simple-web-app/README.md)
- Completed [Chapter 6: Containerized Applications](../06-containerized-apps/README.md)
- Completed [Chapter 7: Data Storage Solutions](../07-data-storage/README.md)
- Completed [Chapter 8: Diagnostics and Troubleshooting](../08-diagnostics-troubleshooting/README.md)

## 🎯 Learning Objectives

- ✅ Design multi-tier application architecture
- ✅ Deploy 5+ interconnected Azure services
- ✅ Configure service-to-service authentication
- ✅ Implement event-driven communication
- ✅ Set up centralized logging and monitoring
- ✅ Create disaster recovery plan

## Real-World Scenario

Your company is building a video streaming platform that requires: web frontend ([Static Web Apps](../GLOSSARY.md#static-web-apps)), API backend ([Container Apps](../GLOSSARY.md#azure-container-apps)), video processing (Functions), storage ([Blob](../GLOSSARY.md#blob-storage) + [CDN](../GLOSSARY.md#cdn-content-delivery-network)), database ([Cosmos DB](../GLOSSARY.md#cosmos-db)), search (Cognitive Search), and caching ([Redis](../GLOSSARY.md#redis-cache)). You'll use [Azure MCP](../GLOSSARY.md#azure-mcp) to architect and deploy this complex system.

---

## Part 1: Architecture Planning

**Ask Azure MCP**:

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

---

## Assignment

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

### Success Criteria

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

### What is Supabase?

Open-source Firebase alternative. Complete BaaS (Backend-as-a-Service) with database, auth, storage, and realtime APIs. Uses PostgreSQL!

### Portfolio Value

"Deployed complete Supabase BaaS platform on Azure - PostgreSQL, Auth, Storage, Realtime, REST API"

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

---

### Deployment Using Azure MCP

#### Step 1: Deploy PostgreSQL for Supabase

**Prompt to Azure MCP**:
```
Deploy PostgreSQL for Supabase backend:
- Resource group: supabase-rg in East US
- PostgreSQL Flexible Server D2s_v3 named supabase-db-[MYINITIALS]
- PostgreSQL 15
- Database named postgres (default)
- Enable extensions: uuid-ossp, pgcrypto, pgjwt
- Configure high availability
- Tag with chapter=09 project=supabase
```

**Agent mode will** generate infrastructure code → ask "Continue?" → create PostgreSQL server with Supabase-required extensions and HA configuration.

#### Step 2: Deploy Container Apps Environment

**Prompt to Azure MCP**:
```
Create Container Apps environment for Supabase microservices:
- Environment: supabase-env
- Resource group: supabase-rg
- Log Analytics workspace
- Internal network isolation
```

**Agent mode will** generate infrastructure code → ask "Continue?" → create the Container Apps environment for hosting Supabase services.

#### Step 3: Deploy Supabase Kong (API Gateway)

**Prompt to Azure MCP**:
```
Deploy Kong API Gateway to Container Apps:
- Container App: supabase-kong
- Image: kong:latest
- External ingress on port 8000
- CPU: 1.0, Memory: 2Gi
- Environment variables for PostgreSQL connection
- Scale: 2-4 replicas
```

**Agent mode will** generate deployment code → ask "Continue?" → deploy Kong gateway and configure it to route Supabase API requests.

#### Prompt 4: Deploy Supabase Auth Service

```
Deploy Supabase GoTrue auth service:
- Container App: supabase-auth
- Image: supabase/gotrue:latest
- Internal ingress only
- Connect to PostgreSQL
- Configure JWT secrets
- Enable email auth provider
```

#### Prompt 5: Deploy PostgREST API

```
Deploy PostgREST for auto-generated REST API:
- Container App: supabase-rest
- Image: postgrest/postgrest:latest
- Connect to PostgreSQL
- Configure database schema
- Enable JWT validation
```

#### Prompt 6: Deploy Realtime Service

```
Deploy Supabase Realtime for WebSocket subscriptions:
- Container App: supabase-realtime
- Image: supabase/realtime:latest
- WebSocket support enabled
- Redis for pub/sub
- Connect to PostgreSQL for change data capture
```

#### Prompt 7: Deploy Storage Service

```
Deploy Supabase Storage with Azure Blob backend:
- Container App: supabase-storage
- Image: supabase/storage-api:latest
- Mount Azure Blob Storage
- Configure file upload limits
- Enable image transformations
```

#### Prompt 8: Configure Redis for Realtime

```
Deploy Azure Cache for Redis for Supabase:
- Name: supabase-redis-[MYINITIALS]
- SKU: Basic C0 (cost-effective for learning)
- Connect to Realtime service
```

---

### Verification

**Access Supabase**:
1. Kong API Gateway URL: `https://supabase-kong.[CONTAINERAPP-DOMAIN]`
2. Test endpoints:
   - `/auth/v1/health` (Auth service)
   - `/rest/v1/` (PostgREST API)
   - `/realtime/v1/websocket` (Realtime)
   - `/storage/v1/health` (Storage)

#### Expected Result

```
✅ All services return HTTP 200
✅ Can register new user via Auth API
✅ Can query database via REST API
✅ Can upload file to Storage
✅ Can subscribe to realtime changes
```

---

### Quick Troubleshooting Prompts

#### Issue: Services Can't Connect to PostgreSQL

```
@azure Supabase services in supabase-rg can't connect to PostgreSQL
Check: connection strings, firewall rules, PostgreSQL extensions, network policies
Provide diagnostic commands
```

#### Issue: Kong Gateway Returns 502

```
Debug Supabase Kong gateway connectivity
Check: backend service health, routing configuration, container logs
Generate troubleshooting commands
```

---

### Assignment (Optional)

Use Azure MCP and Supabase to:
1. Create a simple todo app using Supabase client library
2. Implement user registration and login
3. Create database tables via REST API
4. Upload images to Storage
5. Subscribe to realtime table changes
6. Configure row-level security (RLS)

**Deliverable**: Working app + Supabase API URL

---

### Cleanup Prompt

```
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

### What is Strapi?

Leading open-source headless CMS. Build APIs fast. Perfect for content-driven apps.

### Portfolio Value

"Deployed Strapi headless CMS on Azure with PostgreSQL and media storage"

### Azure Services Required

- App Service (Node.js LTS)
- PostgreSQL Flexible Server
- Blob Storage (media library)
- CDN (optional, for media delivery)

---

### Deployment Using Azure MCP

#### Prompt 1: Deploy Strapi Infrastructure

```
Deploy Strapi CMS:
- Resource group: strapi-cms-rg in East US
- App Service B2 Linux with Node.js LTS runtime named strapi-app-[MYINITIALS]
- PostgreSQL Flexible Server B1ms named strapi-db-[MYINITIALS]
- Database: strapi_cms
- Storage account for media: strapistorage[MYINITIALS]
- Tag with chapter=09 project=strapi
```

#### Prompt 2: Configure Strapi Environment

```
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

#### Prompt 3: Deploy Strapi Application

```
Deploy Strapi to App Service:
- Use Docker image: strapi/strapi:latest
- Or deploy from Git repository
- Configure startup command if needed
- Enable continuous deployment
```

---

### Verification

**Access Strapi**: Navigate to `https://strapi-app-[MYINITIALS].azurewebsites.net/admin`

#### Expected Result

```
✅ Strapi admin panel loads
✅ Can create admin account
✅ Can create content types
✅ Can add collection entries
✅ Can upload media to Azure Storage
✅ REST API endpoints work
✅ GraphQL endpoint works (if enabled)
```

---

### Quick Setup

#### First-Time Setup

1. Create admin account
2. Create content type (e.g., "Article")
3. Add fields (title, content, image)
4. Create entry
5. Make API public
6. Test API: `/api/articles`

---

### Assignment (Optional)

Use Azure MCP and Strapi to:
1. Create 3 different content types
2. Add media uploads with image resizing
3. Configure REST API permissions
4. Enable GraphQL plugin
5. Create webhook to external service
6. Add custom API endpoint

**Deliverable**: Strapi admin URL + API documentation

---

### Cleanup Prompt

```
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

## Cleanup Using Azure MCP

> [!CAUTION]
> Complete this cleanup to avoid unexpected Azure charges. **THIS IS THE MOST EXPENSIVE CHAPTER** - deploying 8+ services can cost $200+/month if left running!

**📌 IMPORTANT NOTE**: If you plan to complete Chapter 10 (Capstone Project) immediately, you may want to **reuse some of these resources**. Read the "Optional: Selective Cleanup" section below.

### Option A: Complete Cleanup (if not doing Chapter 10 immediately)

**Prompt to Azure MCP**:
```
Delete resource groups: streaming-platform-rg, supabase-rg, strapi-rg
List all resources in each group first, then delete all groups
```

**Agent mode will**:
1. Generate deletion commands → Show "Continue?" → Execute after approval
2. List all resources in each group
3. Delete all multi-service architecture resources
4. Confirm deletion completion

**Manual alternative**:
```bash
# List everything that will be deleted
az resource list --resource-group streaming-platform-rg --output table

# Delete entire resource group (most efficient)
az group delete --name streaming-platform-rg --yes --no-wait
az group delete --name supabase-rg --yes --no-wait
az group delete --name strapi-rg --yes --no-wait
```

### Option B: Selective Cleanup (if continuing to Chapter 10 immediately)

Some resources from Chapter 9 can be reused in Chapter 10 to save deployment time:
- **Keep**: Key Vault, Application Insights, Log Analytics workspace
- **Delete**: All application-specific services

**Cost Impact**:
- Before deletion: ~$150-250/month
- After complete deletion: $0/month
- After selective deletion (keeping 3 resources): ~$5-10/month

---

## Key Takeaways

1. **Multi-Service Complexity**: Real applications require many interconnected services
2. **BaaS Platforms**: Supabase demonstrates complete backend-as-a-service architecture
3. **Headless CMS**: Strapi shows modern API-first content management
4. **Microservices**: Complex architectures require proper service communication patterns
5. **Portfolio Value**: Both projects are highly impressive on resumes
6. **Cost Management**: Complex architectures are expensive - plan carefully

---

## What's Next?

**[Chapter 10: Production-Ready Deployment (Capstone)](../10-production-deployment/README.md)**

You're ready for the final challenge: deploying a complete production-ready SaaS application with all best practices, security, monitoring, and disaster recovery.
