# Deep Research & Planning Workflow

## Purpose
Comprehensive research and planning workflow that combines codebase analysis, external research, and sequential thinking to create precise implementation plans with specific actions and code locations.

## When to Use
- **Complex Implementation Tasks**: When building new features requiring integration with existing codebase
- **Architecture Integration**: When new components must align with existing patterns and structures
- **Technology Selection**: When choosing between implementation approaches with codebase constraints
- **Refactoring Plans**: When modifying existing code requires understanding current patterns

## Step 1: Define Research Scope

Before beginning, clearly establish:
- **Task Objective**: Specific feature, fix, or improvement to implement
- **Success Criteria**: Measurable outcomes that define completion
- **Constraints**: Performance, compatibility, or architectural limitations
- **Integration Points**: Which existing components will be affected

## Step 2: Codebase Analysis Phase

### 2.1: Identify Relevant Components
```xml
<list_code_definition_names>
<path>[relevant directory path]</path>
</list_code_definition_names>
```

### 2.2: Examine Key Files
For each relevant component identified:
```xml
<read_file>
<path>[specific file path]</path>
</read_file>
```

### 2.3: Search for Existing Patterns
```xml
<search_files>
<path>[directory to search]</path>
<regex>[pattern to find similar implementations]</regex>
<file_pattern>[file type filter]</file_pattern>
</search_files>
```

### 2.4: Document Current State
Create precise inventory of:
- **Existing Functions**: Name, location, parameters, return types
- **Current Patterns**: How similar functionality is implemented
- **Dependencies**: What libraries/services are already in use
- **Integration Points**: Specific places where new code will connect

## Step 3: External Research Phase

### 3.1: Industry Best Practices Research
```xml
<use_mcp_tool>
<server_name>perplexity-ask</server_name>
<tool_name>perplexity_ask</tool_name>
<arguments>
{
  "messages": [
    {
      "role": "user",
      "content": "[Specific question about implementation approach with technology stack context: React Native, Expo, Firebase, TypeScript]"
    }
  ]
}
</arguments>
</use_mcp_tool>
```

### 3.2: Technology-Specific Research
Focus research on:
- **Library Compatibility**: Specific versions compatible with existing stack
- **Implementation Patterns**: Proven approaches for the technology stack
- **Performance Considerations**: Specific optimizations for mobile/React Native
- **Security Implications**: Best practices for the specific use case

## Step 4: Sequential Thinking Synthesis

### 4.1: Process Combined Information
```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking</server_name>
<tool_name>sequentialthinking</tool_name>
<arguments>
{
  "thought": "Based on codebase analysis showing [specific findings] and research indicating [specific best practices], I need to devise a precise implementation plan for [task objective]. Let me start by analyzing the integration points...",
  "nextThoughtNeeded": true,
  "thoughtNumber": 1,
  "totalThoughts": 8
}
</arguments>
</use_mcp_tool>
```

### 4.2: Continue Sequential Analysis
Process through systematic thinking covering:
- **Integration Strategy**: How new code connects to existing systems
- **Implementation Sequence**: Order of file modifications and new file creation
- **Risk Assessment**: Potential conflicts or breaking changes
- **Testing Strategy**: How to validate each implementation step
- **Performance Impact**: Expected effects on app performance
- **Rollback Plan**: How to reverse changes if needed

## Step 5: Generate Precise Implementation Plan

### 5.1: Structured Plan Template
```markdown
# Implementation Plan: [Task Title]

## Summary
**Objective**: [Specific goal with measurable outcome]
**Estimated Effort**: [Time/complexity assessment]
**Risk Level**: [Low/Medium/High with specific risks]

## Prerequisites
- [ ] [Specific dependencies or setup requirements]
- [ ] [Required permissions or access]
- [ ] [Environment configuration needs]

## Implementation Steps

### Step 1: [Specific Action]
**Files to Modify**: 
- `[exact file path]` - [specific changes needed]
- `[exact file path]` - [specific changes needed]

**New Files to Create**:
- `[exact file path]` - [purpose and key components]

**Code Changes**:
```typescript
// In [file path] at line [number]
// Replace:
[existing code]
// With:
[new code]
```

**Validation**: [How to verify this step works]

### Step 2: [Next Specific Action]
[Same detailed format as Step 1]

## Integration Points
- **Function Calls**: [Existing functions that will call new code]
- **Data Flow**: [How data moves through the system]
- **State Management**: [Impact on existing state patterns]
- **Event Handling**: [New events or event modifications]

## Testing Plan
- [ ] [Unit tests for new functions]
- [ ] [Integration tests for modified workflows]
- [ ] [Manual testing steps with expected outcomes]

## Performance Considerations
- **Bundle Size Impact**: [Estimated size increase]
- **Runtime Performance**: [Expected performance effects]
- **Memory Usage**: [Impact on memory consumption]

## Rollback Procedure
1. [Specific steps to reverse changes]
2. [Files to restore]
3. [Configuration to reset]
```

