# Pindex - Complete Reference

This is the authoritative source for Pindex - a universal, architecture-agnostic framework for structured software development with AI assistance.

## Table of Contents

1. [Core Philosophy](#core-philosophy)
2. [Universal Workflow](#universal-workflow)
3. [Architecture Adaptation](#architecture-adaptation)
4. [Command Reference](#command-reference)
5. [EARS Requirements Format](#ears-requirements-format)
6. [Test-Driven Development](#test-driven-development)
7. [Quality Gates](#quality-gates)
8. [Advanced Features](#advanced-features)
9. [Best Practices](#best-practices)

## Core Philosophy

### Universal Principles

This framework is designed to work with:

- **Any Language**: JavaScript, Python, Go, Java, C#, Ruby, Rust, etc.
- **Any Architecture**: Monolithic, Microservices, Serverless, Event-driven, MVC, Clean/Hexagonal, etc.
- **Any Project State**: Greenfield, Legacy, Brownfield, Refactoring
- **Any Development Style**: Object-oriented, Functional, Procedural, Mixed
- **Any Platform**: Web, Mobile, Desktop, CLI, Embedded, Cloud-native

### Adaptation Over Prescription

Rather than enforcing specific patterns, the framework:

1. **Discovers** existing project structure and conventions
2. **Adapts** to current architecture and practices
3. **Suggests** improvements while respecting constraints
4. **Generates** appropriate patterns for new projects

## Universal Workflow

### 6-Phase Development Cycle

```
┌─────────┐     ┌──────────────┐     ┌────────┐     ┌───────┐     ┌──────────┐     ┌──────────┐
│ PLAN    │ --> │ REQUIREMENTS │ --> │ DESIGN │ --> │ TASKS │ --> │ VALIDATE │ --> │ EXECUTE  │
└─────────┘     └──────────────┘     └────────┘     └───────┘     └──────────┘     └──────────┘
     ↓                  ↓                 ↓              ↓              ↓              ↓
  Features          WHAT needs         HOW to        Breaking       Ensure        Implement
  Breakdown         to be built        build it      it down      Alignment      with TDD
```

### Phase 1: Planning

**Command**: `/spec:plan [project-description] [all]`

**Key Clarification**: The "planning discussion" happens WITHIN this command through interactive dialogue. The "all" flag generates requirements from that discussion.

**Process**:

1. Interactive discussion to understand project goals
2. Discovers existing project structure (if applicable)
3. Proposes and refines feature breakdown through dialogue
4. Creates feature directories based on approved plan
   - Standard mode: Seeds with empty template requirements
   - With "all" flag: Generates draft EARS requirements from the discussion marked with `<!-- DRAFT -->`

**For Existing Codebases**:

- Scans current architecture
- Identifies patterns and conventions
- Suggests features that align with existing structure

### Phase 2: Requirements

**Command**: `/spec:requirements [feature-name]`

**Process**:

1. Interactive requirements gathering
2. If draft requirements exist (from `/spec:plan ... all`):
   - Refines and validates draft requirements
   - Removes draft marker when finalized
3. EARS format specification
4. Technology-agnostic requirements
5. Clear acceptance criteria

**Adapts To**:

- Domain-specific terminology
- Existing system constraints
- Integration requirements
- Current tech stack limitations

### Phase 3: Design

**Command**: `/spec:design`

**Process**:

1. Reads existing project architecture
2. Proposes technical approach aligned with current patterns
3. Offers tech stack options for new projects
4. Creates design that fits project context

**Flexibility**:

- Respects existing architecture patterns
- Suggests compatible technologies
- Adapts to team preferences
- Considers technical debt and migration paths

### Phase 4: Tasks

**Command**: `/spec:tasks`

**Process**:

1. Breaks design into implementable steps
2. Adapts task structure to project type
3. Includes TDD approach suitable for tech stack
4. Considers existing test frameworks

**Task Categories** (adapted to project needs):

- Infrastructure/Setup (if needed)
- Core Implementation
- Integration Points
- Testing Strategy
- Documentation

### Phase 5: Validation

**Command**: `/spec:validate [feature-name]`

**Process**:

1. Cross-validates all specifications
2. Ensures requirements → design → tasks alignment
3. Verifies architecture and convention compliance
4. Identifies and reports gaps
5. Optionally fixes inconsistencies

**Benefits**:

- Catches misalignments before implementation
- Ensures complete coverage
- Maintains architectural consistency
- Reduces implementation errors

### Phase 6: Implementation

**Command**: `/spec:execute [feature-name]`

**TLDR Generation**: 
- Generated when implementation stops (complete or partial)
- Documents what was actually built vs planned
- Tracks completed tasks vs total tasks
- Includes reason for stopping if partial

**Options**:

1. **TDD Implementation**: Red-Green-Refactor cycle
2. **Standard Implementation**: Traditional development
3. **Collaborative**: Human-AI pair programming
4. **Self-Implementation**: Use specs as guide

## Architecture Adaptation

### Project Discovery

When starting with an existing codebase, the framework:

1. **Analyzes Structure**:
   - File organization patterns
   - Naming conventions
   - Architecture style
   - Technology stack
   - Test frameworks

2. **Identifies Patterns**:
   - Design patterns in use
   - Coding standards
   - Documentation style
   - Build/deployment processes

3. **Generates Context Files**:
   - Creates `architecture.md` describing discovered structure
   - Creates `conventions.md` documenting observed patterns
   - Adapts templates to match project style

### Architecture Pattern Support

The framework adapts to common patterns:

#### Monolithic Applications

- Single codebase structure
- Shared module organization
- Centralized configuration

#### Microservices

- Service boundaries
- Inter-service communication
- Independent deployments

#### Serverless

- Function-based organization
- Event-driven patterns
- Cloud service integration

#### MVC/MVP/MVVM

- Model-View separation
- Controller/Presenter patterns
- Data binding approaches

#### Clean/Hexagonal Architecture

- Domain-driven design
- Port and adapter patterns
- Dependency inversion

#### Event-Driven Architecture

- Event sourcing patterns
- CQRS implementation
- Message queue integration

### Technology Stack Flexibility

The framework supports any stack:

#### Frontend

- React, Vue, Angular, Svelte
- Vanilla JavaScript, TypeScript
- Mobile (React Native, Flutter)
- Desktop (Electron, Tauri)

#### Backend

- Node.js, Python, Go, Java, C#
- REST, GraphQL, gRPC
- Serverless functions
- Traditional servers

#### Databases

- SQL (PostgreSQL, MySQL, SQLite)
- NoSQL (MongoDB, DynamoDB, Redis)
- Graph (Neo4j, Neptune)
- Time-series (InfluxDB, TimescaleDB)

#### Testing

- Unit test frameworks (Jest, pytest, Go test, JUnit)
- E2E frameworks (Playwright, Cypress, Selenium)
- BDD frameworks (Cucumber, Behave)

## Command Purpose Clarifications

### Validation Commands - Two Different Types

1. **`/spec:check` - Framework Health Check**
   - Validates Pindex framework installation
   - Checks for missing files and templates
   - Verifies command structure and frontmatter
   - Ensures framework integrity
   - **Use when**: Framework seems broken or after updates

2. **`/spec:validate` - Feature Specification Validation**
   - Validates feature specification alignment
   - Ensures requirements→design→tasks consistency
   - Checks architecture compliance
   - Identifies gaps in specifications
   - **Use when**: Before implementation or to verify specs

These serve completely different purposes and should not be confused.

## Command Reference

### Core Workflow Commands

#### `/spec:plan [description] [all]`

Breaks down project into features, discovers architecture

- Without "all": Creates structure with template requirements
- With "all": Generates draft EARS requirements from the interactive discussion

#### `/spec:requirements [feature-name]`

Details EARS-formatted requirements interactively

#### `/spec:design [feature-name]`

Generates technical design adapted to project

#### `/spec:tasks [feature-name]`

Creates TDD task breakdown

#### `/spec:validate [feature-name]`

Validates alignment between requirements, design, and tasks

#### `/spec:execute [feature-name]`

Implements tasks with chosen approach

### Utility Commands

#### `/spec:feature [description]`

Adds single feature to existing project

#### `/spec:list`

Lists all features with documentation status

#### `/spec:status`

Shows comprehensive implementation progress

#### `/spec:check`

Validates framework installation and project consistency

#### `/spec:advanced [feature-name]`

Enterprise-grade analysis (security, performance, risk)

#### `/spec:help`

Displays comprehensive help

### Feature Selection

All feature-specific commands accept an optional feature name:

- With argument: Uses specified feature
- Without argument: Lists available features and asks for selection
- No auto-selection: Always requires explicit confirmation

## EARS Requirements Format

### Universal Requirement Templates

EARS (Easy Approach to Requirements Syntax) works for any project type:

1. **Ubiquitous**: `The system SHALL [requirement]`
   - Basic functional requirements
   - Example: "The system SHALL persist user preferences"

2. **Event-Driven**: `WHEN [trigger] THEN the system SHALL [response]`
   - User interactions, system events
   - Example: "WHEN a user submits a form THEN the system SHALL validate inputs"

3. **State-Driven**: `WHILE [state] the system SHALL [requirement]`
   - Ongoing conditions, modes
   - Example: "WHILE in maintenance mode the system SHALL reject new transactions"

4. **Conditional**: `IF [condition] THEN the system SHALL [requirement]`
   - Business rules, edge cases
   - Example: "IF payment fails THEN the system SHALL retry with exponential backoff"

5. **Optional**: `WHERE [feature included] the system SHALL [requirement]`
   - Feature flags, optional modules
   - Example: "WHERE analytics is enabled the system SHALL track user interactions"

### Best Practices

- **Technology-agnostic**: Avoid implementation details in requirements
- **Testable**: Each requirement should be verifiable
- **Atomic**: One requirement per statement
- **Specific**: Use measurable criteria ("within 2 seconds" not "quickly")
- **Complete**: Cover happy paths, edge cases, and error conditions

## Test-Driven Development

### Adaptive TDD Approach

The framework adapts TDD to your technology stack:

#### Red-Green-Refactor Cycle

1. **Red Phase** (Write Failing Test):
   - Adapts to your test framework
   - Uses project's assertion style
   - Follows existing test patterns

2. **Green Phase** (Make Test Pass):
   - Minimal implementation
   - Respects project conventions
   - Uses existing utilities/helpers

3. **Refactor Phase** (Improve Code):
   - Applies project's design patterns
   - Maintains architectural boundaries
   - Follows team's code style

### Test Strategy Adaptation

#### For Web Applications

- Component tests (React Testing Library, Vue Test Utils)
- API endpoint tests
- E2E user journey tests

#### For CLI Tools

- Command parsing tests
- Output formatting tests
- Integration tests with mock filesystem

#### For Libraries

- Public API tests
- Edge case handling
- Performance benchmarks

#### For Microservices

- Service contract tests
- Integration tests with mocks
- End-to-end workflow tests

## Quality Gates

### Phase Validation Criteria

Quality gates adapt to project context but maintain core validations:

#### Requirements Quality

- ✅ EARS format compliance
- ✅ Testable and measurable
- ✅ Technology-agnostic
- ✅ Complete coverage
- ✅ Aligned with project constraints

#### Design Quality

- ✅ Addresses all requirements
- ✅ Fits existing architecture
- ✅ Feasible with current resources
- ✅ Scalability considered
- ✅ Security addressed

#### Task Quality

- ✅ Appropriately granular
- ✅ Proper dependencies
- ✅ Test scenarios defined
- ✅ Fits team workflow
- ✅ Clear acceptance criteria

#### Implementation Quality

- ✅ Tests pass
- ✅ Code follows conventions
- ✅ Documentation updated
- ✅ Integration verified
- ✅ Performance acceptable

## Advanced Features

### Enhanced Analysis Mode

**Command**: `/spec:advanced`

Provides enterprise-grade analysis:

#### Security Analysis (STRIDE)

- **Spoofing**: Identity verification
- **Tampering**: Data integrity
- **Repudiation**: Audit trails
- **Information Disclosure**: Data protection
- **Denial of Service**: Availability
- **Elevation of Privilege**: Access control

#### Performance Analysis

- Bottleneck identification
- Scalability assessment
- Resource optimization
- Caching strategies
- Load distribution

#### Risk Assessment

- Technical risks
- Business risks
- Mitigation strategies
- Contingency planning

### Integration Support

#### External Specifications

- OpenAPI/Swagger import
- GraphQL schema integration
- Protocol buffer definitions
- Database schemas

#### Version Control Integration

- Feature branch workflows
- Commit message templates
- PR/MR descriptions
- Change tracking

## Best Practices

### Working with Existing Codebases

1. **Start with Discovery**:
   - Let framework analyze existing structure
   - Review generated architecture.md
   - Validate discovered conventions

2. **Respect Existing Patterns**:
   - Align new features with current architecture
   - Use established naming conventions
   - Follow team's coding standards

3. **Incremental Adoption**:
   - Start with single feature
   - Validate approach with team
   - Adjust process as needed

### Working on New Projects

1. **Define Architecture Early**:
   - Choose architecture pattern in planning phase
   - Document decisions in architecture.md
   - Establish conventions upfront

2. **Start Simple**:
   - Begin with core features
   - Add complexity gradually
   - Refactor as patterns emerge

3. **Maintain Flexibility**:
   - Avoid over-engineering
   - Keep options open
   - Refactor when clear patterns emerge

### Context Management

1. **Keep Context Focused**:
   - Work on one feature at a time
   - Reset when switching contexts
   - Start fresh sessions for new phases

2. **Performance Optimization**:
   - Start new sessions between major phases
   - Minimize context size
   - Focus on current task

### Team Collaboration

1. **Explicit Approval Gates**:
   - Review at each phase
   - Get team buy-in
   - Document decisions

2. **Knowledge Sharing**:
   - Update documentation
   - Share architectural decisions
   - Maintain clear commit history

## File Structure

### Framework Files (Static)

```
.claude/
├── CLAUDE.md                    # This complete reference
├── commands/spec/               # Command definitions
│   ├── plan.md                 # Planning command
│   ├── requirements.md         # Requirements command
│   ├── design.md              # Design command
│   ├── tasks.md               # Tasks command
│   ├── validate.md            # Validation command
│   ├── execute.md             # Execution command
│   ├── feature.md             # Single feature command
│   ├── advanced.md            # Advanced analysis
│   ├── list.md                # List features with status
│   ├── status.md              # Show detailed progress
│   ├── check.md               # Framework consistency check
│   └── help.md                # Help command
└── templates/                   # Adaptive templates
    ├── requirements.md         # Requirements template
    ├── design.md              # Design template
    ├── tasks.md               # Tasks template
    └── tldr.md                # Implementation summary template
```

### Project Files (Generated/Discovered)

```
project-root/
├── CLAUDE.md                    # Quick reference (static)
├── architecture.md              # Discovered/generated architecture
├── conventions.md               # Discovered/generated conventions
└── features/                    # Feature specifications
    └── [NN-feature-name]/
        ├── requirements.md      # EARS requirements
        ├── design.md           # Technical design
        ├── tasks.md            # Implementation tasks
        └── tldr.md             # Implementation summary (after execution)
```

## XML Tags and Structured Reasoning

The framework now uses XML tags for structured prompting:

- `<analysis>` - For analyzing existing code and context
- `<thinking>` - For step-by-step reasoning about decisions
- `<decision>` - For documenting chosen approaches
- `<output>` - For final formatted responses
- `<reusability-scan>` - For identifying reusable components
- `<requirements-generation>` - For creating EARS requirements

## Thinking Commands

Internal reasoning prompts for complex decisions:

- `think` - Basic reasoning for simple decisions
- `think hard` - Extended analysis for design choices
- `think harder` - Deep analysis for complex problems
- `ultrathink` - Maximum depth for critical decisions

Apply at key decision points:

- Architecture pattern selection
- Technology stack choices
- Complex requirement analysis
- Security and performance optimization
- Risk assessment and mitigation

## Context Management Guidelines

### Performance Optimization

1. **Use `/clear` strategically**:
   - Between major workflow phases
   - After 2-3 tasks in `/spec:execute`
   - When switching between features

2. **Fresh sessions for complex work**:
   - Start new session for each feature's implementation
   - Reset when moving from planning to execution

3. **Visual workflows** (for UI features):
   - Provide screenshots for validation
   - Use iterative visual feedback
   - Document UI decisions in TLDR

## Enhanced Features

### Comprehensive Status Tracking

- `/spec:list` shows documentation status for each feature
- `/spec:status` displays detailed progress with file indicators
- TLDR documentation tracks what was actually built vs planned

### Framework Validation

- `/spec:check` validates framework installation integrity
- Performs health checks on all components
- Identifies missing files and configuration issues
- Provides recovery recommendations
- Template validation ensures graceful fallback if templates missing
- Cross-reference checking between commands and documentation

### Reusability Analysis

- `/spec:tasks` identifies and documents reusable components
- Tracks modifications to shared code
- Ensures compatibility with existing codebase

### Implementation Documentation

- TLDR generation when implementation stops (complete or partial)
- Documents completed vs planned tasks (e.g., "3 of 6 tasks")
- Tracks files modified, decisions made, test coverage
- Permanent record of what was actually built
- Status tracking: Complete/Partial/MVP

## Initialize-or-Augment Policy

The framework follows smart file management:

1. **Templates as Starting Points**:
   - Used once when file doesn't exist
   - Never overwrites existing content
   - Augments with missing sections

2. **Preserve User Content**:
   - User modifications are sacred
   - Additions are clearly marked
   - Deletions require explicit approval

3. **Intelligent Merging**:
   - Detects existing sections
   - Adds missing components
   - Maintains user customizations

---

Pindex provides structure without prescription, enabling high-quality software development across any technology stack, architecture pattern, or project type. It maintains human oversight while leveraging AI capabilities for accelerated, reliable development.