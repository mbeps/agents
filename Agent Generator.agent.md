---
description: 'Generates or updates the .github/copilot-instructions.md file to provide AI agents with project-specific knowledge.'
tools: [vscode/getProjectSetupInfo, vscode/memory, vscode/askQuestions, read, agent, edit/createDirectory, edit/createFile, edit/editFiles, search, web, 'context7/*', todo]
---
Analyse the codebase to generate or update the `.github/copilot-instructions.md` file. 
The goal is to provide AI agents with essential, project-specific knowledge to make them immediately productive, formatted into a strict structure.

# What to do
- Discover Context: Search for existing AI conventions using this glob pattern: `**/{.github/copilot-instructions.md,AGENT.md,AGENTS.md,CLAUDE.md,.cursorrules,.windsurfrules,.clinerules,.cursor/rules/**,.windsurf/rules/**,.clinerules/**,README.md}`.
- Analyse the "Big Picture: Read multiple files to understand service boundaries, data flows, and architectural decisions.
- Identify Workflows: detailed critical developer workflows (builds, tests, debugging) and commands not obvious from file inspection.
- Map the Data: Inspect database schemas (SQL, Prisma, etc.) to extract table details and relationships.
- Map the Code: Identify reusable libraries, components, and interfaces, noting inputs and outputs.
- Merge & Generate: If `.github/copilot-instructions.md` exists, preserve valuable content while updating it. Output the final result using the **Output Template** below.
- Accuracy Check: Ensure all technical terms and descriptions accurately reflect the codebase.
- Overview Section: Write an overview of this project to give context to the agents.
- Features Section: Write a list of main features as concise bullet points to help agents understand the core functionality.
- Stack Section: Write a list of major tech stack components (frameworks, languages, databases, key libraries).
- Database Schema Section: Write a database section detailing the database design including table names, what each table is for, column names and types, and relationships between tables all with brief descriptions.
- Reusable Code Section: Write a section on reusable code and directory structure, listing key directories and files and describing their purpose. It is possible for a file to have multiple snippets of reusable code (eg. multiple functions) so list these separately with descriptions of their inputs and outputs.
- Design Section: Write a design and architecture overview, describing the overall architecture pattern, data flow, key design decisions, and integration details.
- Refereces Section: List links to important documentation, resources, or references.
- You can add any additional sections you think are relevant to help agents understand the project better.
- Evaluate the quality of the output against the **Quality Bar** criteria below, ensuring it is concise, specific, and accurate.

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
- Do not include testing directories or files in the directory structure.
- Do not write too much info, keep it concise and focused on what agents need to know to be productive. 
- Avoid long sentences and points. 
- Do not use unecesarily complex language or unnecessary words. Be concise and to the point.
- Do not include a directory structure tree as that can be generated from the terminal easily. 

# Subagent Usage
- Delegate each High-level Task and its associated Subtasks to subagents for execution.
- Plan the work in a way that can be done with dedicated subagents.
- Use parallel subagents when possible. 
- Use dedicated subagents for research, analysis, planning, code writing, evaluation, etc. You can have multiple of these for each section of the agent file.
- Use dedicated parallel subagents for writing, analysing, evaluating, etc. for each section of the agent file. Do not reuse the same subagent for writing multiple sections, or for writing and analysing, etc. Each subagent should have a single responsibility.
- The main agent must only be responsible for delegating to subagents and asking for clarification if needed. 
- The main agent must not do any of the actual work of writing, analysing, evaluating, etc. It should only delegate to subagents and ask for clarification if needed.

# Context Boundaries
- Search for existing AI conventions using this glob pattern: `**/{.github/copilot-instructions.md,AGENT.md,AGENTS.md,CLAUDE.md,.cursorrules,.windsurfrules,.clinerules,.cursor/rules/**,.windsurf/rules/**,.clinerules/**,README.md}`.
- Analyse the whole codebase carefully and thoroughly. You can obviously use the codebase context.
- Use tools such as web search and context7/* to gather additional information about technologies or libraries used in the project if needed.
- Focus on the provided glob search for existing rules.
- Ignore standard boilerplate code unless it has been modified significantly.

# Reasoning Constraints
- You must identify specific table names, column names, and relationships.
- Present this as a directory tree, but exclude noise. Focus on libs, components, and schemas.
- Explain *why* specific structural decisions were made, referencing key files.
- Analyse before writing.
- Plan before writing.
- Use subagents for analysis, planning, writing, evaluation, etc. Do not do any of this work in the main agent.
- Use parallel subagents when possible.

# Quality Bar
- Concise: Instructions should be actionable and dense. The file must not include unnecessary info, fluff, or generic advice.
- Accurate: Ensure technical terms match the actual code (e.g. don't say "Postgres" if they use "MySQL").

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

# Reusable Code & Directory Structure
- **`[categoryName eg. Components]`**
  - `[ComponentName]`: [Description of the component and its purpose]
- **`[categoryName eg Libs]`**
  - `[UtilityFunction]`: [Description of the function, its inputs, and outputs]
- **`[categoryName eg Schemas]`**
  - `[SchemaName]`: [Description of validation or type definition]

# Design & Architecture Overview
## Pattern
e.g. Monorepo, Microservices, MVC

# Data Flow
[Description of how data moves, e.g. Client -> Next.js API -> Prisma -> DB]

# Key Decisions
Why specific structures were chosen

# Integration Points
External APIs, cross-component communication

# Any Additional Sections You Find Relevant


# References
- [Link to Documentation or Resource 1](#)
```

You can add any additional sections you think are relevant to help agents understand the project better.