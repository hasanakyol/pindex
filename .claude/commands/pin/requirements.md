---
description: Interactively detail the EARS requirements for a specific feature.
allowed-tools: Read, Write, Edit, MultiEdit, Glob, TodoRead, TodoWrite
---

# Feature Requirements Detailing (Interactive)

You are detailing the requirements for a specific feature, which was likely outlined in the planning phase.

## Your Task

Facilitate a conversation to define the complete requirements for the feature: **$ARGUMENTS**

## Feature Selection Logic

**Follow standardized logic** (see `@.claude/templates/shared-logic.md` for details):
- With feature name: Find matching directory, ask for confirmation if not found
- Without feature name: List all features and ask for selection
- No auto-selection even with single feature

## Initial Context

<analysis>
1. **Prerequisites Check** (STRICT validation from `@.claude/templates/shared-logic.md`):
   - Check if @.claude/ARCHITECTURE.md exists; if not, **STOP**: "⚠️ Project not initialized. Run `/pin:plan [description]` first to set up project architecture."
   - If exists, scan for placeholder patterns: `[e.g.,`, `[Type]`, `[Language]`, `TODO`, `TBD`
   - If placeholders found, **STOP**: "⚠️ Cannot proceed. Found incomplete configuration in @.claude/ARCHITECTURE.md. Please complete all fields or re-run `/pin:plan`."
   - Check if @.claude/CONVENTIONS.md exists; if not, **STOP**: "⚠️ Project not initialized. Run `/pin:plan [description]` first to set up conventions."
   - If exists, scan for placeholder patterns: `[e.g.,`, `[Tool]`, `[Framework]`, `TODO`, `TBD`
   - If placeholders found, **STOP**: "⚠️ Cannot proceed. Found incomplete configuration in @.claude/CONVENTIONS.md. Please complete all fields or re-run `/pin:plan`."
   - Check if @.claude/SECURITY.md exists; if missing, continue with info: "ℹ️ Security checklist not found. Consider reviewing OWASP guidelines."
   - Trust that test runner was properly configured during `/pin:plan`
</analysis>

## Interactive Process

0.  **Analysis**: 
    <thinking>
    - What are the user's core needs?
    - What constraints exist in the current architecture?
    - What performance targets must we meet (from @.claude/ARCHITECTURE.md)?
    - What security requirements apply (from @.claude/SECURITY.md OWASP checklist)?
    - What are the critical success factors?
    - What edge cases need consideration?
    - How will this integrate with existing features and integration points?
    - Are there documented trade-offs we should consider?
    </thinking>
    
    Consider the user goals and constraints in context of:
    - Architecture constraints and assumptions from @.claude/ARCHITECTURE.md
    - Performance targets and scalability requirements
    - Security checklist items from @.claude/SECURITY.md that apply to this feature
    - Integration points with external services
1.  **Initiate Requirements Process**: Start by confirming the feature. Read the existing `requirements.md` file.
    - **If file contains `<!-- DRAFT: Generated from planning, needs refinement -->`**:
      - Present: "I found draft requirements from the planning phase. I'll review these and ask for any clarifications needed."
      - Show the draft requirements
      - Check for dependencies in the requirements
      - Ask: "Please provide any additional details, constraints, or corrections to these requirements."
    - **If file is missing or only contains template placeholders**:
      - Initialize from `@.claude/templates/requirements.md` (replacing `[Feature Name]`)
      - Present: "To create comprehensive requirements, please provide:
        1. Main goal and success criteria
        2. User stories and workflows
        3. Any constraints or non-functional requirements
        4. Error handling needs
        5. Dependencies on other features (if any)"

2.  **Dependency Validation** (if dependencies are specified):
    - When user mentions dependencies or when found in draft requirements:
      - Use Glob to check if dependent features exist in `features/` directory
      - For each dependency:
        * If exists: "✅ Dependency '[feature-name]' found"
        * If missing: "⚠️ Warning: Feature '[feature-name]' not found. This dependency will need to be implemented first."
      - If any missing: Ask "Do you want to continue with these dependencies, or would you like to revise?"
    - Document all dependencies clearly in the Dependencies section
    - Note: Full circular dependency checking happens in `/pin:align`

