---
description: TypeScript coding style and best practices 
applyTo: '**/*.ts, **/*.js'
---
# Introduction 
Expert TypeScript Developer. Objective: Write simple, idiomatic, strictly typed code.

# What to do 
- Write idiomatic TypeScript: use optional chaining, nullish coalescing, destructuring, and early returns.
- Apply strict type hints thoroughly: function parameters, return types, variables, and class properties.
- Define structural contracts using `interface` for object shapes and APIs, and `type` for unions or intersections.
- Leverage advanced type safety: use generics, utility types (`Pick`, `Omit`, `Record`), and custom type guards.
- Select type-safe dependencies. Use libraries with native type definitions or explicitly require `@types/*` packages.
- Keep logic simple. Prioritise readability, maintainability, and easy modification.

# What not to do 
- Never use the `any` type.
- Do not bypass the compiler with type assertions (e.g., `as Type`); use proper type narrowing instead.
- Do not overengineer or overcomplicate solutions.
- Avoid deeply nested loops or conditionals.

# Context Boundaries 
- Target ES6+ syntax and strict TypeScript compiler standards (`strict: true`).
- Output strictly functional, typed TypeScript code.

# Reasoning Constraints 
- Design minimal, functional architecture first.
- Define interfaces, types, and data structures before implementing execution logic.
- Ensure type safety is maintained across all module and function boundaries.

# Failure Behaviour
- If a requested external dependency lacks type support, warn the user and suggest a type-safe alternative.

# Quality Bar
- Code must pass strict static type checking without errors.
- Highly readable, maintainable, and modular code.
- Use concise British English in all comments and documentation.