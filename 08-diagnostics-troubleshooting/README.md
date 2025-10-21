# Chapter 8: Diagnostics and Troubleshooting

Use agent mode to diagnose and fix Azure infrastructure issues quickly. In this chapter, you'll learn AI-assisted troubleshooting techniques to identify performance bottlenecks, analyze Application Insights telemetry, resolve deployment failures, and optimize resource performance.

## Prerequisites

- Completed [Course Setup](../00-course-setup/README.md)
- Completed [Chapter 1: First Deployment](../01-first-deployment/README.md)
- Completed [Chapter 2: Advanced Prompt Patterns](../02-cli-mastery/README.md)
- Completed [Chapter 3: Infrastructure-as-Code with Bicep](../03-bicep-templates/README.md)
- Completed [Chapter 4: Terraform Basics](../04-terraform-basics/README.md)
- Completed [Chapter 5: Production Web Application](../05-simple-web-app/README.md)
- Completed [Chapter 6: Containerized Applications](../06-containerized-apps/README.md)
- Completed [Chapter 7: Data Storage Solutions](../07-data-storage/README.md)

## 🎯 Learning Objectives

- ✅ Use agent mode for troubleshooting Azure resources
- ✅ Query Azure Monitor logs effectively
- ✅ Analyze Application Insights telemetry
- ✅ Identify performance bottlenecks
- ✅ Resolve common deployment failures
- ✅ Optimize resource performance

## Real-World Scenario

> Your production App Service is experiencing high response times and occasional 500 errors. Users are complaining. You need to diagnose and fix the issue quickly. You'll use Azure MCP's diagnostic tools to identify the root cause and generate fixes.

---

## Part 1: Common Issues and Diagnostics

### Issue: Slow Response Times

```
Investigate why my App Service 'slowapp' has response times > 5 seconds.
Check: CPU usage, memory, database queries, external API calls, and network latency.
Generate diagnostic commands and analysis.
```

### Issue: Intermittent 500 Errors

```
My web app returns 500 errors randomly. Analyze:
- Application logs for exceptions
- App Service metrics
- Database connection pool
- Memory leaks
Provide diagnostic commands and probable causes.
```

---

## Part 2: Performance Optimization

**Prompt to Azure MCP**:
```
Based on diagnostics showing high CPU usage on my App Service,
perform these optimizations:
1. Scale up App Service to next tier
2. Enable auto-scaling rules (CPU > 70%)
3. Configure CDN for static content
4. Enable caching with Azure Cache for Redis Basic tier
```

**agent mode will**:
1. Generate scaling/optimization code → Show "Continue?" → Execute after approval
2. Scale up the App Service Plan
3. Configure auto-scaling rules
4. Create and configure CDN endpoint
5. Deploy Redis cache, update app settings, and return new configuration details

---

## Assignment

1. Deploy a problematic application (provided with known issues)
2. Use AI diagnostic tools to identify all problems
3. Generate and execute fix commands
4. Verify performance improvements
5. Document troubleshooting process
6. Create monitoring alerts to prevent recurrence

### Success Criteria

- ✅ Identified root causes using AI diagnostics
- ✅ Generated appropriate fix commands
- ✅ Performance improved measurably
- ✅ Monitoring configured to prevent recurrence
- ✅ Documented troubleshooting methodology
- ✅ Response time under 500ms, 99.9% uptime achieved

---

## Cleanup Using Azure MCP

> [!IMPORTANT]
> Complete this cleanup to avoid unexpected Azure charges. This chapter had you create test resources for diagnostics practice. Clean them up promptly.

### Method 1: Use Azure MCP (RECOMMENDED)

**Prompt to Azure MCP**:
```
Delete all resources created in Chapter 8:
- Test App Service 'slowapp' and its plan
- Application Insights instances
- Log Analytics workspaces
- Redis cache instances
- Resource group: diagnostics-demo-rg
```

**agent mode will**:
1. Generate deletion commands → Show "Continue?" → Execute after approval
2. Delete all diagnostics test resources
3. Remove resource group and contained resources
4. Confirm deletion completion

### Method 2: Manual Cleanup with Azure CLI

```bash
# Step 1: Delete App Service and plan
az webapp delete \
  --name slowapp \
  --resource-group diagnostics-demo-rg

az appservice plan delete \
  --name slowapp-plan \
  --resource-group diagnostics-demo-rg \
  --yes

# Step 3: Delete Redis cache if created
az redis delete \
  --name diagnostics-cache \
  --resource-group diagnostics-demo-rg \
  --yes

# Step 4: Delete Application Insights
az monitor app-insights component delete \
  --app slowapp-insights \
  --resource-group diagnostics-demo-rg

# Step 5: Delete Log Analytics workspace
az monitor log-analytics workspace delete \
  --workspace-name diagnostics-logs \
  --resource-group diagnostics-demo-rg \
  --yes

# Step 6: Delete resource group
az group delete --name diagnostics-demo-rg --yes --no-wait
```

---

### Before You Delete

- [ ] Export any diagnostic logs or insights you want to keep
- [ ] Save screenshots of diagnostics dashboards for documentation
- [ ] Document the troubleshooting methodology you learned
- [ ] Verify resource group names match what you created

---

### Verify Complete Deletion

**Verify resource group is gone (Bash/macOS/Linux):**
```bash
az group list --output table | grep diagnostics
```

**Verify resource group is gone (PowerShell/Windows):**
```powershell
az group list --output table | Select-String "diagnostics"
```

**Check for orphaned resources:**
```bash
# Check for orphaned App Services
az webapp list --query "[?name=='slowapp']" -o table
# Should return empty
```

**Cost Impact**:
- Before deletion: ~$30-60/month
- After deletion: $0/month

---

## Key Takeaways

1. **AI-Assisted Diagnostics**: Use agent mode to quickly identify and troubleshoot issues
2. **Logs Are Critical**: Application Insights and Log Analytics provide deep insights
3. **Performance Optimization**: Identify bottlenecks before scaling resources
4. **Preventive Monitoring**: Set up alerts to catch issues before users complain
5. **Document Solutions**: Save troubleshooting steps for future reference
6. **Cost Optimization**: Fix issues efficiently without over-provisioning resources

---

## What's Next?

**[Chapter 9: Multi-Service Architecture (Supabase, Strapi)](../09-multi-service-architecture/README.md)**

Now that you know how to troubleshoot issues, you'll deploy the most complex architectures yet: complete multi-service applications including Supabase (Firebase alternative) and Strapi (headless CMS).
