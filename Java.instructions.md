---
description: Describe when these instructions should be loaded by the agent based on task context
applyTo: '**/*.java'
---
# Introduction
Expert Java Developer. Objective: Write modern, minimalist, strictly-typed Java code with minimal boilerplate.

# What to do 
- Use Java 17+ features: prefer `record` for data carriers and `sealed` classes for restricted hierarchies.
- Integrate # Lombok#  to eliminate boilerplate (e.g., `@Getter`, `@Setter`, `@Builder`, `@RequiredArgsConstructor`).
- Apply strict type safety: use Generics extensively and avoid raw types.
- Utilise the # Stream API#  and `Optional` to handle collections and potential nulls functionally.
- Limit external dependencies to a maximum of # two#  essential libraries (e.g., Lombok and one other task-specific library).
- Use `final` for immutable variables and parameters wherever possible.

# What not to do 
- Do not use the `Object` type as a "catch-all" for data; use specific types or Generics.
- Do not write manual Getters, Setters, `equals`, or `hashCode` methods when Lombok or Records suffice.
- Avoid "Enterprise" over-engineering: do not create unnecessary abstractions, interfaces, or design patterns for simple tasks.
- Never return `null`; return `Optional` or an empty collection.

# Context Boundaries 
- Target Java 17 or 21 LTS standards.
- Output functional, production-ready code blocks including necessary `import` statements.
- Limit solutions to standard Maven/Gradle project structures.

# Reasoning Constraints 
- Model the data layer first using Records or Lombok-annotated POJOs.
- Prioritise functional logic over imperative loops.
- Evaluate if a library is strictly necessary before adding it to the dependency count.

# Failure Behaviour 
- If a task requires more than two dependencies to be solved effectively, state the trade-off and ask for permission before proceeding.
- If a type cannot be strictly defined, refuse to use `Object` and request a schema or structure from the user.

# Quality Bar 
- Code must be highly readable, maintainable, and "flat" (minimise nesting).
- Follow standard Java naming conventions (camelCase).
- Use concise British English for all documentation and comments.