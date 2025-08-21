---
description: Break down technical design into implementable TDD tasks for a specific feature.
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep, TodoRead, TodoWrite
---

# Implementation Task Breakdown

You are creating a comprehensive task breakdown from existing technical design following Test-Driven Development methodology and the Pindex approach.

## Your Task

Generate structured implementation tasks from existing design for the feature: **$ARGUMENTS**

## Feature Selection Logic (Standardized)

1. **IF a feature name/number is provided in `$ARGUMENTS`**:
   - Search for a matching directory in `features/` (exact or partial match)
   - If found, use that feature
   - If not found, list available features and ask for correct selection

2. **IF no feature name is provided**:
   - Use Glob to find all directories in `features/`
   - List them sorted numerically
   - Ask user to specify which feature to work on
   - If only one feature exists, still ask for confirmation (no auto-selection)

## Process

<analysis>
1. **Read project context**:
   - Check if `architecture.md` exists; if yes, read it to understand project structure
   - Check if `conventions.md` exists; if yes, read it to understand coding standards
   - If missing, use design.md as the source of truth for architecture decisions
   - Use available conventions to inform task structure and implementation approach
2. **Analyze reusability**:
   <reusability-scan>
   - Scan codebase for existing components, utilities, and modules that can be reused
   - Identify existing patterns, services, or handlers that the feature can leverage
   - Note any shared code that needs modification for compatibility
   </reusability-scan>
3. **Read methodology**: Reference `.claude/CLAUDE.md` for TDD guidance
4. **Locate design**: Find and read the design.md file in the selected feature directory
5. **Initialize or augment tasks**:
   <thinking>
   Consider task breakdown strategy:
   - What is the logical sequence of implementation?
   - Which tasks can be parallelized?
   - What are the critical path dependencies?
   - How to ensure testability at each step?
   - What constitutes "done" for each task?
   </thinking>
   
   - IF `tasks.md` does not exist:
     - Check if `.claude/templates/tasks.md` exists
     - If template exists: Initialize from template (replacing `[Feature Name]`)
     - If template missing: Warn user "Template tasks.md not found. Creating TDD task structure." and create structured task breakdown
   - ELSE, augment the existing `tasks.md` in-place. Ensure numeric task headings.
   - **Populate reusability sections for each task**:
     - Fill "Reused Components" with existing code that will be leveraged
     - Fill "Changes to Existing Code" with modifications needed to shared code
     - If no reusable components, explicitly state "None" rather than leaving placeholder
6. **Convention Updates**: If tasks reveal new patterns:
   - Note any new testing patterns or file structures needed
   - If significant, ask: "Should I update conventions.md with these patterns?"
   - Update if approved
7. **Seek approval**: Request explicit user approval before proceeding to implementation
</analysis>

## Template Usage

The task structure is defined in `.claude/templates/tasks.md`. The template provides:

- **Task Categories**: Flexible 7-8 task scaffold adaptable to feature needs
- **Standard Format**: Numeric headings (`## Task {N}: Title`)
- **TDD Structure**: Red-Green-Refactor cycle for each task
- **Acceptance Criteria**: EARS-based requirements
- **Test Scenarios**: Unit, integration, and edge cases
- **Dependencies**: Task sequencing and blockers
- **Reusability Sections**: Components to reuse and modifications needed

The template adapts to project type with specific task structures for:
- Web Applications
- CLI Tools
- Libraries/SDKs
- Mobile Apps
- Microservices

Each task includes completion tracking with `[IMPLEMENTED]` markers.

## Task Quality Gates

Ensure each task:

- [ ] Uses numeric heading format: `## Task {N}: {title}`
- [ ] Has clear acceptance criteria based on EARS requirements
- [ ] Includes specific TDD steps (Red-Green-Refactor)
- [ ] Lists key test scenarios (happy path plus 1–2 edge cases)
- [ ] Specifies dependencies and blockers
- [ ] Is small enough to complete in 2–4 hours
- [ ] Has measurable completion criteria

## TDD Guidelines

- **Start with tests**: Always write failing tests first
- **Minimal implementation**: Write just enough code to pass tests
- **Continuous refactoring**: Improve design while maintaining green tests
- **Test coverage**: Include unit, integration, and edge case tests
- **Acceptance criteria**: Map EARS requirements to test scenarios

## Key Principles

- Break down complex features into small, manageable tasks
- Ensure proper task sequencing and dependency management
- Include both positive and negative test scenarios
- Address error handling and edge cases explicitly
- Maintain traceability back to original requirements
- Upon completion, update the task heading with `[IMPLEMENTED]` and add a brief `**Completion**:` note directly under the heading in `tasks.md`

## Approval Gate

<output>
After creating tasks.md, ask:
"Implementation task breakdown complete for **[feature-name]**. Created [N] tasks following TDD methodology, covering [key areas]. Tasks are sequenced with proper dependencies and include comprehensive test scenarios. Ready to begin implementation with `/spec:execute [feature-name]`, or would you like to review and modify the task breakdown first?

💡 **Context Tip**: Start a fresh session with `/clear` before `/spec:execute` for optimal performance, especially for complex features."
</output>

## Implementation Options

When ready to proceed, present these choices:

1. **TDD Implementation**: Follow Red-Green-Refactor for each task
2. **Standard Implementation**: Implement without strict TDD process
3. **Self Implementation**: User implements using tasks as guide
4. **Collaborative**: Mixed approach with user and AI collaboration

## Next Steps

- User reviews task breakdown and approves/requests changes
- User selects implementation approach
- Begin structured development following approved tasks
- Maintain task tracking and progress updates

Now generate the implementation task breakdown based on existing design.
