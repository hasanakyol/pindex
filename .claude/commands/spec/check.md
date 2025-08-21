---
description: Framework health check - validates Pindex installation, file structure, and system integrity (NOT feature validation)
allowed-tools: Read, Glob, Grep
---

# Framework Health Check

**Purpose**: System-level validation of Pindex framework installation (different from `/spec:validate` which checks feature specification alignment).

You are validating the Pindex framework installation and project consistency.

## Your Task

Perform a comprehensive health check of the framework installation and project structure.

## Process

<analysis>
### 1. Framework Installation Check

Check core framework files:
- `.claude/CLAUDE.md` - Main documentation
- `.claude/commands/spec/*` - All command files
- `.claude/templates/*` - All template files
- `CLAUDE.md` - Quick reference
- `architecture.md` - Project architecture
- `conventions.md` - Coding conventions

### 2. Command Verification

Verify all commands are present and properly formatted:
- plan.md, requirements.md, design.md, tasks.md
- execute.md, validate.md, advanced.md
- list.md, status.md, help.md, check.md, feature.md

Check each command has:
- Valid frontmatter with description and allowed-tools
- Proper markdown structure
- No syntax errors

### 3. Template Validation

Verify all templates exist and are valid:
- requirements.md - EARS requirements template
- design.md - Technical design template
- tasks.md - TDD task breakdown template
- tldr.md - Implementation summary template

### 4. Feature Structure Check

For each feature in `features/`:
- Verify directory naming convention (NN-feature-slug)
- Check file presence and structure
- Validate EARS format in requirements
- Check task numbering in tasks.md
- Verify [IMPLEMENTED] markers are properly formatted

### 5. Project Consistency

Cross-validate:
- Architecture patterns are consistent across features
- Conventions are followed in all specifications
- No orphaned or conflicting configurations
- Dependencies between features are valid
</analysis>

<thinking>
Consider what issues might affect framework operation:
1. Missing files that are referenced
2. Malformed markdown or frontmatter
3. Inconsistent naming patterns
4. Broken cross-references
5. Permission issues with tools
</thinking>

## Health Check Report Format

<output>
```markdown
# Pindex Framework Health Check Report

## Installation Status
✅ Framework Version: 1.0.0
✅ Installation Path: .claude/

## Core Files
| File | Status | Issues |
|------|--------|--------|
| .claude/CLAUDE.md | ✅ Present | None |
| CLAUDE.md | ✅ Present | None |
| architecture.md | ⚠️ Template | Needs customization |

## Commands (12/12)
✅ All commands present and valid
- No syntax errors detected
- Frontmatter properly formatted
- Tool permissions appropriate

## Templates (4/4)
✅ All templates present
- requirements.md ✅
- design.md ✅
- tasks.md ✅
- tldr.md ✅

## Features
Found [N] features:
- [N] with complete specifications
- [N] with partial specifications
- [N] with implementation complete

## Issues Found
[List any issues discovered]

## Recommendations
[Specific actions to resolve issues]

## Overall Health: [HEALTHY/WARNING/ERROR]
```
</output>

## Implementation

1. **Scan Framework Structure**:
   - Use Glob to find all framework files
   - Verify against expected file list
   - Check file readability

2. **Validate Command Files**:
   - Read each command file
   - Parse frontmatter
   - Check markdown structure

3. **Check Feature Consistency**:
   - Scan all feature directories
   - Validate naming conventions
   - Check specification completeness

4. **Generate Report**:
   - Categorize findings by severity
   - Provide actionable recommendations
   - Calculate overall health score

## Quality Gates

The framework passes health check when:
- [ ] All core files are present
- [ ] All commands have valid frontmatter
- [ ] All referenced templates exist
- [ ] No critical errors found
- [ ] Feature structure follows conventions

## Error Categories

### Critical (Framework Won't Work)
- Missing command files
- Invalid frontmatter syntax
- Missing CLAUDE.md files

### Warning (Reduced Functionality)
- Missing templates
- Incomplete feature specifications
- Inconsistent naming

### Info (Best Practice Violations)
- Unused features
- Outdated documentation
- Minor formatting issues

## Recovery Actions

If critical issues found, suggest:
1. Re-clone framework from repository
2. Manually create missing files
3. Fix syntax errors in frontmatter
4. Update file permissions

## Next Steps

After health check:
- If HEALTHY: "✅ Framework is properly installed and configured. Ready for use!"
- If WARNING: "⚠️ Framework has minor issues. Review recommendations above."
- If ERROR: "❌ Critical issues found. Follow recovery actions to fix."

Now performing comprehensive health check...