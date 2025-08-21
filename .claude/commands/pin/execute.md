---
description: Execute the implementation plan from tasks.md for a specific feature.
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep, Bash, TodoRead, TodoWrite
---

# Execute Feature Implementation

## Feature: $ARGUMENTS

You are executing a feature implementation based on the structured specifications.

## Feature Selection Logic

**Follow standardized logic** (see `@.claude/templates/shared-logic.md` for details):
- With feature name: Find matching directory, ask for confirmation if not found
- Without feature name: List all features and ask for selection
- No auto-selection even with single feature

**Context Loading:**

- **Prerequisites Check** (STRICT validation from `@.claude/templates/shared-logic.md`):
  - Check if `@.claude/ARCHITECTURE.md` exists; if not, **STOP**: "⚠️ Project not initialized. Run `/pin:plan [description]` first to set up project architecture."
  - If exists, scan for placeholder patterns: `[e.g.,`, `[Type]`, `[Language]`, `TODO`, `TBD`
  - If placeholders found, **STOP**: "⚠️ Cannot proceed. Found incomplete configuration in @.claude/ARCHITECTURE.md. Please complete all fields or re-run `/pin:plan`."
  - Check if `@.claude/CONVENTIONS.md` exists; if not, **STOP**: "⚠️ Project not initialized. Run `/pin:plan [description]` first to set up conventions."
  - If exists, scan for placeholder patterns: `[e.g.,`, `[Tool]`, `[Framework]`, `TODO`, `TBD`
  - If placeholders found, **STOP**: "⚠️ Cannot proceed. Found incomplete configuration in @.claude/CONVENTIONS.md. Please complete all fields or re-run `/pin:plan`."
  - Check if `@.claude/SECURITY.md` exists; if yes, review OWASP checklist (not blocking if missing)
  - **Trust test runner**: Assume test runner was properly configured during `/pin:plan`
- **Feature Context** (read all upfront for complete understanding):
  - Read complete `requirements.md` to understand all functional and non-functional requirements
  - Read complete `design.md` to understand the full technical architecture and design decisions
  - Read complete `tasks.md` to understand the full implementation plan and task dependencies

## Your Task

Implement the feature by executing the plan in `tasks.md`.

## Core Philosophy: Minimal but Complete

**"Minimal" in TDD means the SIMPLEST COMPLETE SOLUTION**
- ✅ Minimal complexity, maximum functionality
- ✅ Simplest architecture that solves the problem
- ✅ Least code that meets all requirements
- ❌ NOT shortcuts, stubs, or placeholders
- ❌ NOT "we'll fix it later" implementations

Think: "What's the simplest way this would work in production?"

## Execution Process

## Production Code Standards

**Core Principle**: Implement complete, working functionality rather than placeholders or mocks.

**Key Requirements**:
- Fully functional features (not partial implementations)
- Real database connections and API integrations
- Proper authentication and authorization
- Comprehensive error handling and validation

**Implementation Guidelines**:

**✅ Good Practices**:
- Real database connections and queries
- Actual API integrations (authentication, payments, etc.)
- Environment variables for configuration
- Feature flags for optional functionality
- Mocks only in test files

**❌ Avoid**:
- Hardcoded fake data or responses
- TODO comments in implementation
- Console.log instead of real functionality
- Placeholder implementations

- **Preconditions**:
  - IF `tasks.md` does not exist in the selected feature directory:
    - INFORM the user: "No tasks.md found. Please run `/pin:tasks` to generate the implementation plan before executing."
    - STOP.
  - **Feature Dependency Check**:
    - Read `requirements.md` and check the "Dependencies" section
    - For each listed feature dependency:
      - Verify the dependent feature directory exists in `features/`
      - Check if dependent feature is implemented by looking for `tldr.md` with status "Complete"
      - If dependency is not implemented, **WARN**: "⚠️ Dependency [feature-name] is not yet complete. This may cause integration issues. Continue? (yes/no)"
      - If user says no, **STOP**: "Please implement dependencies first or update requirements to remove dependency."

0.  **Load Complete Feature Context**:
    <analysis>
    - Read complete `requirements.md` to understand all requirements
    - Read complete `design.md` to understand the full technical approach
    - Read complete `tasks.md` to understand the complete implementation plan
    - Identify integration points between tasks:
      - Data flow dependencies between components
      - API contracts that span multiple tasks
      - State management that crosses task boundaries
      - Shared services or utilities
    - This ensures proper understanding of how current work fits into the overall feature
    </analysis>

