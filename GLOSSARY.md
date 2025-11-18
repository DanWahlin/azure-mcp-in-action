# Glossary

A comprehensive glossary of terms used throughout the Azure Infrastructure with AI Assistance course.

---

## A

### Agent Mode

A mode in GitHub Copilot that acts as an autonomous, real-time collaborator performing multi-step tasks based on natural language prompts. Agent mode can analyze codebases, read files, propose edits, run terminal commands, and iterate on solutions automatically with self-healing capabilities.

**How it works**: Agent mode loops through determining relevant context, offering code changes and terminal commands, monitoring correctness, and iterating to fix issues autonomously.

**What it can do**: Create applications from scratch, refactor across multiple files, write and run tests, migrate code to modern frameworks, install packages, and more.

**In this course**: Used primarily for creating, modifying, and deleting Azure resources through natural language prompts.

**Contrast with**: Ask mode (for questions and learning without taking actions).

**See**: [Chapter 1: First Deployment](./01-first-deployment/README.md)

### App Service

Azure's fully managed platform for building, deploying, and scaling web applications. Supports multiple languages (Node.js, Python, .NET, Java, PHP) and runtimes without managing underlying infrastructure.

**Why it matters**: One of the simplest ways to deploy web applications to Azure. No server management required.

**Example**: Deploying a Node.js web app on Linux with HTTPS enabled by default.

**See**: [Chapter 1: First Deployment](./01-first-deployment/README.md)

### App Service Plan

The compute resources (CPU, memory, storage) that power your App Service. Multiple apps can share the same plan to reduce costs. Plans have different SKUs (Free, Basic, Standard, Premium) with varying capabilities and pricing.

**Pricing tiers**:
- **F1 (Free)**: Free tier, limited resources, good for learning
- **B1 (Basic)**: Basic tier, custom domains, SSL
- **S1 (Standard)**: Standard tier, auto-scaling, deployment slots
- **P1V2 (Premium)**: Premium tier, better performance, more scaling

**See**: [Chapter 1: First Deployment](./01-first-deployment/README.md)

### Azure CLI

The Azure Command-Line Interface (CLI) is a cross-platform command-line tool for managing Azure resources. Provides commands to create, configure, and delete Azure resources from the terminal.

**Key features**:
- Cross-platform (Windows, macOS, Linux)
- Interactive and scriptable
- Consistent command structure (`az <service> <operation>`)
- JSON output for programmatic processing

**Common commands**:
- `az login` - Authenticate to Azure
- `az group create` - Create a resource group
- `az webapp create` - Create a web app
- `az resource list` - List all resources

**See**: [Chapter 0: Course Setup](./00-course-setup/README.md), [Chapter 1: First Deployment](./01-first-deployment/README.md)

### Azure Developer CLI

A command-line tool (azd) that simplifies Azure application deployment through templates and conventions. Azure Developer CLI provides a unified workflow for provisioning infrastructure, deploying code, and managing environments across multiple Azure services.

**Key features**:
- Infrastructure provisioning with Bicep or Terraform
- Environment management (dev, staging, production)
- Local state management
- Post-provision hooks for automation
- GitHub Actions integration

**Common commands**:
- `azd init` - Initialize a new project
- `azd up` - Provision infrastructure and deploy code
- `azd down` - Delete all Azure resources
- `azd env get-value` - Retrieve deployment outputs

**Why it matters**: azd eliminates the need to manually manage resource dependencies, parameter files, and deployment order. It provides a consistent deployment experience whether using Bicep or Terraform.

**See**: [Chapter 3: n8n Deployment](./03-n8n/README.md)

### Application Insights

Azure's application performance monitoring (APM) service that collects telemetry data about your application's performance, errors, and usage. Provides distributed tracing, custom metrics, and availability tests.

**What it tracks**: Response times, error rates, dependencies, user behavior, custom events.

**See**: [Chapter 8: Diagnostics and Troubleshooting](./08-diagnostics-troubleshooting/README.md)

### Ask Mode

