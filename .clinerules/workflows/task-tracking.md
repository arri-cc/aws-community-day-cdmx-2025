# Task Tracking Workflow

Enhanced workflow using centralized configuration for consistent issue tracking and documentation integration.

## Step 1: Load Configuration

```xml
<read_file>
<path>.clinerules/repo-config.json</path>
</read_file>
```

## Step 2: List Current Issues

Get an overview of active issues using configuration:

```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/github</server_name>
<tool_name>list_issues</tool_name>
<arguments>
{
  "owner": "{config.repository.owner}",
  "repo": "{config.repository.repo}",
  "state": "open",
  "sort": "updated",
  "direction": "desc"
}
</arguments>
</use_mcp_tool>
```

## Step 3: Get Issue Details

For specific issues you want to track, get detailed information:

```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/github</server_name>
<tool_name>get_issue</tool_name>
<arguments>
{
  "owner": "{config.repository.owner}",
  "repo": "{config.repository.repo}",
  "issue_number": "{issue_number}"
}
</arguments>
</use_mcp_tool>
```

## Step 4: Update Current Task Documentation

Update cline_docs/currentTask.md to include issue tracking with proper formatting:

```markdown
## Related GitHub Issues

The following issues are tracked for current work:

### In Progress
1. [#{issue_number} - {config.issueTypes[type].titlePrefix}{title}](https://github.com/{config.repository.owner}/{config.repository.repo}/issues/{issue_number})
   **Status**: In Progress - {milestone_title}
   **Context**: {brief description of what this issue addresses}
   **Next Steps**: {what needs to be done next}

### Ready for Review
2. [#{issue_number} - {title}](https://github.com/{config.repository.owner}/{config.repository.repo}/issues/{issue_number})
   **Status**: Ready for Review - {milestone_title}
   **Context**: {brief description}
   **PR**: {link to PR if applicable}

### Blocked
3. [#{issue_number} - {title}](https://github.com/{config.repository.owner}/{config.repository.repo}/issues/{issue_number})
   **Status**: Blocked - {milestone_title}
   **Context**: {brief description}
   **Blocking Issue**: {what is blocking progress}
```

## Step 5: Update Project Roadmap

If issues represent major roadmap items, update cline_docs/projectRoadmap.md:

```markdown
## {milestone_title}

- [x] {completed task} - Issue #{number} ({config.issueTypes[type].titlePrefix})
- [ ] {in progress task} - Issue #{number} ({config.issueTypes[type].titlePrefix}) (In Progress)
- [ ] {planned task} - Issue #{number} ({config.issueTypes[type].titlePrefix}) (Ready)
```

## Step 6: Issue Status Management

### Close Completed Issues

```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/github</server_name>
<tool_name>update_issue</tool_name>
<arguments>
{
  "owner": "{config.repository.owner}",
  "repo": "{config.repository.repo}",
  "issue_number": "{issue_number}",
  "state": "closed"
}
</arguments>
</use_mcp_tool>
```

### Add Progress Comments

```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/github</server_name>
<tool_name>add_issue_comment</tool_name>
<arguments>
{
  "owner": "{config.repository.owner}",
  "repo": "{config.repository.repo}",
  "issue_number": "{issue_number}",
  "body": "## Progress Update\n\n**Completed:**\n- {item 1}\n- {item 2}\n\n**Next Steps:**\n- {next item}\n- {another item}\n\n**Blockers:**\n- {any blocking issues}"
}
</arguments>
</use_mcp_tool>
```

### Update Labels with Configuration-Based Labels

```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/github</server_name>
<tool_name>update_issue</tool_name>
<arguments>
{
  "owner": "{config.repository.owner}",
  "repo": "{config.repository.repo}",
  "issue_number": "{issue_number}",
  "labels": "{config.issueTypes[type].labels plus status labels}"
}
</arguments>
</use_mcp_tool>
```

## Step 7: Project Association

Ensure all tracked issues are associated with the GitHub project:

```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/github</server_name>
<tool_name>update_issue</tool_name>
<arguments>
{
  "owner": "{config.repository.owner}",
  "repo": "{config.repository.repo}",
  "issue_number": "{issue_number}",
  "body": "{updated body with project reference if needed}"
}
</arguments>
</use_mcp_tool>
```