1.  **Auto-Resume and Progress**:
    - Determine progress by parsing `tasks.md` for headings `## Task {n}:` and markers `[IMPLEMENTED]`.
    - IF no headings matching `## Task {N}:` are found:
      - WARN the user that task headings may be malformed. They must follow the format: `## Task {N}: {Title}`.
      - SUGGEST running `/pin:tasks` again to regenerate properly formatted headings or manually correct the headings.
      - STOP.
    - IF all tasks are already marked `[IMPLEMENTED]`:
      - ASK: "All tasks are complete. Would you like to generate/update the TLDR summary? (yes/no)"
      - If yes: Generate TLDR with status "Complete"
      - If no: Exit
    - Otherwise, identify the next task without `[IMPLEMENTED]`. Announce progress, e.g., "Progress: {completed}/{total} tasks complete. Starting Task {N}...".

2.  **Analysis & Planning**:
    <thinking>
    For the current task, consider:
    - What is the complete, production-ready implementation needed?
    - How does this fit with existing architecture?
    - What patterns should be followed?
    - What edge cases need handling?
    - How to ensure backward compatibility?
    - Which previous tasks does this integrate with?
    - What integration tests will validate the connections?
    </thinking>

    - With full context loaded, analyze how the current task fits into the overall feature
    - Identify integration points with previously completed tasks
    - Plan integration test scenarios for task interactions
    - Create a concise plan for this single task, informed by complete requirements and design
    - Break it into small steps; prefer minimal process overhead (avoid unnecessary todos).
    - Identify implementation patterns aligned with `design.md` and @.claude/CONVENTIONS.md.

    ⚠️ **PRODUCTION CODE REQUIREMENTS**:
    - **NEVER** create placeholder implementations or mock data in production code
    - **NEVER** use hardcoded test data, fake responses, or stub functions
    - **NEVER** write "TODO: implement later" in implementation files
    - **ALWAYS** create fully functional, deployable code
    - **ALWAYS** implement real database connections, API calls, and business logic
    - **ONLY** use mocks/stubs in test files for external dependencies

3.  **Execute Current Task (TDD Cycle - PRODUCTION READY)**:
    - Follow the task order strictly—one task at a time.
    - For the current task, strictly follow the Red-Green-Refactor cycle:
      1.  **Red**: Write a failing test that corresponds to the acceptance criteria.
      2.  **Green**: Write the MINIMAL COMPLETE IMPLEMENTATION to make the test pass.

          ## 🔴 STOP - Production Code Check
          Before writing any code to a file, verify:
          - ❌ No "TODO" or "FIXME" comments in the code
          - ❌ No "return mockData" or hardcoded test responses
          - ❌ No "console.log" debug statements (use proper logging)
          - ❌ No fake database queries (like `SELECT * FROM fake_table`)
          - ❌ No placeholder API endpoints (like `/api/placeholder`)
          - ✅ Real database connections with actual queries
          - ✅ Real API integrations with proper error handling
          - ✅ Actual business logic, not simplified shortcuts

          If ANY prohibited patterns exist, STOP and regenerate the code properly.
          This check happens AFTER generating but BEFORE writing to files.

          ⚠️ **CRITICAL: "Minimal" means SIMPLEST COMPLETE SOLUTION, not INCOMPLETE**
          - **Minimal = Simplest code that FULLY solves the problem** (not partially)
          - **Minimal = Least complex architecture that MEETS ALL requirements** (not placeholder)
          - **Minimal = Fewest moving parts while being PRODUCTION-READY** (not mock)

          Think of it as: "What's the simplest way to correctly implement this feature?"
          NOT: "What's the quickest hack to make the test green?"

          **✅ CORRECT Green Phase Examples**:
          - Database operation: Real query with proper error handling
          - API endpoint: Fully functional with validation, auth, and response
          - UI component: Complete with all props, states, and event handlers
          - Service function: Full implementation with edge cases handled

          **❌ INCORRECT Green Phase Examples (NEVER DO THIS)**:
          - `return { data: 'mock data' }` // NO: This is a placeholder
          - `// TODO: implement database connection` // NO: This is incomplete
          - `setTimeout(() => resolve('fake'), 100)` // NO: This is a mock
          - `if (true) return hardcodedResponse` // NO: This is a stub

      3.  **Refactor**: Improve the code's structure and quality without changing its behavior.
          - **Validate**: Re-run the test to ensure refactoring didn't break functionality
          - If test fails after refactoring, fix immediately before proceeding
    - **After completing the current task**:
      1.  **RUN TESTS**: Execute tests and fix any failures before proceeding
      2.  **UPDATE TASK**: Mark as `[IMPLEMENTED]` in tasks.md with brief completion note
      3.  **ASK CONTINUATION**: "Task {N} complete. Continue to Task {N+1}? (yes/no)"
      4.  **CONTINUE** or **STOP** based on user response
    - Run validation checks after each small implementation step.

