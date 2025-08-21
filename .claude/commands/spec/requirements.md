---
description: Interactively detail the EARS requirements for a specific feature.
allowed-tools: Read, Write, Edit, MultiEdit, Glob, TodoRead, TodoWrite
---

# Feature Requirements Detailing (Interactive)

You are detailing the requirements for a specific feature, which was likely outlined in the planning phase.

## Your Task

Facilitate a conversation to define the complete requirements for the feature: **$ARGUMENTS**

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

## Initial Context

<analysis>
1. **Read project context**:
   - Check if `architecture.md` exists; if yes, read it to understand project structure
   - Check if `conventions.md` exists; if yes, read it to understand coding standards
   - If either file is missing, note this but continue (they may be created later)
   - Use available context to inform requirement discussions
</analysis>

## Interactive Process

0.  **Analysis**: 
    <thinking>
    - What are the user's core needs?
    - What constraints exist in the current architecture?
    - What are the critical success factors?
    - What edge cases need consideration?
    - How will this integrate with existing features?
    </thinking>
    
    Consider the user goals and constraints in context of the existing architecture.
1.  **Initiate Requirements Process**: Start by confirming the feature. Read the existing `requirements.md` file.
    - **If file contains `<!-- DRAFT: Generated from planning, needs refinement -->`**:
      - Present: "I found draft requirements from the planning phase. I'll review these and ask for any clarifications needed."
      - Show the draft requirements
      - Ask: "Please provide any additional details, constraints, or corrections to these requirements."
    - **If file is missing or only contains template placeholders**:
      - Initialize from `.claude/templates/requirements.md` (replacing `[Feature Name]`)
      - Present: "To create comprehensive requirements, please provide:
        1. Main goal and success criteria
        2. User stories and workflows
        3. Any constraints or non-functional requirements
        4. Error handling needs"

2.  **Process User Input**: 
    <requirements-generation>
    Based on the information provided, generate comprehensive EARS requirements:
    - Transform user stories into formal EARS format
    - Include functional requirements (what the system does)
    - Include non-functional requirements (performance, security, usability)
    - Add error handling and edge cases
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
    - If approved, update `architecture.md` and/or `conventions.md` with meaningful additions

6.  **Final Approval**: Once the user confirms the requirements are complete:
    - **If draft marker exists**: Remove the `<!-- DRAFT: Generated from planning, needs refinement -->` line
    - Save the finalized requirements
    - Update architecture/conventions if changes were approved
    - Conclude the process

## Template Usage

The requirements structure is defined in `.claude/templates/requirements.md`. The template provides:

- **EARS Format**: Ubiquitous, Event-Driven, State-Driven, Conditional, Optional patterns
- **Sections**: Functional requirements, non-functional requirements, constraints, acceptance criteria
- **Adaptability**: Adjusts to project type (Web, CLI, Library, Mobile, Service)
- **Scope**: MVP-first approach with clear out-of-scope section

See template file for complete EARS syntax and structure.

## Final Approval Gate

<output>
After updating the file, conclude with the standard approval gate:
"Requirements for **[feature-name]** are now detailed in `features/[feature-name]/requirements.md`. Ready to proceed to the design phase with `/spec:design [feature-name]`?

💡 **Context Tip**: Consider using `/clear` before proceeding to the design phase for optimal performance."
</output>

## Key Guidelines

- Be conversational and inquisitive.
- Guide the user towards providing specific, testable details.
- Translate the user's needs into formal EARS requirements collaboratively.
- Persist changes to the `requirements.md` file as they are approved.

Now, start the interactive process to detail the specification for: **$ARGUMENTS**
