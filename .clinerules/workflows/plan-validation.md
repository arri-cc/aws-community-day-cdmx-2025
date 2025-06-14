# Plan Validation Workflow

## Purpose
Systematic validation workflow using sequential thinking to critically analyze implementation plans, identify gaps, verify feasibility, and provide precise feedback for plan improvement.

## When to Use
- **Before Implementation**: Validate plans created by `deep-research-planning.md` or other planning processes
- **Plan Review**: When existing plans need critical evaluation before proceeding
- **Risk Assessment**: When implementation plans require thorough risk analysis
- **Architecture Validation**: When plans involve significant architectural decisions

## Step 1: Plan Input and Context Setup

### 1.1: Load Plan to Validate
Identify the source of the plan:

**From currentTask.md**:
```xml
<read_file>
<path>cline_docs/currentTask.md</path>
</read_file>
```

**From GitHub Issue**:
```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/github</server_name>
<tool_name>get_issue</tool_name>
<arguments>
{
  "owner": "arri-cc",
  "repo": "today-is-my-bday",
  "issue_number": [issue_number]
}
</arguments>
</use_mcp_tool>
```

**From Direct Input**: 
User provides plan directly in request

### 1.2: Define Validation Criteria
Establish specific validation checkpoints:
- **Feasibility**: Can this be implemented with current technology stack?
- **Completeness**: Are all necessary steps and components included?
- **Integration**: Does this align with existing architecture patterns?
- **Risk Assessment**: What could go wrong and how severe would it be?
- **Performance Impact**: Will this affect app performance negatively?
- **Security Implications**: Does this introduce security vulnerabilities?

## Step 2: Codebase Context Verification

### 2.1: Validate Referenced Files
For each file mentioned in the plan:
```xml
<read_file>
<path>[file_path_from_plan]</path>
</read_file>
```

### 2.2: Check Integration Points
Verify claimed integration points exist:
```xml
<search_files>
<path>[relevant_directory]</path>
<regex>[pattern_to_verify_integration_point]</regex>
<file_pattern>*.ts|*.tsx|*.js|*.jsx</file_pattern>
</search_files>
```

### 2.3: Examine Dependencies
Review current dependencies that plan claims to use:
```xml
<read_file>
<path>packages/mobile/package.json</path>
</read_file>
```

## Step 3: Sequential Thinking Validation

### 3.1: Initialize Critical Analysis
```xml
<use_mcp_tool>
<server_name>github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking</server_name>
<tool_name>sequentialthinking</tool_name>
<arguments>
{
  "thought": "I need to systematically validate this implementation plan: [brief plan summary]. Let me start by checking if the claimed file locations and integration points actually exist in the codebase...",
  "nextThoughtNeeded": true,
  "thoughtNumber": 1,
  "totalThoughts": 10
}
</arguments>
</use_mcp_tool>
```

### 3.2: Systematic Validation Process
Continue sequential thinking through these validation dimensions:

**Thought 2-3: Technical Feasibility**
- Do the proposed technologies actually work together?
- Are the claimed capabilities accurate?
- Will the proposed approach work on both iOS and Android?

**Thought 4-5: Architecture Alignment**
- Does this follow existing code patterns?
- Will this create architectural debt or inconsistencies?
- Are there better approaches using existing infrastructure?

**Thought 6-7: Implementation Completeness**
- Are all necessary steps included?
- Are there missing error handling considerations?
- What about testing and validation steps?

**Thought 8-9: Risk and Performance Analysis**
- What are the failure scenarios and their impact?
- Will this affect app performance, battery, or memory usage?
- Are there security implications not addressed?

**Thought 10+: Final Assessment and Recommendations**
- Overall validation: PASS/FAIL/NEEDS_REVISION
- Specific issues that must be addressed
- Recommended improvements or alternatives

## Step 4: Generate Precise Validation Report

