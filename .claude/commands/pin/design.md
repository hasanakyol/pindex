---
description: Generate technical design from EARS requirements.
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep
---

# Technical Design
Feature: **$ARGUMENTS**

## Process

1. **Setup**:
   - READ @.claude/core/feature-selection.md and apply
   - READ @.claude/core/validation-rules.md and validate
   - READ requirements.md and all EARS requirements

2. **Check dependencies**:
   - Extract from requirements Dependencies section
   - Build dependency graph, check for cycles
   - WARN if circular: "[A]→[B]→[A] may cause issues"

3. **Design generation**:
   - READ @.claude/ARCHITECTURE.md for tech stack
   - READ @.claude/core/standards-table.md for design standards
   - Map each EARS → technical solution
   - NO placeholders: complete specs only
   - Include: schemas, endpoints, error codes

4. **Write design**:
   - READ @.claude/templates/design.md
   - Fill ALL sections with concrete details
   - Update ARCHITECTURE/CONVENTIONS if new patterns

## Output
READ @.claude/core/output-formats.md
"Design complete for **[feature]**. Ready for `/pin:tasks [feature]`?"