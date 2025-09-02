---
description: Interactively detail EARS requirements for a feature.
allowed-tools: Read, Write, Edit, MultiEdit, Glob
---

# Requirements Generation
Feature: **$ARGUMENTS**

## Process

1. **Setup**:
   - READ @.claude/core/feature-selection.md and apply
   - READ @.claude/core/validation-rules.md and validate
   - READ existing requirements.md (check for `<!-- DRAFT -->`)

2. **Interactive gathering**:
   - Ask: goals, user stories, constraints, errors, dependencies
   - If dependencies mentioned: verify they exist in features/
   - Warn if missing dependencies

3. **Generate EARS**:
   - READ @.claude/core/standards-table.md for metrics
   - Transform stories → formal EARS with SPECIFIC values
   - Include measurable performance, security, scalability
   - NO vague terms: "fast", "secure", "appropriate"

4. **Finalize**:
   - Remove `<!-- DRAFT -->` if present
   - Save complete requirements
   - If new patterns needed: update ARCHITECTURE/CONVENTIONS

## Output
READ @.claude/core/output-formats.md
"Requirements complete for **[feature]**. Ready for `/pin:design [feature]`?"