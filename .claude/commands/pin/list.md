---
description: List all features with documentation status.
allowed-tools: Read, Glob
---

# List Features

## Process

1. **Find features**: Glob features/* directories
2. **Check status** per feature:
   - requirements.md: Has DRAFT marker or content?
   - design.md: Has content beyond template?
   - tasks.md: Has actual tasks?
   - tldr.md: Exists?
3. **Sort**: By NN- prefix numerically
4. **Display**:
   ```
   | # | Feature | Req | Des | Tasks | TLDR | Status |
   |---|---------|-----|-----|-------|------|--------|
   | 1 | 01-name | ✅  | ✅  | ✅    | ✅   | Complete |
   | 2 | 02-next | ✅  | ✅  | 📝   | ❌   | Tasks |
   
   ✅ Content | 📝 Template | ❌ Missing
   ```

## Output
READ @.claude/core/output-formats.md (lightweight command note)