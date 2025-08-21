---
description: Interactively breaks down a project description into a plan with multiple features. Optional 'all' flag generates draft requirements.
allowed-tools: Read, Write, Glob, Grep, TodoRead, TodoWrite
---

# Project Planning and Feature Breakdown

You are initiating a new project by breaking down a high-level goal into a structured plan of individual, manageable features.

## Your Task

Facilitate a conversation to define a list of features for the project: **$ARGUMENTS**

## Mode Selection

Parse `$ARGUMENTS` to determine mode:

- **Standard Mode**: If `$ARGUMENTS` does not end with " all" → Creates feature structure with template requirements
- **Draft Requirements Mode**: If `$ARGUMENTS` ends with " all" → Creates feature structure with draft EARS requirements generated from the interactive discussion
- Extract project description by removing " all" suffix if present
- Example: `$ARGUMENTS` = "task management app all" → Mode: Requirements Generation, Project: "task management app"

## Project Discovery (for existing codebases)

<analysis>
If working with an existing codebase:

1. **Analyze Project Structure**:
   - Scan for project type indicators:
     - Web App: package.json with express/fastify/next, requirements.txt with django/flask, etc.
     - CLI Tool: package.json with commander/yargs, setup.py with click, go.mod with cobra, etc.
     - Library/SDK: package.json with "main", setup.py with packages, go.mod with module declaration
     - Mobile App: package.json with react-native, pubspec.yaml, Info.plist, AndroidManifest.xml
     - Microservice: Dockerfile, kubernetes configs, service mesh configs
   - Detect build tools and package managers
2. **Identify Architecture**:
   - Framework detection (React, Vue, Django, Spring, etc.)
   - Architecture patterns (MVC, microservices, serverless, etc.)
   - Testing frameworks in use (detect from package.json scripts, pytest.ini, go.mod, etc.)
3. **Document Findings**:
   - Generate/update `.claude/ARCHITECTURE.md` with discovered project type and structure
   - Generate/update `.claude/CONVENTIONS.md` with detected coding standards
   - **Document test runner command** (e.g., 'npm test', 'pytest', 'go test ./...') in CONVENTIONS.md
4. **Inform Planning**:
   - Use discovered context to suggest features that align with existing structure
   - Select appropriate task templates based on project type
</analysis>

## Interactive Process

1.  **Project Context**: First determine if this is a new project or adding to an existing codebase.
    - For existing projects: "I'll analyze your current project structure first..."
    - For new projects: "Let's define your project architecture preferences..."

2.  **Architecture Setup** (for new projects):
    - "What type of project is this? (Web App, API Service, CLI Tool, Library/SDK, Mobile App, Monorepo, etc.)"
    - "Which architecture pattern fits best? (Monolithic for MVPs, Microservices for scale, Serverless for events, Event-driven, Clean Architecture, etc.)"
    - "What runtime and framework? (e.g., Bun with Hono, Node.js with Fastify, Deno with Fresh)"
    - "For web apps: Next.js 14 App Router, Remix, SvelteKit, or Astro?"
    - "Database preference? (PostgreSQL with Neon/Supabase, SQLite with Turso, MongoDB Atlas, etc.)"
    - "Monorepo setup needed? (Turborepo, Nx, single-package)"
    - **"What test framework and runner?** (e.g., 'npm test' with Jest, 'bun test' with Bun, 'pytest' for Python, 'go test' for Go)"
    - Review .claude/SECURITY.md checklist together for security requirements
    - Use responses to fill in the actual values in .claude/ARCHITECTURE.md placeholders
    - Document test runner command in .claude/CONVENTIONS.md for later use

