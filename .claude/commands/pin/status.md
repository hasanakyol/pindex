---
description: Show comprehensive implementation progress.
allowed-tools: Read, Glob, Grep
---

# Implementation Status

## Process

1. **Find features**: Glob features/* directories
2. **Per feature analyze**:
   - Count tasks: Grep `## Task \d+:` in tasks.md
   - Count completed: Grep `## Task.*\[IMPLEMENTED\]`
   - Check dependencies in requirements.md
   - Check if dep features exist and have tldr.md
   - Calculate: (completed/total) * 100

3. **Display comprehensive**:
   ```
   | Feature | Req | Des | Tasks | TLDR | Deps | Progress |
   |---------|-----|-----|-------|------|------|----------|
   | 01-name | ✅  | ✅  | 5/10  | ❌   | ✅   | 50%      |
   
   Dependencies:
   - 01 depends on: 02 (Complete ✅)
   
   Recommended order:
   1. Complete 01 (no blockers)
   2. Then 03 (waiting for 01)
   
   Summary: 5 features, 1 complete (20%)
   ```

## Output
READ @.claude/core/output-formats.md (lightweight command note)