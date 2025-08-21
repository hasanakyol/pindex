---
description: Generate technical design from existing EARS requirements for a specific feature.
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep, TodoRead, TodoWrite
---

# Technical Design Generation

You are creating a comprehensive technical design based on existing EARS requirements following the Pindex methodology.

## Your Task

Generate technical design from existing requirements for the feature: **$ARGUMENTS**

## Feature Selection Logic

**Follow standardized logic** (see `@.claude/templates/shared-logic.md` for details):
- With feature name: Find matching directory, ask for confirmation if not found
- Without feature name: List all features and ask for selection
- No auto-selection even with single feature

## Process

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
   - Scan codebase for existing patterns and reusable components
</analysis>

2. **Locate requirements**: Find and read the requirements.md file in the selected feature directory

3. **Dependency Analysis** (check for circular dependencies):
   - Extract dependencies from the requirements.md Dependencies section
   - For each dependency:
     - Check if that feature's requirements.md exists
     - If exists, read its dependencies
     - Build a dependency graph
   - Check for circular dependencies:
     - If current feature appears in its own dependency chain
     - **WARN**: "⚠️ Warning: Potential circular dependency detected: [feature-a] → [feature-b] → [feature-a]. This may cause implementation issues."
     - Ask: "Do you want to continue with this design, or revise the dependencies first?"
   - Note: Hard enforcement happens in `/pin:align`

4. **Tech stack alignment**:
   <thinking>
   Evaluate architecture options based on @.claude/ARCHITECTURE.md:
   - What patterns exist in the current codebase?
   - Does this align with our chosen architecture pattern?
   - Which approach minimizes technical debt?
   - What provides the best performance per our targets?
   - How can we ensure maintainability?
   - What are the security implications per our @.claude/SECURITY.md OWASP checklist?
   - Are there trade-offs documented we should consider?
   </thinking>
   
   Reference @.claude/ARCHITECTURE.md for:
   - Chosen architecture pattern and rationale
   - Technology stack decisions
   - Performance targets to meet
   - Security measures to implement (from @.claude/SECURITY.md OWASP checklist)
   - Integration points to consider
   
   - For existing projects: Propose design that fits current architecture
   - For new projects: Present architecture options based on project type
   - Gather user preferences with up to 3 focused follow-ups
   <decision>
   Based on analysis, the optimal approach is:
   - Architecture pattern: [chosen pattern]
   - Key technologies: [selected stack]
   - Rationale: [why this approach]
   </decision>

4. **Initialize or augment design**:
   
   🚨 **CRITICAL: PRODUCTION-READY DESIGN STANDARDS**
   This framework generates PRODUCTION-READY DESIGNS, not drafts or concepts. Every design must be:
   - **COMPLETE**: Fully detailed with no "TBD", "TODO", or "to be determined" sections
   - **CONCRETE**: Actual schemas, real API specs, specific technologies - no placeholders
   - **IMPLEMENTABLE**: Ready for immediate development without gaps
   - **SPECIFIC**: Exact field types, response codes, error messages - no ambiguity
   
   **Examples of what this means**:
   | ❌ WRONG (Never Do This) | ✅ CORRECT (Always Do This) |
   |--------------------------|-----------------------------|
   | "API endpoint: /api/users (details TBD)" | Full endpoint spec with request/response schemas |
   | "Database: some SQL database" | "PostgreSQL 15 with specific schema definitions" |
   | "Auth: standard authentication" | "JWT with RS256, 1hr expiry, refresh tokens" |
   | "Error handling: appropriate errors" | Specific error codes, messages, and recovery flows |
   | "Performance: should be fast" | "< 200ms p95, with Redis caching strategy" |
   
   - IF `design.md` does not exist in the feature directory:
     - Check if `@.claude/templates/design.md` exists
     - If template exists: 
       - Use Write tool to create `features/[feature]/design.md` from template
       - Replace `[Feature Name]` placeholder with actual feature name
       - DO NOT leave any other placeholders - fill with project-specific content
       - EVERY section must have concrete, implementable details
     - **Template Fallback** (using standardized behavior): Check for `@.claude/templates/design.md`, warn and create basic structure if missing
   - ELSE (if design.md already exists):
     - Use Edit/MultiEdit to augment existing content
     - Fill any remaining placeholders with project-specific values
     - Replace any "TBD" or vague sections with concrete specifications
     - Expand sections including "Reusability and Integration"
     - Do NOT overwrite the file wholesale
   - Ensure design aligns with @.claude/ARCHITECTURE.md patterns and @.claude/CONVENTIONS.md standards

