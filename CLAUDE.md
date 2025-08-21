# CLAUDE.md - Quick Reference

This file provides quick reference for Claude Code when working with Pindex.

## What is This?

**Pindex** - A **universal, architecture-agnostic** framework for building software through structured specifications. Works with any language, any architecture pattern, new or existing codebases.

## Context Management Best Practices

- **Between Phases**: Use `/clear` when moving between major phases (requirements → design → tasks)
- **During Execute**: Start fresh session after completing 2-3 tasks to maintain performance
- **Large Projects**: Reset context after planning phase before detailing requirements
- **Visual Features**: Use screenshots for UI validation with `/spec:validate`

## Quick Start Commands

```bash
# New project (two modes)
/spec:plan "Your project description"        # Interactive discussion → empty templates
/spec:plan "Your project description" all    # Interactive discussion → draft EARS requirements from that discussion

# Add single feature
/spec:feature "Feature description"

# Develop feature (in order - all take optional feature-name)
/spec:requirements [feature-name]
/spec:design [feature-name]
/spec:tasks [feature-name]
/spec:validate [feature-name]    # Ensure alignment (recommended)
/spec:execute [feature-name]

# Utilities
/spec:list                       # List features with documentation status
/spec:status                     # Show comprehensive progress
/spec:validate [feature-name]   # Feature validation: specs alignment (req→design→tasks)
/spec:check                      # Framework validation: installation health & integrity
/spec:advanced [feature-name]   # Enterprise analysis (STRIDE, risk, performance)
/spec:help                       # Detailed help

## Command Distinctions
- **`/spec:check`**: System-level framework health (files, installation, structure)
- **`/spec:validate`**: Feature-level specification alignment (requirements→design→tasks)
```

## Workflow at a Glance

1. **Plan** → Interactive discussion to break down into features (optionally generating draft requirements from discussion)
2. **Requirements** → Define/refine WHAT (EARS format)
3. **Design** → Define HOW (tech specs)
4. **Tasks** → Break into TDD steps
5. **Validate** → Ensure alignment (recommended before execute)
6. **Execute** → Implement with tests

## Key Principles

- **Architecture-agnostic**: Works with any project structure
- **Explicit approval gates**: User control at each phase
- **Test-driven**: Red-Green-Refactor methodology
- **Iterative**: Refine at any phase
- **Context-aware**: Adapts to existing codebases

## Feature Selection

- All commands accept optional feature-name argument
- Without argument: Lists features and asks for selection
- With argument: Uses specified feature
- No auto-selection even with single feature

## Full Documentation

See `.claude/CLAUDE.md` for:

- Complete methodology details
- EARS requirements syntax
- TDD implementation guide
- Quality gates and validation
- Advanced features

## Project-Specific Files

When working with this framework, the following files will be discovered or generated:

- `architecture.md` - Your project's specific architecture (generated/discovered)
- `conventions.md` - Your project's coding standards (generated/discovered)
- `features/*/` - Feature specifications with:
  - `requirements.md` - EARS requirements
  - `design.md` - Technical design
  - `tasks.md` - TDD implementation tasks
  - `tldr.md` - Implementation summary (generated when stopping, complete or partial)

---
# important-instruction-reminders
Do what has been asked; nothing more, nothing less.
NEVER create files unless they're absolutely necessary for achieving your goal.
ALWAYS prefer editing an existing file to creating a new one.
NEVER proactively create documentation files (*.md) or README files. Only create documentation files if explicitly requested by the User.