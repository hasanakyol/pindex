# Shared Logic Templates

This file contains reusable logic templates to ensure consistency across commands.

## Feature Selection Logic (Standardized)

1. **IF a feature name/number is provided in `$ARGUMENTS`**:
   - Search for a matching directory in `features/` (exact or partial match)
   - If found, use that feature
   - If not found, list available features and ask for correct selection

2. **IF no feature name is provided**:
   - Use Glob to find all directories in `features/`
   - List them sorted numerically (01-, 02-, etc.)
   - Present format: "Available features: [list with brief descriptions]"
   - Ask user to specify which feature to work on
   - **IMPORTANT**: No auto-selection even with single feature - always ask for confirmation

## Architecture & Conventions Validation (Standardized)

### Validation Rules

**Context**: All commands except `/pin:plan` should check for project initialization.

1. **MISSING FILES** → **STRICT** enforcement:
   - @.claude/ARCHITECTURE.md missing → **STOP** "⚠️ Project not initialized. Run `/pin:plan [description]` first to set up project architecture."
   - @.claude/CONVENTIONS.md missing → **STOP** "⚠️ Project not initialized. Run `/pin:plan [description]` first to set up conventions."
   - @.claude/SECURITY.md missing → **CONTINUE** with info "ℹ️ Security checklist not found. Consider reviewing OWASP guidelines."
   - Template files missing → **WARN** and create basic structure

