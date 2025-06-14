# Milestone Management Workflow

This workflow manages milestone synchronization between GitHub and local configuration using GitHub CLI for complete and accurate milestone discovery.

## Step 1: Load Repository Configuration

```xml
<read_file>
<path>.clinerules/repo-config.json</path>
</read_file>
```

## Step 2: Fetch Complete GitHub Milestones

Use GitHub CLI to get all milestones directly from the GitHub API:

```xml
<execute_command>
<command>gh api repos/arri-cc/today-is-my-bday/milestones --jq '.[] | {number, title, description}'</command>
<requires_approval>false</requires_approval>
</execute_command>
```

## Step 3: Parse and Analyze Milestone Data

Review the complete milestone data from GitHub and compare against the local configuration to identify:
- Missing milestones in local config
- Outdated milestone information
- Milestone ID mismatches
- Description updates

## Step 4: Update Local Configuration

If discrepancies are found, update the local `.clinerules/repo-config.json` file with complete GitHub milestone data:

```xml
<replace_in_file>
<path>.clinerules/repo-config.json</path>
<diff>
<<<<<<< SEARCH
  "milestones": [
    {
      "id": 1,
      "title": "Phase 1: Core Architecture",
      "description": "Foundation and core functionality"
    },
    {
      "id": 2, 
      "title": "Phase 2: Enhanced Features",
      "description": "Advanced functionality and UX improvements"
    },
    {
      "id": 3,
      "title": "Phase 3: Production Ready", 
      "description": "Performance, security, and deployment"
    }
  ],
=======
  "milestones": [
    [Complete GitHub milestone data from API response]
  ],
>>>>>>> REPLACE
</diff>
</replace_in_file>
```

## Step 5: Present Updated Milestone Options

Display the synchronized milestone list that will be available for issue creation workflows.

## Benefits of GitHub CLI Approach

- **Complete Discovery**: Gets all milestones, not just those with assigned issues
- **Direct API Access**: Bypasses MCP tool limitations that only show partial data
- **Structured Data**: Proper JSON parsing for reliable integration
- **Accurate Synchronization**: Local config stays current with GitHub reality
- **Reliable Foundation**: Ensures issue creation workflows have correct milestone options

## Usage Guidelines

- Use this workflow when milestone information seems outdated
- Run before major issue creation campaigns to ensure accurate milestone options
- Execute after GitHub milestones are added, removed, or modified
- Maintain milestone IDs consistently between GitHub and local config
- Assumes GitHub CLI (`gh`) is installed and authenticated

## Error Handling

If the GitHub CLI command fails:
- Check GitHub CLI authentication: `gh auth status`
- Verify repository access permissions
- Ensure network connectivity to GitHub
- Fall back to manual milestone configuration if needed

## Expected Output Format

The GitHub CLI command returns milestone data in this format:
```json
{
  "number": 1,
  "title": "User Onboarding Conversation Flow",
  "description": "Implement a structured onboarding flow to capture user preferences, goals, and tone"
}
{
  "number": 2,
  "title": "Voice Interaction & Feedback Experience", 
  "description": "Design and implement a cohesive, intuitive audio and interaction experience"
}
```

This data is then used to update the local configuration for consistent milestone references across all workflows.
