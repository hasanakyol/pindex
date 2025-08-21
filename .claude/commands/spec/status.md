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
    c. **Calculate progress**: - Task completion percentage: (completed/total) \* 100 - Overall status: "Planning", "Designing", "Implementing", "Complete"
3.  **Display comprehensive status**: Present in an enhanced table format.

## Example Output

```
Feature Implementation Status:

| Feature                  | Req | Des | Tasks     | TLDR | Status        | Progress |
|--------------------------|-----|-----|-----------|------|---------------|----------|
| 01-project-setup        | ✅  | ✅  | 5/6       | ❌   | Implementing  | 83%      |
| 02-basic-todo-crud      | ✅  | ✅  | 10/10     | ✅   | Complete      | 100%     |
| 03-tags-system          | ✅  | ✅  | 2/10      | ❌   | Implementing  | 20%      |
| 04-user-auth            | ✅  | ❌  | -         | ❌   | Designing     | 0%       |
| 05-notifications        | ❌  | ❌  | -         | ❌   | Planning      | 0%       |

Summary:
- Total Features: 5
- Complete: 1 (20%)
- In Progress: 2 (40%)
- Planning/Design: 2 (40%)
```
