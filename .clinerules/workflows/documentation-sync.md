# Documentation Synchronization Workflow

Use this workflow to maintain consistent and up-to-date project documentation across the cline_docs system.

## Step 1: Check Current Documentation State

Review the current state of all documentation files:

```xml
<list_files>
<path>cline_docs</path>
<recursive>false</recursive>
</list_files>
```

Read key documentation files to assess current state:

```xml
<read_file>
<path>cline_docs/currentTask.md</path>
</read_file>
```

```xml
<read_file>
<path>cline_docs/projectRoadmap.md</path>
</read_file>
```

## Step 2: Identify Required Updates

Based on recent changes, determine which documents need updates:

### Documentation Files to Review:

1. **projectRoadmap.md** - Update when:
   - High-level goals change
   - Major roadmap tasks are completed
   - New phases or milestones are defined

2. **currentTask.md** - Update when:
   - Completing significant tasks or subtasks
   - Starting new work streams
   - Status changes for active issues

3. **techStack.md** - Update when:
   - Significant technology decisions are made
   - New frameworks or tools are adopted
   - Architecture patterns change

4. **codebaseSummary.md** - Update when:
   - Significant changes affect overall structure
   - Major new components are introduced
   - Data flow patterns change

5. **historicalDecisionsAndCaveats.md** - Update when:
   - Major historical decisions need clarification
   - Important architectural caveats are discovered
   - Lessons learned from significant issues

## Step 3: Update Documentation Files

### Update currentTask.md

```xml
<replace_in_file>
<path>cline_docs/currentTask.md</path>
<diff>
<<<<<<< SEARCH
[content to replace]
=======
[new content]
>>>>>>> REPLACE
</diff>
</replace_in_file>
```

### Update projectRoadmap.md

```xml
<replace_in_file>
<path>cline_docs/projectRoadmap.md</path>
<diff>
<<<<<<< SEARCH
- [ ] [task description]
=======
- [x] [task description] - Completed [date]
>>>>>>> REPLACE
</diff>
</replace_in_file>
```

## Step 4: Cross-Reference Validation

Ensure consistency across documentation:

### Check Issue References

```xml
<search_files>
<path>cline_docs</path>
<regex>#\d+</regex>
<file_pattern>*.md</file_pattern>
</search_files>
```

### Validate Links

```xml
<search_files>
<path>cline_docs</path>
<regex>https://github\.com/arri-cc/today-is-my-bday</regex>
<file_pattern>*.md</file_pattern>
</search_files>
```

## Step 5: Create Documentation PR (if needed)

For significant documentation changes that should be tracked:

### Create a Documentation Branch

```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/github</server_name>
<tool_name>create_branch</tool_name>
<arguments>
{
  "owner": "arri-cc",
  "repo": "today-is-my-bday",
  "branch": "docs-update-[date]",
  "from_branch": "main"
}
</arguments>
</use_mcp_tool>
```

### Push Documentation Updates

```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/github</server_name>
<tool_name>push_files</tool_name>
<arguments>
{
  "owner": "arri-cc",
  "repo": "today-is-my-bday",
  "branch": "docs-update-[date]",
  "files": [
    {
      "path": "cline_docs/currentTask.md",
      "content": "[updated content]"
    },
    {
      "path": "cline_docs/projectRoadmap.md", 
      "content": "[updated content]"
    }
  ],
  "message": "docs: update project documentation\n\n- Updated currentTask.md with latest progress\n- Refreshed projectRoadmap.md status\n- Synchronized cross-references"
}
</arguments>
</use_mcp_tool>
```

### Create Pull Request

```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/github</server_name>
<tool_name>create_pull_request</tool_name>
<arguments>
{
  "owner": "arri-cc",
  "repo": "today-is-my-bday",
  "title": "docs: Update project documentation",
  "head": "docs-update-[date]",
  "base": "main",
  "body": "## Documentation Updates\n\n### Files Updated:\n- cline_docs/currentTask.md\n- cline_docs/projectRoadmap.md\n- cline_docs/[other files]\n\n### Changes Made:\n- [Description of changes]\n- [Rationale for updates]\n\n### Cross-References Validated:\n- [x] GitHub issue links\n- [x] Internal documentation links\n- [x] Status consistency\n\n## Review Notes\n\nThis PR ensures our documentation accurately reflects the current state of the project and maintains consistency across all files."
}
</arguments>
</use_mcp_tool>
```

## Documentation Maintenance Guidelines

### Update Frequency:

- **currentTask.md**: After each significant task completion
- **projectRoadmap.md**: Weekly or when major milestones change
- **techStack.md**: When architectural decisions are made
- **codebaseSummary.md**: When significant structural changes occur
- **historicalDecisionsAndCaveats.md**: Infrequently, only for major decisions

### Content Guidelines:

1. **Be Concise**: Focus on essential information
2. **Use Consistent Formatting**: Follow established patterns
3. **Maintain Cross-References**: Keep links and references current
4. **Date Important Changes**: Include timestamps for significant updates
5. **Avoid Duplication**: Reference other docs rather than repeating information

### Quality Checks:

- All GitHub issue references are valid and accessible
- Internal links between documentation files work correctly
- Status information is consistent across files
- Recent changes are reflected in appropriate documents
- Formatting follows established conventions

## Automation Opportunities

Consider creating additional workflows for:
- Automated link validation
- Documentation freshness checks
- Cross-reference synchronization
- Template compliance verification

## Integration with Other Workflows

This workflow complements:
- `/task-tracking.md` - Sync issue status with documentation
- `/github-issue.md` - Ensure new issues are reflected in docs
- `/architecture-decision.md` - Document ADR outcomes
