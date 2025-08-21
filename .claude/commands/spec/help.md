---
description: Display help information for spec:driven development commands
allowed-tools: Read, TodoRead, TodoWrite
---

# Pindex Help

Quick reference for the Pindex development methodology commands.

## Available Commands

### Core Workflow Commands

#### `/spec:feature "Add password reset"`

**Purpose**: Add a single feature after initial release without full planning

- **Input**: A short feature description (used to derive the slug)
- **Output**: `features/{NN}-{slug}/requirements.md` seeded from templates
- **Usage**: Anytime you want to add a one-off feature
- **Next steps**: Proceed with `/spec:requirements {NN-slug}` → `/spec:design` → `/spec:tasks` → `/spec:execute`

#### `/spec:plan [project-description] [all]`

**Purpose**: Interactively break down a project into features through discussion.

- **Input**: A high-level description (starts interactive discussion), optional "all" flag
- **Process**: Interactive dialogue to understand project needs and define features
- **Output**:
  - Standard: Numbered directories with empty template `requirements.md`
  - With "all": Numbered directories with draft EARS requirements generated from the discussion
- **Usage**: Start of Phase 1 - Planning
- **Examples**:
  - `/spec:plan "A task management app"` - Interactive discussion → empty templates
  - `/spec:plan "A task management app" all` - Interactive discussion → draft requirements from that discussion

#### `/spec:requirements [feature-name]`

**Purpose**: Interactively detail or refine the EARS requirements for a specific feature.

- **Input**: Optional feature name (e.g., `01-project-setup`)
- **Output**: A detailed `features/[feature-name]/requirements.md`
- **Behavior**:
  - If draft requirements exist: Refines them and removes draft marker
  - If only template exists: Creates requirements from scratch
- **Usage**: Phase 2 - After planning is complete
- **Prerequisite**: Must have a feature directory created by `/spec:plan` or `/spec:feature`

#### `/spec:design`

**Purpose**: Generate technical design from existing requirements

- **Input**: Existing `requirements.md` in current feature context
- **Output**: `design.md` with architecture and implementation approach
- **Usage**: Phase 2 - After requirements approval
- **Prerequisite**: Must have approved requirements.md

#### `/spec:tasks`

**Purpose**: Break down design into TDD implementation tasks

- **Input**: Existing `design.md` in current feature context
- **Output**: `tasks.md` with structured implementation plan
- **Usage**: Phase 3 - After design approval
- **Prerequisite**: Must have approved design.md

#### `/spec:validate [feature-name]`

**Purpose**: Validate alignment between requirements, design, tasks, and TLDR

- **Input**: Optional feature name
- **Output**: Validation report with gap analysis
- **Usage**: Before implementation or to ensure consistency
- **Features**: Cross-document validation, TLDR checking, architecture compliance

#### `/spec:execute [feature-name]`

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

#### `/spec:check`

**Purpose**: Perform comprehensive framework health check

- **Input**: None
- **Output**: Detailed validation report with installation status
- **Usage**: Verify framework integrity and diagnose issues
- **Features**: Component validation, syntax checking, recovery guidance

#### `/spec:list`

**Purpose**: List all features with documentation status

- **Input**: None
- **Output**: Table showing features and their specification status
- **Usage**: To see project overview
- **Features**: Shows Req/Des/Tasks/TLDR status for each feature

#### `/spec:status`

**Purpose**: Show comprehensive implementation progress

- **Input**: None
- **Output**: Detailed progress table with completion percentages
- **Usage**: To track project implementation status
- **Features**: Task counts, completion percentages, status indicators

#### `/spec:check`

**Purpose**: Validate framework installation and project consistency

- **Input**: None
- **Output**: Health check report with recommendations
- **Usage**: To verify framework integrity or diagnose issues
- **Features**: Template validation, command verification, feature structure check

#### `/spec:advanced [feature-name]`

**Purpose**: Apply enterprise-grade analysis with threat modeling and risk assessment

- **Input**: Existing specifications in current feature context
- **Output**: Enhanced specifications with security, scalability, and risk analysis
- **Usage**: Can be used at any phase for comprehensive analysis
- **Features**: STRIDE threat modeling, performance analysis, edge case identification