The default mode in GitHub Copilot that provides answers to your questions in the chat pane without modifying code or resources. Ask mode is fast, helpful, and focused entirely on answering questions.

**How it works**: You can highlight code, ask a question in Copilot Chat, and it generates an answer - explaining code, suggesting tests, providing code snippets, or discussing edge cases.

**Chat participants**: Use prefixes like `@azure` to scope questions to specific domains. For example, `@azure` directs questions to the Azure chat participant for Azure-specific knowledge and help.

**In this course**: **This course focuses on agent mode.** Ask mode is optional if you want to learn about Azure services, understand pricing, compare options, or get architectural guidance. See [ask-mode.md](./ask-mode.md) for details.

**Example**: `@azure What is the monthly cost of an F1 App Service plan?`

**Contrast with**: Agent mode (for autonomous multi-step tasks and resource creation).

**See**: [Chapter 1: First Deployment](./01-first-deployment/README.md)

### Auto-scaling

A cloud computing method that dynamically adjusts computational resources automatically based on actual demand, without human intervention. The number of active servers or instances increases when load is high and decreases when activity is low.

**How it works**: Monitors specific metrics (CPU utilization, memory usage, bandwidth, HTTP queue length, custom metrics) and automatically scales resources to match real-time demand according to predefined policies.

**Types of scaling**:
- **Horizontal (scale out/in)**: Adding or removing machines/nodes
- **Vertical (scale up/down)**: Adding or reducing power (RAM, CPU, storage) to existing nodes

**Benefits**:
- **Cost efficiency**: Pay only for resources actually needed; most cloud providers charge based on usage
- **Performance & availability**: Maintains consistent performance regardless of demand
- **Automatic management**: Handles traffic spikes without manual intervention

**Providers**: Available across AWS, Google Cloud, Microsoft Azure, and Oracle Cloud Infrastructure.

**See**: [Chapter 6: Containerized Applications](./06-containerized-apps/README.md)

### Azure CLI

The command-line interface for managing Azure resources. Works across Windows, macOS, and Linux. Commands start with `az` and follow the pattern `az <service> <command> <parameters>`.

**Example**: `az group list --output table`

**See**: [Chapter 1: First Deployment](./01-first-deployment/README.md)

### Azure MCP

An MCP (Model Context Protocol) server implementation that provides Azure-specific tools and capabilities within the GitHub Copilot for Azure extension. Exposes Azure operations as MCP tools, resources, and prompts that AI agents can use.

**What it does**: Acts as the bridge between GitHub Copilot's AI and your Azure subscription, implementing the MCP standard to enable:
- Azure resource management tools (create, update, delete, query)
- Azure documentation and best practices as resources
- Azure-specific prompt templates
- Automatic authentication, API calls, and command execution

**How it works**: When you use GitHub Copilot agent mode with Azure prompts, Azure MCP translates your natural language requests into Azure CLI commands, Bicep templates, or API calls through the MCP protocol.

**Why it matters**: Enables standardized AI-to-Azure communication, allowing you to describe what you want in natural language without knowing specific commands or APIs.

