---
description: Display Pindex command help.
allowed-tools: Read
---

# Pindex Help

## Commands

### Workflow Commands
- `/pin:plan [desc] [--all]` - Break project into features
- `/pin:requirements [feat]` - Detail EARS requirements
- `/pin:design [feat]` - Generate technical design
- `/pin:tasks [feat]` - Create TDD tasks
- `/pin:align [feat]` - Validate alignment
- `/pin:execute [feat]` - Implement with TDD

### Utility Commands
- `/pin:feature [desc]` - Add single feature
- `/pin:list` - Show features with status
- `/pin:status` - Show implementation progress
- `/pin:help` - This help

## Workflow
```
plan → requirements → design → tasks → align → execute
```

## EARS Format
- Ubiquitous: `The system SHALL [requirement]`
- Event: `WHEN [trigger] THEN the system SHALL [response]`
- State: `WHILE [state] the system SHALL [requirement]`
- Conditional: `IF [condition] THEN the system SHALL [requirement]`

## TDD Cycle
1. 🔴 RED: Write failing test
2. 🟢 GREEN: Minimal complete implementation
3. 🔄 REFACTOR: Improve structure
4. ✅ VALIDATE: Re-run tests

## Tips
- Use `/clear` between phases for performance
- After 2-3 tasks in execute, consider fresh session
- All commands accept optional feature name

## Documentation
Full details: READ @.claude/CLAUDE.md