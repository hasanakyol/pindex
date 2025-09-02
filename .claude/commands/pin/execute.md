---
description: Execute TDD implementation from tasks.md.
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep, Bash
---

# Execute Implementation
Feature: **$ARGUMENTS**

## Process

1. **Setup**:
   - READ @.claude/core/feature-selection.md and apply
   - READ @.claude/core/validation-rules.md and validate
   - READ complete requirements.md, design.md, tasks.md upfront
   - Check dependencies: verify in features/, warn if missing
   - IF no tasks.md: "Run `/pin:tasks` first"

2. **Auto-resume**:
   - Find next task without `[IMPLEMENTED]`
   - IF all done: Ask to generate/update TLDR
   - Announce: "Task N of M starting..."

3. **Per task (TDD)**:
   - READ @.claude/core/tdd-process.md for cycle
   - READ @.claude/core/standards-table.md for code quality
   - RED: Write failing test
   - GREEN: Minimal COMPLETE implementation (NO mocks)
   - REFACTOR: Improve structure
   - VALIDATE: Re-run tests
   - INTEGRATE: Test with previous tasks (if N>1)

4. **After task**:
   - Run test command from CONVENTIONS.md
   - Mark task `[IMPLEMENTED]` in tasks.md
   - Ask: "Task N complete. Continue to Task N+1?"

5. **Generate TLDR** (when stopping):
   - Status: Complete/Partial/MVP
   - Tasks completed vs total
   - Files changed, decisions made
   - READ @.claude/templates/tldr.md

## Language Standards
READ CONVENTIONS.md for language-specific rules:
- TypeScript: strict mode, no any, handle null
- Python: type hints, no bare except, context managers

## Output
READ @.claude/core/output-formats.md
💡 After 2-3 tasks: Consider `/clear` and resume