3.  **Gather Project Information**: Present a structured request for project details:
    - "To create an effective project plan, please provide:
    1. Overall objective and key outcomes
    2. Target users and use cases
    3. Core features needed (I'll help break these down further)
    4. Any technical constraints or preferences
    5. Performance requirements (if any)
    6. Security considerations (if any)"
    - For existing projects, add: "Should new features follow your existing patterns or introduce new approaches?"

3.  **Analysis**:
    <thinking>
    Consider the following aspects:
    - What is the minimal viable feature set?
    - What are the dependencies between features?
    - What provides the most immediate value?
    - How can we sequence for iterative delivery?
    - What existing code can be leveraged?
    </thinking>

    Determine the simplest, value-first way to sequence capabilities, considering any existing architecture.
    3a. **Propose Feature Breakdown**: Based on the user's input and project context, present a complete feature list: \* "Based on your requirements, here's the proposed feature breakdown: 1. **Project Setup**: Configure the basic application structure, dependencies, and test framework 2. **Task CRUD API**: Implement API endpoints for creating, reading, updating, and deleting tasks
    [Complete list]

          Please review and let me know any changes (add/remove/reorder features)."

4.  **Finalize Plan**: Once the user approves, proceed with creating the feature structure.

5.  **Architecture & Conventions**:
    - For new projects:
      - Read `.claude/ARCHITECTURE.md` and `.claude/CONVENTIONS.md` templates
      - Replace ALL placeholders marked with [e.g., ...] or [brackets] with actual values
      - Example replacements:
        * `**Type**: [e.g., Web Application, API Service, CLI Tool, Library]`
          → `**Type**: Web Application`
        * `**Language**: [e.g., TypeScript, Python 3.11, Go 1.21]`
          → `**Language**: TypeScript`
        * `**Test Framework**: [e.g., Jest + React Testing Library]`
          → `**Test Framework**: Jest + React Testing Library`
        * `**Test Runner**: [e.g., npm test, pytest, go test]`
          → `**Test Runner**: npm test`
      - Remove the "e.g.," part, keep only the actual value
      - Ensure both files are declarative and specific to this project
      - **CRITICAL**: Verify no placeholders remain by checking for "[" characters
    - For existing projects:
      - Update `.claude/ARCHITECTURE.md` with discovered patterns, replacing placeholders
      - Document existing conventions in `.claude/CONVENTIONS.md` as concrete practices
      - **Detect and document test runner command** from package.json/Makefile/etc.
      - Note any technical debt in the "Future Considerations" section

6.  **Template Usage**: The requirements structure is defined in `.claude/templates/requirements.md`
    - Template provides EARS format sections
    - Adapts to project type (Web, CLI, Library, Mobile, Service)
    - See template file for complete structure

7.  **Architecture Validation & File Generation**:
    - **VALIDATION GATE**: Before proceeding with feature generation:
      - Check `.claude/ARCHITECTURE.md` for any remaining placeholders
      - Check `.claude/CONVENTIONS.md` for any remaining placeholders
      - Verify test runner command is specified in CONVENTIONS.md
      - If placeholders found:
        * **STOP** and inform user: "⚠️ Architecture setup incomplete. Found placeholders in [file]. Please provide:
          [List specific unfilled placeholders]
          Cannot proceed until all architecture decisions are concrete."
        * DO NOT create feature directories until resolved
        * Return to architecture questions to fill missing information
    - Once validated, generate/update `.claude/ARCHITECTURE.md` and `.claude/CONVENTIONS.md`:
      - Use Edit or MultiEdit to replace placeholders with actual values
      - Each placeholder like `[e.g., something]` should become the actual value
      - Ensure test runner is documented under "Quick Commands" or "Testing" section
      - Do NOT leave any bracketed placeholders in the final files
      - Ensure all sections have concrete, project-specific information
    - For each feature in the approved plan:
      - Create a numbered feature directory: `features/[NN]-[feature-slug]/` (e.g., `features/01-project-setup/`).
      - **Standard Mode**:
        - Check if `.claude/templates/requirements.md` exists
        - If yes: Copy it EXACTLY as-is, only replacing the `[Feature Name]` placeholder with the actual feature title
        - If no: Notify user "Warning: requirements.md template not found. Creating basic structure." and create a basic requirements.md with standard EARS sections
        - Do NOT fill in any actual requirements details
      - **Draft Requirements Mode** (when "--all" flag is used):
        - Start with `.claude/templates/requirements.md` as base (replacing `[Feature Name]`)
        - Add `<!-- DRAFT: Generated from interactive planning discussion above, needs refinement -->` at the top of the file
        - Generate comprehensive EARS requirements based on the discussion that just occurred in this command:
          - Core Functionality with detailed EARS requirements from feature discussion
          - User/System Interactions with complete workflows
          - Error Handling with thorough error cases and recovery
          - Non-Functional Requirements fully specified for project type
          - Keep template structure and headings intact
        - Generate high-quality, detailed requirements (not placeholder content)
        - Leave sections empty only if genuinely not applicable
        - Note: These requirements benefit from refinement via `/pin:requirements` for validation and additions
      - Do NOT create `design.md` or `tasks.md` at this stage. These will be initialized exactly once by `/pin:design` and `/pin:tasks` respectively.
      - If the requirements template file is missing, notify the user and create a structured placeholder with clear section headers instead.

## Final Approval Gate

<output>
After creating the directories and files, conclude with a summary and next steps:

**Standard Mode**:
"Project plan complete for [project description]. I have created [N] feature directories in `features/`. Each contains a template `requirements.md`.

You can now proceed to detail the requirements for any feature by running `/pin:requirements [feature-name]` (e.g., `/pin:requirements 01-project-setup`)."

**Requirements Generation Mode**:
"Project plan complete for [project description]. I have created [N] feature directories in `features/` with draft requirements generated from our interactive discussion above.

These requirements are marked for review. You can validate and refine them by running `/pin:requirements [feature-name]` (e.g., `/pin:requirements 01-project-setup`). The draft marker will be removed once requirements are finalized."
</output>

## Context Management Note

💡 **Performance Tip**: Consider using `/clear` to reset context before proceeding to the requirements phase, especially for large projects.

## Key Guidelines

- Be conversational and strategic.
- Guide the user towards a logical, sequential plan.
- Break down complexity into smaller, manageable parts.
- Do not generate any files until the user has explicitly approved the final plan.

Now, start the interactive process to define the project plan.
