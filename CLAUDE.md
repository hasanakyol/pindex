# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What is Pindex?

Pindex is a universal, architecture-agnostic framework for building software through structured specifications. It's designed to work with Claude Code through slash commands (`/pin:*`) that guide development through a 6-phase workflow.

## Framework Development Commands

Since this is the Pindex framework repository itself (not a project using Pindex), there are no build/test commands. The framework consists of markdown templates and command definitions.

To test changes to the framework:
1. Copy the `.claude` directory to a test project
2. Test the slash commands in Claude Code within that project

## Framework Architecture

### Core Structure
```
.claude/
├── CLAUDE.md                    # Complete framework reference (21KB)
├── commands/pin/               # Slash command definitions (~85% smaller than v1)
│   └── *.md                    # Each command reads shared logic via READ directives
├── core/                       # Reusable logic modules (DRY principle)
│   ├── feature-selection.md   # Standardized feature selection logic
│   ├── validation-rules.md    # Prerequisites and validation rules
│   ├── standards-table.md     # Quality standards reference
│   ├── tdd-process.md        # TDD cycle definition
│   ├── output-formats.md      # Consistent output message formats
│   └── shared-logic.md       # Index of all shared logic modules
└── templates/                  # Document templates for feature specs
    ├── requirements.md         # EARS requirements template
    ├── design.md              # Technical design template
    ├── tasks.md               # TDD task breakdown template
    └── tldr.md                # Implementation summary template
```

### Key Design Principles

1. **Token Efficiency**: v2 refactoring achieved ~85% token reduction by extracting shared logic
2. **DRY Principle**: No duplicated logic across commands - all shared logic in `core/`
3. **READ Directives**: Commands use `READ:` to access shared logic modules
4. **Modular Design**: Each command is self-contained but references shared components
5. **Template Adaptation**: Templates adapt to project type (Web, CLI, Library, etc.)

### Command Flow

Each `/pin:*` command follows this pattern:
1. Reads prerequisites via `READ: @.claude/core/validation-rules.md#prerequisites`
2. Performs its specific function
3. Uses shared output formats from `core/output-formats.md`
4. References quality standards from `core/standards-table.md`

### Important Files

- **CLAUDE.md (root)**: Quick reference for users - keep concise
- **.claude/CLAUDE.md**: Complete methodology documentation - comprehensive
- **README.md**: Public-facing documentation with installation instructions

## Making Changes to Pindex

### When Modifying Commands
- Update the command file in `.claude/commands/pin/`
- If adding new shared logic, place it in `.claude/core/` and update `shared-logic.md`
- Ensure READ directives point to correct sections

### When Modifying Templates
- Templates in `.claude/templates/` use placeholders that get replaced during generation
- Maintain compatibility with the "initialize-or-augment" policy (never overwrite user content)

### When Updating Documentation
- Keep root `CLAUDE.md` as quick reference only
- Put detailed documentation in `.claude/CLAUDE.md`
- Update README.md for public-facing changes

## Context Management

When working on Pindex framework improvements:
- Focus on one command or component at a time
- Test changes in a separate project directory
- Remember that users will use these commands through Claude Code

## Testing Framework Changes

To test your changes:
```bash
# Create test project
mkdir ~/test-pindex
cd ~/test-pindex

# Copy framework
cp -r /path/to/pindex/.claude .
cp /path/to/pindex/CLAUDE.md .

# Test in Claude Code
# Try the /pin:* commands
```

## Important Reminders

- Do not create files unless necessary for the framework functionality
- Prefer editing existing files over creating new ones
- The framework should work with any project type, not just web applications
- Maintain backwards compatibility when making changes