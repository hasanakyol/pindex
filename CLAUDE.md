# CLAUDE.md - Quick Reference

This file provides quick reference for Claude Code when working with Pindex.

## What is This?

**Pindex** - A **universal, adaptable** framework for building software through structured specifications. Provides excellent support for web applications while adapting to any language, architecture pattern, or project type.

## Context Management Best Practices

- **Between Phases**: Use `/clear` when moving between major phases (requirements → design → tasks)
- **During Execute**: Start fresh session after completing 2-3 tasks to maintain performance
- **Large Projects**: Reset context after planning phase before detailing requirements
- **Visual Features**: Use screenshots for UI validation with `/pin:align`

## Quick Start Commands

```bash
# New project (two modes)
/pin:plan "Your project description"          # Interactive discussion → empty templates
/pin:plan "Your project description" --all    # Interactive discussion → draft EARS requirements

# Add single feature
/pin:feature "Feature description"

# Develop feature (in order - all take optional feature-name)
/pin:requirements [feature-name]
/pin:design [feature-name]
/pin:tasks [feature-name]
/pin:align [feature-name]      # Ensure alignment (recommended)
/pin:execute [feature-name]

# Utilities
/pin:list                       # List features with documentation status
/pin:status                     # Show comprehensive progress
/pin:align [feature-name]       # Feature alignment: specs alignment (req→design→tasks)
/pin:help                       # Detailed help
```

## Workflow at a Glance

1. **Plan** → Interactive discussion to break down into features (optionally generating draft requirements from discussion)
2. **Requirements** → Define/refine WHAT (EARS format)
3. **Design** → Define HOW (tech specs)
4. **Tasks** → Break into TDD steps
5. **Align** → Ensure alignment (recommended before execute)
6. **Execute** → Implement with tests

## Key Principles

- **Universal adaptation**: Works with any project type through adaptive templates
- **Web-optimized**: Excellent defaults and examples for modern web development
- **Explicit approval gates**: User control at each phase
- **Test-driven**: Red-Green-Refactor-Validate methodology
- **Production-ready**: Focus on deployable code, not prototypes
- **Context-aware**: Adapts to existing codebases and conventions

## Feature Selection

- All commands accept optional feature-name argument
- Without argument: Lists features and asks for selection
- With argument: Uses specified feature
- No auto-selection even with single feature

## Full Documentation

See `@.claude/CLAUDE.md` for:

- Complete methodology details
- EARS requirements syntax
- TDD implementation guide
- Quality gates and validation
- Advanced features

## Framework Structure

### Core Logic (`@.claude/core/`)
Reusable logic extracted for efficiency (~85% token reduction):
- `feature-selection.md` - Standardized feature selection
- `validation-rules.md` - Prerequisites and validation
- `standards-table.md` - Quality standards reference
- `tdd-process.md` - TDD cycle definition
- `output-formats.md` - Output message formats
- `shared-logic.md` - Index of all core logic

### Templates (`@.claude/templates/`)
Document templates for feature specifications:
- `requirements.md` - EARS requirements template
- `design.md` - Technical design template
- `tasks.md` - TDD task breakdown template
- `tldr.md` - Implementation summary template

### Project Files (Generated)
- `@.claude/ARCHITECTURE.md` - Your project's specific architecture
- `@.claude/CONVENTIONS.md` - Your project's coding standards
- `@.claude/SECURITY.md` - OWASP security checklist
- `features/*/` - Feature specifications

---
# important-instruction-reminders
Do what has been asked; nothing more, nothing less.
NEVER create files unless they're absolutely necessary for achieving your goal.
ALWAYS prefer editing an existing file to creating a new one.
NEVER proactively create documentation files (*.md) or README files. Only create documentation files if explicitly requested by the User.
