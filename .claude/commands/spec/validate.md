---
description: Feature validation - ensures requirements→design→tasks alignment and specification consistency (NOT framework installation)
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep, TodoRead, TodoWrite
---

# Specification Validation & Synchronization

**Purpose**: Feature-level validation of specification alignment (different from `/spec:check` which validates framework installation).

You are validating and synchronizing all specifications for a feature to ensure consistency, completeness, and alignment with project architecture and conventions.

## Your Task

Validate and synchronize specifications for the feature: **$ARGUMENTS**

## Feature Selection Logic (Standardized)

1. **IF a feature name/number is provided in `$ARGUMENTS`**:
   - Search for a matching directory in `features/` (exact or partial match)
   - If found, use that feature
   - If not found, list available features and ask for correct selection

2. **IF no feature name is provided**:
   - Use Glob to find all directories in `features/`
   - List them sorted numerically
   - Ask user to specify which feature to work on
   - If only one feature exists, still ask for confirmation (no auto-selection)

## Validation Process

<analysis>
### 1. Read All Specifications

Read in this order:

1. `architecture.md` - Project architecture patterns
2. `conventions.md` - Coding standards and practices
3. `features/[feature]/requirements.md` - EARS requirements
4. `features/[feature]/design.md` - Technical design
5. `features/[feature]/tasks.md` - Implementation tasks
6. `features/[feature]/tldr.md` - Implementation summary (if exists)
</analysis>

### 2. Cross-Document Validation

<thinking>
Systematically check each layer of alignment:
- Are all requirements addressed in design?
- Does every design element trace to requirements?
- Are all design components covered by tasks?
- Do tasks follow the established patterns?
- Is the implementation consistent with specifications?
</thinking>

#### Requirements → Design Alignment

Verify that:

- [ ] Every EARS requirement has corresponding design elements
- [ ] All WHEN/THEN conditions are addressed in design
- [ ] All state conditions (WHILE) have design considerations
- [ ] All conditional requirements (IF) are covered
- [ ] No design elements exist without backing requirements

#### Design → Tasks Alignment

Verify that:

- [ ] Every design component has implementation tasks
- [ ] API endpoints in design have corresponding task items
- [ ] Data models in design are covered by tasks
- [ ] Security measures in design appear in tasks
- [ ] Performance considerations have implementation steps
- [ ] No tasks exist without design justification

#### Architecture Alignment

Verify that:

- [ ] Design follows established architectural patterns
- [ ] Component boundaries match architecture style
- [ ] Technology choices align with tech stack
- [ ] Service/module organization is consistent
- [ ] Integration patterns match existing approach

#### Convention Compliance

Verify that:

- [ ] Tasks follow established coding conventions
- [ ] Testing approach matches project standards
- [ ] File organization aligns with conventions
- [ ] Naming patterns are consistent
- [ ] Documentation style matches project norms

#### Implementation Documentation

Verify that (if tasks are marked as completed):

- [ ] TLDR documentation exists for completed features
- [ ] TLDR accurately reflects what was built
- [ ] Files listed in TLDR match actual implementation
- [ ] Key decisions are documented
- [ ] Test coverage is documented

### 3. Gap Analysis

Identify and categorize gaps:

#### Critical Gaps (Must Fix)

- Missing requirements coverage in design
- Unimplemented design elements in tasks
- Architecture violations
- Security requirements not addressed
- Missing error handling

#### Important Gaps (Should Fix)

- Incomplete test coverage planning
- Missing performance considerations
- Insufficient observability planning
- Incomplete API documentation
- Missing edge case handling

#### Minor Gaps (Nice to Fix)

- Documentation inconsistencies
- Naming convention deviations
- Optional optimizations
- Enhanced logging opportunities

### 4. Synchronization Actions

Based on gaps found, propose updates:

#### Requirements Updates

- Add missing acceptance criteria
- Clarify ambiguous requirements
- Add overlooked edge cases
- Enhance testability

#### Design Updates

- Add missing technical components
- Enhance security measures
- Improve error handling strategies
- Add performance optimizations
- Update to match architecture patterns

#### Tasks Updates

- Add missing implementation steps
- Enhance test scenarios
- Add validation steps
- Include integration tasks
- Update dependencies

#### Architecture/Convention Updates

- Document new patterns introduced
- Add new technology decisions
- Update coding standards if needed
- Document new best practices discovered

### 5. Implementation

<output>
After analysis, ask user:
"I've completed validation of **[feature-name]**. [Summary of findings]"

If gaps found:
"Found [N] critical gaps, [M] important gaps, and [P] minor gaps. Would you like me to:

1. Show detailed gap analysis
2. Auto-fix all gaps
3. Fix only critical gaps
4. Review gaps one by one"

If no gaps:
"✅ All specifications are in sync and aligned with architecture. The feature is ready for implementation."

### 6. Update Process

If user approves updates:

- Update files in order of dependency:
  - architecture.md / conventions.md (if needed)
  - requirements.md (if needed)
  - design.md (if needed)
  - tasks.md (if needed)

## Validation Report Format

```markdown
## Validation Report for [Feature Name]

### Summary

- Requirements: [N items] ✅/⚠️/❌
- Design Coverage: [X%] ✅/⚠️/❌
- Task Coverage: [Y%] ✅/⚠️/❌
- Implementation Documentation: ✅/⚠️/❌
- Architecture Alignment: ✅/⚠️/❌
- Convention Compliance: ✅/⚠️/❌

### Requirements → Design Traceability

| Requirement | Design Element | Status     |
| ----------- | -------------- | ---------- |
| REQ-001     | Component X    | ✅ Covered |
| REQ-002     | Missing        | ❌ Gap     |

### Design → Tasks Traceability

| Design Component    | Task(s) | Status     |
| ------------------- | ------- | ---------- |
| API Endpoint /users | Task 3  | ✅ Covered |
| Auth Service        | Missing | ❌ Gap     |

### Gaps Identified

#### Critical

1. [Gap description]
   - Impact: [description]
   - Suggested fix: [action]

#### Important

1. [Gap description]
   - Impact: [description]
   - Suggested fix: [action]

### Recommendations

1. [Specific action items]
2. [Priority order]
```

## Quality Gates

The validation passes when:

- [ ] All critical gaps are resolved
- [ ] Requirements have 100% design coverage
- [ ] Design has 100% task coverage
- [ ] No architecture violations exist
- [ ] Convention compliance is achieved
- [ ] All security requirements are addressed
- [ ] Error handling is comprehensive

## Next Steps

After successful validation:

- User can proceed with `/spec:execute [feature-name]`
- All specifications are guaranteed to be in sync
- Implementation can begin with confidence

Or if gaps remain:

- User reviews proposed fixes
- Approves updates to specifications
- Re-runs validation to confirm
</output>

## Context Management

💡 **Tip**: After validation, if proceeding to `/spec:execute`, use `/clear` to start with fresh context.

Now validate the specifications for the selected feature.
