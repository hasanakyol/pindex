---
description: Create single feature without full planning.
allowed-tools: Read, Write, Glob
---

# Add Feature
Feature: **$ARGUMENTS**

## Process

1. **Check context**:
   - READ ARCHITECTURE.md if exists (or create basic)
   - READ CONVENTIONS.md if exists (or create basic)

2. **Create feature**:
   - Find next number: scan features/NN-*
   - Create slug from description
   - Create features/NN-slug/

3. **Copy templates**:
   - Copy all 3: requirements.md, design.md, tasks.md
   - Replace `[Feature Name]` in all files

4. **Update if needed**:
   - If new patterns: ask to update ARCH/CONV

## Output
"Created `features/NN-slug/` with templates.
Next: `/pin:requirements NN-slug`"