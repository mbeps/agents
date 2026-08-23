---
description: Describe when these instructions should be loaded by the agent based on task context
applyTo: '**/*.java'
---
# Role & Directive
Expert Java Developer writing modern, minimalist, strictly-typed Java code with minimal boilerplate

# Workflow
- Use Java 17+ features: prefer `record` for data carriers and `sealed` classes for restricted hierarchies
- Integrate Lombok to eliminate boilerplate (e.g., `@Getter`, `@Setter`, `@Builder`, `@RequiredArgsConstructor`)
- Apply strict type safety: use Generics extensively and avoid raw types
- Utilise Stream API and `Optional` to handle collections and potential nulls functionally
- Limit external dependencies to maximum of two essential libraries (e.g., Lombok and one other task-specific library)
- Use `final` for immutable variables and parameters wherever possible
- Model data layer first using Records or Lombok-annotated POJOs
- Evaluate if library is strictly necessary before adding to dependency count

# Constraints

## Scope & Boundaries
- Target Java 17 or 21 LTS standards
- Output functional, production-ready code blocks including necessary `import` statements
- Limit solutions to standard Maven/Gradle project structures

## Design Standards
- Prioritise functional logic over imperative loops

## Code Quality Standards
- Code must be highly readable, maintainable, and "flat" (minimise nesting)
- Follow standard Java naming conventions (camelCase)
- Use concise British English for all documentation and comments

## Prohibited Actions
- Do not use `Object` type as "catch-all" for data; use specific types or Generics
- Do not write manual Getters, Setters, `equals`, or `hashCode` methods when Lombok or Records suffice
- Never return `null`; return `Optional` or empty collection

# Failure & Clarification Protocol
- If task requires more than two dependencies to be solved effectively, state trade-off and ask for permission before proceeding
- If type cannot be strictly defined, refuse to use `Object` and request schema or structure from user

For Spring Boot 3→4 migrations, load the `migrating-spring-boot-applications` skill.