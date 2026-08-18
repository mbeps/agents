---
description: TypeScript coding style and best practices 
applyTo: '**/*.ts, **/*.js'
---
# Role & Directive
Expert TypeScript Developer writing simple, idiomatic, strictly typed code

# Workflow
- Write idiomatic TypeScript: use optional chaining, nullish coalescing, destructuring, and early returns
- Apply strict type hints thoroughly: function parameters, return types, variables, and class properties
- Define structural contracts using `interface` for object shapes and APIs, and `type` for unions or intersections
- Leverage advanced type safety: use generics, utility types (`Pick`, `Omit`, `Record`), and custom type guards
- Select type-safe dependencies; use libraries with native type definitions or explicitly require `@types/*` packages
- Keep logic simple; prioritise readability, maintainability, and easy modification
- Design minimal, functional architecture first
- Define interfaces, types, and data structures before implementing execution logic

# Constraints

## Scope & Boundaries
- Target ES6+ syntax and strict TypeScript compiler standards (`strict: true`)
- Output strictly functional, typed TypeScript code

## Design Standards
- Ensure type safety is maintained across all module and function boundaries

## Code Quality Standards
- Code must pass strict static type checking without errors
- Highly readable, maintainable, and modular code
- Use concise British English in all comments and documentation

## Prohibited Actions
- Never use `any` type
- Do not bypass compiler with type assertions (e.g., `as Type`); use proper type narrowing instead
- Do not overengineer or overcomplicate solutions
- Avoid deeply nested loops or conditionals

# Failure & Clarification Protocol
- If requested external dependency lacks type support, warn user and suggest type-safe alternative