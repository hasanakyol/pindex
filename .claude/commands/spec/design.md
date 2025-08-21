---
description: Generate technical design from existing EARS requirements for a specific feature.
allowed-tools: Read, Write, Edit, MultiEdit, Glob, Grep, TodoRead, TodoWrite
---

# Technical Design Generation

You are creating a comprehensive technical design based on existing EARS requirements following the Pindex methodology.

## Your Task

Generate technical design from existing requirements for the feature: **$ARGUMENTS**

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

## Process

<analysis>
1. **Analyze project context**
   - Check if `architecture.md` exists; if yes, read it to understand project structure
   - Check if `conventions.md` exists; if yes, read it to understand coding standards
   - If missing, note that architecture/conventions will be established with this design
   - Scan codebase for existing patterns, frameworks, and components
   - Identify reusable modules, services, utilities, or handlers
   - Note findings under "Reusability and Integration"
   - Example: "Found existing User model in models/user.py and AuthService in services/auth.py; will extend auth.login() to support OTP"
</analysis>

2. **Locate requirements**: Find and read the requirements.md file in the selected feature directory

3. **Tech stack alignment**:
   <thinking>
   Evaluate architecture options:
   - What patterns exist in the current codebase?
   - Which approach minimizes technical debt?
   - What provides the best performance?
   - How can we ensure maintainability?
   - What are the security implications?
   </thinking>
   
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
   - IF `design.md` does not exist:
     - Check if `.claude/templates/design.md` exists
     - If template exists: Initialize from template (replacing `[Feature Name]`)
     - If template missing: Warn user "Template design.md not found. Creating from structure." and create structured design document
   - ELSE, augment the existing `design.md` in-place by filling placeholders and expanding sections (including "Reusability and Integration"). Do NOT overwrite the file wholesale.
   - Ensure design aligns with discovered/established architecture patterns

5. **Architecture/Convention Updates**: If design introduces new patterns:
   - Identify new architectural decisions (new services, layers, patterns)
   - Note new technology choices or integrations
   - Identify new conventions being established
   - Ask user: "This design introduces [specific additions] to the architecture. Should I update architecture.md and conventions.md?"
   - If approved, update files with meaningful additions

6. **Seek approval**: Request explicit user approval of the design before proceeding

## Tech Stack Options (for new projects)

Adapt options based on project type:

### For Web Applications:

1. **Full-Stack JavaScript** (Node.js + React/Vue + Database)
2. **Python Backend + Modern Frontend** (FastAPI/Django + React/Vue + Database)
3. **Cloud-Native Microservices** (Kubernetes + API Gateway + Managed Services)
4. **Enterprise Java/C#** (Spring Boot/.NET + Enterprise patterns)
5. **Custom/Other** (User specifies or modifies above options)

### For CLI Tools:

1. **Go** (Fast, single binary, cross-platform)
2. **Python** (Rich ecosystem, easy distribution)
3. **Node.js** (JavaScript ecosystem, npm distribution)
4. **Rust** (Performance, memory safety)
5. **Custom/Other**

### For Libraries/SDKs:

1. **TypeScript** (Type safety, npm ecosystem)
2. **Python** (PyPI distribution, wide adoption)
3. **Go** (Module system, performance)
4. **Multiple Languages** (Polyglot support)
5. **Custom/Other**

### For Mobile Apps:

1. **React Native** (Cross-platform, JavaScript)
2. **Flutter** (Cross-platform, Dart)
3. **Native** (Swift/Kotlin)
4. **Progressive Web App** (Web technologies)
5. **Custom/Other**

Then ask up to 3 follow-up questions about:

- Specific frameworks/libraries within chosen stack
- Database preferences and data modeling approach
- Deployment and infrastructure preferences

## Template Usage

The design document structure is defined in `.claude/templates/design.md`. The template includes:

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

- [ ] Addresses every EARS requirement
- [ ] Includes security considerations
- [ ] Defines clear component boundaries
- [ ] Specifies data models and relationships
- [ ] Covers error handling and edge cases
- [ ] Includes performance considerations
- [ ] Is implementable with chosen tech stack

## Key Guidelines

- Map each EARS requirement to specific technical solutions
- Address all WHEN/THEN conditions with technical approaches
- Include comprehensive error handling strategies
- Consider scalability and maintainability
- Specify clear interfaces between components
- Include testing strategy for design validation

## Approval Gate

<output>
After creating design.md, ask:
"Technical design complete for **[feature-name]**. The design addresses all requirements using [tech stack] with [key architectural decisions]. Ready to proceed to task breakdown with `/spec:tasks [feature-name]`, or would you like to review and modify the design first?

💡 **Performance Tip**: Consider using `/clear` before proceeding to tasks phase for optimal context management."
</output>

## Next Steps

- User reviews design and approves/requests changes
- Once approved, user can run `/spec:tasks` to proceed to implementation planning
- Design serves as blueprint for structured development

Now generate the technical design based on existing requirements.
