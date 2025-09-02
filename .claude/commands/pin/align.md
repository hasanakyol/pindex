---
description: Validate alignment between requirements→design→tasks.
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep
---

# Specification Alignment
Feature: **$ARGUMENTS**

## Process

1. **Setup**:
   - READ @.claude/core/feature-selection.md and apply
   - READ @.claude/core/validation-rules.md and validate
   - READ all: requirements.md, design.md, tasks.md, tldr.md (if exists)

2. **Check dependencies**:
   - Extract from requirements, build graph
   - Check circular: current in own chain = CRITICAL
   - Example: A→B→C→A is circular

3. **Validate alignment**:
   - Requirements → Design: Every EARS has solution
   - Design → Tasks: Every component has task
   - Tasks follow TDD format
   - No placeholders/mocks/TBD
   - OWASP security addressed

4. **Gap analysis**:
   - Critical: Missing coverage, circular deps, security gaps
   - Important: Incomplete tests, performance missing
   - Minor: Naming, documentation

5. **Report**:
   ```
   Summary: Req[N] Des[X%] Tasks[Y%] Deps[✅/⚠️/❌]
   
   Gaps:
   - Critical: [list]
   - Important: [list]
   ```

6. **Fix options**:
   - Show detailed analysis
   - Auto-fix all/critical
   - Review one by one

## Output
READ @.claude/core/output-formats.md
"Alignment complete. [N critical, M important] gaps found. Fix?"