5. **Architecture/Convention Updates**: If design introduces new patterns:
   - Identify new architectural decisions (new services, layers, patterns)
   - Note new technology choices or integrations
   - Identify new conventions being established
   - Ask user: "This design introduces [specific additions] to the architecture. Should I update @.claude/ARCHITECTURE.md and @.claude/CONVENTIONS.md?"
   - If approved, update files with meaningful additions

6. **Seek approval**: Request explicit user approval of the design before proceeding

## Tech Stack Alignment

Read from @.claude/ARCHITECTURE.md to understand:
- **Project Type**: What kind of application this is
- **Architecture Pattern**: The chosen architectural approach
- **Technology Stack**: Language, framework, and runtime already decided
- **Data Layer**: Database and ORM choices
- **Infrastructure**: Deployment and hosting decisions

Use these established choices to inform the design. Do not present options or choices - work with what's already been decided in @.claude/ARCHITECTURE.md.

If @.claude/ARCHITECTURE.md has placeholders (contains [e.g., ...]):
- This means `/pin:plan` hasn't been run properly
- Ask user: "I notice @.claude/ARCHITECTURE.md still has placeholders. Please run `/pin:plan` first to establish project architecture, or provide the key decisions (project type, language, framework) so I can update @.claude/ARCHITECTURE.md."

## Template Usage

The design document structure is defined in `@.claude/templates/design.md`. The template includes:

- **Technical Overview**: Architecture approach, tech stack, key decisions
- **System Architecture**: Components, data flow, integrations
- **Data Design**: Schema, models, relationships
- **API Design**: Endpoints, authentication, authorization
- **Security Design**: Protection measures, validation strategies
- **Performance & Scalability**: Caching, optimization, scaling
- **Observability**: Logging, metrics, monitoring
- **Deployment**: Environments, configuration, migrations
- **Testing Strategy**: Coverage targets, test scenarios

The template adapts to project type (Web, CLI, Library, Mobile, Microservices) with appropriate sections.

## Design Quality Gates

Ensure design:

- [ ] Addresses every EARS requirement with specific technical solutions
- [ ] Includes concrete security measures (not just "considerations")
- [ ] Defines clear component boundaries with exact interfaces
- [ ] Specifies complete data models with all fields, types, and validations
- [ ] Covers error handling with specific error codes and recovery flows
- [ ] Includes measurable performance targets and optimization strategies
- [ ] Is immediately implementable without any ambiguity or gaps
- [ ] Contains NO placeholders, "TBD", "TODO", or vague descriptions
- [ ] Has specific technology choices, not generic categories
- [ ] Includes exact API contracts, database schemas, and configurations

## Key Guidelines

- Map each EARS requirement to specific, complete technical solutions
- Address all WHEN/THEN conditions with exact implementation approaches
- Include comprehensive error handling with specific error codes and messages
- Define concrete scalability targets and specific optimization strategies
- Specify exact interfaces with full schemas, types, and contracts
- Include detailed testing strategy with coverage targets and test scenarios
- **NEVER** use placeholder text like "appropriate", "standard", "typical", or "TBD"
- **ALWAYS** provide complete specifications ready for immediate implementation
- **ENSURE** every technical decision is explicit and unambiguous

## Approval Gate

<output>
After creating design.md, ask:
"Technical design complete for **[feature-name]**. The design addresses all requirements using [tech stack] with [key architectural decisions]. Ready to proceed to task breakdown with `/pin:tasks [feature-name]`, or would you like to review and modify the design first?

💡 **Performance Tip**: Consider using `/clear` before proceeding to tasks phase for optimal context management."
</output>

## Next Steps

- User reviews design and approves/requests changes
- Once approved, user can run `/pin:tasks` to proceed to implementation planning
- Design serves as blueprint for structured development

Now generate the technical design based on existing requirements.
