---
description: Create a single feature and start the standard spec workflow
allowed-tools: Read, Write, Glob, TodoRead, TodoWrite
---

# Add One-Off Feature

Create a single feature without running full project planning. This uses the same standard workflow and templates as the rest of the system.

## Your Task
Create a new feature directory for: **$ARGUMENTS**
Seed requirements from the template and guide the user into the standard workflow.

## Analysis

<thinking>
Consider:
- What is the next available feature number?
- How should the feature slug be formatted?
- Does this align with existing architecture?
- What conventions should be followed?
</thinking>

- Determine the minimal information needed to set up this feature (name/slug)
- Analyze numbering and slug conventions to match existing features

## Process

<analysis>
1. **Read Project Context**
   - Check if `architecture.md` exists; if yes, read it to understand existing project structure
   - If missing, this may be the first feature - create basic architecture.md
   - Check if `conventions.md` exists; if yes, read it to understand coding standards
   - If missing, create basic conventions.md
   - Use available context to ensure new feature aligns with current architecture
   - Note any patterns or conventions to follow

2. **Feature Setup**
   <decision>
   Based on analysis:
   - Next number: [NN]
   - Feature slug: [derived-slug]
   - Alignment: [how it fits architecture]
   </decision>

   - Determine the next available feature number by scanning `features/` for existing directories in the form `NN-...`
   - Create: `features/{NN}-{feature-slug}/` (where {NN} is the number and {feature-slug} is derived from the feature description)

   ## Template Usage
   - Initialize `requirements.md` from `@.claude/templates/requirements.md`
   - Template provides EARS format structure adaptable to project type
   - Replace `[Feature Name]` placeholder with actual feature name
   - Do NOT create `design.md` or `tasks.md` yet (deferred creation)

3. **Architecture/Convention Updates**
   - If this feature might introduce new patterns, note them
   - After creating feature directory, ask: "This feature might establish [new patterns]. Should I update architecture.md/conventions.md?"
   - If approved or if files don't exist, create/update them
</analysis>

3. **Proceed with Standard Workflow**
   - Instruct the user to continue with the normal phases (using the actual created directory name):
     - `/pin:requirements {NN}-{feature-slug}` — detail requirements using EARS
     - `/pin:design {NN}-{feature-slug}` — generate design from requirements
     - `/pin:tasks {NN}-{feature-slug}` — create implementation tasks from design
     - `/pin:execute {NN}-{feature-slug}` — implement tasks one at a time (TDD)

## Details & Conventions

- Feature numbering:
  - Use zero-padded 2-digit numbers starting at 01. If existing features are 01, 02, 03, the next is 04.
- Slug rules:
  - Lowercase, words separated by hyphens, non-alphanumeric stripped (e.g., "Add password reset" → `password-reset`)
- Requirements template:
  - Use the requirements template from `@.claude/templates/requirements.md`
- Tasks conventions:
  - When tasks are later created, enforce numeric headings: `## Task {N}: {Title}`
  - During execution, use inline completion: append `[IMPLEMENTED]` and add a `**Completion**:` note under the heading

## Outputs

- `features/{NN}-{feature-slug}/requirements.md` (e.g., `features/03-csv-export/requirements.md`)

## Final Output Message

<output>
After creating the feature directory and requirements file, output:
"Created new feature directory `features/{NN}-{feature-slug}/` with requirements template.

Next, define the requirements with `/pin:requirements {NN}-{feature-slug}`."

(Replace {NN}-{feature-slug} with the actual created directory name, e.g., `03-csv-export`)
</output>

## Context Management

💡 **Tip**: After creating the feature, consider using `/clear` before proceeding to `/pin:requirements` for optimal performance.

## Example

User: `/feature "Add CSV export"`

Assistant:
- Created `features/03-csv-export/`
- Seeded requirements from template
- Next: `/pin:requirements 03-csv-export` → `/pin:design 03-csv-export` → `/pin:tasks 03-csv-export` → `/pin:execute 03-csv-export`
