# 🚀 Azure MCP in Action

[![GitHub license](https://img.shields.io/github/license/YOUR-USERNAME/azure-mcp-in-action.svg)](https://github.com/YOUR-USERNAME/azure-mcp-in-action/blob/main/LICENSE)
[![GitHub contributors](https://img.shields.io/github/contributors/YOUR-USERNAME/azure-mcp-in-action.svg)](https://github.com/YOUR-USERNAME/azure-mcp-in-action/graphs/contributors/)
[![GitHub issues](https://img.shields.io/github/issues/YOUR-USERNAME/azure-mcp-in-action.svg)](https://github.com/YOUR-USERNAME/azure-mcp-in-action/issues/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

Learn Azure deployments using GitHub Copilot for Azure and AI-assisted infrastructure management.

---

## 🎯 What You'll Learn

This course teaches you to deploy Azure infrastructure using **GitHub Copilot in [agent mode](./GLOSSARY.md#agent-mode) with [Azure MCP](./GLOSSARY.md#azure-mcp)**. Agent mode **generates infrastructure code and executes deployment commands** through natural language prompts with approval gates. You review the code, approve execution, and verify results. You'll leverage AI to accelerate your Azure development from hours to minutes.

### Real-World Projects You'll Deploy

The active chapters (0-3) focus on foundational skills plus the n8n automation scenario. Legacy chapters (Ghost, Superset, Metabase, Supabase, Strapi, etc.) are preserved under the `old/` directory while content is refreshed. Feel free to explore them, but the primary guided path currently covers Chapters 0-3.

### Core Skills

- ✅ **Prompt Engineering for Infrastructure** - Create Azure resources through natural language with agent mode
- ✅ **Agent mode proficiency** - Generate, approve, execute, and verify deployments with AI assistance
- ✅ **[Infrastructure-as-Code](./GLOSSARY.md#infrastructure-as-code-iac)** - [Bicep](./GLOSSARY.md#bicep) and [Terraform](./GLOSSARY.md#terraform) template generation
- ✅ **Container Orchestration** - [Container Apps](./GLOSSARY.md#azure-container-apps) and [AKS](./GLOSSARY.md#azure-kubernetes-service-aks) deployments
- ✅ **Data Services** - SQL, [Cosmos DB](./GLOSSARY.md#cosmos-db), [Blob Storage](./GLOSSARY.md#blob-storage), and BI platforms
- ✅ **Production Deployments** - Security, monitoring, cost optimization

---

## 🔥 Why This Course is Different

### Agent-First, Real-World Approach

Most Azure courses teach services in isolation. This course teaches **production deployment patterns** using **real open-source projects** that companies actually use.

### AI-Assisted Learning

- **[Generate → Approve → Execute Workflow](./GLOSSARY.md#generate--approve--execute-workflow)** for rapid deployment
- Agent mode generates code and executes commands with approval checkpoints
- Accelerate learning by 10x with AI assistance
- Focus on understanding, not memorization

### Portfolio-Ready Projects

Every chapter includes deployments you can showcase:
- "Deployed Apache Superset on Azure Kubernetes Service"
- "Architected Supabase BaaS platform on Azure"
- "Implemented production Ghost CMS with MySQL and CDN"

---

## 📚 Course Structure

The active track currently includes **4 chapters** (setup + three hands-on chapters). Archived chapters live under [`old/`](./old) until they are updated.

| # | Chapter | OSS Projects | Key Skills | Time |
|---|---------|--------------|------------|------|
| 0 | [Course Setup & Safety](./00-course-setup/README.md) | - | Azure account, safety, cost management | 90 min |
| 1 | [First Azure Deployment](./01-first-deployment/README.md) | **Node.js Hello World** | Generate → Approve → Execute workflow, first [App Service](./GLOSSARY.md#app-service) | 60 min |
| 2 | [Advanced Prompt Patterns](./02-prompt-patterns/README.md) | - | Advanced prompts, patterns | 75 min |
| 3 | [n8n Automation Agents](./03-n8n/README.md) | **n8n (Bicep + Terraform)** | Specialized Copilot agents, Container Apps, PostgreSQL | 90 min |

> Looking for the previous chapters (Terraform basics, Ghost, Superset, etc.)? Check the `old/` folder while we migrate that content into the new agent-focused approach.

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

- [Azure CLI](https://learn.microsoft.com/cli/azure/install-azure-cli) - Latest version (see [glossary](./GLOSSARY.md#azure-cli))
- [VS Code](https://code.visualstudio.com/) - Code editor
- [GitHub Copilot for Azure](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azure-github-copilot) - VS Code extension (see [glossary](./GLOSSARY.md#github-copilot-for-azure))
- [Git](https://git-scm.com/) - Version control

### Azure Account

You'll need ONE of the following:

- ✅ **Existing Azure subscription** (recommended if you have one)
- ✅ **Free Azure account** (free credits available) - [Sign up here](https://azure.microsoft.com/free/)

**Cost Management**: Chapter 0 sets up billing alerts and teaches cleanup practices to minimize costs

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

| Chapter | Scenario | Tier/SKU | Cleanup Required |
|---------|----------|----------|------------------|
| 0 | Course setup + billing safeguards | Free tier | N/A |
| 1 | First App Service deployment | F1 (Free) | Yes |
| 2 | Prompt practice & queries (no resources) | N/A | Yes |
| 3 | n8n on Container Apps + PostgreSQL | Paid (consumption/burstable) | Yes (immediate) |

### Safety Features

- ✅ Billing alerts configured in Chapter 0 (BEFORE any deployments)
- ✅ Resource tagging for easy cleanup
- ✅ Cleanup scripts provided for every chapter
- ✅ Azure MCP cleanup prompts included
- ✅ Cost estimates shown upfront

---

## 📖 Learning Path

### For Complete Beginners

1. Start with [Chapter 0](./00-course-setup/README.md) (mandatory).
2. Work through Chapters 1-3 to practice App Service basics, advanced prompt patterns, and the n8n deployment.
3. Explore the `old/` directory when you want previews of upcoming refreshed chapters.

**Timeline**: ~1 week (1 hour/day)

### For Experienced Azure Users

1. Review Chapter 0 quickly (or skip if you already have the safety setup).
2. Jump straight to Chapter 3 to compare the Bicep vs Terraform agents.
3. Dip into `old/` for deeper OSS case studies as needed.

### For Kubernetes Learners

1. Finish Chapters 0-3 now to learn the agent workflows.
2. Until the refreshed AKS content ships, explore `old/06-containerized-apps` for the Superset-on-AKS walkthrough.

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
├── 02-prompt-patterns/       # Advanced Azure MCP patterns
├── 03-n8n/                   # Copilot agents for n8n (Bicep & Terraform)
├── old/                      # Archived chapters (Ghost, Superset, etc.)
├── scripts/                  # Validation and helper scripts
├── prompts/                  # Reusable prompt patterns
├── GLOSSARY.md               # Comprehensive terminology
├── README.md                 # This file
└── package.json              # Course metadata
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

Ready to learn Azure infrastructure with AI assistance?

**[👉 Begin with Chapter 0: Course Setup](./00-course-setup/README.md)**

---

_Built with ❤️ by developers, for developers_
