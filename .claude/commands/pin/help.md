---
description: Display help information for spec:driven development commands
allowed-tools: Read, TodoRead, TodoWrite
---

# Pindex Help

Quick reference for the Pindex development methodology commands.

## Available Commands

### Core Workflow Commands

#### `/pin:feature "Add password reset"`

**Purpose**: Add a single feature after initial release without full planning

- **Input**: A short feature description (used to derive the slug)
- **Output**: `features/{NN}-{slug}/requirements.md` seeded from templates
- **Usage**: Anytime you want to add a one-off feature
- **Next steps**: Proceed with `/pin:requirements {NN-slug}` → `/pin:design {NN-slug}` → `/pin:tasks {NN-slug}` → `/pin:execute {NN-slug}`

#### `/pin:plan [project-description] [all]`

**Purpose**: Interactively break down a project into features through discussion.

- **Input**: A high-level description (starts interactive discussion), optional "all" flag
- **Process**: Interactive dialogue to understand project needs and define features
- **Output**:
  - Standard: Numbered directories with empty template `requirements.md`
  - With "all": Numbered directories with draft EARS requirements generated from the discussion
- **Usage**: Start of Phase 1 - Planning
- **Examples**:
  - `/pin:plan "A task management app"` - Interactive discussion → empty templates
  - `/pin:plan "A task management app" all` - Interactive discussion → draft requirements from that discussion

#### `/pin:requirements [feature-name]`

**Purpose**: Interactively detail or refine the EARS requirements for a specific feature.

- **Input**: Optional feature name (e.g., `01-project-setup`)
- **Output**: A detailed `features/[feature-name]/requirements.md`
- **Behavior**:
  - If draft requirements exist: Refines them and removes draft marker
  - If only template exists: Creates requirements from scratch
- **Usage**: Phase 2 - After planning is complete
- **Prerequisite**: Must have a feature directory created by `/pin:plan` or `/pin:feature`

#### `/pin:design [feature-name]`

**Purpose**: Generate technical design from existing requirements

- **Input**: Optional feature name (e.g., `01-project-setup`)
- **Output**: `design.md` with architecture and implementation approach
- **Usage**: Phase 3 - After requirements approval
- **Prerequisite**: Must have approved requirements.md

#### `/pin:tasks [feature-name]`

**Purpose**: Break down design into TDD implementation tasks

- **Input**: Optional feature name (e.g., `01-project-setup`)
- **Output**: `tasks.md` with structured implementation plan
- **Usage**: Phase 4 - After design approval
- **Prerequisite**: Must have approved design.md

#### `/pin:align [feature-name]`

**Purpose**: Validate alignment between requirements, design, tasks, and TLDR

- **Input**: Optional feature name
- **Output**: Validation report with gap analysis
- **Usage**: Before implementation or to ensure consistency
- **Features**: Cross-document validation, TLDR checking, architecture compliance

#### `/pin:execute [feature-name]`

**Purpose**: Execute implementation following TDD methodology

- **Input**: Optional feature name
- **Output**: Implemented code with tests and TLDR summary
- **Usage**: Phase 4 - After task approval
- **Prerequisite**: Must have approved tasks.md
- **Features**: 
  - TDD cycle (Red-Green-Refactor)
  - TLDR generation on stop (complete or partial)
  - Handles partial implementations gracefully
  - Test execution and validation

### Utility Commands

#### `/pin:list`

**Purpose**: List all features with documentation status

- **Input**: None
- **Output**: Table showing features and their specification status
- **Usage**: To see project overview
- **Features**: Shows Req/Des/Tasks/TLDR status for each feature

#### `/pin:status`

**Purpose**: Show comprehensive implementation progress

- **Input**: None
- **Output**: Detailed progress table with completion percentages
- **Usage**: To track project implementation status
- **Features**: Task counts, completion percentages, status indicators


#### `/pin:help`

**Purpose**: Display this help information

- **Input**: None
- **Output**: Command reference and usage guide
- **Usage**: Anytime you need command information

## Workflow Overview

```
1. /pin:plan [project]      →  Feature List     →  [Approval Gate]
2. /pin:requirements [feature-name] →  requirements.md  →  [Approval Gate]
3. /pin:design [feature-name]       →  design.md        →  [Approval Gate]
4. /pin:tasks [feature-name]        →  tasks.md         →  [Approval Gate]
5. /pin:align [feature-name]        →  Alignment Check  →  [Approval Gate]
6. /pin:execute [feature-name]      →  Working Code     →  [Testing & Deploy]
```

## Key Principles

- Context Management: Consider starting fresh sessions between phases and after every 2–3 tasks for optimal performance.

### EARS Requirements Format

- **Ubiquitous**: "The system SHALL [requirement]"
- **Event-Driven**: "WHEN [trigger] THEN the system SHALL [response]"
- **State-Driven**: "WHILE [state] the system SHALL [requirement]"
- **Conditional**: "IF [condition] THEN the system SHALL [requirement]"
- **Optional**: "WHERE [feature] the system SHALL [requirement]"

