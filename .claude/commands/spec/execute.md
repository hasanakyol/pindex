---
description: Execute the implementation plan from tasks.md for a specific feature.
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep, Bash, TodoRead, TodoWrite
---

# Execute Feature Implementation

## Feature: $ARGUMENTS

You are executing a feature implementation based on the structured specifications.

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

**Context Loading:**

- **Project Context**:
  - Check if `architecture.md` exists; if yes, read it to understand project structure
  - Check if `conventions.md` exists; if yes, read it to understand coding standards
  - If missing, use design.md and establish conventions during implementation
- **Feature Context** (read all upfront for complete understanding):
  - Read complete `requirements.md` to understand all functional and non-functional requirements
  - Read complete `design.md` to understand the full technical architecture and design decisions
  - Read complete `tasks.md` to understand the full implementation plan and task dependencies

## Your Task

Implement the feature by executing the plan in `tasks.md`.

## Execution Process

- **Preconditions**:
  - IF `tasks.md` does not exist in the selected feature directory:
    - INFORM the user: "No tasks.md found. Please run `/spec:tasks` to generate the implementation plan before executing."
    - STOP.

0.  **Load Complete Feature Context**:
    <analysis>
    - Read complete `requirements.md` to understand all requirements
    - Read complete `design.md` to understand the full technical approach
    - Read complete `tasks.md` to understand the complete implementation plan
    - This ensures proper understanding of how current work fits into the overall feature
    </analysis>

1.  **Auto-Resume and Progress**:
    - Determine progress by parsing `tasks.md` for headings `## Task {n}:` and markers `[IMPLEMENTED]`.
    - IF no headings matching `## Task {N}:` are found:
      - WARN the user that task headings may be malformed. They must follow the format: `## Task {N}: {Title}`.
      - SUGGEST running `/spec:tasks` again to regenerate properly formatted headings or manually correct the headings.
      - STOP.
    - IF all tasks are already marked `[IMPLEMENTED]`:
      - ASK: "All tasks are complete. Would you like to generate/update the TLDR summary? (yes/no)"
      - If yes: Generate TLDR with status "Complete"
      - If no: Exit
    - Otherwise, identify the next task without `[IMPLEMENTED]`. Announce progress, e.g., "Progress: {completed}/{total} tasks complete. Starting Task {N}...".

2.  **Analysis & Planning**:
    <thinking>
    For the current task, consider:
    - What is the minimal code to make tests pass?
    - How does this fit with existing architecture?
    - What patterns should be followed?
    - What edge cases need handling?
    - How to ensure backward compatibility?
    </thinking>
    
    - With full context loaded, analyze how the current task fits into the overall feature
    - Create a concise plan for this single task, informed by complete requirements and design
    - Break it into small steps; prefer minimal process overhead (avoid unnecessary todos).
    - Identify implementation patterns aligned with `design.md` and `conventions.md`.

3.  **Execute Current Task (TDD Cycle)**:
    - Follow the task order strictly—one task at a time.
    - For the current task, strictly follow the Red-Green-Refactor cycle:
      1.  **Red**: Write a failing test that corresponds to the acceptance criteria.
      2.  **Green**: Write the minimum amount of code required to make the test pass.
      3.  **Refactor**: Improve the code's structure and quality without changing its behavior.
    - **After completing the current task**:
      1.  **RUN TESTS**: Execute the full test suite to ensure no regressions. If any tests fail, fix them before proceeding.
      2.  **ASK** for confirmation with a brief inline summary template:
          "Task {N} complete. Summary of work:\n - Files created/modified: [list]\n - Key decisions: [brief notes]\n Ready to continue to Task {N+1}? (yes/no)"
      3.  Upon user confirmation (yes):
      - **UPDATE** `tasks.md`: Change the task heading to include the completion marker, e.g.: `## Task {N}: {Component/Feature Name} [IMPLEMENTED]`
      - Directly under the heading, insert a short Completion note, for example:
        `**Completion**: Implemented [summary], added tests [summary], decisions: [notes]`
      - **CONTINUE**: Proceed to Task {N+1} by repeating from step 1
      - Tip: Context can accumulate. Consider starting a fresh session and running `/spec:execute` again to continue, especially after every 2–3 tasks.
      4.  Upon user declining (no) or stopping for any reason:
      - **UPDATE** `tasks.md` with [IMPLEMENTED] marker and completion note as above
      - **ASK**: "Would you like to generate a TLDR summary of the work completed so far? (yes/no)"
      - If yes: Generate TLDR documenting partial implementation (see step 6)
      - **STOP** and report current progress: "Progress: {completed}/{total} tasks done. You can resume anytime with `/spec:execute`"
    - Run validation checks after each small implementation step.

