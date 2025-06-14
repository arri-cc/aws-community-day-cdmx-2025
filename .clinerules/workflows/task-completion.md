# Task Completion Workflow

## Purpose
Mandatory workflow triggered after human confirmation of completed work to ensure systematic documentation updates and knowledge capture.

## When to Use
- **MANDATORY**: After human confirms "this is done and working"
- Following successful implementation of features
- After architectural changes are completed and tested
- When major decisions have been implemented

## Step 1: Update Current Task Documentation
Update `cline_docs/currentTask.md`:

```
use_mcp_tool: replace_in_file or write_to_file
```

**Required Updates:**
- Mark completed objectives with [x]
- Document what was actually implemented
- Note any deviations from original plan
- Update next steps section
- Add reference to related GitHub issues

## Step 2: Update Historical Decisions (If Applicable)
For major architectural decisions, update `cline_docs/historicalDecisionsAndCaveats.md`:

```
use_mcp_tool: replace_in_file
```

**When to Update:**
- New architectural patterns introduced
- Important technical decisions made
- Significant caveats or limitations discovered
- Major dependency changes
- Critical bug fixes with broader implications

**What to Document:**
- Decision rationale
- Alternatives considered
- Implementation approach chosen
- Key caveats for future work

## Step 3: Update Codebase Summary (If Applicable)
For structural changes, update `cline_docs/codebaseSummary.md`:

```
use_mcp_tool: replace_in_file
```

**When to Update:**
- New components or modules added
- Data flow changes
- External dependencies modified
- Integration points changed

## Step 4: Cross-Reference GitHub Issues
Update related GitHub issues with completion status:

```
use_mcp_tool: use_mcp_tool
server_name: github.com/modelcontextprotocol/servers/tree/main/src/github
tool_name: add_issue_comment
```

**Required Actions:**
- Add completion comment to related issues
- Reference commit hashes if applicable
- Close issues if fully resolved
- Update issue status/labels

## Step 5: Trigger Documentation Sync (If Needed)
For major changes affecting multiple docs:

```
.clinerules/workflows/documentation-sync.md
```

## Guidelines
- **Non-Optional**: This workflow must be completed after human confirmation
- **Scope**: Only update documents for significant changes, not minor tasks
- **Cross-References**: Maintain links between GitHub issues and documentation
- **Historical Value**: Focus on decisions that will matter for future development

## Integration
- Triggered by: Human confirmation of completed work
- Links to: `documentation-sync.md`, GitHub issues
- Updates: `currentTask.md`, `historicalDecisionsAndCaveats.md`, `codebaseSummary.md`

## Template Comments for GitHub Issues
```
✅ **Work Completed**
- [Brief description of what was implemented]
- Commit: [hash if applicable]
- Documentation updated: [list files updated]
- Testing status: [confirmed working by human]

**Key Decisions Made:**
- [List any architectural or technical decisions]

**Next Steps:**
- [Reference follow-up issues or next tasks]
