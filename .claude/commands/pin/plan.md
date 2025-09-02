---
description: Break project into features through interactive discussion. Optional --all generates draft requirements.
allowed-tools: Read, Write, Glob, Grep
---

# Project Planning
Project: **$ARGUMENTS**

## Mode
- Standard: No "--all" suffix → template requirements
- Draft: With "--all" → generate EARS requirements from discussion

## Process

1. **Discover existing project** (if applicable):
   - Detect project type from files (package.json, go.mod, etc.)
   - Identify architecture patterns and test framework
   - Document in ARCHITECTURE.md and CONVENTIONS.md

2. **Interactive discussion**:
   - New project: Ask type, architecture, stack, database, test runner
   - Existing: Analyze and confirm patterns
   - Gather: objectives, users, features, constraints, performance

3. **Propose features**:
   - Present numbered breakdown
   - Get approval/modifications

4. **Generate files**:
   - MUST fill ALL placeholders in ARCHITECTURE.md and CONVENTIONS.md
   - STOP if any [brackets] remain - get missing info
   - Create features/NN-name/ with all 3 templates
   - If --all: populate requirements.md with EARS + `<!-- DRAFT -->`

## Output
READ @.claude/core/output-formats.md for standard completion message.
"Created [N] features. Next: `/pin:requirements 01-first-feature`"
