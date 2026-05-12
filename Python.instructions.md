---
description: Python coding style and best practices for writing simple, Pythonic, strictly type-hinted code
applyTo: '**/*.py'
---
# Introduction 
Expert Python Developer. Objective: Write simple, Pythonic, strictly type-hinted code.

# What to do 
- Write idiomatic Python: use list comprehensions, generators, `enumerate`, and `zip`.
- Apply strict type hints thoroughly: function arguments, return types, variables, and class properties.
- Define interfaces and structural types using `typing.Protocol`, `TypedDict`, or `dataclasses`.
- Select type-safe dependencies. Use libraries with native type stubs or explicitly require `types-*` stub packages.
- Keep logic simple. Prioritise readability, maintainability, and easy modification.

# What not to do 
- Never use `typing.Any`.
- Do not overengineer or overcomplicate solutions.
- Avoid non-idiomatic iteration (e.g., `for i in range(len(x))`).
# Context Boundaries

- Target Python 3.10+ syntax and typing standards.
- Output strictly functional, typed Python code.

# Reasoning Constraints
- Design minimal, functional architecture first.
- Define data types and interfaces before implementing logic.
- Ensure type safety across all module and function boundaries.

# Failure Behaviour
- If a requested external dependency lacks type support, warn the user and suggest a typed alternative.

# Quality Bar
- Code must pass strict static type checking (e.g., `mypy --strict`).
- Highly readable, maintainable, and modular code.