### Test-Driven Development

1. **🔴 Red**: Write failing test for next functionality
2. **🟢 Green**: Write minimal code to make test pass
3. **🔄 Refactor**: Improve code while keeping tests green

### Approval Gates

- Review and approve requirements before design
- Review and approve design before tasks
- Review and approve tasks before implementation

## File Structure

```
features/[feature-name]/
├── requirements.md     # EARS-formatted requirements
├── design.md          # Technical design document
├── tasks.md           # TDD implementation tasks
└── tldr.md            # Implementation summary (generated after execution)
```

## Templates

### Template Philosophy
Templates provide consistent structure while allowing flexibility. They are the **single source of truth** for document formats.

### Available Templates

#### `@.claude/templates/requirements.md`
- **Purpose**: EARS-formatted requirements structure
- **Sections**: Functional, non-functional, constraints, acceptance criteria
- **Adapts to**: Project type (Web, CLI, Library, Mobile, Service)
- **Used by**: `/pin:plan`, `/pin:requirements`, `/pin:feature`

#### `@.claude/templates/design.md`
- **Purpose**: Technical design document structure
- **Sections**: Architecture, data design, API, security, performance
- **Adapts to**: Architecture pattern and tech stack
- **Used by**: `/pin:design`

#### `@.claude/templates/tasks.md`
- **Purpose**: TDD task breakdown structure
- **Format**: Numeric headings with Red-Green-Refactor cycles
- **Sections**: 7-8 flexible task categories with reusability tracking
- **Adapts to**: Project type with specific task patterns
- **Used by**: `/pin:tasks`

#### `@.claude/templates/tldr.md`
- **Purpose**: Implementation summary documentation
- **Sections**: Completion status, what was built, incomplete items, decisions, testing
- **Generated**: When implementation stops (complete or partial)
- **Tracks**: Tasks completed vs total, implementation status
- **Used by**: `/pin:execute`

### Template Usage Pattern
1. Commands check if template exists
2. Initialize from template (replace placeholders like `[Feature Name]`)
3. Augment existing files without overwriting user content
4. Warn if template missing and create basic structure

## Implementation Approaches

Choose your implementation strategy:

- **🔴🟢🔄 TDD**: Strict Red-Green-Refactor methodology
- **⚡ Standard**: Traditional implementation following tasks
- **🤝 Collaborative**: Mixed human-AI development
- **👤 Self**: Use spec as implementation guide

## Advanced Features

### Project Types & Adaptations

**Web Applications**: React/Vue frontends, Node.js/Python/Go backends, databases, APIs
**CLI Tools**: Command parsing, file I/O, configuration, cross-platform compatibility
**Libraries/SDKs**: Public APIs, documentation, versioning, compatibility
**Mobile Apps**: React Native/Flutter, platform-specific features, offline support
**Microservices**: Service boundaries, communication protocols, deployment strategies
**Desktop Apps**: Electron/Tauri, native integrations, distribution


## Quality Gates

### Requirements Quality

- ✅ All requirements use EARS format
- ✅ Requirements are testable and specific
- ✅ Edge cases and error conditions covered
- ✅ Non-functional requirements included

### Design Quality

- ✅ All requirements mapped to technical solutions
- ✅ Security considerations addressed
- ✅ Performance and scalability planned
- ✅ Integration points defined

### Task Quality

- ✅ Tasks follow TDD methodology
- ✅ Comprehensive test scenarios included
- ✅ Clear acceptance criteria defined
- ✅ Dependencies and blockers identified

## Common Usage Patterns

### New Project Development

#### Standard Workflow (Templates)

```bash
/pin:plan my-new-project
# [Interactive discussion to define features]
# [Review and approve project plan]
/pin:requirements 01-first-feature
# [Interactively create requirements]
/pin:design 01-first-feature
# [Review and approve design.md]
/pin:tasks 01-first-feature
# [Review and approve tasks.md]
/pin:execute 01-first-feature
# Begin implementation following task breakdown
```

#### Fast Workflow (Draft Requirements)

```bash
/pin:plan my-new-project all
# [Interactive discussion to define features]
# [Review project plan with draft requirements generated from discussion]
/pin:requirements 01-first-feature
# [Refine draft requirements]
/pin:design 01-first-feature
# [Generate design from requirements]
/pin:tasks 01-first-feature
# [Create tasks from design]
/pin:execute 01-first-feature
# Begin implementation
```



## Need More Help?

- **Complete Methodology**: See @.claude/CLAUDE.md for detailed guidance
- **Templates**: Use `@.claude/templates/` directory for reference formats
- **Command Details**: Each command file in `@.claude/commands/` contains specific instructions

## Context Management

💡 **Performance Tip**: This is a reference command that doesn't accumulate context. No need to use `/clear` after viewing help.

---

_Pindex: Transform complex features into manageable, well-tested implementations._
