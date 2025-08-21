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
   - Testing frameworks in use
3. **Document Findings**:
   - Generate/update `architecture.md` with discovered project type and structure
   - Generate/update `conventions.md` with detected coding standards
4. **Inform Planning**:
   - Use discovered context to suggest features that align with existing structure
   - Select appropriate task templates based on project type
</analysis>

## Interactive Process

1.  **Project Context**: First determine if this is a new project or adding to an existing codebase.
    - For existing projects: "I'll analyze your current project structure first..."
    - For new projects: "Let's define your project architecture preferences..."

2.  **Gather Project Information**: Present a structured request for project details:
    - "To create an effective project plan, please provide:
    1. Overall objective and key outcomes
    2. Target users and use cases
    3. Core features needed (I'll help break these down further)
    4. Any technical constraints or preferences"
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
    - For new projects: Propose initial architecture and conventions, create `architecture.md` and `conventions.md`
    - For existing projects: Update `architecture.md` and `conventions.md` with discovered patterns

6.  **Template Usage**: The requirements structure is defined in `.claude/templates/requirements.md`
    - Template provides EARS format sections
    - Adapts to project type (Web, CLI, Library, Mobile, Service)
    - See template file for complete structure

7.  **Final Approval & File Generation**: Once the user confirms the feature plan is complete, proceed with file generation.
    - Generate/update `architecture.md` and `conventions.md` based on project analysis or user choices
    - For each feature in the approved plan:
      - Create a numbered feature directory: `features/[NN]-[feature-slug]/` (e.g., `features/01-project-setup/`).
      - **Standard Mode**:
        - Check if `.claude/templates/requirements.md` exists
        - If yes: Copy it EXACTLY as-is, only replacing the `[Feature Name]` placeholder with the actual feature title
        - If no: Notify user "Warning: requirements.md template not found. Creating basic structure." and create a basic requirements.md with standard EARS sections
        - Do NOT fill in any actual requirements details
      - **Draft Requirements Mode** (when "all" flag is used):
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
        - Note: These requirements benefit from refinement via `/spec:requirements` for validation and additions
      - Do NOT create `design.md` or `tasks.md` at this stage. These will be initialized exactly once by `/spec:design` and `/spec:tasks` respectively.
      - If the requirements template file is missing, notify the user and create a structured placeholder with clear section headers instead.

## Final Approval Gate

<output>
After creating the directories and files, conclude with a summary and next steps:

**Standard Mode**:
"Project plan complete for [project description]. I have created [N] feature directories in `features/`. Each contains a template `requirements.md`.

You can now proceed to detail the requirements for any feature by running `/spec:requirements [feature-name]` (e.g., `/spec:requirements 01-project-setup`)."

**Requirements Generation Mode**:
"Project plan complete for [project description]. I have created [N] feature directories in `features/` with draft requirements generated from our interactive discussion above.

These requirements are marked for review. You can validate and refine them by running `/spec:requirements [feature-name]` (e.g., `/spec:requirements 01-project-setup`). The draft marker will be removed once requirements are finalized."
</output>

## Context Management Note

💡 **Performance Tip**: Consider using `/clear` to reset context before proceeding to the requirements phase, especially for large projects.

## Key Guidelines

- Be conversational and strategic.
- Guide the user towards a logical, sequential plan.
- Break down complexity into smaller, manageable parts.
- Do not generate any files until the user has explicitly approved the final plan.

Now, start the interactive process to define the project plan.
