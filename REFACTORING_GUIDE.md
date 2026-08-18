# Refactoring Guide for Agent and Prompt Files

## Target Structure

All agent and prompt files must follow this 4-section architecture:

### 1. Role & Directive
- Identity statement (who you are)
- Primary objective
- Delegation rule (if orchestrator)
- Tools list (for .agent.md files)

### 2. Workflow / Steps to Follow
- Use "Steps to Follow" with numbered list when order matters
- Use "Workflow" with unordered list when no strict order
- Merge procedural items from old "What to do" and "Reasoning Constraints"
- Each step should be action-oriented and concise

### 3. Constraints
Multiple subsections allowed:
- Scope & Boundaries (what can/cannot do)
- Code Standards (quality requirements)
- Subagent Usage (delegation rules)
- Context Boundaries (available resources)
- Other domain-specific constraints

Merge content from:
- Old "What not to do" (converted to positive boundaries)
- Non-procedural items from "Reasoning Constraints"
- Quality checks from "Quality Bar"

### 4. Failure & Clarification Protocol
- When to ask for clarification
- How to handle errors
- What to do when blocked
- Merge from old "Failure Behaviour"

## Conversion Rules

### From "What to do" → Workflow/Steps
- Extract procedural tasks
- Make action-oriented
- Remove redundancy
- Add to numbered/unordered list

### From "What not to do" → Constraints
- Convert negative to authoritative boundary
- "Do not X" becomes "X is prohibited" or "Scope excludes X"
- Group related constraints together

### From "Reasoning Constraints" → Split
- Procedural (analyse → plan → implement) → Workflow
- Invariants (always verify, never guess) → Constraints

### From "Quality Bar" → Split
- Verification checks → add to verification step in Workflow
- Quality standards → Constraints > Code Standards

## Token Efficiency Rules

Remove unnecessary words:
- "the" unless grammatically required
- Full stops at end of bullet points
- Filler words ("basically", "essentially", "obviously")
- Redundant phrases ("it is important to note that")

Keep concise:
- One idea per bullet
- Short sentences
- Direct language

## Formatting Rules

NO rich text:
- Avoid `**bold**` and `*italic*`
- Use CAPS SPARINGLY for emphasis
- Use section headers for hierarchy

Lists:
- Numbered when order matters
- Unordered when parallel/independent
- Consistent bullet style

## Example Transformation

OLD:
```markdown
# What to do
- Analyse the codebase carefully
- Plan your approach before coding
- Write simple, maintainable code
- Test your implementation

# What not to do  
- Do not overcomplicate the solution
- Do not write code without planning first

# Reasoning Constraints
- Think step-by-step before writing code
- Verify your code meets requirements

# Quality Bar
- Code must be maintainable
- No unnecessary complexity
```

NEW:
```markdown
# Role & Directive
You are a coding agent implementing features with simplicity and maintainability as primary goals

# Steps to Follow
1. Analyse relevant codebase sections
2. Plan approach and outline steps
3. Implement solution
4. Test implementation
5. Verify code meets requirements and quality standards

# Constraints

## Scope
- Solution complexity must be proportional to problem
- Planning precedes implementation

## Code Standards  
- Maintainability required
- Unnecessary complexity prohibited

# Failure & Clarification Protocol
- If requirements unclear, request clarification before proceeding
- If blocked, state specific issue and await guidance
```
