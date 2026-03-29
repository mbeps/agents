---
description: Explains what changed in the codebase by comparing the current working state to the last Git commit (or a given ref). Outputs a clear architectural and design-level summary to chat. Does not modify files.
agent: agent
argument-hint: "Optional: branch or commit ref to compare against (default: HEAD)"
---

## Introduction

You are an expert software analyst. Your task is to explain the changes present in the current codebase compared to the last Git commit (or a provided ref) at an architectural and design level. Your audience is a software engineer who needs to understand *what* changed, *why* it changed, and any key design decisions — not just a diff listing.

## What to do

- **Step 1 — Collect the diff:** Spawn a subagent to run `git diff HEAD` (or against the provided ref) and `git status` to enumerate all changed, added, and deleted files. Return the raw diff and file list.
- **Step 2 — Analyse in parallel:** For each logical area of change (e.g. a module, layer, or feature), spawn a dedicated subagent to deep-read the relevant changed files and produce a concise analysis covering: what was changed, what was removed or added, and any evident design decisions or patterns.
- **Step 3 — Synthesise:** Spawn a final subagent to merge all analyses into a single structured explanation (see Output Template). It must identify cross-cutting concerns, architectural shifts, and the overall intent of the change set.
- **Step 4 — Output:** Present the synthesised explanation directly in the chat. Do not create or modify any files.

## What not to do

- Do not modify, create, or delete any files.
- Do not suggest code improvements or refactors.
- Do not reproduce large blocks of raw diff or source code — summarise instead.
- Do not speculate beyond what the diff evidence supports.
- Do not skip the parallel analysis step, even for small change sets.

## Context Boundaries

- Source of truth is the git diff. Read changed files for context, but do not stray into unchanged code unless it is directly required to understand a change.
- If no ref is provided, compare against `HEAD` (last commit vs. working tree including staged changes).
- Output is chat-only. No files are written.

## Reasoning Constraints

- Group changes by logical concern (feature, layer, module) rather than listing files one by one.
- For each group, answer: *What changed? What was the design decision? What is the impact?*
- Highlight any breaking changes, interface modifications, or dependency shifts explicitly.
- If a change is purely cosmetic (formatting, rename), label it as such and keep its entry brief.

## Failure Behaviour

- If the repository has no commits, state that clearly and stop.
- If `git diff` returns empty, report that the working tree is clean with no uncommitted changes.
- If a changed file cannot be read, note it as unreadable and continue with the rest.

## Quality Bar

- Group-level summaries must be one short paragraph each — no bullet-point walls.
- The overall summary must not exceed a single screen of text.
- Use plain British English. No jargon unless it is a recognised technical term.

## Subagent Usage

- You must use subagents.
- Use parallel subagents when possible.
- Delegate each High-level Task and its associated Subtasks to subagents for execution.
- Plan the work in a way that can be done with dedicated subagents.
- Use dedicated subagents for research, analysis, planning, writing, evaluation, etc.
- Use dedicated parallel subagents for writing, analysing, evaluating, etc. for each section. Do not reuse the same subagent for writing multiple sections, or for writing and analysing. Each subagent has a single responsibility.
- The main agent must only delegate to subagents and ask for clarification if needed.
- The main agent must not do any of the actual work of writing, analysing, or evaluating.

---

## Output Template

```
# Overview
[One paragraph: the overall intent and scope of the change set.]

# Changes by Area

## [Area / Module Name]
**What changed:** [Concise description.]
**Design decision:** [Why this approach was taken, if evident.]
**Impact:** [Effect on the system — API, behaviour, dependencies, etc.]

(repeat per area)

# Cross-Cutting Concerns
[Breaking changes, shared interface modifications, dependency updates, or patterns applied across multiple areas.]

# Notable Omissions / Open Questions
[Anything the diff suggests was started but not completed, or decisions that appear unresolved.]
```
