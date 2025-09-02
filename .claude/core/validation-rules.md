# Validation Rules

## Prerequisites (STRICT)
STOP if missing: @.claude/ARCHITECTURE.md or @.claude/CONVENTIONS.md
→ "⚠️ Project not initialized. Run `/pin:plan [description]` first."

STOP if placeholders found: [e.g., [Type], [Language], TODO, TBD
→ "⚠️ Cannot proceed. Found incomplete configuration. Complete all fields or re-run `/pin:plan`."

INFO if missing: @.claude/SECURITY.md
→ "ℹ️ Security checklist not found. Consider reviewing OWASP guidelines."

## Test Runner
Trust test runner from /pin:plan - already validated
Only /pin:execute uses it directly
If missing in execute: "⚠️ Project setup incomplete. Re-run `/pin:plan`."

## Placeholder Patterns
Check for: [e.g., [Type], [...], TODO, TBD, "later", empty after colon