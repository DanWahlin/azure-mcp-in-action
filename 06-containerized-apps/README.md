# Chapter 6: Containerized Applications (n8n, Apache Superset)

Deploy containerized applications to Azure Container Apps and Azure Kubernetes Service (AKS). In this chapter, you'll learn container orchestration without Kubernetes complexity by deploying n8n (workflow automation) and Apache Superset (data visualization) using agent mode to handle all the infrastructure setup.

## Prerequisites

- Completed [Course Setup](../00-course-setup/README.md)
- Completed [Chapter 1: First Deployment](../01-first-deployment/README.md)
- Completed [Chapter 2: Advanced Prompt Patterns](../02-cli-mastery/README.md)
- Completed [Chapter 3: Infrastructure-as-Code with Bicep](../03-bicep-templates/README.md)
- Completed [Chapter 4: Terraform Basics](../04-terraform-basics/README.md)
- Completed [Chapter 5: Production Web Application](../05-simple-web-app/README.md)

## 🎯 Learning Objectives

- ✅ Containerize applications with Docker
- ✅ Deploy to Azure Container Registry
- ✅ Run containers on Azure Container Apps
- ✅ Configure service-to-service communication
- ✅ Implement auto-scaling for containers
- ✅ Manage secrets with Key Vault integration

## Real-World Scenario

> Your microservices application has 5 services that need to scale independently. Kubernetes is overkill for your team size, but you need container orchestration. Azure Container Apps provides the right balance—you'll use Azure MCP to deploy your entire microservices architecture.

---

## Part 1: Understanding Container Apps vs AKS

**Ask Azure MCP**:

```
@azure When should I use Azure Container Apps vs AKS?
Consider: team size, complexity, cost, and management overhead.
```

---

## Part 2: Deploy with Azure MCP

**Prompt to Azure MCP**:
```
Deploy a containerized Node.js API to Azure Container Apps:
1. Create Container Apps environment
2. Deploy container from Docker Hub: node:lts-alpine
3. Configure ingress for HTTPS
4. Set environment variables from Key Vault
5. Enable auto-scaling (1-10 replicas based on HTTP requests)
6. Set up managed identity for Azure services access

Resource group: containerapp-demo-rg in East US
Tags: chapter=06, project=containerapp-demo
```

**agent mode will**:
1. Generate infrastructure code → Show "Continue?" → Execute after approval
2. Create Container Apps environment with Log Analytics
3. Deploy the container with specified configuration
4. Configure HTTPS ingress and set up auto-scaling rules
5. Enable managed identity and return the container app URL

**Verify**:
- Azure Portal: Check Container Apps environment and app
- Azure CLI: `az containerapp list --resource-group containerapp-demo-rg --output table`

---

## Assignment

1. Containerize a multi-service application (frontend + backend + database)
2. Deploy to Azure Container Apps
3. Configure internal and external ingress
4. Implement auto-scaling policies
5. Set up monitoring with Application Insights
6. Test scaling under load

### Success Criteria

- ✅ All services deployed and communicating
- ✅ Auto-scaling triggers correctly
- ✅ Secrets managed securely
- ✅ Monitoring shows real-time metrics
- ✅ Cost under $30/month
- ✅ Zero-downtime rolling updates work

---

## 🚀 Real-World Project: Deploy n8n Workflow Automation

**⏱️ Time**: 15-20 minutes | **Cost**: ~$20-30/month | **Hype**: ⭐⭐⭐⭐⭐ (43k GitHub stars)

### What is n8n?

Self-hosted workflow automation platform (Zapier alternative) with 400+ integrations. Perfect for Container Apps deployment.

### Portfolio Value

"Deployed self-hosted n8n automation platform on Azure Container Apps with persistent storage"

### Azure Services Required

- Container Apps Environment
- Container App (n8n)
- PostgreSQL (workflow storage)
- Azure Files (persistent data)

---

### Deployment Using Azure MCP

#### Step 1: Create Complete n8n Infrastructure

