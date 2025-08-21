---
description: List all available features (specs)
allowed-tools: Read, Glob, TodoRead, TodoWrite
---

# List All Features

You are listing all the available features (specs) in the project.

## Your Task

List all feature directories located under `features/`.

## Process

1.  **Find features**: Use the `Glob` tool to find all directories inside the `features/` directory.
2.  **Check documentation**: For each feature, check which specification files exist:
    - `requirements.md` - Requirements specification
    - `design.md` - Technical design
    - `tasks.md` - Implementation tasks
    - `tldr.md` - Implementation summary
3.  **Sort numerically**: Sort the list by the leading zero-padded number (NN) in the directory name (e.g., 01-, 02-, 03-).
4.  **Display enhanced list**: Present the sorted feature directories with their documentation status.

## Example Output

```
Available Features:

| # | Feature                  | Req | Des | Tasks | TLDR | Status       |
|---|--------------------------|-----|-----|-------|------|--------------|
| 1 | 01-project-setup        | ✅  | ✅  | ✅    | ✅   | Complete     |
| 2 | 02-basic-todo-crud      | ✅  | ✅  | ✅    | ❌   | Implementing |
| 3 | 03-tags-system          | ✅  | ✅  | ❌    | ❌   | Designing    |
| 4 | 04-user-authentication  | ✅  | ❌  | ❌    | ❌   | Requirements |
| 5 | 05-notifications        | ❌  | ❌  | ❌    | ❌   | Planned      |

Legend:
- Req: Requirements | Des: Design | Tasks: Task breakdown | TLDR: Implementation summary
- Status is inferred from which documents exist
```