## Step 6: Validation and Refinement

### 6.1: Plan Validation Checklist
- [ ] **Completeness**: All necessary files and functions identified
- [ ] **Precision**: Exact line numbers and code changes specified
- [ ] **Integration**: All connection points to existing code documented
- [ ] **Testing**: Clear validation steps for each implementation phase
- [ ] **Risk Management**: Potential issues identified with mitigation strategies

### 6.2: GitHub Issue Creation (Optional)
If this represents a new work stream:
```
.clinerules/workflows/github-issue.md
```

## Output Format

### Research Summary
```markdown
## Codebase Analysis Results
**Relevant Files Examined**: [Count] files in [directories]
**Existing Patterns Found**: 
- [Pattern 1]: Implemented in [files] using [approach]
- [Pattern 2]: Implemented in [files] using [approach]

**Integration Points Identified**:
- [Component 1]: [Specific integration method]
- [Component 2]: [Specific integration method]

## External Research Findings
**Key Technologies Validated**:
- [Library/Tool]: Version [X.Y.Z] - [Specific capability confirmed]
- [Pattern/Approach]: [Specific implementation method confirmed]

**Best Practices Confirmed**:
- [Practice 1]: [How it applies to our codebase]
- [Practice 2]: [How it applies to our codebase]

## Implementation Confidence
**Overall Assessment**: [High/Medium/Low]
**Key Risks**: [Specific technical risks with mitigation plans]
**Recommended Approach**: [Chosen implementation strategy with justification]
```

## Guidelines

### When to Use This Workflow
- **Feature Development**: New user-facing functionality
- **System Integration**: Adding third-party services or libraries
- **Architecture Changes**: Modifications affecting multiple components
- **Performance Optimization**: Changes requiring understanding of current implementation

### Precision Requirements
- **File Paths**: Must be exact and verified to exist
- **Function Names**: Must match existing codebase exactly
- **Line Numbers**: Should be approximate but useful for locating code
- **Code Examples**: Must be syntactically correct and runnable

### Integration Guidelines
- **Follows**: `plan-mode-start.md` for complex tasks
- **May Trigger**: `github-issue.md` for tracking
- **Feeds Into**: `architecture-decision.md` for major decisions
- **Updates**: `currentTask.md` with implementation plan

### Quality Assurance
- **Verify All Paths**: Ensure all referenced files exist
- **Check Syntax**: All code examples must be valid
- **Validate Integration**: Confirm all connection points are correct
- **Test Assumptions**: Verify research findings apply to current codebase

## Example Usage Scenarios

### Scenario 1: Adding Speech-to-Text Feature
1. **Codebase Analysis**: Examine existing audio components, RecordingManager, recognition patterns
2. **Research**: Find React Native speech libraries compatible with Expo
3. **Sequential Thinking**: Plan integration with existing audio architecture
4. **Output**: Precise plan showing exact modifications to RecordingManager.ts and new files needed

### Scenario 2: Implementing User Preferences Storage
1. **Codebase Analysis**: Review current Firebase usage, user data patterns, storage services
2. **Research**: Firestore best practices for user preferences, security rules patterns
3. **Sequential Thinking**: Design data model and integration with existing user management
4. **Output**: Exact Firestore schema, specific functions to modify, new service files to create

### Scenario 3: Performance Optimization
1. **Codebase Analysis**: Identify performance bottlenecks in current implementation
2. **Research**: React Native optimization techniques, profiling tools, best practices
3. **Sequential Thinking**: Plan optimization strategy with minimal breaking changes
4. **Output**: Specific code changes with before/after performance expectations
