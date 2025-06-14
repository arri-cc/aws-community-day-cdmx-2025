# Commit Message Generation Workflow

This workflow generates standardized commit messages with GitHub issue association using conventional commit format.

## Step 1: Load Configuration and Context

```xml
<read_file>
<path>.clinerules/repo-config.json</path>
</read_file>
```

```xml
<read_file>
<path>cline_docs/currentTask.md</path>
</read_file>
```

## Step 2: Analyze Staged Changes

```xml
<execute_command>
<command>git status --porcelain</command>
<requires_approval>false</requires_approval>
</execute_command>
```

```xml
<execute_command>
<command>git diff --cached --name-only</command>
<requires_approval>false</requires_approval>
</execute_command>
```

## Step 3: Determine Commit Type and Scope

### Commit Type Mapping
Based on the current GitHub issue type from `currentTask.md`:

- **feat:** New features (from enhancement issues)
- **fix:** Bug fixes (from bug_report issues)
- **chore:** Maintenance tasks (from chore issues)
- **docs:** Documentation (from rfc issues)
- **style:** Code style changes
- **refactor:** Code refactoring
- **test:** Adding or updating tests

### Scope Detection
Analyze changed file paths to determine scope:

- Changes in `packages/mobile/` → scope: `mobile`
- Changes in `packages/functions/` → scope: `functions`
- Changes in `packages/shared/` → scope: `shared`
- Changes in `workflows/` → scope: `workflows`
- Changes in `.clinerules/` → scope: `config`
- Changes in root config files → scope: `config`
- Changes in documentation → scope: `docs`

## Step 4: Generate Commit Message

### Format
```
{type}({scope}): {description} (#{issue-number})

[optional body]

[optional footer]
```

### Examples
```
feat(mobile): add voice recording component (#52)
fix(functions): resolve auth token refresh issue (#53)
chore(workflows): refactor github operations to use MCP tools (#52)
docs(config): update milestone management workflow (#54)
```

## Step 5: Present Generated Message

Display the generated commit message and ask for confirmation or modifications.

## Step 6: Execute Commit (Optional)

```xml
<execute_command>
<command>git commit -m "{generated_message}"</command>
<requires_approval>true</requires_approval>
</execute_command>
```

## Guidelines

### Description Best Practices
- Use imperative mood ("add feature" not "added feature")
- Start with lowercase letter
- No period at the end
- Keep under 72 characters total
- Be specific but concise

### Multi-Change Commits
For commits affecting multiple scopes:
- Use the primary scope
- Mention other areas in the body
- Consider splitting into multiple commits if changes are unrelated

### Breaking Changes
- Add `!` after scope: `feat(mobile)!: redesign navigation structure`
- Include BREAKING CHANGE in footer
- Explain migration path in body

### Issue Association
- Always include issue number when working on tracked issues
- Use format: `(#{issue-number})`
- Ensure issue number matches current task

## Scope Detection Logic

```javascript
// Pseudocode for scope detection
function detectScope(changedFiles) {
  const scopeMap = {
    'packages/mobile/': 'mobile',
    'packages/functions/': 'functions', 
    'packages/shared/': 'shared',
    'workflows/': 'workflows',
    '.clinerules/': 'config',
    '.github/': 'config',
    'README.md': 'docs',
    'package.json': 'config'
  };
  
  // Find most common scope from changed files
  // Return primary scope or 'config' for mixed changes
}
```

## Usage Examples

### Feature Development
```
git add packages/mobile/components/VoiceRecorder.tsx
# Run workflow
# Generates: feat(mobile): add voice recording component (#52)
```

### Bug Fix
```
git add packages/functions/handlers/authHandler.js
# Run workflow  
# Generates: fix(functions): resolve token refresh issue (#53)
```

### Documentation Update
```
git add workflows/github-issue.md
# Run workflow
# Generates: docs(workflows): update issue creation process (#54)
```

### Configuration Change
```
git add .clinerules/repo-config.json
# Run workflow
# Generates: chore(config): add milestone management settings (#55)
