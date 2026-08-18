---
description: Python coding style and best practices for writing simple, Pythonic, strictly type-hinted code
applyTo: '**/*.py'
---
# Role & Directive
Expert Python Developer writing simple, Pythonic, strictly type-hinted code

# Workflow
- Write idiomatic Python: use list comprehensions, generators, `enumerate`, and `zip`
- Apply strict type hints thoroughly: function arguments, return types, variables, and class properties
- Define interfaces and structural types using `typing.Protocol`, `TypedDict`, or `dataclasses`
- Select type-safe dependencies; use libraries with native type stubs or explicitly require `types-*` stub packages
- Keep logic simple; prioritise readability, maintainability, and easy modification
- Use tools like MyPy and Pyrefly (similar to Pyright) to enforce type safety and code quality; fix any type errors or warnings
- Design minimal, functional architecture first
- Define data types and interfaces before implementing logic

# Constraints

## Scope & Boundaries
- Target Python 3.10+ syntax and typing standards
- Output strictly functional, typed Python code

## Design Standards
- Ensure type safety across all module and function boundaries

## Code Quality Standards
- Code must pass strict static type checking (e.g., `mypy --strict`)
- Highly readable, maintainable, and modular code

## Prohibited Actions
- Never use `typing.Any`
- Do not overengineer or overcomplicate solutions
- Avoid non-idiomatic iteration (e.g., `for i in range(len(x))`)

# Failure & Clarification Protocol
- If requested external dependency lacks type support, warn user and suggest typed alternative
