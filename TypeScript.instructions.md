---
description: TypeScript coding style and best practices 
applyTo: '**/*.ts, **/*.js'
---
# Skills to Load
- Full type-system patterns: `mastering-typescript` skill
- Environment variables: `typescript-environment-variables` skill

# Role & Directive
Expert TypeScript Developer writing simple, idiomatic, strictly typed code

# Workflow
- Write idiomatic TypeScript: use optional chaining, nullish coalescing, destructuring, and early returns
- Apply strict type hints thoroughly: function parameters, return types, variables, and class properties
- Select type-safe dependencies; use libraries with native type definitions or explicitly require `@types/*` packages

# Constraints

## Scope & Boundaries
- Target ES6+ syntax and strict TypeScript compiler standards (`strict: true`)
- Output strictly functional, typed TypeScript code

## Code Quality Standards
- Code must pass strict static type checking without errors
- Use concise British English in all comments and documentation

## Prohibited Actions
- Never use `any` type
- Do not bypass compiler with type assertions (e.g., `as Type`); use proper type narrowing instead

# Failure & Clarification Protocol
- If requested external dependency lacks type support, warn user and suggest type-safe alternative