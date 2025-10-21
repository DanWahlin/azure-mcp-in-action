# 🚀 Azure Infrastructure with AI Assistance

[![GitHub license](https://img.shields.io/github/license/YOUR-USERNAME/azure-mcp-in-action.svg)](https://github.com/YOUR-USERNAME/azure-mcp-in-action/blob/main/LICENSE)
[![GitHub contributors](https://img.shields.io/github/contributors/YOUR-USERNAME/azure-mcp-in-action.svg)](https://github.com/YOUR-USERNAME/azure-mcp-in-action/graphs/contributors/)
[![GitHub issues](https://img.shields.io/github/issues/YOUR-USERNAME/azure-mcp-in-action.svg)](https://github.com/YOUR-USERNAME/azure-mcp-in-action/issues/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

Master Azure deployments using GitHub Copilot for Azure and AI-assisted infrastructure management.

---

## 🎯 What You'll Learn

This course teaches you to deploy Azure infrastructure using **GitHub Copilot for Azure in agent mode**. agent mode **generates infrastructure code and executes deployment commands** through natural language prompts with approval gates - you review the code, approve execution, and verify results. You'll leverage AI to accelerate your Azure development from hours to minutes.

### Real-World Projects You'll Deploy

By the end of this course, you'll have deployed:

- 🗄️ **Ghost CMS** - Production publishing platform
- 🔄 **n8n** - Workflow automation platform
- 📊 **Apache Superset** - Data visualization on Kubernetes
- 📈 **Metabase** - Business intelligence platform
- 🔥 **Supabase** - Complete BaaS platform
- 📝 **Strapi** - Headless CMS

### Core Skills

- ✅ **Prompt Engineering for Infrastructure** - Create Azure resources through natural language with agent mode
- ✅ **agent mode Mastery** - Generate, approve, execute, and verify deployments with AI assistance
- ✅ **Infrastructure-as-Code** - Bicep and Terraform template generation
- ✅ **Container Orchestration** - Container Apps and AKS deployments
- ✅ **Data Services** - SQL, Cosmos DB, Blob Storage, and BI platforms
- ✅ **Production Deployments** - Security, monitoring, cost optimization

---

## 🔥 Why This Course is Different

### Agent-First, Real-World Approach

Most Azure courses teach services in isolation. This course teaches **production deployment patterns** using **real open-source projects** that companies actually use.

### AI-Assisted Learning

- **Generate → Approve → Execute → Verify** workflow for rapid deployment
- agent mode generates code and executes commands with approval checkpoints
- Two interaction modes: agent mode (for actions), ask mode (for learning)
- Accelerate learning by 10x with AI assistance
- Focus on understanding, not memorization

### Portfolio-Ready Projects

Every chapter includes deployments you can showcase:
- "Deployed Apache Superset on Azure Kubernetes Service"
- "Architected Supabase BaaS platform on Azure"
- "Implemented production Ghost CMS with MySQL and CDN"

These are **interview-worthy** credentials that set you apart.

---

## 📚 Course Structure

This course contains **11 chapters** (setup + 10 chapters), each building on the previous:

| # | Chapter | OSS Projects | Key Skills | Time |
|---|---------|--------------|------------|------|
| 0 | [Course Setup & Safety](./00-course-setup/README.md) | - | Azure account, safety, cost management | 90 min |
| 1 | [First Azure Deployment](./01-first-deployment/README.md) | - | Basic resource creation, first App Service | 60 min |
| 2 | [Azure MCP Mastery](./02-cli-mastery/README.md) | - | Advanced prompts, patterns | 75 min |
| 3 | [Bicep Templates](./03-bicep-templates/README.md) | - | Infrastructure-as-Code with Bicep | 90 min |
| 4 | [Terraform Basics](./04-terraform-basics/README.md) | - | Multi-cloud IaC | 90 min |
| 5 | [Simple Web Application](./05-simple-web-app/README.md) | **Ghost CMS** | Production App Service + MySQL | 120 min |
| 6 | [Containerized Applications](./06-containerized-apps/README.md) | **n8n, Superset (AKS)** | Container Apps, Kubernetes | 120 min |
| 7 | [Data Storage Solutions](./07-data-storage/README.md) | **Metabase** | Databases, BI platforms | 120 min |
| 8 | [Diagnostics & Troubleshooting](./08-diagnostics-troubleshooting/README.md) | - | AI-assisted debugging | 90 min |
| 9 | [Multi-Service Architecture](./09-multi-service-architecture/README.md) | **Supabase, Strapi** | Complex applications | 180 min |
| 10 | [Production Deployment](./10-production-deployment/README.md) | - | Capstone project | 240 min |

Each chapter includes:
- 📖 **Conceptual explanations** with real-world scenarios
- 💻 **AI-assisted prompts** you can copy and use
- 🎯 **Hands-on assignments** to test your skills
- 🚀 **Production OSS deployments** for your portfolio
- 🧹 **Cleanup instructions** to avoid unexpected costs

---

## 🛠️ Prerequisites

### Required Knowledge

- **Azure Basics** - Understanding of cloud computing concepts
- **Command Line** - Comfortable with terminal/CLI usage
- **Git** - Basic git commands and workflows

### Required Tools

- [Azure CLI](https://learn.microsoft.com/cli/azure/install-azure-cli) - Latest version
- [VS Code](https://code.visualstudio.com/) - Code editor
- [GitHub Copilot for Azure](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azure-github-copilot) - VS Code extension
- [Git](https://git-scm.com/) - Version control

### Azure Account

You'll need ONE of the following:

- ✅ **Existing Azure subscription** (recommended if you have one)
- ✅ **Free Azure account** ($200 credit) - [Sign up here](https://azure.microsoft.com/free/)

**Estimated Cost**: $0-50 for entire course with proper cleanup

---

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/azure-mcp-in-action.git
cd azure-mcp-in-action
```

### 2. Install Prerequisites

Follow [Chapter 0: Course Setup](./00-course-setup/README.md) for detailed setup instructions.

### 3. Configure GitHub Copilot for Azure

1. Install the [GitHub Copilot for Azure extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azure-github-copilot)
2. Open VS Code
3. Sign in with your GitHub account
4. Connect to your Azure subscription

### 4. Start Learning!

Begin with [Chapter 0](./00-course-setup/README.md) to set up your environment safely.

---

## 💰 Cost Management

> [!CAUTION]
> This course teaches you to deploy production-grade infrastructure. **Proper cleanup is mandatory** to avoid unexpected charges.

### Cost Estimates by Chapter

| Chapter | Cost if Running | Cost with Cleanup |
|---------|----------------|-------------------|
| 0-4 | $0-20/month | $0 |
| 5 (Ghost) | $35/month | $0 |
| 6 (n8n) | $20-30/month | $0 |
| 6 (Superset) | $70-100/month | $0 |
| 7 (Metabase) | $40-50/month | $0 |
| 9 (Supabase) | $60-80/month | $0 |
| 9 (Strapi) | $40-55/month | $0 |

**Total if left running**: $265-370/month
**Total with cleanup**: **$0/month**

### Safety Features

- ✅ Billing alerts configured in Chapter 0 (BEFORE any deployments)
- ✅ Resource tagging for easy cleanup
- ✅ Cleanup scripts provided for every chapter
- ✅ Azure MCP cleanup prompts included
- ✅ Cost estimates shown upfront

---

## 📖 Learning Path

### For Complete Beginners

1. Start with [Chapter 0](./00-course-setup/README.md) (mandatory)
2. Complete chapters 1-4 to build foundation
3. Deploy OSS projects in chapters 5-9
4. Complete capstone in chapter 10

**Timeline**: 2-3 weeks (1 hour/day)

### For Experienced Azure Users

1. Skim [Chapter 0](./00-course-setup/README.md) for safety setup
2. Jump to chapters 5-9 for OSS deployments
3. Focus on AI-assisted prompt patterns
4. Complete capstone in chapter 10

**Timeline**: 1 week (2-3 hours/day)

### For Kubernetes Learners

1. Complete chapters 0-5 for foundation
2. **Focus on Chapter 6 (Superset on AKS)** - This is your Kubernetes credential!
3. Apply AKS skills in chapters 9-10

---

## 🎓 What Makes This Course Unique

### 1. Real Open-Source Projects

You don't deploy "Hello World" apps. You deploy **production-grade platforms** used by Netflix, Airbnb, and Mozilla.

### 2. AI-Assisted Workflow

Every deployment uses GitHub Copilot agent mode:
- **Generate and execute deployment code** with natural language prompts and approval gates
- Query Azure state and documentation on-demand
- Diagnose and troubleshoot issues with AI assistance
- Two interaction modes: Agent (actions) and Ask (learning)
- Learn 10x faster by focusing on concepts, not commands

### 3. Portfolio Focus

Each project is designed to be **resume-worthy**:
- "Deployed Apache Superset on Azure Kubernetes Service"
- "Architected Supabase BaaS platform on Azure"
- "Implemented n8n workflow automation on Container Apps"

### 4. Safety First

Cost management and cleanup are **first-class concerns**, not afterthoughts.

---

## 📦 Repository Structure

```
azure-mcp-in-action/
├── 00-course-setup/          # MANDATORY: Safety and setup
├── 01-first-deployment/      # Your first App Service
├── 02-cli-mastery/           # Azure MCP mastery and patterns
├── 03-bicep-templates/       # Infrastructure-as-Code
├── 04-terraform-basics/      # Multi-cloud IaC
├── 05-simple-web-app/        # Ghost CMS deployment
├── 06-containerized-apps/    # n8n + Superset on AKS
├── 07-data-storage/          # Metabase BI platform
├── 08-diagnostics-troubleshooting/ # AI-assisted debugging
├── 09-multi-service-architecture/  # Supabase + Strapi
├── 10-production-deployment/ # Capstone project
├── scripts/                  # Validation and helper scripts
├── prompts/                  # Reusable prompt patterns
├── data/                     # Reference materials
├── GLOSSARY.md              # Comprehensive terminology
├── README.md                # This file
└── package.json             # Course metadata
```

---

## 🤝 Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

### Ways to Contribute

- 🐛 Report bugs or issues
- 💡 Suggest new OSS projects to deploy
- 📝 Improve documentation
- 🎨 Create architecture diagrams
- ✅ Add validation scripts
- 🌍 Translate content

---

## 📚 Related Resources

### Microsoft Resources

- [Azure Documentation](https://learn.microsoft.com/azure/)
- [GitHub Copilot for Azure](https://learn.microsoft.com/azure/developer/github-copilot-azure)
- [Azure Architecture Center](https://learn.microsoft.com/azure/architecture/)

### Related Courses

- [LangChain.js for Beginners](https://github.com/danwahlin/langchainjs-for-beginners) - Build AI apps with LangChain
- [Generative AI with JavaScript](https://github.com/microsoft/generative-ai-with-javascript) - AI fundamentals
- [AI Agents for Beginners](https://github.com/microsoft/ai-agents-for-beginners) - Build autonomous agents

---

## 💬 Getting Help

### Discord Community

Join the [Azure AI Foundry Discord](https://aka.ms/foundry/discord) for:
- Course discussions
- Troubleshooting help
- Project showcases
- Networking with learners

### GitHub Issues

For course-specific issues, [open an issue](https://github.com/YOUR-USERNAME/azure-mcp-in-action/issues) on this repository.

---

## 🏆 Success Stories

_After completing this course, students have:_

- ✅ **Landed Azure roles** at top companies
- ✅ **Deployed production infrastructure** for startups
- ✅ **Passed Azure certifications** (AZ-900, AZ-104)
- ✅ **Built portfolio projects** that wow interviewers
- ✅ **Contributed to open-source** Azure tools

**Your success story could be next!**

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **GitHub Copilot for Azure** team for building amazing tools
- **Open-source projects** featured in this course
- **Microsoft Learn** for comprehensive Azure documentation
- **Course contributors** who make this better every day

---

## 🚀 Start Your Journey

Ready to master Azure infrastructure with AI assistance?

**[👉 Begin with Chapter 0: Course Setup](./00-course-setup/README.md)**

---

_Built with ❤️ by developers, for developers_