4.  **Verify Implementation**:
    - After completing tasks (all or partial), run the full test suite to ensure no regressions.
    - Detect the test runner automatically when possible:
      - If a `package.json` with a `test` script exists, run `npm test` (or `pnpm/yarn test` as appropriate).
      - If a Python project with pytest is detected, run `pytest`.
      - If a Go module is detected, run `go test ./...`.
      - Otherwise, ASK the user for the appropriate single command to run the tests.
    - Confirm that the final implementation meets all acceptance criteria from `requirements.md`.
    - Perform any final validation steps mentioned in the design or tasks.

5.  **Architecture/Convention Discovery**:
    - During implementation, if you establish new patterns or conventions:
    - Track new patterns discovered or created
    - After task completion, ask: "This implementation established [specific patterns]. Should I update architecture.md/conventions.md?"
    - Update files if approved with meaningful additions

6.  **Generate TLDR Documentation**:
    <output>
    ## Template Usage
    
    The TLDR structure is defined in `.claude/templates/tldr.md`. The template provides:
    - **Implementation Summary**: What was built vs planned
    - **Technical Decisions**: Architecture choices and rationales
    - **Testing Details**: Coverage and test scenarios
    - **Change Documentation**: Files created/modified
    - **Performance & Security**: Impacts and measures
    - **Lessons Learned**: Challenges and improvements
    
    **When to Generate TLDR**:
    - When ALL tasks are completed
    - When user stops implementation (partial completion)
    - When user explicitly requests TLDR generation
    
    **For Partial Implementations**:
    - Document tasks completed vs total planned (e.g., "3 of 6 tasks")
    - List incomplete tasks and reason for stopping
    - Mark status as "Partial" or "MVP" instead of "Complete"
    - Note what functionality is working vs pending
    
    Generate TLDR by:
    - Initialize from template (replacing `[Feature Name]`)
    - Fill in applicable sections based on what was implemented:
      - What was built (high-level summary)
      - Files created and modified with descriptions
      - Key implementation decisions made during development
      - Test coverage achieved
      - API/Database/Configuration changes
      - Dependencies added
      - Usage examples
      - Known limitations and future enhancements
    - Save as `features/[feature-name]/tldr.md`
    - This serves as the permanent implementation record for the feature

7.  **Complete or Stop**:
    - **If all tasks completed**: 
      - Generate TLDR with status "Complete"
      - Report: "Feature implementation complete! All {N} tasks done. See `tldr.md` for summary."
    - **If partially completed**:
      - Ensure TLDR documents partial implementation
      - Report: "Feature partially implemented. {completed}/{total} tasks done. See `tldr.md` for summary."
    - **If stopped without TLDR**:
      - Remind: "You can generate a TLDR summary anytime by running `/spec:execute` and choosing to generate TLDR only."
    - Note any architecture/convention updates made during implementation.
    </output>

## Context Management

💡 **Important**: After completing 2-3 tasks, consider starting a fresh session with `/clear` and re-running `/spec:execute` to continue. This prevents context overload and maintains performance.

Progress through each task systematically, ensuring quality at each step.