### 4.1: Structured Validation Output
```markdown
# Plan Validation Report

## Plan Summary
**Plan Title**: [Title of plan being validated]
**Plan Source**: [currentTask.md / GitHub Issue #X / Direct Input]
**Validation Date**: [Current date]
**Validator**: Cline Sequential Thinking Analysis

## Validation Status: [APPROVED / NEEDS_REVISION / REJECTED]

## Critical Findings

### ✅ PASSED Validations
- [Specific aspect] - [Why it passed with evidence]
- [Specific aspect] - [Why it passed with evidence]

### ⚠️ CONCERNS Identified
- [Specific concern] - [Severity: LOW/MEDIUM/HIGH] 
  - **Issue**: [Exact problem identified]
  - **Evidence**: [File/line/code that proves this]
  - **Impact**: [What could go wrong]
  - **Recommendation**: [Specific action to address]

### ❌ FAILED Validations
- [Critical failure] - [Severity: BLOCKING]
  - **Issue**: [Exact problem that prevents implementation]
  - **Evidence**: [Proof that this won't work]
  - **Required Fix**: [What must be changed before proceeding]

## Detailed Analysis

### Technical Feasibility Assessment
**Overall Feasibility**: [FEASIBLE / CHALLENGING / NOT_FEASIBLE]

**File Existence Verification**:
- ✅ `[file_path]` - Exists and contains expected functions
- ❌ `[file_path]` - Does not exist, plan assumption incorrect
- ⚠️ `[file_path]` - Exists but different from plan expectations

**Dependency Verification**:
- ✅ `[library@version]` - Available and compatible
- ❌ `[library@version]` - Not installed or incompatible version
- ⚠️ `[library@version]` - Available but may have performance implications

**Integration Point Verification**:
- ✅ `[function/component]` - Exists and has correct interface
- ❌ `[function/component]` - Does not exist or has different signature
- ⚠️ `[function/component]` - Exists but integration approach may cause issues

### Architecture Alignment Assessment
**Alignment Score**: [HIGH / MEDIUM / LOW]

**Pattern Consistency**:
- [Pattern claimed in plan] - [MATCHES / DIFFERS FROM] existing patterns in [specific files]
- [Integration approach] - [FOLLOWS / VIOLATES] established patterns in [component area]

**Architectural Impact**:
- **Positive**: [How this improves architecture]
- **Negative**: [How this creates tech debt or inconsistencies]
- **Neutral**: [Aspects that don't significantly impact architecture]

### Performance and Security Assessment
**Performance Impact**: [POSITIVE / NEUTRAL / NEGATIVE]
- Bundle size: [Estimated impact with reasoning]
- Runtime performance: [Expected effects on app responsiveness]
- Memory usage: [Impact on app memory footprint]
- Battery usage: [Effects on device battery consumption]

**Security Implications**: [SECURE / NEEDS_REVIEW / INSECURE]
- Data handling: [How plan handles sensitive data]
- Network communications: [Security of external calls]
- Storage: [Security of data persistence approach]

### Completeness Assessment
**Plan Completeness**: [COMPLETE / MOSTLY_COMPLETE / INCOMPLETE]

**Missing Elements**:
- [ ] Error handling for [specific scenarios]
- [ ] Testing strategy for [specific components]
- [ ] Migration/rollback procedures
- [ ] Performance monitoring considerations
- [ ] Security review requirements

**Implementation Gaps**:
- [Specific step missing from plan]
- [Integration detail not specified]
- [Configuration requirement not addressed]
```

## Step 5: Actionable Recommendations

### 5.1: Priority-Ordered Action Items
Based on validation results, provide specific actions:

**CRITICAL (Must Fix Before Implementation)**:
1. [Specific action with exact file/line references]
2. [Specific action with exact file/line references]

**HIGH (Should Fix Before Implementation)**:
1. [Specific improvement with exact changes needed]
2. [Specific improvement with exact changes needed]

**MEDIUM (Consider for Better Implementation)**:
1. [Optional enhancement with rationale]
2. [Optional enhancement with rationale]