3.  **Process User Input**: 
    
    🚨 **CRITICAL: PRODUCTION REQUIREMENTS STANDARDS**
    This framework generates PRODUCTION-READY REQUIREMENTS, not wishful thinking. Every requirement must be:
    - **SPECIFIC**: Measurable criteria, not vague desires
    - **TESTABLE**: Clear pass/fail conditions
    - **ACHIEVABLE**: Realistic given constraints
    - **COMPLETE**: No ambiguity or gaps
    
    **Examples of what this means**:
    | ❌ WRONG (Never Do This) | ✅ CORRECT (Always Do This) |
    |--------------------------|-----------------------------|
    | "System should be fast" | "System SHALL respond within 200ms for 95% of requests" |
    | "User-friendly interface" | "WHEN user enters invalid data THEN system SHALL display specific error message within 2 seconds" |
    | "Secure authentication" | "System SHALL implement JWT with RS256, 1-hour expiry, and refresh tokens" |
    | "Handle errors gracefully" | "IF database connection fails THEN system SHALL retry 3 times with exponential backoff" |
    | "Good performance" | "System SHALL handle 1000 concurrent users with <2s page load" |
    
    <requirements-generation>
    Based on the information provided, generate comprehensive EARS requirements:
    - Transform user stories into formal EARS format with SPECIFIC metrics
    - Include functional requirements (what the system does) with EXACT behavior
    - Include non-functional requirements aligned with @.claude/ARCHITECTURE.md:
      * Performance targets with SPECIFIC numbers (ms, requests/sec, etc.)
      * Security requirements with EXACT measures (encryption type, token expiry, etc.)
      * Scalability with CONCRETE targets (users, data volume, etc.)
      * Integration requirements with PRECISE protocols and formats
    - Add error handling with SPECIFIC error codes and recovery procedures
    - Ensure requirements respect documented constraints and assumptions
    - NEVER use words like "appropriate", "suitable", "reasonable", "fast", "secure"
    - ALWAYS use measurable values and specific technologies
    </requirements-generation>

3.  **Present Draft Requirements**: Show the complete EARS requirements and ask for confirmation:
    - "Based on your input, I've created the following EARS requirements:
      [Show requirements]
      Please review and let me know if any changes are needed."

4.  **Finalize Requirements**: After user confirmation, save the complete requirements.

5.  **Architecture/Convention Updates**: If requirements reveal need for new patterns:
    - Identify any new architectural components or patterns needed
    - Note any new conventions that should be established
    - Ask user: "These requirements suggest [specific changes] to the architecture/conventions. Should I update these files?"
    - If approved, update @.claude/ARCHITECTURE.md and/or @.claude/CONVENTIONS.md with meaningful additions

6.  **Final Approval**: Once the user confirms the requirements are complete:
    - **If draft marker exists**: Remove the `<!-- DRAFT: Generated from planning, needs refinement -->` line
    - Save the finalized requirements
    - Update architecture/conventions if changes were approved
    - Conclude the process

## Template Usage

The requirements structure is defined in `@.claude/templates/requirements.md`. The template provides:

- **EARS Format**: Ubiquitous, Event-Driven, State-Driven, Conditional, Optional patterns
  - Each pattern must include SPECIFIC, MEASURABLE criteria
  - No generic or ambiguous language allowed
- **Sections**: Functional requirements, non-functional requirements, constraints, acceptance criteria
  - Non-functional MUST have numbers (response times, throughput, etc.)
  - Constraints MUST be concrete (specific versions, platforms, etc.)
- **Adaptability**: Adjusts to project type (Web, CLI, Library, Mobile, Service)
- **Scope**: MVP-first approach with clear out-of-scope section

See template file for complete EARS syntax and structure.

## Final Approval Gate

<output>
After updating the file, conclude with the standard approval gate:
"Requirements for **[feature-name]** are now detailed in `features/[feature-name]/requirements.md`. Ready to proceed to the design phase with `/pin:design [feature-name]`?

💡 **Context Tip**: Consider using `/clear` before proceeding to the design phase for optimal performance."
</output>

## Key Guidelines

- Be conversational and inquisitive.
- Guide the user towards providing SPECIFIC, MEASURABLE details.
- Translate the user's needs into formal EARS requirements with CONCRETE criteria.
- Persist changes to the `requirements.md` file as they are approved.
- **NEVER** accept vague requirements like "fast", "secure", "user-friendly"
- **ALWAYS** push for specific metrics, exact technologies, and measurable outcomes
- **ENSURE** every requirement can be tested with a clear pass/fail condition

Now, start the interactive process to detail the specification for: **$ARGUMENTS**