4.  **Verify Implementation**:
    - After completing tasks (all or partial), run the full test suite to ensure no regressions.
    - **Use test runner from @.claude/CONVENTIONS.md**:
      - Read the test runner command from the "Quick Commands" or "Testing" section
      - Execute the command directly (e.g., `npm test`, `bun test`, `pytest`, `go test ./...`)
      - If somehow missing/invalid, **STOP**: "⚠️ Project setup incomplete. Please re-run `/pin:plan` to properly configure the test runner."
      - Trust that `/pin:plan` validated it properly
    - Confirm that the final implementation meets all acceptance criteria from `requirements.md`.
    - Perform any final validation steps mentioned in the design or tasks.

5.  **Architecture/Convention Discovery**:
    - During implementation, if you establish new patterns or conventions:
    - Track new patterns discovered or created
    - After task completion, ask: "This implementation established [specific patterns]. Should I update @.claude/ARCHITECTURE.md or @.claude/CONVENTIONS.md?"
    - Update files if approved with meaningful additions

6.  **Generate TLDR Documentation** (when stopping):
    - **When**: After user stops execution (complete or partial) OR when all tasks are complete
    - **Actions**:
      - Create tldr.md from template if it doesn't exist
      - Populate with:
        * Overall "Status" field (Complete/Partial/MVP)
        * "Reason if partial" if not all tasks completed
        * Task completion timeline showing which tasks were completed
        * Summary of what was actually built vs planned
        * Files created/modified during implementation
        * Key technical decisions made
        * Test coverage achieved
        * "Last Updated" timestamp
    - **Note**: TLDR is generated ONCE when implementation stops, not progressively

## Context Management

💡 **Important**: After completing 2-3 tasks, consider starting a fresh session with `/clear` and re-running `/pin:execute` to continue. This prevents context overload and maintains performance.

## Minimal Implementation Examples

**Remember: Minimal means simplest COMPLETE solution, not incomplete solution**

| Task | ❌ Wrong "Minimal" (Stub/Mock) | ✅ Correct Minimal (Simple but Complete) |
|------|--------------------------------|------------------------------------------|
| User login | `if (username === 'admin') return true` | Real auth: hash check + JWT/session generation |
| Product listing API | `return [{ id: 1, name: 'Test' }]` | Database query with basic pagination |
| Email notifications | `console.log('Would send email')` | SendGrid/SES integration with templates |
| File upload | `return '/fake/path.jpg'` | S3/filesystem storage with validation |
| Search feature | `return items.filter(i => i.includes(q))` | Database full-text search or Elasticsearch |
| Payment processing | `return { paid: true }` | Stripe/PayPal integration with webhooks |

**The Pattern**: Start with the simplest architecture that actually works in production.
- For auth: Maybe just JWT, not OAuth + SAML + MFA on day one
- For search: Maybe PostgreSQL FTS, not Elasticsearch initially
- For files: Maybe local disk, not S3 initially
- BUT: Always real implementations, never fake ones

## Language-Specific Production Standards

Apply these standards based on the project language specified in @.claude/ARCHITECTURE.md and @.claude/CONVENTIONS.md.

**Note**: Language and stack were already determined during `/pin:plan` and used throughout design and tasks. This section simply enforces the standards for the chosen language during implementation.

### TypeScript/JavaScript
When implementing in TypeScript, enforce these critical standards:
- **NO `any` types**: Use `unknown` or proper types, enable `strict: true`
- **Handle null/undefined**: Use optional chaining (`?.`) and nullish coalescing (`??`)
- **Async/await properly**: Never ignore Promises, always handle errors with try/catch
- **Type guards over assertions**: Validate at runtime, don't just cast with `as`
- **Explicit return types**: Annotate function returns to catch missing returns
- **Strict null checks**: Ensure `strictNullChecks` is enabled
- **No `!` operator**: Avoid non-null assertions except when absolutely certain

### Python
When implementing in Python, enforce these standards:
- **Type hints everywhere**: Use proper type annotations (Python 3.9+)
- **Handle exceptions explicitly**: No bare `except:` clauses
- **Use context managers**: `with` statements for resources (files, connections)
- **Avoid mutable defaults**: Never use `[]` or `{}` as default parameters
- **Proper async/await**: Use `asyncio` correctly with error handling
- **Input validation**: Validate types and ranges, use `pydantic` for models
- **No global state**: Avoid global variables, use dependency injection

### General Standards (All Languages)
- **Validate all inputs**: Never trust external data
- **Log errors properly**: Include context, not sensitive data
- **Use dependency injection**: Avoid hard-coded dependencies
- **Test error paths**: Don't just test happy paths
- **Document assumptions**: Make implicit knowledge explicit
- **Follow project conventions**: Use established patterns in the codebase
- **Resource cleanup**: Always close files, connections, and streams
- **No hardcoded secrets**: Use environment variables or secret managers

Progress through each task systematically, ensuring quality at each step.
