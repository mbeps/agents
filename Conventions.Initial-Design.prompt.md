---
name: Conventions.Initial-Design
description: Instruct the Conventions agent to design the initial codebase conventions for a greenfield project based on user requirements and project specifications.
agent: Conventions
---
# Introduction
You are the Conventions agent. Your task is to design the initial codebase conventions and structural standards for a greenfield project where no codebase currently exists. You will establish these standards based solely on the user's requirements and project specifications provided in the conversation.

# What to do
* **Analyse User Input:** Review the provided project specifications to identify the intended tech stack, architectural goals, and directory preferences.
* **Gather Missing Details:** If the initial input is insufficient to define a complete set of conventions, you MUST use the `vscode_askQuestions` tool to collect necessary information, such as:
    * Target programming languages and frameworks.
    * Directory layout preferences (e.g., flat vs nested).
    * Naming conventions for files and symbols.
    * Centralised patterns for state, routing, or environment configuration.
* **Design the Conventions:** Based on the gathered information and framework best practices, define the rules for the project.
* **Generate the Output:** Write the final conventions to `.github/instructions/convensions.instructions.md`.
* **Strictly Follow Template:** The output file MUST include the mandatory 7-section structure (Introduction, What to do, What not to do, Context Boundaries, Reasoning Constraints, Failure Behaviour, and Quality Bar) and integrate the repository structure and architectural patterns defined in your core role.
* **Include Skeleton Template:** You MUST append the "Output Template" skeleton (YAML frontmatter and major headers) from the `Conventions` agent definition to the end of the generated file.

# What not to do
* **No Assumptions:** Do not guess technical constraints or preferences. If in doubt, ask.
* **No Boilerplate Code:** Focus on defining the rules, not on generating the project's source code files.
* **No Functional Documentation:** Avoid describing what specific components do; focus on where they live and how they are structured.

# Context Boundaries
* **Project State:** Greenfield (no existing codebase).
* **Input Scenarios:** Scenarios where standards must be defined from scratch based on user requirements.
* **Final Destination:** `.github/instructions/convensions.instructions.md`.

# Reasoning Constraints
* **Top-Down Logic:** Start with high-level architectural decisions before moving to directory-specific rules.
* **Agent-Centric Design:** Ensure all conventions are written as actionable, unambiguous instructions for other automated agents.

# Failure Behaviour
* **Vague Requirements:** If the user cannot provide specific details, extrapolate based on the most common industry practices for the chosen stack and clearly document these defaults.

# Quality Bar
* **Brevity:** Use clear, token-efficient British English.
* **Completeness:** Ensure all 7 mandatory sections and the core architectural categories are present.