## Step 8: Cross-Reference Management

### Link Issues to Documentation

When working on issues, ensure proper cross-referencing:

#### In Code Comments
```typescript
// Related to GitHub issue #{issue_number}: {issue_title}
// See: https://github.com/{config.repository.owner}/{config.repository.repo}/issues/{issue_number}
```

#### In Commit Messages (using commit-message.md workflow)
```bash
{config.issueTypes[type].commitType}: {description} (#{issue_number})

{optional body describing changes}

Addresses requirements in #{issue_number}
```

#### In Pull Requests
```markdown
## Related Issues

Closes #{issue_number}
Related to #{related_issue_number}

## Changes Made

{description of changes that address the issues}
```

## Issue Type Integration

### Issue Type Mapping from Configuration

Based on `.clinerules/repo-config.json`:

- **feat** (enhancement) → `feat:` commits, `enhancement` labels
- **fix** (bug_report) → `fix:` commits, `bug` labels  
- **chore** (chore) → `chore:` commits, `chore` labels
- **rfc** (rfc) → `docs:` commits, `rfc, proposal` labels

### RFC Subissue Tracking

For RFC issues with subissues:

```markdown
## RFC Implementation Tracking

### Parent RFC
[#{rfc_number} - rfc: {title}](https://github.com/{owner}/{repo}/issues/{rfc_number})

### Implementation Issues
- [ ] [#{sub1} - feat: {subissue 1 title}](https://github.com/{owner}/{repo}/issues/{sub1})
- [ ] [#{sub2} - fix: {subissue 2 title}](https://github.com/{owner}/{repo}/issues/{sub2})
- [ ] [#{sub3} - chore: {subissue 3 title}](https://github.com/{owner}/{repo}/issues/{sub3})
```

## Milestone Integration

### Milestone-Based Organization

Organize issues by milestones from configuration:

```markdown
## Phase 1: Core Architecture
- [ ] #{issue1} - feat: {feature 1}
- [x] #{issue2} - fix: {bug fix 1}
- [ ] #{issue3} - chore: {maintenance task}

## Phase 2: Enhanced Features  
- [ ] #{issue4} - feat: {feature 2}
- [ ] #{issue5} - rfc: {architecture decision}

## Phase 3: Production Ready
- [ ] #{issue6} - chore: {deployment preparation}
- [ ] #{issue7} - feat: {production feature}
```

## Status Tracking Guidelines

### Issue Lifecycle with Configuration:
1. **Open** - Issue created using configured templates and labels
2. **In Progress** - Actively being worked on, tracked in currentTask.md
3. **Ready for Review** - Implementation complete, needs review
4. **Blocked** - Cannot proceed due to dependencies  
5. **Closed** - Completed using proper commit message format

### Documentation Sync Strategy:
- Update currentTask.md whenever issue status changes
- Update projectRoadmap.md when major milestones are reached
- Update codebaseSummary.md when issues result in significant architectural changes
- Use `/documentation-sync.md` workflow after human confirmation of completion

### Configuration-Based Labels:
- Base labels from `config.issueTypes[type].labels`
- Status labels: `in-progress`, `ready-for-review`, `blocked`
- Priority labels: `priority-high`, `priority-medium`, `priority-low`
- Context labels: `help-wanted`, `good-first-issue`

## Workflow Integration

This workflow integrates with other workflows:

- **`/github-issue.md`** - Creates issues this workflow tracks
- **`/commit-message.md`** - Generates commit messages referencing tracked issues
- **`/architecture-decision.md`** - Creates RFC issues with subissue tracking
- **`/documentation-sync.md`** - Updates documentation when issues are completed
- **`/milestone-management.md`** - Manages milestone assignments for issues

## Configuration Benefits

Using centralized configuration provides:

- **Consistent Issue References**: All workflows use same owner/repo format
- **Standardized Labeling**: Issue types map to consistent labels
- **Milestone Integration**: Issues assigned to configured milestones
- **Commit Message Mapping**: Issue types map to conventional commit types
- **Project Association**: All issues linked to configured project ID
