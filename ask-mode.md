# Ask Mode Reference Guide

This guide covers GitHub Copilot's **Ask Mode** for learning about Azure without taking actions.

> **Note**: This course focuses on **Agent Mode** for hands-on infrastructure deployment. Ask mode is available if you want to learn concepts or get architectural guidance, but it's not required for completing the course.

---

## What is Ask Mode?

Ask mode is the default mode in GitHub Copilot that provides answers to your questions in the chat pane without modifying code or creating resources. It's fast, helpful, and focused entirely on answering questions.

**Contrast with Agent Mode**: Agent mode generates code, executes commands, and creates/modifies Azure resources with your approval.

---

## When to Use Ask Mode

**Use Ask Mode when you want to**:
- Get Azure guidance and architectural recommendations
- Compare Azure services (e.g., "Should I use X or Y?")
- Learn best practices without taking action
- Understand Azure concepts and terminology
- Get documentation quickly

**Use Agent Mode when you want to**:
- Create, update, or delete Azure resources
- Deploy applications and infrastructure
- Execute commands and run deployments
- Troubleshoot issues with diagnostic commands

---

## How to Activate Ask Mode

1. Open GitHub Copilot Chat in VS Code (`Cmd+Shift+I` or `Ctrl+Shift+I`)
2. Click the mode dropdown at the bottom of the chat panel
3. Select **Ask**
4. Start prompts with `@azure` to scope questions to Azure

---

## Example Prompts

### Service Comparison
```
@azure What's the difference between Azure Container Apps and Azure Kubernetes Service?
@azure Should I use SQL Database or Cosmos DB for my application?
```

### Architecture Guidance
```
@azure What App Service tier should I use for 10,000 requests/day?
@azure How should I architect a multi-region deployment?
@azure What's the best way to secure connection strings?
```

### Best Practices
```
@azure What are best practices for App Service deployments?
@azure How do I optimize Azure costs for a web application?
@azure What security measures should I implement for production?
```

### Learning Concepts
```
@azure Explain how Azure managed identities work
@azure What is the difference between horizontal and vertical scaling?
@azure How does Azure auto-scaling work?
```

---

## What Happens in Ask Mode

When you use Ask mode:
1. Copilot analyzes your question
2. Searches Azure documentation and best practices
3. Provides explanations, comparisons, and recommendations
4. **No code generation or resource creation**
5. **No "Allow" buttons** - it's purely informational

---

## Quick Reference Table

| Task | Mode | How to Use |
|------|------|------------|
| Get Azure advice | Ask | `@azure What's the difference between...?` |
| Compare services | Ask | `@azure Should I use X or Y for...?` |
| Learn best practices | Ask | `@azure What are best practices for...?` |
| Understand concepts | Ask | `@azure Explain how X works` |
| Create resources | Agent | Natural language prompt with "Azure" |
| Deploy applications | Agent | Natural language prompt with "Azure" |
| Update/delete resources | Agent | Natural language prompt with "Azure" |

---

## Ask Mode vs Agent Mode Summary

| Feature | Ask Mode | Agent Mode |
|---------|----------|------------|
| **Purpose** | Learning & guidance | Taking actions |
| **Prefix** | `@azure` | Natural language with "Azure" |
| **Output** | Explanations & advice | Code + execution |
| **Resource Creation** | ❌ No | ✅ Yes (with approval) |
| **Command Execution** | ❌ No | ✅ Yes (with approval) |
| **Approval Required** | ❌ No | ✅ Yes ("Allow" buttons) |
| **Best For** | Understanding concepts | Deploying infrastructure |

---

## Example: Architecture Planning with Ask Mode

Before deploying a web application, you might use Ask mode to plan:

**Step 1: Service Selection**
```
@azure I need to deploy a Node.js API that handles 10,000 requests/day.
Should I use App Service or Container Apps?
```

**Step 2: Database Selection**
```
@azure My application needs to store user profiles and product catalogs.
Should I use SQL Database, Cosmos DB, or both?
```

**Step 3: Best Practices**
```
@azure What are the best practices for securing App Service with a database?
```

**Then switch to Agent Mode** to actually create the resources.

---

## When Ask Mode is Useful in the Course

While this course focuses on agent mode for hands-on deployment, Ask mode can be helpful:

1. **Before deployments**: Get architectural guidance
2. **Service selection**: Compare Azure services for your needs
3. **Learning concepts**: Understand how Azure features work
4. **Best practices**: Learn recommendations before implementing

---

## Important Notes

- **Ask mode doesn't create resources** - it only provides information
- **Use `@azure` prefix** to scope questions to Azure
- **Agent mode is required** for all hands-on exercises in this course
- **You can switch modes** anytime using the dropdown in Copilot chat

---

## Related Resources

- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [Azure Documentation](https://docs.microsoft.com/azure)
- [Return to Course](./README.md)