**Prompt to Azure MCP**:
```
Deploy n8n workflow automation platform:
- Resource group: n8n-automation-rg in East US
- Container Apps environment: n8n-env with Log Analytics
- PostgreSQL Flexible Server: n8n-postgres-[MYINITIALS] (Burstable B1ms)
- Database: n8n_db with SSL enabled, firewall allows Container Apps
- Tags: chapter=06, project=n8n
```

**agent mode will**:
1. Generate infrastructure code → Show "Continue?" → Execute after approval
2. Create all infrastructure resources
3. Configure PostgreSQL with proper firewall rules
4. Return connection strings

#### Step 2: Deploy n8n Container

**Prompt to Azure MCP**:
```
Deploy n8n to Container Apps:
- Container App name: n8n-app in environment n8n-env
- Image: docker.n8n.io/n8nio/n8n:latest
- Resources: 0.5 CPU cores, 1.0 GB memory
- External ingress on port 5678 with HTTPS
- Scaling: min 1, max 3 replicas
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

**agent mode will**:
1. Generate deployment code → Show "Continue?" → Execute after approval
2. Deploy n8n container
3. Configure all environment variables and set up auto-scaling
4. Return n8n URL

#### Step 3: Configure Persistent Storage (Optional)

```
#azure_generate_azure_cli_command
Add Azure Files persistent volume to n8n-app:
- Storage account name: n8nstorage[MYINITIALS]
- File share name: n8n-data
- Mount path: /home/node/.n8n
This persists custom nodes and workflow data
```

---

### Verification

**Access n8n**: Navigate to the Container App's URL from `az containerapp show --name n8n-app --resource-group n8n-automation-rg --query properties.configuration.ingress.fqdn`

#### Expected Result

```
✅ n8n welcome screen loads
✅ Can create owner account
✅ Can create a test workflow
✅ Workflows save to PostgreSQL
✅ Can trigger workflow manually
```

---

### Quick Troubleshooting Prompts

#### Issue: n8n Won't Start

```
@azure n8n container app n8n-app in n8n-automation-rg won't start
Check: container logs, database connectivity, environment variables
Provide diagnostic commands
```

#### Issue: Workflows Don't Save

```
#azure_generate_azure_cli_command
Check PostgreSQL connection for n8n-app
Verify database credentials and network access
Generate connection test commands
```

---

### Assignment (Optional)

Use Azure MCP to:
1. Create 3 different n8n workflows (HTTP request, schedule, webhook)
2. Configure custom domain
3. Add email notifications integration
4. Set up workflow backups

**Deliverable**: n8n URL + screenshot of workflows

---

### Cleanup Using Azure MCP

**Prompt to Azure MCP**:
```
Delete resource group n8n-automation-rg and all resources inside it
```

**agent mode will** generate deletion commands → ask "Continue?" → execute to delete all n8n resources including Container Apps environment, PostgreSQL, and storage.

**Manual alternative**:
```bash
az group delete --name n8n-automation-rg --yes --no-wait
```

**Cost After Deletion**: $0/month

---

## 🚀 BONUS: Apache Superset on AKS

**⏱️ Time**: 60-90 minutes | **Cost**: ~$70-100/month | **Hype**: ⭐⭐⭐⭐⭐ (59k GitHub stars)

> ⚠️ **ADVANCED BONUS CONTENT**: This introduces Azure Kubernetes Service (AKS). AKS is industry-standard for production container deployments. **Skip if you're not ready for Kubernetes.**

### What is Superset?

Modern data visualization platform used by Airbnb, Netflix, Twitter. Open-source alternative to Tableau.

### Portfolio Value

"Deployed Apache Superset on Azure Kubernetes Service" - **THIS IS YOUR KUBERNETES CREDENTIAL**

### Azure Services Required

- Azure Kubernetes Service (AKS cluster)
- NGINX Ingress Controller
- PostgreSQL (Helm chart)
- Redis (Helm chart)
- LoadBalancer (automatic)

---

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

---

### Deployment Using Azure MCP

#### Step 1: Create AKS Cluster

**Prompt to Azure MCP**:
```
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

#### Prompt 2: Get Cluster Credentials

```
#azure_generate_azure_cli_command
Get AKS credentials for superset-aks cluster
Configure kubectl to connect to cluster
Verify nodes are ready
```

