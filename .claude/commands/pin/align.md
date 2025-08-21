---
description: Feature alignment - ensures requirements→design→tasks alignment and specification consistency
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep, TodoRead, TodoWrite
---

# Specification Alignment & Synchronization

**Purpose**: Feature-level validation of specification alignment and consistency.

You are validating and synchronizing all specifications for a feature to ensure consistency, completeness, and alignment with project architecture and conventions.

## Your Task

Validate and align specifications for the feature: **$ARGUMENTS**

## Feature Selection Logic

**Follow standardized logic** (see `@.claude/templates/shared-logic.md` for details):
- With feature name: Find matching directory, ask for confirmation if not found
- Without feature name: List all features and ask for selection
- No auto-selection even with single feature

## Alignment Process

<analysis>
### 1. Read and Validate All Specifications

**Prerequisites Check** (STRICT validation from `@.claude/templates/shared-logic.md`):

1. Check if @.claude/ARCHITECTURE.md exists; if not, **STOP**: "⚠️ Project not initialized. Run `/pin:plan [description]` first."
2. If exists, scan for placeholder patterns: `[e.g.,`, `[Type]`, `[Language]`, `TODO`, `TBD`
   - If placeholders found, **STOP**: "⚠️ Cannot proceed. Found incomplete configuration in @.claude/ARCHITECTURE.md. Please complete all fields or re-run `/pin:plan`."
3. Check if @.claude/CONVENTIONS.md exists; if not, **STOP**: "⚠️ Project not initialized. Run `/pin:plan [description]` first."
4. If exists, scan for placeholder patterns: `[e.g.,`, `[Tool]`, `[Framework]`, `TODO`, `TBD`
   - If placeholders found, **STOP**: "⚠️ Cannot proceed. Found incomplete configuration in @.claude/CONVENTIONS.md. Please complete all fields or re-run `/pin:plan`."
5. Check if @.claude/SECURITY.md exists; if missing, continue with info: "ℹ️ Security checklist not found."
6. Trust that test runner was properly configured during `/pin:plan`

**Feature Specifications** (read in order):
1. `features/[feature]/requirements.md` - EARS requirements
2. `features/[feature]/design.md` - Technical design
3. `features/[feature]/tasks.md` - Implementation tasks
4. `features/[feature]/tldr.md` - Implementation summary (if exists)
5. **Circular Dependency Check**:
   - Extract dependencies from current feature's requirements.md
   - For each dependency, recursively check its dependencies
   - Track visited features to detect cycles
   - If current feature appears in its own dependency chain: **CRITICAL GAP**
   - Example cycle: feature-a → feature-b → feature-c → feature-a
</analysis>

### 2. Cross-Document Validation

<thinking>
Systematically check each layer of alignment:
- Are all requirements addressed in design?
- Does every design element trace to requirements?
- Are all design components covered by tasks?
- Do tasks follow the established patterns?
- Is the implementation consistent with specifications?
- Are feature dependencies properly tracked and valid?
</thinking>

#### Requirements Format & Quality

Verify that:

- [ ] Requirements follow EARS format (SHALL, WHEN/THEN, WHILE, IF/THEN, WHERE)
- [ ] Each requirement is testable and measurable
- [ ] No implementation details in requirements (technology-agnostic)
- [ ] Acceptance criteria are clear and specific
- [ ] No ambiguous terms ("fast", "easy", "intuitive")
- [ ] Requirements are organized by logical categories
- [ ] Feature dependencies are documented if they exist

#### Requirements → Design Alignment

Verify that:

- [ ] Every EARS requirement has corresponding design elements
- [ ] All WHEN/THEN conditions are addressed in design
- [ ] All state conditions (WHILE) have design considerations
- [ ] All conditional requirements (IF) are covered
- [ ] No design elements exist without backing requirements

#### Design Quality & Completeness

Verify that:

- [ ] API endpoints have request/response schemas defined
- [ ] Data models include all fields, types, and validations
- [ ] Error handling strategy is documented
- [ ] Performance targets are specified
- [ ] Caching strategy is defined (if applicable)
- [ ] Database indexes are planned
- [ ] No placeholder components ("TBD", "TODO", etc.)

#### Design → Tasks Alignment

Verify that:

- [ ] Every design component has implementation tasks
- [ ] API endpoints in design have corresponding task items
- [ ] Data models in design are covered by tasks
- [ ] Security measures in design appear in tasks
- [ ] Performance considerations have implementation steps
- [ ] No tasks exist without design justification

#### Task Structure & TDD Compliance

Verify that:

- [ ] Each task follows TDD format (test scenarios → implementation → validation)
- [ ] Tasks have clear acceptance criteria
- [ ] Test scenarios cover happy path and edge cases
- [ ] Tasks are properly numbered and sequenced
- [ ] Dependencies between tasks are explicit
- [ ] No placeholder or mock implementations suggested
- [ ] Tasks specify integration testing requirements

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

#### Security Compliance (OWASP)

Verify that:

- [ ] Authentication/authorization requirements are addressed
- [ ] Input validation is specified for all user inputs
- [ ] Data protection measures are in design
- [ ] Security headers and policies are planned
- [ ] Error handling doesn't expose sensitive info
- [ ] Logging excludes PII/sensitive data
- [ ] Rate limiting is implemented where needed

