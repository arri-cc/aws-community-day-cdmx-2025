# Research Validation Workflow

## Purpose
Extended research workflow using Perplexity to validate architectural approaches, investigate best practices, and gather external insights during planning phases.

## When to Use
- **Planning Phase**: When evaluating complex architectural decisions
- **Technology Evaluation**: Comparing implementation approaches or frameworks
- **Best Practices Research**: Investigating industry standards for specific patterns
- **Problem Validation**: Confirming that proposed solutions align with current practices
- **Uncertainty Resolution**: When internal knowledge needs external validation

## Step 1: Define Research Questions
Before using Perplexity, clearly define:
- **Primary Question**: What specific decision needs validation?
- **Context**: What is the current project constraint or requirement?
- **Scope**: What aspects need research (performance, security, maintainability, etc.)?
- **Decision Criteria**: What factors will influence the final choice?

## Step 2: Conduct Perplexity Research
Use the Perplexity MCP tool for targeted research:

```
use_mcp_tool: perplexity_ask
server_name: perplexity-ask
tool_name: perplexity_ask
arguments: {
  "messages": [
    {
      "role": "user", 
      "content": "[Structured research question with context]"
    }
  ]
}
```

**Research Question Templates:**

### Technology Comparison
```
"I'm building a React Native app with [specific requirements]. I'm considering [Option A] vs [Option B] for [specific use case]. What are the current best practices, performance implications, and maintenance considerations for each approach in 2024/2025?"
```

### Architecture Pattern Validation
```
"For a [project type] with [specific constraints], I'm planning to use [architectural pattern]. What are the current best practices, common pitfalls, and recommended implementations for this pattern? Are there better alternatives I should consider?"
```

### Implementation Approach
```
"I need to implement [specific feature] in [technology stack]. What are the most reliable, performant, and maintainable approaches currently recommended? What libraries or patterns should I consider or avoid?"
```

## Step 3: Analyze Research Results
Evaluate Perplexity responses for:
- **Relevance**: Does this apply to our specific use case?
- **Currency**: Are the recommendations current (2024/2025)?
- **Authority**: Are sources reputable and technical?
- **Practical Application**: Can this be implemented given our constraints?
- **Risk Assessment**: What are potential downsides or limitations?

## Step 4: Integrate Findings into Planning
Document research findings in planning discussion:

### Research Summary Template
```markdown
## Research Validation

**Question Investigated:** [Primary research question]

**Key Findings:**
- [Finding 1 with implications]
- [Finding 2 with implications]
- [Finding 3 with implications]

**Validated Approach:** [Final recommended approach]

**Trade-offs Confirmed:**
- **Benefits:** [List validated benefits]
- **Limitations:** [List confirmed limitations]
- **Alternatives Considered:** [Brief notes on other options]

**Implementation Confidence:** [High/Medium/Low] based on research validation
```

## Step 5: Update Architectural Assessment
Incorporate research findings into the Planning Mode Assessment Framework response structure:
- **Architectural Assessment**: Include research-backed evaluation
- **Technical Implementation Guidance**: Reference validated best practices
- **Key Tradeoffs**: Include research-informed tradeoffs

## Guidelines

### When to Use Perplexity Research
- **Complex Decisions**: When choosing between multiple technical approaches
- **Unknown Territory**: Working with technologies or patterns outside usual expertise
- **Validation Needed**: When internal assessment needs external confirmation
- **Best Practices**: When industry standards might have evolved

### When NOT to Use
- **Simple Decisions**: Basic implementation questions with obvious answers
- **Time-Sensitive**: When rapid iteration is more valuable than perfect research
- **Well-Established Patterns**: For common patterns already documented in project

### Research Quality Guidelines
- **Specific Questions**: Ask targeted questions rather than broad "what should I do?"
- **Context Rich**: Include relevant project constraints and requirements
- **Multiple Angles**: Consider performance, security, maintainability, etc.
- **Source Evaluation**: Critically assess the authority and currency of findings

## Integration
- **Triggered by**: Complex decisions in Plan Mode
- **Links to**: `plan-mode-start.md`, `architecture-decision.md`
- **Feeds into**: Planning discussions, GitHub issue creation
- **Documentation**: Research findings should be captured in architectural decisions

## Example Usage Scenarios

### 1. Speech Recognition Library Selection
```
Research Question: "For a React Native Expo app requiring offline speech-to-text with high accuracy, what are the best library options in 2024? I need to compare performance, bundle size, offline capabilities, and iOS/Android support for libraries like react-native-voice, @react-native-voice/voice, and alternatives."
```

### 2. State Management Pattern
```
Research Question: "For a conversational AI mobile app with complex state (audio states, conversation history, user preferences), should I use Redux Toolkit, Zustand, React Context, or another pattern? What are the current recommendations for React Native apps with real-time audio and persistent storage requirements?"
```

### 3. Firebase Security Patterns
```
Research Question: "What are the current best practices for Firestore security rules for a mental health app storing personal conversations? I need to ensure user data isolation while supporting features like conversation history and weekly planning data."
