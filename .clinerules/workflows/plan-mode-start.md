# Plan Mode Start Workflow

## Purpose
Mandatory workflow for beginning any substantial task in Plan Mode to ensure consistent architecture planning and proper assessment.

## When to Use
- **MANDATORY**: Start of any substantial task in Plan Mode
- Before architectural decisions
- When evaluating implementation approaches
- Beginning feature development planning

## Step 1: Essential Documentation Review
Read essential documents in prescribed order:

```
use_mcp_tool: read_file
- projectRoadmap.md
- currentTask.md  
- techStack.md
- codebaseSummary.md
- historicalDecisionsAndCaveats.md
- coreRequirements.md (if relevant)
```

## Step 2: Apply Planning Mode Assessment Framework
Use the structured assessment approach from Architect Role Guidelines:

### Technical Architecture Assessment
Evaluate against these domains:
- React Native/Expo Architecture considerations
- Firebase Integration patterns
- Speech Technology Integration requirements
- Conversational AI Design needs
- Data Extraction & Flow Control requirements
- Mobile-Specific Constraints

### Response Structure Requirements
Include in planning response:
1. **Architectural Assessment** - Evaluation against best practices
2. **Technical Implementation Guidance** - Code structure recommendations
3. **Conversation Design Patterns** - AI prompt considerations (if applicable)
4. **Data Modeling Considerations** - Database schema recommendations
5. **User Experience Continuity** - Network state handling
6. **Key Tradeoffs** - Explicit benefits and costs

## Step 3: Create GitHub Issue for Tracking
If this is a new work stream, use:
```
.clinerules/workflows/github-issue.md
```

## Step 4: Validate Approach (Optional)
For complex decisions, consider:
```
.clinerules/workflows/research-validation.md
```

## Guidelines
- **Non-Optional**: This workflow must be completed before proceeding with substantial planning
- **Token Efficiency**: Read only documents that have changed since last context
- **Documentation**: Decisions should be trackable through GitHub issues
- **Mode Adherence**: Stay in Architect role throughout planning

## Integration
- Links to: `github-issue.md`, `research-validation.md`, `task-tracking.md`
- Followed by: Planning discussion, then transition to Act Mode
- Updates: None (this is a read-only assessment workflow)
