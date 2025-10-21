# agent mode Migration Summary

## Completed Updates

### Core Files (100% Complete)
- ✅ **00-course-setup/README.md** - Chapter 0 fully updated
  - Part 2a: Two modes (Agent/Ask) with activation instructions
  - Part 3: Generate → Approve → Execute → Verify workflow
  - Part 8: Exercises using agent mode
  - All references to tool-specific commands removed

- ✅ **AGENTS.md** - AI agent guidance fully updated
  - Core principles updated
  - Two modes documented (Agent/Ask)
  - All workflows updated with approval gates
  - Success metrics revised

- ✅ **README.md** - Main course README updated
  - Course description updated
  - Interaction modes changed from 3 to 2
  - Workflow updated to Generate → Approve → Execute → Verify

### Chapter Files (Partially Complete)
- ✅ **01-first-deployment/README.md** - Fully updated
  - Real-world scenario updated
  - Part 2: agent mode activation instructions added
  - Part 3: Workflow explanation updated
  - Success criteria and key takeaways updated

- ✅ **02-cli-mastery/README.md** - Partially updated
  - Pattern 1 example updated with agent mode workflow
  - Remaining: ~9 more "Azure MCP will" instances

- ✅ **05-simple-web-app/README.md** - Partially updated
  - Real-world scenario updated
  - Part 1: ask mode instructions added
  - Remaining: ~6 "Azure MCP will" instances

## Remaining Updates Needed

### Pattern to Replace

**OLD Pattern:**
```markdown
**Azure MCP will**:
- Create the resource
- Configure settings
- Return confirmation
```

**NEW Pattern:**
```markdown
**What happens in agent mode**:
1. Generates infrastructure code (Bicep or CLI commands)
2. Shows "Continue?" button for you to review
3. After approval, executes commands in terminal
4. Commands create the resource with your settings
5. Returns confirmation with details
```

**OR Shorter Version:**
```markdown
**agent mode will**:
1. Generate code → Ask "Continue?" → Execute after approval
2. Create the resource with your settings
3. Return confirmation
```

### Files Needing Updates

1. **02-cli-mastery/README.md** - 10 instances
   - Lines: 106, 126, 141, 158, 177, 201, 216, 241, 260, 314

2. **03-bicep-templates/README.md** - 1 instance

3. **04-terraform-basics/README.md** - 1 instance

4. **05-simple-web-app/README.md** - 6 instances
   - Lines: 68, 98, 167, 189, 201, 290

5. **06-containerized-apps/README.md** - 5 instances
   - Lines: 51, 120, 146, 221, plus 1 more

6. **07-data-storage/README.md** - 5 instances
   - Lines: 58, 127, 152, 226, 250

7. **08-diagnostics-troubleshooting/README.md** - 2 instances

8. **09-multi-service-architecture/README.md** - 4 instances

9. **10-production-deployment/README.md** - 4 instances

10. **.plans/azure-mcp-plan.md** - 1 instance (actually has correct info)

## Additional Search Patterns

To find all remaining instances, use:
```bash
grep -rn "Azure MCP will" --include="*.md"
grep -rn "directly creat" --include="*.md" -i
grep -rn "directly manag" --include="*.md" -i
grep -rn "#azure_generate_azure_cli_command" --include="*.md"
```

## Key Terminology Changes

| Old Term | New Term |
|----------|----------|
| "Azure MCP directly creates" | "agent mode generates code, you approve, agent executes commands that create" |
| "Azure MCP will" | "agent mode will" or "What happens in agent mode" |
| "Three modes" | "Two modes" |
| "Mode 1: Direct Resource Creation" | "agent mode" |
| "Mode 2: Ask Questions" | "ask mode" |
| "Mode 3: Generate Commands" | (Removed - not needed in agent mode) |
| "Prompt → Create → Verify" | "Generate → Approve → Execute → Verify" |

## Instructions for Remaining Updates

For each file:

1. Search for "Azure MCP will"
2. Replace with agent mode workflow (see patterns above)
3. Add mode activation instructions where missing
4. Update any "directly creates" language
5. Remove references to `#azure_generate_azure_cli_command` in agent mode sections
6. Keep `@azure` only for ask mode examples

## Verification Checklist

After updating each file, verify:
- [ ] No mentions of "Azure MCP directly creates"
- [ ] No "Azure MCP will" without clarification
- [ ] agent mode activation instructions included
- [ ] Approval workflow ("Continue?" buttons) mentioned
- [ ] Two modes clearly distinguished (Agent vs Ask)
- [ ] No tool-specific commands in agent mode examples
