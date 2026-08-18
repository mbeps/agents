# Refactoring Template for Agent Instructions

This template standardizes agent instruction documents using a 4-section architecture optimized for token efficiency and clarity.

---

## Template Structure

### 1. Role & Directive

Define agent identity and core delegation rule

```markdown
# [Agent Name/Purpose]

You are the [role description]. Your responsibility is to [primary function].

[Core delegation principle - what work must/must not be done directly]
```

Example:
```markdown
# Introduction

You are the orchestrating agent. Your sole responsibility is to delegate all work to subagents and synthesize their outputs. You never read files, write code, or perform analysis yourself. ALL work is done via subagents.
```

---

### 2. Workflow / Steps to Follow

Ordered execution lifecycle - use numbered lists when sequence matters, unordered for flexible workflows

```markdown
# Workflow

1. [First required step]
2. [Second required step]
3. [Third required step]
   - Sub-step if needed
   - Another sub-step

OR for flexible workflows:

# Steps to Follow

- [Action item with context]
- [Another action with context]
- [Conditional action: "When X, do Y"]
```

Example mandatory workflow:
```markdown
# Workflow

1. User Request
2. Load required skills: `skill-name-1` and `skill-name-2`
3. Spawn SUBAGENT #1: Research & Spec
   - Read Graphify index at ./graphify/ if available
   - Analyze relevant parts of codebase
   - Create spec document in ./subagents/
   - Return summary
4. Receive results, spawn next subagent
5. Spawn SUBAGENT #2: Implementation
   - Receive spec file path
   - Implement based on spec
   - Return completion summary
```

---

### 3. Constraints

Scope boundaries, code standards, execution rules - can have multiple subsections

#### 3.1 Core Constraints

```markdown
# Constraints

- NEVER [forbidden action] — [alternative approach]
- Do NOT [anti-pattern] — [correct pattern]
- [Boundary rule with rationale]
- [Code standard or quality requirement]
```

#### 3.2 Subagent Usage (if applicable)

```markdown
## Subagent Usage

Tool API:
```
runSubagent(
  description: "3-5 word summary",  // REQUIRED
  prompt: "Detailed instructions"   // REQUIRED
)
```

NEVER include `agentName` — always use default subagent

Error reference:
- "disabled by user" — remove `agentName` from call
- "missing required property" — include BOTH description and prompt

Prompt templates:

Research subagent:
```
Research [topic]. Analyze relevant files in codebase.
Create spec document at: docs/SubAgent docs/[NAME].md
Return: summary of findings and spec file path
```

Implementation subagent:
```
Read spec at: docs/SubAgent docs/[NAME].md
Implement according to spec
Return: summary of changes made
```
```

#### 3.3 Context Boundaries (if applicable)

```markdown
## Context Boundaries

- All research outputs must be written to docs/SubAgent docs/ as spec documents
- Subagents receive context via explicit instructions in prompt parameter, not via shared state
- Each subagent operates in fresh context; pass all required information explicitly
- Main agent compiles final outputs from subagent return values only — does not inspect files directly
- Main agent can read orchestration skill, but subagents cannot read it or call runSubagent
```

---

### 4. Failure & Clarification Protocol

Error handling and ambiguity resolution

```markdown
# Failure Behavior

If [tool/action] returns error:
- "[error message]" — [resolution approach]
- "[another error]" — [resolution approach]

If [condition produces incorrect output]:
- [Recovery action with rationale]
- Do NOT [anti-pattern during recovery]

# Clarification Protocol

When requirements are ambiguous:
1. [First clarification step]
2. [How to proceed after clarification]
```

Example:
```markdown
# Failure Behavior

If runSubagent returns error:
- "disabled by user" — you likely included agentName. Remove it and retry
- "missing required property" — ensure both description and prompt are provided

If subagent produces incorrect or incomplete output, spawn new evaluation subagent to identify issue and corrective subagent to fix it. Do not attempt to fix yourself

# Clarification Protocol

When requirements are ambiguous:
1. Ask user for clarification with specific questions
2. Delegate with clarified context once received
```

---

## Migration Guide: Old Format → New Format

### Consolidation Rules

| Old Section                          | New Location                 |
| ------------------------------------ | ---------------------------- |
| "What to do" (procedural tasks)      | → Workflow / Steps to Follow |
| "What not to do"                     | → Constraints (renamed)      |
| "Reasoning Constraints" (procedural) | → Workflow steps             |
| "Reasoning Constraints" (invariants) | → Constraints                |
| "Quality Bar" (verification)         | → Workflow verification step |
| "Quality Bar" (standards)            | → Constraints                |
| "Context Boundaries"                 | → Constraints subsection     |
| "Subagent Usage"                     | → Constraints subsection     |