**See**: [Course Setup](./00-course-setup/README.md#part-4-understanding-model-context-protocol-mcp)

### Azure Container Apps

A serverless container platform that runs containers without managing Kubernetes complexity. Provides auto-scaling, ingress, secrets management, and built-in service discovery.

**When to use**: When you need container orchestration but don't need full Kubernetes features.

**Contrast with**: Azure Kubernetes Service (AKS) provides full Kubernetes control but requires more management.

**See**: [Chapter 6: Containerized Applications](./06-containerized-apps/README.md)

### Azure Kubernetes Service (AKS)

Azure's managed Kubernetes service that provides full control over container orchestration, networking, and scaling. Industry-standard for production container deployments.

**When to use**: Complex microservices, need Kubernetes features, team has Kubernetes expertise.

**Trade-offs**:
- ✅ Full Kubernetes features and ecosystem
- ✅ Industry-standard, portable across clouds
- ❌ Higher complexity and learning curve
- ❌ More expensive (~$70-100/month minimum)

**See**: [Chapter 6: Apache Superset on AKS](./06-containerized-apps/README.md#-bonus-apache-superset-on-aks)

### Azure Portal

The web-based user interface for managing Azure resources at [portal.azure.com](https://portal.azure.com). Provides visual dashboards, resource creation wizards, and monitoring tools.

**See**: [Chapter 1: Verify Resource Creation](./01-first-deployment/README.md#method-1-azure-portal-verification)

### Azure SQL Database

Azure's fully managed relational database service based on Microsoft SQL Server. Provides automatic backups, patching, scaling, and high availability.

**Pricing tiers**:
- **Basic**: $5/month, 2GB storage
- **Standard S0**: $15/month, 250GB storage
- **Premium**: Higher performance and features

**See**: [Chapter 7: Data Storage Solutions](./07-data-storage/README.md)

---

## B

### Bicep

Azure's domain-specific language for declarative infrastructure-as-code. Simpler and more concise than ARM templates (JSON). Compiles to ARM templates during deployment.

**Benefits**:
- ✅ Cleaner syntax than JSON
- ✅ Type safety and IntelliSense
- ✅ Modular with parameters and modules
- ✅ Native Azure support

**Example use**: Define an entire application infrastructure (App Service, database, storage) in one .bicep file.

**See**: [Chapter 3: Infrastructure-as-Code with Bicep](./03-bicep-templates/README.md)

### Blob Storage

Azure's object storage service for unstructured data like images, videos, documents, and backups. Organized in containers with different access tiers for cost optimization.

**Access tiers**:
- **Hot**: Frequent access, higher storage cost, lower access cost
- **Cool**: Infrequent access (30+ days), lower storage cost
- **Archive**: Rare access (180+ days), lowest storage cost, hours to retrieve

**See**: [Chapter 7: Data Storage Solutions](./07-data-storage/README.md)

---

## C

### CDN (Content Delivery Network)

A distributed network of servers that cache static content (images, CSS, JavaScript) closer to users geographically, reducing latency and improving performance.

**Why it matters**: Faster page loads globally, reduced bandwidth costs, offloads traffic from origin server.

**See**: [Chapter 8: Performance Optimization](./08-diagnostics-troubleshooting/README.md)

### Container Apps Environment

The secure boundary around a group of Container Apps that share the same virtual network, logging workspace, and configuration. Multiple Container Apps within one environment can communicate securely.

**See**: [Chapter 6: Containerized Applications](./06-containerized-apps/README.md)

### Cosmos DB

Azure's globally distributed, multi-model NoSQL database. Supports multiple APIs (SQL, MongoDB, Cassandra, Gremlin, Table) with guaranteed low latency and high availability.

**Pricing models**:
- **Serverless**: Pay per request, good for development and variable workloads
- **Provisioned**: Reserved throughput, predictable costs

**When to use**: Global distribution, flexible schema, need for multiple APIs, real-time applications.

**See**: [Chapter 7: Data Storage Solutions](./07-data-storage/README.md)

---

## D

### Deployment Slot

A live application with its own hostname that runs as a separate instance within Azure App Service. Deployment slots enable you to deploy and test application changes in isolated environments before making them available to end users.

**Key characteristics**:
- Each slot is a full-fledged App Service instance with a unique hostname
- Slots share the same App Service Plan
- Content and configuration can be swapped between slots

**Common pattern**:
1. Deploy new version to staging slot
2. Test and warm up in staging
3. Swap staging and production slots (near-zero downtime)
4. If issues arise, swap back instantly for rollback

**Requirements**: Available in Standard, Premium, or Isolated tier App Service plans. Free and Basic tiers do not support deployment slots.

**Benefits**: Validate changes before production, eliminate downtime during deployments, instant rollback capability.

**See**: [Chapter 5: Production Web Application](./05-simple-web-app/README.md)

---

## F

### Free Tier (F1)

The free pricing tier for App Service Plans that costs $0/month. Limited to 60 CPU minutes/day and 1GB RAM, but perfect for learning and development.

**Limitations**: No custom domains, no SSL certificates, no auto-scaling, stops if exceeds CPU quota.

**See**: [Chapter 1: First Deployment](./01-first-deployment/README.md)

---

## G

### Generate → Approve → Execute Workflow

The core workflow in GitHub Copilot agent mode where the AI:
1. **Generate**: Creates infrastructure code (Bicep, CLI commands)
2. **Approve**: Shows "Allow" button for you to review before execution
3. **Execute**: Runs the approved commands
4. **Verify**: Confirms what was created

**Why it matters**: Maintains control while using AI assistance. You always review before resources are created.

**See**: [Chapter 1: First Deployment](./01-first-deployment/README.md)

### GitHub Copilot for Azure

A chat participant extension for GitHub Copilot that provides Azure-specific assistance directly within VS Code. Enables you to ask questions about Azure services, manage resources, troubleshoot deployments, and access Azure documentation without leaving your code editor.

**How to use**: Prefix questions with `@azure` in GitHub Copilot Chat to invoke the Azure chat participant (e.g., `@azure What App Service tier should I use?`).

**Capabilities**:
- Learn about Azure services and best practices
- Troubleshoot Azure resources and deployments
- Get help with Azure-specific development tasks
- Access Azure documentation contextually
- In agent mode: Deploy and manage Azure resources using natural language prompts

**Integration**: Works within GitHub Copilot's ask mode (for questions) and agent mode (for resource creation and management).

**See**: [Course Setup](./00-course-setup/README.md)

---

## H

### Helm

A package manager for Kubernetes that streamlines installing and managing Kubernetes applications. Often described as "like apt/yum/homebrew for Kubernetes," Helm helps you define, install, and upgrade even the most complex Kubernetes applications.

**Key concepts**:
- **Charts**: Packages of pre-configured Kubernetes resources that describe an application's resources
- **Releases**: A Helm chart deployed with a particular configuration
- **Templates**: Support for defining templates using Go template syntax to generate Kubernetes resource manifests dynamically

**Benefits**:
- Charts are easy to create, version, share, and publish
- Simplifies complex deployments through a single command-line interface
- Use `helm rollback` to roll back to an older version of a release
- Graduated CNCF project, maintained by the Helm community

**Example**: Installing NGINX Ingress Controller or PostgreSQL with a single `helm install` command.

**See**: [Chapter 6: Apache Superset on AKS](./06-containerized-apps/README.md)

### HTTPS-only

A security setting that forces all HTTP traffic to redirect to HTTPS, ensuring encrypted communication. Azure App Service enables this by default.

**Why it matters**: Protects data in transit, required for modern web applications, improves SEO.

**See**: [Chapter 1: First Deployment](./01-first-deployment/README.md)

---

## I

### Infrastructure-as-Code (IaC)

The practice of managing and provisioning computing infrastructure through machine-readable definition files (code) rather than manual processes, interactive configuration tools, or physical hardware configuration.

**How it works**: Configuration files contain infrastructure specifications (networks, virtual machines, load balancers, connection topologies) which makes it easier to edit, distribute, and version control infrastructure.

**Two approaches**:
- **Declarative**: Describe the desired end state; the tool figures out how to achieve it
- **Imperative**: Define step-by-step commands to set up resources and reach the desired state

**Benefits**:
- ✅ Reproducible and consistent deployments
- ✅ Version control and change history
- ✅ Code review and team collaboration
- ✅ Automated testing and validation
- ✅ Prevents configuration drift and missing dependencies
- ✅ Faster provisioning and scaling

**Popular tools**: Terraform (HashiCorp, multi-cloud), AWS CloudFormation, Azure Resource Manager/Bicep, Ansible, Pulumi

**See**: [Chapter 3: Bicep Templates](./03-bicep-templates/README.md), [Chapter 4: Terraform Basics](./04-terraform-basics/README.md)

---

## K

### Key Vault

Azure's service for securely storing and managing secrets (passwords, API keys, certificates, connection strings). Applications access secrets at runtime without hardcoding credentials.

**What it stores**:
- Secrets (passwords, API keys, connection strings)
- Encryption keys
- SSL/TLS certificates

**Why it matters**: Prevents credential exposure in code, centralizes secret management, provides audit logging.

**See**: [Chapter 2: Advanced Prompt Patterns](./02-prompt-patterns/README.md)

---

## L

### Lifecycle Policy

Rules that automatically move blob storage data between access tiers (Hot → Cool → Archive) or delete old data based on age. Reduces storage costs without manual intervention.

**Example**: Move files to Cool tier after 30 days, Archive after 180 days, delete after 365 days.

**See**: [Chapter 7: Data Storage Solutions](./07-data-storage/README.md)

### Log Analytics

Azure's service for collecting, analyzing, and visualizing log data from multiple sources. Uses Kusto Query Language (KQL) for powerful log queries.

**What it collects**: Application logs, container logs, performance metrics, security events.

**See**: [Chapter 8: Diagnostics and Troubleshooting](./08-diagnostics-troubleshooting/README.md)

---

## M

### MCP (Model Context Protocol)

An open standard, open-source protocol introduced by Anthropic in November 2024 to standardize how AI systems like large language models (LLMs) integrate and share data with external tools, systems, and data sources. Think of it as "USB-C for AI" - providing a universal way to connect AI applications to various services and data sources.

**Core components**: MCP servers expose three primitives to LLMs: Tools (executable functions), Resources (file-like structured data), and Prompts (predefined templates).

**Purpose**: Replaces fragmented custom integrations with a single protocol, helping AI models access data beyond their training - overcoming information silos and legacy systems.

**Adoption**: Officially adopted by OpenAI (March 2025) across ChatGPT, Agents SDK, and APIs. Google DeepMind confirmed support in Gemini models (April 2025). Pre-built MCP servers available for Google Drive, Slack, GitHub, Postgres, and more.

**In this course**: GitHub Copilot for Azure uses MCP to communicate with Azure services behind the scenes.

**Why it matters**: Makes skills transferable across MCP-enabled tools and represents the emerging industry standard for AI tool integration.

**See**: [Course Setup - Part 4](./00-course-setup/README.md#part-4-understanding-model-context-protocol-mcp), [Azure MCP](./GLOSSARY.md#azure-mcp)

### Managed Identity

An identity in Microsoft Entra ID (formerly Azure AD) automatically managed by Azure. Allows Azure services to authenticate to other Azure services without storing credentials in code.

**Types**:
- **System-assigned**: Created with the resource, deleted when resource is deleted
- **User-assigned**: Created independently, can be shared across resources

**Why it matters**: Eliminates the need for connection strings and credentials in code, improves security, simplifies access management.

**Example**: App Service uses managed identity to access Key Vault secrets without storing credentials.

**See**: [Chapter 2: Advanced Prompt Patterns](./02-prompt-patterns/README.md)

---

## P

### PostgreSQL Flexible Server

Azure's managed PostgreSQL database service with flexible configuration options. Provides automatic backups, patching, scaling, and high availability.

**Pricing tiers**:
- **Burstable B1ms**: ~$12/month, 1-2 vCores, good for development
- **General Purpose**: ~$100+/month, consistent performance
- **Memory Optimized**: Highest performance for demanding workloads

**See**: [Chapter 6: n8n Deployment](./06-containerized-apps/README.md)

### Private Endpoint

A network interface that connects privately to an Azure service using a private IP address from your virtual network. Traffic between your VNet and the service stays on the Microsoft backbone network.

**Why it matters**: Eliminates exposure to public internet, improves security, meets compliance requirements.

**See**: [Chapter 7: Data Storage Solutions](./07-data-storage/README.md)

---

## R

### Redis Cache

An in-memory data store used for caching frequently accessed data, session storage, and real-time analytics. Dramatically improves application performance by reducing database load.

**Pricing tiers**:
- **Basic C0**: ~$16/month, 250MB cache
- **Standard**: Replication for high availability
- **Premium**: Advanced features like persistence and clustering

**Use cases**: Session storage, caching database queries, leaderboards, real-time analytics.

**See**: [Chapter 8: Performance Optimization](./08-diagnostics-troubleshooting/README.md)

### Resource Group

A logical container that holds related Azure resources for an application or project. Resources in a group share the same lifecycle and can be managed together.

**Best practices**:
- One resource group per environment (dev, staging, prod)
- Use naming conventions (`projectname-environment-rg`)
- Delete entire resource group to clean up all contained resources

**Example**: `learning-rg-abc` contains App Service, App Service Plan, and database for a learning project.

**See**: [Chapter 1: First Deployment](./01-first-deployment/README.md)

### RTO (Recovery Time Objective)

The maximum acceptable time your application can be down after a disaster before business impact becomes unacceptable.

**Example**: RTO of 4 hours means the application must be restored within 4 hours of an outage.

**See**: [Chapter 10: Production Deployment](./10-production-deployment/README.md)

### RPO (Recovery Point Objective)

The maximum acceptable amount of data loss measured in time. Determines how frequently you need backups.

**Example**: RPO of 1 hour means you can lose at most 1 hour of data, requiring at least hourly backups.

**See**: [Chapter 10: Production Deployment](./10-production-deployment/README.md)

---

## S

### SKU (Stock Keeping Unit)

The specific tier and configuration of an Azure service. Different SKUs offer different performance, features, and pricing.

**Examples**:
- App Service: F1 (Free), B1 (Basic), S1 (Standard), P1V2 (Premium)
- Azure SQL: Basic, Standard S0-S12, Premium P1-P15
- Storage: Standard, Premium

**See**: [Chapter 1: First Deployment](./01-first-deployment/README.md)

### Static Web Apps

Azure's service for hosting static websites (HTML, CSS, JavaScript) with built-in CI/CD from GitHub/GitLab. Includes serverless API support via Azure Functions.

**Free tier**: 100GB bandwidth/month, perfect for frontend applications.

**See**: [Chapter 5: Production Web Application](./05-simple-web-app/README.md)

### Storage Account

A namespace in Azure that provides access to Blob, File, Queue, and Table storage. Multiple storage types can coexist in one account.

**Replication options**:
- **LRS (Locally Redundant)**: 3 copies in one datacenter
- **GRS (Geo-Redundant)**: Copies to secondary region for disaster recovery
- **ZRS (Zone-Redundant)**: Copies across availability zones

**See**: [Chapter 7: Data Storage Solutions](./07-data-storage/README.md)

---

## T

### Terraform

An open-source infrastructure-as-code tool by HashiCorp that works across multiple cloud providers (Azure, AWS, GCP). Uses HashiCorp Configuration Language (HCL).

**Benefits**:
- ✅ Multi-cloud support
- ✅ Large ecosystem and modules
- ✅ State management
- ✅ Plan before apply

**Contrast with**: Bicep (Azure-specific but simpler for Azure-only deployments)

**See**: [Chapter 4: Terraform Basics](./04-terraform-basics/README.md)

---

## V

### Virtual Network (VNet)

An isolated network in Azure that enables secure communication between Azure resources. Provides IP address management, subnets, network security groups, and private connectivity.

**Use cases**: Isolate resources, control traffic flow, connect to on-premises networks, use private endpoints.

**See**: [Chapter 10: Production Deployment](./10-production-deployment/README.md)

---

## W

### Web Application Firewall (WAF)

A security service that protects web applications from common exploits like SQL injection, cross-site scripting (XSS), and other OWASP top 10 vulnerabilities.

**Where it runs**: Application Gateway, Front Door, CDN

**See**: [Chapter 10: Security Hardening](./10-production-deployment/README.md)

---

## Related Resources

- [Course Home](./README.md)
- [Course Setup](./00-course-setup/README.md)
- [Azure Documentation](https://learn.microsoft.com/azure/)
- [GitHub Copilot for Azure](https://learn.microsoft.com/azure/developer/github-copilot-azure)