2. **INCOMPLETE FILES** (placeholders found) → **STRICT** enforcement:
   - **ALL workflow commands** (requirements, design, tasks, align, execute) → **STOP** "⚠️ Cannot proceed. Found incomplete configuration in [file]. Please complete all fields or re-run `/pin:plan` to set up properly."
   - **Utility commands** (list, status, help) → **INFO** only (read-only operations don't need complete config)
   
   Placeholder patterns to check: `[e.g.,`, `[Type]`, `[Language]`, `[Tool]`, `[Framework]`

### Rationale for Strict Validation

The framework uses **STRICT** validation to ensure production-ready specifications:

**Why Strict Enforcement?**
- Prevents downstream errors from incomplete configuration
- Ensures all commands work with concrete, actionable information
- Eliminates ambiguity in technical specifications
- Forces early decision-making for cleaner implementation
- Reduces repeated validation checks across commands

**The `/pin:plan` Exception**:
- Only `/pin:plan` creates and populates configuration files
- It's the ONE place where placeholders are allowed (temporarily)
- Must complete ALL configuration before ending the planning phase
- Test runner MUST be specified and validated before planning completes
- No other command should find placeholders if planning was done correctly

**All Other Commands**:
- Assume configuration is complete and correct
- Stop immediately if ANY placeholders found (except utility commands)
- This ensures every command can rely on concrete values
- No need for repeated validation of the same fields
- Trust that `/pin:plan` did its job properly

3. **TEST RUNNER SPECIAL HANDLING**:
   - **During `/pin:plan`**: MUST be captured and validated before completion
   - **All other commands**: Trust it exists (already validated during planning)
   - **Only `/pin:execute`**: Reads and uses the test runner command directly
   - If somehow missing in execute: **STOP** with error about incomplete project setup

**Enhanced Validation Patterns**:
- Placeholder patterns: `[e.g.,`, `[Type]`, `[Language]`, `[Tool]`, `[Framework]`, brackets `[...]`
- Invalid values: "TBD", "TODO", "later", "will configure", "to be determined", "N/A"
- Empty values: Empty strings, just whitespace, or missing after colon
- Test runner specific: Must contain actual command words like "test", "pytest", "jest", "vitest", "mocha", "go test", "cargo test", etc.

**Exception**: The `/pin:plan` command skips these checks since it creates the files.

### Validation Implementation Pattern

```markdown
<analysis>
### Prerequisites Check (STRICT)
1. Check for @.claude/ARCHITECTURE.md and @.claude/CONVENTIONS.md existence
   - If either missing → **STOP** immediately with clear message
2. If files exist, scan for ANY placeholders:
   - Patterns: `[e.g.,`, `[Type]`, brackets `[...]`, "TBD", "TODO", "later"
   - If found in workflow commands → **STOP** immediately
   - If found in utility commands → **INFO** message only
3. Check for @.claude/SECURITY.md (informational only, never blocks)
4. NO repeated test runner validation (trust `/pin:plan` did its job)
   - Exception: `/pin:execute` uses the test runner but assumes it's valid
</analysis>
```

## Template Fallback Behavior (Standardized)

When templates are missing, follow this consistent approach:

1. **Check if template exists**: Use Read tool on `@.claude/templates/[template-name].md`
2. **If template exists**: 
   - Use template as base
   - Replace placeholders like `[Feature Name]` with actual values
   - Fill in sections with project-specific content
3. **If template missing**:
   - **WARN**: "⚠️ Template [template-name].md not found. Creating basic structure."
   - Create minimal structured document appropriate for the document type
   - Continue operation (don't block)

## Context Management Guidance (Standardized)

Provide consistent context management advice:

**Between Phases**: "💡 **Context Tip**: Consider using `/clear` before proceeding to [next-phase] for optimal performance."

**During Implementation**: "💡 **Performance Tip**: After completing 2-3 tasks, consider starting a fresh session with `/clear` and re-running the command to continue."

**Read-Only Commands**: "💡 **Performance Tip**: This is a lightweight command that doesn't accumulate significant context. No need to use `/clear` after this command."

## Language Detection (Standardized)

### Detection Order (stop at first match)

1. **TypeScript**: `package.json` exists + any `.ts`/`.tsx` files found
2. **JavaScript**: `package.json` exists + `.js`/`.jsx` files (no `.ts`)
3. **Python**: `requirements.txt` OR `setup.py` OR `pyproject.toml` OR `.py` files
4. **Go**: `go.mod` exists
5. **Rust**: `Cargo.toml` exists
6. **Java**: `pom.xml` OR `build.gradle` exists
7. **C#**: `*.csproj` files exist
8. **Ruby**: `Gemfile` exists
9. **PHP**: `composer.json` exists
10. **Other**: Default to generic standards

### Usage in Commands

When language-specific logic is needed:
1. Detect language using above rules
2. Apply language-specific standards from CONVENTIONS.md
3. If CONVENTIONS.md has placeholders, use detected language as default
4. Log detected language for user awareness: "ℹ️ Detected [language] project, applying [language] standards"

### Implementation Pattern

```markdown
<analysis>
### Language Detection
- Check for language indicators in order
- First match determines primary language
- Apply corresponding standards from CONVENTIONS.md
- If CONVENTIONS.md incomplete, use built-in defaults for detected language
</analysis>
```

## Universal Project Type Adaptation (Standardized)

**Project Type Detection**: Scan for these indicators to adapt templates and guidance:
- **Web Apps**: package.json with web frameworks, HTML/CSS files
- **CLI Tools**: package.json with commander/yargs, setup.py with click, go.mod with cobra
- **Libraries**: package.json with "main", setup.py with packages, public API exports
- **Mobile Apps**: react-native config, pubspec.yaml, platform-specific files
- **Desktop Apps**: electron/tauri config, native dependencies
- **Microservices**: Dockerfile, k8s configs, service mesh

**Adaptation Rules**:
1. **Requirements**: Adjust EARS examples for project context (API endpoints vs CLI commands)
2. **Design**: Include relevant sections (UI components vs command structure vs API contracts)
3. **Tasks**: Adapt task categories (frontend/backend vs parsing/output vs public API)
4. **Testing**: Match test types to project (component tests vs CLI integration vs library API)
5. **Performance**: Use appropriate metrics (Core Web Vitals vs response time vs throughput)

## Validation Summary Format (Standardized)

After validation, report issues using this format:

### If blocking issues (STOP)
```
⚠️ Cannot proceed. [Count] critical issue(s) found:
- [Issue 1]
- [Issue 2]

Resolution: [Specific action user should take]
```

### If non-blocking issues (WARN)
```
⚠️ [Count] warning(s) found (continuing):
- [Warning 1]
- [Warning 2]

Recommendation: [Optional action user could take]
```

### If all valid
```
✅ All prerequisites validated. Proceeding with [command action].
```

## Error Messages (Standardized)

**Feature Not Found**: "Feature '[name]' not found. Available features: [list]. Please specify an existing feature."

**Prerequisites Missing**: "⚠️ Project not properly initialized. Please run `/pin:plan [project-description]` first to set up [missing-component]."

**Placeholders Found**: "⚠️ Found placeholders in [file]. Please complete configuration or re-run `/pin:plan` to set up properly."

**Template Missing**: "⚠️ Template [name].md not found. Creating basic structure."

**Language Detected**: "ℹ️ Detected [language] project. Applying [language]-specific standards."

**Success with Next Steps**: "[Action] complete for **[feature-name]**. Ready to proceed with `/pin:[next-command] [feature-name]`?"

## Dependency Validation (Standardized)

### Unified Dependency Checking Approach

**ALL commands that read dependencies** use the same validation:
1. Check if dependent features exist in `features/` directory
2. Build dependency graph and check for circular dependencies
3. Check implementation status (tldr.md exists with "Complete" status)

**Severity by command**:
- **`/pin:requirements`**: **INFO** only - documenting dependencies is allowed
- **`/pin:design`**: **WARN** for issues but continue - design can proceed with caveats
- **`/pin:tasks`**: **WARN** for issues but continue - tasks can be planned
- **`/pin:align`**: **STOP** for circular dependencies - must be resolved
- **`/pin:execute`**: **WARN** for missing dependencies - user decides to continue or not

### Dependency Check Implementation

```markdown
<analysis>
### Dependency Validation
1. Extract dependencies from requirements.md
2. For each dependency:
   - Check if feature directory exists
   - If checking circularity: Read dependency's requirements
   - Build dependency chain recursively
3. Report findings with appropriate severity
</analysis>
```

### Circular Dependency Detection Algorithm

1. Start with current feature
2. For each dependency:
   - Add to visited set
   - Recursively check its dependencies
   - If current feature found in chain: circular dependency
3. Report full dependency chain if circular

### Test Runner Validation (Standardized)

**During `/pin:plan`** (ONLY place to validate):
- For new projects: REQUIRE test runner before proceeding
- For existing projects: AUTO-DETECT from package.json, Makefile, etc.
- If not found: ASK user explicitly
- Validate it looks like a real command (contains "test", "pytest", etc.)
- Never proceed with placeholder test runners
- Store in @.claude/CONVENTIONS.md as concrete value

**All other commands**:
- TRUST that test runner exists and is valid
- Do NOT re-validate what `/pin:plan` already checked

**During `/pin:execute`** (uses but doesn't validate):
- Read test runner from CONVENTIONS.md
- Use it directly to run tests
- If somehow missing/invalid: STOP with "Project setup incomplete. Please re-run `/pin:plan`."

## TLDR Generation Timing (Standardized)

**TLDR is generated EXACTLY ONCE when implementation stops**:

### Trigger Points for TLDR Generation:
1. **User stops execution** (answers "no" to "Continue to next task?")
2. **All tasks completed** (no more tasks to implement)
3. **User explicitly requests** TLDR generation when resuming completed feature
4. **Fatal error prevents continuation** (with user acknowledgment)

### TLDR Content Rules:
- **Status**: "Complete" if all tasks done, "Partial" if some remain, "MVP" if core done but enhancements remain
- **Reason if partial**: Required field when status is not "Complete"
- **Task Timeline**: List ONLY completed tasks with `[IMPLEMENTED]` marker
- **In-progress tasks**: Note as "Task N: [Started but not completed]" if work was begun
- **Files**: Document all files created/modified during THIS session
- **Decisions**: Key technical choices made during implementation

### Important:
- TLDR is NOT updated progressively - it's a snapshot at stopping point
- If resuming later, existing TLDR can be replaced with updated version
- TLDR represents "what was built" not "what was planned"

## Approval Gates (Standardized)

**Standard Format**: 
```
"[Phase] complete for **[feature-name]**. [Brief summary of what was created/analyzed]. Ready to proceed to [next-phase] with `/pin:[next-command] [feature-name]`, or would you like to review and modify first?

💡 **Context Tip**: [Appropriate context management advice]"
```