#### Implementation Documentation

Verify that (if tasks are marked as completed):

- [ ] TLDR documentation exists for completed features
- [ ] TLDR accurately reflects what was built
- [ ] Files listed in TLDR match actual implementation
- [ ] Key decisions are documented
- [ ] Test coverage is documented

#### Feature Dependencies

Verify that:

- [ ] Dependencies on other features are documented in requirements
- [ ] Dependent features exist and are implemented/planned
- [ ] **Circular dependencies are detected**:
  - Build dependency graph: Current feature → its dependencies → their dependencies
  - Use depth-first search to detect cycles
  - If cycle found, **CRITICAL**: "❌ Circular dependency detected: [feature-a] → [feature-b] → [feature-c] → [feature-a]. This must be resolved."
- [ ] Integration points between features are specified
- [ ] Dependency order is logical for implementation

### 3. Gap Analysis

Identify and categorize gaps:

#### Critical Gaps (Must Fix)

- Missing requirements coverage in design
- Unimplemented design elements in tasks
- Architecture violations
- Security requirements not addressed
- Missing error handling
- Requirements not in EARS format
- Tasks suggesting placeholder implementations
- Missing authentication/authorization
- No input validation specified
- Database operations without transactions
- Missing or invalid feature dependencies

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
- Document feature dependencies

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
"I've completed alignment validation for **[feature-name]**. [Summary of findings]"

If gaps found:
"Found [N] critical gaps, [M] important gaps, and [P] minor gaps. Would you like me to:

1. Show detailed gap analysis
2. Auto-fix all gaps
3. Fix only critical gaps
4. Review gaps one by one"

If no gaps:
"✅ All specifications are aligned and consistent with architecture. The feature is ready for implementation."

### 6. Update Process

If user approves updates:

- Update files in order of dependency:
  - @.claude/ARCHITECTURE.md / @.claude/CONVENTIONS.md (if needed)
  - requirements.md (if needed)
  - design.md (if needed)
  - tasks.md (if needed)

## Alignment Report Format

```markdown
## Alignment Report for [Feature Name]

### Summary

- Requirements: [N items] ✅/⚠️/❌
- Design Coverage: [X%] ✅/⚠️/❌
- Task Coverage: [Y%] ✅/⚠️/❌
- Implementation Documentation: ✅/⚠️/❌
- Architecture Alignment: ✅/⚠️/❌
- Convention Compliance: ✅/⚠️/❌
- Feature Dependencies: ✅/⚠️/❌

### Requirements → Design Traceability

| Requirement | Design Element | Status     |
| ----------- | -------------- | ---------- |
| User login with credentials | Auth endpoint + JWT service | ✅ Covered |
| Password reset flow | Missing | ❌ Gap     |

### Design → Tasks Traceability

| Design Component    | Task(s) | Status     |
| ------------------- | ------- | ---------- |
| API Endpoint /users | Task 3  | ✅ Covered |
| Auth Service        | Missing | ❌ Gap     |

### Feature Dependencies

| This Feature | Depends On | Status |
| ------------ | ---------- | ------ |
| User Auth    | Core Setup | ✅ OK  |
| Payments     | User Auth  | ⚠️ Not Implemented |

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
</output>

## Quality Gates

The alignment validation passes when:

- [ ] All critical gaps are resolved
- [ ] Requirements have 100% design coverage
- [ ] Design has 100% task coverage
- [ ] No architecture violations exist
- [ ] Convention compliance is achieved
- [ ] All security requirements are addressed
- [ ] Error handling is comprehensive
- [ ] Feature dependencies are valid and documented

## Next Steps

After successful alignment:

- User can proceed with `/pin:execute [feature-name]`
- All specifications are guaranteed to be in sync
- Implementation can begin with confidence

Or if gaps remain:

- User reviews proposed fixes
- Approves updates to specifications
- Re-runs alignment to confirm

## Alignment Examples

### Example: Finding Common Issues

**❌ Bad Requirement** (not EARS):
```
"Users should be able to login quickly"
```
**✅ Fixed**:
```
"WHEN a user submits valid credentials THEN the system SHALL authenticate and respond within 2 seconds"
```

**❌ Bad Design** (placeholder):
```
"API: /api/login (details TBD)"
```
**✅ Fixed**:
```
"POST /api/login
Request: { email: string, password: string }
Response: { token: string, user: {...} }
Auth: JWT with 1hr expiry"
```

**❌ Bad Task** (suggests mock):
```
"Task 1: Create login endpoint that returns mock user data"
```
**✅ Fixed**:
```
"Task 1: Implement login endpoint with database authentication
- Test: Valid credentials return JWT token
- Test: Invalid credentials return 401
- Implementation: Query database, verify password hash, generate JWT"
```

**❌ Missing Dependency**:
```
Requirements with no mention of dependencies
```
**✅ Fixed**:
```
## Dependencies
This feature depends on:
- Feature 01-user-setup: User model and database schema
- Feature 02-auth-core: JWT token generation
```

## Context Management

💡 **Tip**: After alignment, if proceeding to `/pin:execute`, use `/clear` to start with fresh context.

Now validate and align the specifications for the selected feature.