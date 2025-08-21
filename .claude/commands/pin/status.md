---
description: Show the implementation status of all features.
allowed-tools: Read, Glob, Grep, TodoRead, TodoWrite
---

# Feature Implementation Status

You are providing a status overview of all features, showing the progress of task completion.

## Your Task

For each feature, calculate and display the number of completed and pending tasks based on its `tasks.md` file.

## Process

1.  **Find all features**: Use the `Glob` tool to get a list of all directories under `features/`.
2.  **Iterate through features**: For each feature directory:
    a. **Check specification files**: Check existence of: - `requirements.md` - Mark with ✅ if exists, ❌ if missing - `design.md` - Mark with ✅ if exists, ❌ if missing - `tasks.md` - Mark with ✅ if exists, ❌ if missing - `tldr.md` - Mark with ✅ if exists, ❌ if missing
    b. **Count tasks** (only if `tasks.md` exists):
    i. Count the total number of tasks by using `Grep` with pattern `## Task \\d+:` and `output_mode: "count"`.
    ii. Count the number of completed tasks by using `Grep` with pattern `## Task.*\\[IMPLEMENTED\\]` and `output_mode: "count"`.
    c. **Check dependencies** (if `requirements.md` exists):
    i. Read requirements.md and extract feature dependencies from "Dependencies" section
    ii. For each dependency, check if it exists and is implemented (has tldr.md with "Complete" status)
    iii. Track dependency status: "✅ Ready", "⚠️ Partial", "❌ Missing"
    d. **Calculate progress**: - Task completion percentage: (completed/total) \* 100 - Overall status: "Planning", "Designing", "Implementing", "Complete" - Dependency status for ordering recommendations
3.  **Display comprehensive status**: Present in an enhanced table format.

## Example Output

```
Feature Implementation Status:

| Feature                  | Req | Des | Tasks     | TLDR | Dependencies | Status        | Progress |
|--------------------------|-----|-----|-----------|------|--------------|---------------|----------|
| 01-project-setup        | ✅  | ✅  | 5/6       | ❌   | None         | Implementing  | 83%      |
| 02-basic-todo-crud      | ✅  | ✅  | 10/10     | ✅   | ✅ Ready     | Complete      | 100%     |
| 03-tags-system          | ✅  | ✅  | 2/10      | ❌   | ⚠️ Partial   | Implementing  | 20%      |
| 04-user-auth            | ✅  | ❌  | -         | ❌   | ❌ Missing   | Blocked       | 0%       |
| 05-notifications        | ❌  | ❌  | -         | ❌   | -            | Planning      | 0%       |

Dependencies:
- 03-tags-system depends on: 02-basic-todo-crud (Complete ✅)
- 04-user-auth depends on: 01-project-setup (Incomplete ⚠️), 02-basic-todo-crud (Complete ✅)
- 05-notifications depends on: 04-user-auth (Not Started ❌)

Recommended Implementation Order:
1. 01-project-setup (no dependencies, 83% complete)
2. 04-user-auth (waiting for 01-project-setup)
3. 05-notifications (waiting for 04-user-auth)

Summary:
- Total Features: 5
- Complete: 1 (20%)
- In Progress: 2 (40%)
- Blocked: 1 (20%)
- Planning/Design: 1 (20%)
```

## Context Management

💡 **Performance Tip**: This is a lightweight read-only command that doesn't accumulate context. No need to use `/clear` after this command.