#### Prompt 3: Install NGINX Ingress

```bash
# These are standard Helm commands (Azure MCP doesn't generate Helm yet)
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update

helm install ingress-nginx ingress-nginx/ingress-nginx \
  --namespace ingress-nginx \
  --create-namespace \
  --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz
```

#### Prompt 4: Deploy PostgreSQL for Superset

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

#### Prompt 5: Deploy Redis for Caching

```bash
helm install superset-redis bitnami/redis \
  --namespace superset \
  --set auth.enabled=false \
  --set master.persistence.size=5Gi
```

#### Prompt 6: Deploy Apache Superset

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

---

### Verification

**Get Superset URL**:

```bash
# Get LoadBalancer IP
kubectl get svc -n ingress-nginx

# Access Superset at: http://[EXTERNAL-IP]
# Login: admin / AdminPassword123!
```

#### Expected Result

```
✅ Superset login page loads
✅ Can login with admin credentials
✅ Can navigate SQL Lab
✅ Can create database connections
✅ Can build visualizations
```

---

### Quick Troubleshooting Prompts

#### Issue: Pods Not Starting

```
@azure My Superset pods in AKS cluster superset-aks are stuck in Pending
Check: node resources, persistent volume claims, pod events
Provide kubectl diagnostic commands
```

#### Issue: No External IP for Ingress

```
@azure NGINX Ingress Controller in superset-aks has no external IP after 10 minutes
Check: LoadBalancer provisioning, service configuration, Azure networking
Provide troubleshooting steps
```

---

### Assignment (Optional)

Use kubectl and Azure MCP to:
1. Connect Superset to a sample database
2. Create 3 different chart types
3. Build a dashboard with visualizations
4. Configure custom domain with SSL (cert-manager)
5. Scale to 3 Superset replicas

**Deliverable**: Superset dashboard URL + Kubernetes manifests

---

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

## Cleanup Using Azure MCP

**⚠️ IMPORTANT**: Complete this cleanup to avoid unexpected Azure charges

Container Apps environments can cost $30+/month if left running. Clean up immediately after completing the chapter.

### Method 1: Use Azure MCP (RECOMMENDED)

**Prompt to Azure MCP**:
```
Delete resource groups: containerapp-demo-rg, n8n-automation-rg, superset-aks-rg
List all resources in each group first, then delete all groups
```

**agent mode will**:
1. Generate deletion commands → Show "Continue?" → Execute after approval
2. List all resources in each group
3. Delete all container apps, environments, AKS clusters, databases
4. Confirm deletion completion

### Method 2: Manual Cleanup with Azure CLI

```bash
# Step 1: List all resources to verify
az resource list --resource-group containerapp-demo-rg --output table

# Step 2: Delete all container apps first (graceful shutdown)
az containerapp list --resource-group containerapp-demo-rg --query "[].name" -o tsv | \
  xargs -I {} az containerapp delete --name {} --resource-group containerapp-demo-rg --yes

# Step 3: Delete container apps environment
az containerapp env list --resource-group containerapp-demo-rg --query "[].name" -o tsv | \
  xargs -I {} az containerapp env delete --name {} --resource-group containerapp-demo-rg --yes

# Step 4: Delete the entire resource group
az group delete --name containerapp-demo-rg --yes --no-wait
```

**Cost Impact**:
- Before deletion: ~$30-50/month
- After deletion: $0/month

---

## Key Takeaways

1. **Container Apps for Simplicity**: Use Container Apps when you don't need full Kubernetes complexity
2. **AKS for Production**: Use AKS when you need full Kubernetes features and control
3. **Helm for Kubernetes**: Helm charts simplify Kubernetes application deployment
4. **OSS Deployment**: Real-world OSS projects demonstrate practical Azure skills
5. **Portfolio Projects**: Both n8n and Superset are impressive resume credentials
6. **Cost Management**: AKS is expensive - understand costs before deploying

---

## What's Next?

**[Chapter 7: Data Storage Solutions (Metabase)](../07-data-storage/README.md)**

Now that you've mastered containers, you'll learn Azure data services by deploying Metabase BI platform connected to multiple data sources.
