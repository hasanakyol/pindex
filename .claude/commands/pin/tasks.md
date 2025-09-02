---
description: Break down design into TDD implementation tasks.
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep
---

# Task Breakdown
Feature: **$ARGUMENTS**

## Process

1. **Setup**:
   - READ @.claude/core/feature-selection.md and apply
   - READ @.claude/core/validation-rules.md and validate
   - READ design.md for technical approach
   - Scan codebase for reusable components

2. **Generate tasks**:
   - READ @.claude/core/tdd-process.md for TDD cycle
   - READ @.claude/core/standards-table.md for task standards
   - Break design → 7-8 flexible tasks
   - Each task: Red-Green-Refactor-Validate
   - NO mocks/stubs: real implementation only

3. **Write tasks**:
   - READ @.claude/templates/tasks.md
   - Use format: `## Task N: [Title]`
   - Fill reusability sections or write "None"
   - Mark completed with `[IMPLEMENTED]`

## Output
READ @.claude/core/output-formats.md
"Tasks complete for **[feature]**. [N] TDD tasks created. Ready for `/pin:execute [feature]`?"