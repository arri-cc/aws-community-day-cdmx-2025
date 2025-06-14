# GitHub Issue Management Workflow

Enhanced workflow using centralized configuration for consistent issue creation.

## Step 1: Load Configuration

```xml
<read_file>
<path>.clinerules/repo-config.json</path>
</read_file>
```

## Step 2: Investigation Phase

First, check for existing related issues to avoid duplicates:

```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/github</server_name>
<tool_name>search_issues</tool_name>
<arguments>
{
  "q": "repo:{owner}/{repo} is:issue [search terms from issue topic]"
}
</arguments>
</use_mcp_tool>
```

## Step 3: Issue Type Selection

Present available issue types from configuration:

1. **feat** (enhancement) - New features or significant improvements
2. **fix** (bug_report) - Bug fixes or corrections  
3. **chore** (chore) - Maintenance, refactoring, dependencies
4. **rfc** (rfc) - Large architectural proposals requiring discussion

## Step 4: Milestone Selection

Present available milestones from configuration:

1. **Phase 1: Core Architecture** - Foundation and core functionality
2. **Phase 2: Enhanced Features** - Advanced functionality and UX improvements
3. **Phase 3: Production Ready** - Performance, security, and deployment

Ask user to select appropriate milestone for the issue.

## Step 5: Issue Creation

Create the issue using the selected type and milestone:

```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/github</server_name>
<tool_name>create_issue</tool_name>
<arguments>
{
  "owner": "{config.repository.owner}",
  "repo": "{config.repository.repo}",
  "title": "{config.issueTypes[type].titlePrefix}{descriptive title}",
  "body": "{template-based body from GitHub issue templates}",
  "labels": "{config.issueTypes[type].labels}",
  "milestone": "{selected milestone number}"
}
</arguments>
</use_mcp_tool>
```

## Step 6: Project Association

Associate the issue with the GitHub project:

```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/github</server_name>
<tool_name>create_issue</tool_name>
<arguments>
{
  "owner": "{config.repository.owner}",
  "repo": "{config.repository.repo}",
  "issue_number": "{returned issue number}",
  "body": "{add project reference if needed}"
}
</arguments>
</use_mcp_tool>
```

## Step 7: RFC Subissue Workflow (if RFC type)

If the issue type is "rfc" and has subissues in the work breakdown:

1. Document the architectural decision in the RFC issue
2. Create subissues for implementation work items
3. Link subissues to the parent RFC issue
4. Use appropriate issue types (feat/fix/chore) for subissues

## Step 8: Documentation Integration

Update cline_docs/currentTask.md with the new issue reference using the returned issue number.

## Template Integration

The workflow uses GitHub issue templates from `.github/ISSUE_TEMPLATE/`:

- **enhancement.md** - For feat type issues
- **bug_report.md** - For fix type issues  
- **chore.md** - For chore type issues
- **rfc.md** - For rfc type issues

## Configuration Reference

All repository settings, issue types, milestones, and labels are defined in `.clinerules/repo-config.json`:

- Repository: `{owner}/{repo}` with project ID `{projectId}`
- Issue types with templates, labels, and commit types
- Milestone list with IDs and descriptions
- Consistent labeling and categorization