#### `/spec:help`

**Purpose**: Display this help information

- **Input**: None
- **Output**: Command reference and usage guide
- **Usage**: Anytime you need command information

## Workflow Overview

```
1. /spec:plan [project]      →  Feature List     →  [Approval Gate]
2. /spec:requirements [feature] →  requirements.md  →  [Approval Gate]
3. /spec:design               →  design.md        →  [Approval Gate]
4. /spec:tasks                →  tasks.md         →  [Approval Gate]
5. Implementation             →  Working Code     →  [Testing & Deploy]
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

#### `.claude/templates/requirements.md`
- **Purpose**: EARS-formatted requirements structure
- **Sections**: Functional, non-functional, constraints, acceptance criteria
- **Adapts to**: Project type (Web, CLI, Library, Mobile, Service)
- **Used by**: `/spec:plan`, `/spec:requirements`, `/spec:feature`

#### `.claude/templates/design.md`
- **Purpose**: Technical design document structure
- **Sections**: Architecture, data design, API, security, performance
- **Adapts to**: Architecture pattern and tech stack
- **Used by**: `/spec:design`

#### `.claude/templates/tasks.md`
- **Purpose**: TDD task breakdown structure
- **Format**: Numeric headings with Red-Green-Refactor cycles
- **Sections**: 7-8 flexible task categories with reusability tracking
- **Adapts to**: Project type with specific task patterns
- **Used by**: `/spec:tasks`

#### `.claude/templates/tldr.md`
- **Purpose**: Implementation summary documentation
- **Sections**: Completion status, what was built, incomplete items, decisions, testing
- **Generated**: When implementation stops (complete or partial)
- **Tracks**: Tasks completed vs total, implementation status
- **Used by**: `/spec:execute`

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

### Tech Stack Options (in /spec:design)

1. Full-Stack JavaScript (Node.js + React/Vue)
2. Python + Modern Frontend (FastAPI/Django + React/Vue)
3. Cloud-Native Microservices (Kubernetes + API Gateway)
4. Enterprise Java/C# (Spring Boot/.NET)
5. Custom/Other (User-defined stack)

### Advanced Analysis (in /spec:advanced)

- **STRIDE Threat Modeling**: Security vulnerability analysis
- **Risk Assessment**: Probability, impact, and mitigation strategies
- **Scalability Analysis**: Performance bottlenecks and scaling strategies
- **Edge Case Analysis**: Boundary conditions and error scenarios

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
/spec:plan my-new-project
# [Interactive discussion to define features]
# [Review and approve project plan]
/spec:requirements 01-first-feature
# [Interactively create requirements]
/spec:design 01-first-feature
# [Review and approve design.md]
/spec:tasks 01-first-feature
# [Review and approve tasks.md]
/spec:execute 01-first-feature
# Begin implementation following task breakdown
```

#### Fast Workflow (Draft Requirements)

```bash
/spec:plan my-new-project all
# [Interactive discussion to define features]
# [Review project plan with draft requirements generated from discussion]
/spec:requirements 01-first-feature
# [Refine draft requirements]
/spec:design 01-first-feature
# [Generate design from requirements]
/spec:tasks 01-first-feature
# [Create tasks from design]
/spec:execute 01-first-feature
# Begin implementation
```

### Enhanced Security Analysis

```bash
/spec:plan secure-api-gateway-project
# [Approve project plan]
/spec:requirements 01-secure-api-gateway
# [Approve requirements]
/spec:design
# [Approve design]
/spec:advanced  # Add threat modeling and security analysis
# [Review enhanced specifications]
/spec:tasks
```

### Existing Feature Enhancement

```bash
# Navigate to existing feature directory
/spec:advanced  # Analyze existing specifications
# Review security, performance, and risk recommendations
# Update specifications as needed
```

## Need More Help?

- **Complete Methodology**: See `.claude/CLAUDE.md` for detailed guidance
- **Templates**: Use `.claude/templates/` directory for reference formats
- **Command Details**: Each command file in `.claude/commands/` contains specific instructions

---

_Pindex: Transform complex features into manageable, well-tested implementations._
