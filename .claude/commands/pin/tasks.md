---
description: Break down technical design into implementable TDD tasks for a specific feature.
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep, TodoRead, TodoWrite
---

# Implementation Task Breakdown

You are creating a comprehensive task breakdown from existing technical design following Test-Driven Development methodology and the Pindex approach.

## Your Task

Generate structured implementation tasks from existing design for the feature: **$ARGUMENTS**

## Feature Selection Logic

**Follow standardized logic** (see `@.claude/templates/shared-logic.md` for details):
- With feature name: Find matching directory, ask for confirmation if not found
- Without feature name: List all features and ask for selection
- No auto-selection even with single feature

## Process

<analysis>
1. **Prerequisites Check** (STRICT validation from `@.claude/templates/shared-logic.md`):
   - Check if @.claude/ARCHITECTURE.md exists; if not, **STOP**: "⚠️ Project not initialized. Run `/pin:plan [description]` first to set up project architecture."
   - If exists, scan for placeholder patterns: `[e.g.,`, `[Type]`, `[Language]`, `TODO`, `TBD`
   - If placeholders found, **STOP**: "⚠️ Cannot proceed. Found incomplete configuration in @.claude/ARCHITECTURE.md. Please complete all fields or re-run `/pin:plan`."
   
   - Check if @.claude/CONVENTIONS.md exists; if not, **STOP**: "⚠️ Project not initialized. Run `/pin:plan [description]` first to set up conventions."
   - If exists, scan for placeholder patterns: `[e.g.,`, `[Tool]`, `[Framework]`, `TODO`, `TBD`
   - If placeholders found, **STOP**: "⚠️ Cannot proceed. Found incomplete configuration in @.claude/CONVENTIONS.md. Please complete all fields or re-run `/pin:plan`."
   
   - Check if @.claude/SECURITY.md exists; if yes, review OWASP checklist (not blocking if missing)
   - Trust that test runner was properly configured during `/pin:plan`
   - Apply conventions to task structure:
     * Use specified naming conventions for files/functions
     * Follow test organization pattern (alongside or separate)
     * Apply commit message format for task completion
     * Ensure tasks align with Definition of Done criteria
2. **Analyze reusability**:
   <reusability-scan>
   - Scan codebase for existing components, utilities, and modules that can be reused
   - Identify existing patterns, services, or handlers that the feature can leverage
   - Note any shared code that needs modification for compatibility
   </reusability-scan>
3. **Read methodology**: Reference @.claude/CLAUDE.md for TDD guidance
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
   
   🚨 **CRITICAL: PRODUCTION TASK STANDARDS**
   This framework generates PRODUCTION-READY TASKS, not learning exercises. Every task must:
   - **REAL IMPLEMENTATION**: Tasks that build actual functionality, not mocks
   - **COMPLETE TESTS**: Real test scenarios, not placeholder tests
   - **NO STUBS**: Never suggest "mock data" or "stub implementation"
   - **ACTIONABLE**: Specific enough to implement without ambiguity
   
   **Examples of what this means**:
   | ❌ WRONG (Never Do This) | ✅ CORRECT (Always Do This) |
   |--------------------------|-----------------------------|
   | "Create login endpoint with mock response" | "Implement login with database authentication" |
   | "Add placeholder for payment processing" | "Integrate Stripe payment processing with webhooks" |
   | "Create test data structure" | "Implement production database schema with migrations" |
   | "Stub out email service" | "Integrate SendGrid/SES for transactional emails" |
   | "Mock authentication for testing" | "Implement JWT authentication with refresh tokens" |
   
   - IF `tasks.md` does not exist in the feature directory:
     - Check if `@.claude/templates/tasks.md` exists
     - If template exists: 
       - Use Write tool to create `features/[feature]/tasks.md` from template
       - Replace `[Feature Name]` placeholder with actual feature name
       - Fill in all task details based on the design
       - DO NOT leave any placeholders - populate with specific implementation tasks
       - ENSURE no task suggests mocks, stubs, or placeholder implementations
     - **Template Fallback** (using standardized behavior): Check for `@.claude/templates/tasks.md`, warn and create basic structure if missing
   - ELSE (if tasks.md already exists):
     - Use Edit/MultiEdit to augment existing content
     - Ensure numeric task headings (## Task N: Title)
     - Replace any tasks suggesting mocks or stubs with real implementations
   - **Populate all sections with concrete values**:
     - Fill "Reused Components" with existing code that will be leveraged
     - Fill "Changes to Existing Code" with modifications needed to shared code
     - If no reusable components, explicitly state "None" rather than leaving placeholder
     - Ensure all test scenarios test real functionality, not mocks
6. **Convention Updates**: If tasks reveal new patterns:
   - Note any new testing patterns or file structures needed
   - If significant, ask: "Should I update @.claude/CONVENTIONS.md with these patterns?"
   - Update if approved
7. **Seek approval**: Request explicit user approval before proceeding to implementation
</analysis>

## Template Usage

The task structure is defined in `@.claude/templates/tasks.md`. The template provides:

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
- [ ] Includes specific TDD steps (Red-Green-Refactor) for REAL implementation
- [ ] Lists key test scenarios that test actual functionality (not mocks)
- [ ] Specifies dependencies and blockers
- [ ] Is small enough to complete in 2–4 hours
- [ ] Has measurable completion criteria
- [ ] NEVER suggests placeholder, mock, or stub implementations
- [ ] ALWAYS describes production-ready functionality
- [ ] Tests verify real behavior, not fake responses

## TDD Guidelines (from @.claude/CONVENTIONS.md)

- **Start with tests**: Always write failing tests first for REAL functionality
- **Test naming**: Follow pattern from @.claude/CONVENTIONS.md (e.g., "should [expected] when [condition]")
- **Test structure**: Use AAA pattern (Arrange-Act-Assert) from @.claude/CONVENTIONS.md
- **Minimal implementation**: Write the SIMPLEST COMPLETE SOLUTION (not mock/stub)
  - "Minimal" means least complex working code, NOT incomplete code
  - Example: Simple auth = real JWT with database, not `return true`
- **Continuous refactoring**: Improve design while maintaining green tests
- **Test coverage**: Meet targets specified in @.claude/CONVENTIONS.md (80%/90%/100%)
- **Test organization**: Follow project choice (alongside source or separate directory)
- **Acceptance criteria**: Map EARS requirements to test scenarios
- **NO TEST MOCKS IN PRODUCTION CODE**: Only mock external services in test files

## Key Principles

- Break down complex features into small, manageable PRODUCTION tasks
- Ensure proper task sequencing and dependency management
- Include both positive and negative test scenarios for REAL functionality
- Address error handling and edge cases with ACTUAL error handling code
- Maintain traceability back to original requirements
- Upon completion, update the task heading with `[IMPLEMENTED]` and add a brief `**Completion**:` note directly under the heading in `tasks.md`
- **NEVER** create tasks that implement mocks, stubs, or "temporary" solutions
- **ALWAYS** specify tasks that result in deployable, production-ready code
- **ENSURE** every task contributes to the actual working system

## Approval Gate

<output>
After creating tasks.md, ask:
"Implementation task breakdown complete for **[feature-name]**. Created [N] tasks following TDD methodology, covering [key areas]. Tasks are sequenced with proper dependencies and include comprehensive test scenarios. Ready to begin implementation with `/pin:execute [feature-name]`, or would you like to review and modify the task breakdown first?

💡 **Context Tip**: Start a fresh session with `/clear` before `/pin:execute` for optimal performance, especially for complex features."
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