### 5.2: Alternative Approaches (If Major Issues Found)
If validation reveals significant problems, suggest alternatives:

```markdown
## Alternative Approach Recommendation

**Why Current Plan Fails**: [Specific technical reasons]

**Recommended Alternative**:
1. [Step 1 with specific actions]
2. [Step 2 with specific actions]
3. [Step 3 with specific actions]

**Benefits of Alternative**:
- [Specific advantage with evidence]
- [Specific advantage with evidence]

**Implementation Difference**:
- Instead of modifying `[file]`, modify `[different_file]`
- Use `[different_approach]` rather than `[original_approach]`
```

## Step 6: Update Documentation and Tracking

### 6.1: Update Current Task Status
If plan needs revision:
```xml
<replace_in_file>
<path>cline_docs/currentTask.md</path>
<diff>
------- SEARCH
## Status: [current_status]
=======
## Status: Plan Validation Required

### Validation Results
- **Assessment**: [NEEDS_REVISION / REJECTED]
- **Critical Issues**: [Number] blocking issues identified
- **Action Required**: Address validation findings before implementation
- **Validation Report**: [Date] - See plan validation workflow output
+++++++ REPLACE
</diff>
</replace_in_file>
```

### 6.2: Create or Update GitHub Issue (If Applicable)
For significant validation findings:
```
.clinerules/workflows/github-issue.md
```

## Guidelines

### When to Use This Workflow
- **Pre-Implementation Review**: Before starting any complex implementation
- **Plan Quality Assurance**: When plans involve multiple components or integrations
- **Risk Management**: For plans with potential high impact or complexity
- **Team Review**: When plans need validation before team member implementation

### Validation Rigor Levels

**Level 1 - Basic Validation** (5-10 minutes):
- File existence checks
- Basic dependency verification
- High-level feasibility assessment

**Level 2 - Standard Validation** (15-20 minutes):
- Full technical feasibility analysis
- Architecture alignment review
- Integration point verification
- Basic risk assessment

**Level 3 - Comprehensive Validation** (30+ minutes):
- Detailed sequential thinking analysis
- Performance and security implications
- Alternative approach evaluation
- Complete implementation gap analysis

### Precision Requirements

**Evidence-Based Assessment**:
- All validation claims must reference specific files/lines/code
- Use exact error messages or code snippets as evidence
- Provide file paths that can be verified

**Actionable Feedback**:
- Every issue must include specific remediation steps
- Recommendations must include exact code or configuration changes
- Alternative approaches must be implementable

**Measurable Outcomes**:
- Clear PASS/FAIL/NEEDS_REVISION decision
- Numbered priority levels for action items
- Specific criteria for re-validation

## Integration Guidelines

### Workflow Triggers
- **Follows**: `deep-research-planning.md` output validation
- **May Follow**: Manual plan review requests
- **May Trigger**: `github-issue.md` for critical findings
- **Updates**: `currentTask.md` with validation results

### Cross-Reference Validation
When validating plans, verify consistency with:
- `cline_docs/techStack.md` - Technology choices
- `cline_docs/codebaseSummary.md` - Current architecture
- `cline_docs/historicalDecisionsAndCaveats.md` - Past decisions that may affect current plan

## Example Validation Scenarios

### Scenario 1: Speech Feature Implementation Plan
**Validation Focus**: 
- Verify audio permissions handling
- Check React Native audio library compatibility
- Validate integration with existing RecordingManager
- Assess performance impact on mobile device

### Scenario 2: Firebase Data Model Changes
**Validation Focus**:
- Verify Firestore security rules compatibility
- Check existing data migration requirements
- Validate query performance implications
- Assess backward compatibility with existing data

### Scenario 3: UI Component Refactoring Plan
**Validation Focus**:
- Verify component usage throughout app
- Check styling consistency with design system
- Validate accessibility requirements
- Assess testing coverage for changes
