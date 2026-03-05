---
description: 'Generates or updates the .github/copilot-instructions.md file to provide AI agents with project-specific knowledge.'
tools: ['read', 'edit/createDirectory', 'edit/createFile', 'edit/editFiles', 'search', 'web', 'context7/*', 'agent', 'todo']
---
# Goal of the Prompt
Analyse the codebase to generate or update the `.github/copilot-instructions.md` file. The goal is to provide AI agents with essential, project-specific knowledge to make them immediately productive, formatted into a strict structure.

# What to do
- **Discover Context:** Search for existing AI conventions using this glob pattern: `**/{.github/copilot-instructions.md,AGENT.md,AGENTS.md,CLAUDE.md,.cursorrules,.windsurfrules,.clinerules,.cursor/rules/**,.windsurf/rules/**,.clinerules/**,README.md}`.
- **Analyse the "Big Picture":** Read multiple files to understand service boundaries, data flows, and architectural decisions.
- **Identify Workflows:** detailed critical developer workflows (builds, tests, debugging) and commands not obvious from file inspection.
- **Map the Data:** Inspect database schemas (SQL, Prisma, etc.) to extract table details and relationships.
- **Map the Code:** Identify reusable libraries, components, and interfaces, noting inputs and outputs.
- **Merge & Generate:** If `.github/copilot-instructions.md` exists, preserve valuable content while updating it. Output the final result using the **Output Template** below.
- **Accuracy Check:** Ensure all technical terms and descriptions accurately reflect the codebase.
- Write an overview of this project to give context to the agents.
- Write a list of main features as concise bullet points to help agents understand the core functionality.
- Write a list of major tech stack components (frameworks, languages, databases, key libraries).
- Write a database section detailing the database design including table names, what each table is for, column names and types, and relationships between tables all with brief descriptions.
- Write a section on reusable code and directory structure, listing key directories and files, describing their purpose, inputs, and outputs.
- Write a design and architecture overview, describing the overall architecture pattern, data flow, key design decisions, and integration points with external systems.
- You can add any additional sections you think are relevant to help agents understand the project better.
- Use subagents for all the work. Do all the research, analysis, planning, etc in subagents and not in the main agent. The main agent should only be responsible for delegating to subagents and asking for clarification if needed. This will help keep the main agent focused and prevent it from becoming overloaded with tasks.
- Evaluate the quality of the work using a subagent. 

# What not to do
- Do not list minor dependencies (e.g. eslint, prettier, small helpers). List only major stack components.
- Do not include configuration files (e.g. `.env`, `.gitignore`, `tsconfig.json`) in the directory structure.
- Do not give generic advice (e.g. "write tests", "handle errors"). Focus on *this* project's specific approach.
- Do not list aspirational practices; document only what is currently discoverable in the code.
- Do not speculate on features or architecture not evidenced in the codebase.
- Do not include boilerplate code unless it has been significantly modified.
- Do not modify any other files other than `.github/copilot-instructions.md`.
- Do not create false information. If unsure, leave it out.
- Do not include irrelevant information. Keep the output focused.
- Do not do any work in the main agent unless it is to delegate to subagents or to ask for clarification. This includes writing code, running tests, debugging, etc. Always use subagents for these tasks.

# Context Boundaries
- Search for existing AI conventions using this glob pattern: `**/{.github/copilot-instructions.md,AGENT.md,AGENTS.md,CLAUDE.md,.cursorrules,.windsurfrules,.clinerules,.cursor/rules/**,.windsurf/rules/**,.clinerules/**,README.md}`.
- Analyse the whole codebase carefully and thoroughly. You can obviously use the codebase context.
- Use tools such as web search and context7/* to gather additional information about technologies or libraries used in the project if needed.
- Focus on the provided glob search for existing rules.
- Ignore standard boilerplate code unless it has been modified significantly.

# Reasoning Constraints
* **Database:** You must identify specific table names, column names, and relationships.
* **Reusable Code:** Present this as a directory tree, but exclude noise. Focus on libs, components, and schemas.
* **Architecture:** Explain *why* specific structural decisions were made, referencing key files.

# Quality Bar
* **Concise:** Instructions should be actionable and dense (~20-50 lines where possible, though the DB section may expand this).
* **Specific:** Include specific examples from the codebase when describing patterns.
* **Accurate:** Ensure technical terms match the actual code (e.g. don't say "Postgres" if they use "MySQL").

# Output Template
Please generate the response using this exact markdown structure:

```markdown
# Project Overview
[Brief summary of what the application does and its primary purpose]

# Features
- [Feature 1]
- [Feature 2]
- [Feature 3]

# Tech Stack
- **Framework:** [Major framework, e.g. Next.js]
- **Language:** [e.g. TypeScript]
- **Database:** [e.g. PostgreSQL]
- **Key Libraries:** [Only major tools, e.g. Tailwind, Redux, tRPC]

# Database Schema
## [Table Name]
- **Description:** [Purpose of the table]
- **Columns:**
  - `[column_name]`: [Type] - [Description]
- **Relationships:** [Foreign keys and links to other tables]

*(Repeat for all major tables)*

# Reusable Code & Directory Structure
- **`[path/to/components]`**
  - `[ComponentName]`: [Input/Props -> Output/Render description]
- **`[path/to/libs]`**
  - `[UtilityFunction]`: [Input -> Output description]
- **`[path/to/schemas]`**
  - `[SchemaName]`: [Description of validation or type definition]

# Design & Architecture Overview
- **Pattern:** [e.g. Monorepo, Microservices, MVC]
- **Data Flow:** [Description of how data moves, e.g. Client -> Next.js API -> Prisma -> DB]
- **Key Decisions:** [Why specific structures were chosen]
- **Integration Points:** [External APIs, cross-component communication]
```

You can add any additional sections you think are relevant to help agents understand the project better.