### Example: Before

```markdown
# What To Do
- Receive user request and decompose into discrete tasks
- Spawn subagents for every task: research, analysis, planning

# What NOT To Do
- NEVER read files yourself — spawn subagent to do it
- Do NOT perform "quick look" at file before delegating

# Reasoning Constraints
- Decompose every request into smallest independently executable tasks
- Assign single responsibility to each subagent
- Follow phase order: Analysis → Implementation → Evaluation

# Quality Bar
- Subagent prompts must be explicit, self-contained, unambiguous
- Each prompt must state: what to do, which files to use, what to return
- Keep orchestration messages concise
```

### Example: After

```markdown
# Role & Directive

You are the orchestrating agent. Your sole responsibility is to delegate all work to subagents and synthesize their outputs. You never read files, write code, or perform analysis yourself.

# Workflow

1. Receive user request and decompose into discrete tasks
2. Spawn subagents for every task: research, analysis, planning
3. Follow phase order: Analysis → Implementation → Evaluation

# Constraints

- NEVER read files yourself — spawn subagent to do it
- Do NOT perform "quick look" at file before delegating — delegate immediately
- Assign single responsibility to each subagent — do not combine research and writing
- Subagent prompts must be explicit, self-contained, unambiguous
- Each prompt must state: what to do, which files to use, what to return
- Decompose every request into smallest independently executable tasks before spawning subagents
- Keep orchestration messages concise

# Failure Behavior

[Error handling details]
```

---

## Token Efficiency Rules

### Text Optimization

Remove unnecessary articles:
- ❌ "The agent should read the file"
- ✅ "Agent should read file" or "Read file"

No full stops at end of list items:
- ❌ "Spawn subagent for research."
- ✅ "Spawn subagent for research"

Exception: Keep full stops when item contains multiple sentences for readability

### Consolidation

Remove repetitive information:
- If "never read files" appears in both Constraints and examples, keep only in Constraints
- If same rule expressed differently in multiple places, consolidate into single clear statement

Merge related constraints:
- ❌ "Do not read files. Do not edit files. Do not analyze files."
- ✅ "Do not read, edit, or analyze files — delegate to subagents"

### List Types

Numbered lists (order matters):
```markdown
1. First mandatory step
2. Second mandatory step
3. Third mandatory step
```

Unordered lists (flexible/parallel actions):
```markdown
- Action that can happen anytime
- Another flexible action
- Conditional action
```

---

## Formatting Rules

### Rich Text

Avoid bold (`**text**`) and italic (`*text*`) for emphasis
- Use CAPS for strong emphasis: NEVER, MUST, ALWAYS
- Use code formatting for technical terms: `runSubagent`, `agentName`
- Use quotes for error messages: "disabled by user"

### Code Blocks

Use fenced code blocks with language hints:
```markdown
Tool signature:
```typescript
runSubagent(description: string, prompt: string)
```

Template example:
```plaintext
Research [topic]. Analyze files.
Return: summary and file path
```
```

### Section Hierarchy

```
# Primary Section (Role & Directive, Workflow, Constraints, Failure)
## Subsection (Subagent Usage, Context Boundaries)
### Sub-subsection (only if necessary)
```

Avoid deep nesting - keep hierarchy flat for scanability

---

## Validation Checklist

Before finalizing refactored document:

- [ ] All 4 sections present: Role & Directive, Workflow, Constraints, Failure & Clarification
- [ ] No "What to do" or "What not to do" headers remain
- [ ] Procedural content in Workflow, invariants in Constraints
- [ ] Token optimization applied (removed "the", no trailing periods in lists)
- [ ] Rich text formatting minimized (CAPS instead of bold/italic)
- [ ] Numbered lists only where order matters
- [ ] No information loss during consolidation
- [ ] Subagent Usage and Context Boundaries under Constraints (if applicable)
- [ ] Error handling in Failure section
- [ ] Examples use code blocks with language hints

---

## Template Summary

**Optimized 4-section architecture:**

1. **Role & Directive** — Who you are, what you delegate
2. **Workflow** — Ordered execution steps
3. **Constraints** — Boundaries, standards, technical rules (with subsections)
4. **Failure & Clarification** — Error handling and ambiguity resolution

**Key principles:**
- Token efficient (no bloat, no unnecessary articles)
- Clear hierarchy (3 levels max)
- Minimal rich text formatting
- Preserve all information during consolidation
- Subsections live under Constraints when contextual

---

END OF TEMPLATE
