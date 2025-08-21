# Tasks: [Feature Name]

## Task Overview
[Number] tasks for implementation, adapted to project type and architecture

Note on completion and status:
- When a task is completed, append `[IMPLEMENTED]` to its heading
- Add a brief `**Completion**:` line immediately below the task heading summarizing changes and decisions

## Task Structure Guidelines

> IMPORTANT: Use 7-8 tasks as a flexible scaffold. Adapt task titles and content to your specific feature.
> Keep the numbered format (## Task N: Title) but customize everything else.

### For Most Projects:

## Task 1: Foundation & Setup
- Project structure for this feature
- Dependencies and configuration
- Development environment setup
- Initial scaffolding

### Reused Components
- List specific existing code being reused, or write "None" if nothing is reused

### Changes to Existing Code  
- Describe modifications needed to shared code, or write "None" if no changes needed

## Task 2: Core Data Layer (if applicable)
- Data models/structures
- Storage implementation
- Data validation rules
- Core business entities

### Reused Components
- [List any existing data models or storage utilities being reused]

### Changes to Existing Code
- [Describe any schema changes or data migration needs]

## Task 3: Core Logic Implementation
- Primary feature functionality
- Business rules and processing
- Core algorithms
- Main workflows

### Reused Components
- [List any existing logic or utilities being reused]

### Changes to Existing Code
- [Describe any changes to shared logic or interfaces]

## Task 4: External Interfaces (if applicable)
- API endpoints, CLI commands, or UI components
- Input/output handling
- Request/response processing
- User interaction points

### Reused Components
- [List any existing interfaces or handlers being reused]

### Changes to Existing Code
- [Describe any changes to existing interfaces]

## Task 5: Integration & Connectivity (if applicable)
- External service connections
- Third-party integrations
- Inter-component communication
- Event handling

### Reused Components
- [List any existing integrations being reused]

### Changes to Existing Code
- [Describe any changes to integration points]

## Task 6: Quality & Reliability
- Error handling and recovery
- Performance optimization
- Security measures
- Data validation

### Reused Components
- [List any existing quality utilities being reused]

### Changes to Existing Code
- [Describe any improvements to shared error handling or security]

## Task 7: Observability & Monitoring (if applicable)
- Logging implementation
- Metrics and telemetry
- Health checks
- Debugging support

### Reused Components
- [List any existing monitoring utilities being reused]

### Changes to Existing Code
- [Describe any changes to logging or monitoring infrastructure]

## Task 8: Testing & Documentation
- Unit tests
- Integration tests
- End-to-end tests (if applicable)
- Documentation updates
- Usage examples

### Testing Strategy
- [Describe testing approach specific to project type]

### Documentation Updates
- [List documentation that needs updating]

## Project-Specific Adaptations

> Examples of how tasks might be structured for different project types:
> - **CLI**: Command parsing → Core logic → Output → Config → Error handling → Testing
> - **Library**: API design → Core implementation → Validation → Optimization → Examples → Testing
> - **Mobile**: UI components → State → Persistence → Network → Platform features → Testing  
> - **Microservice**: Scaffolding → API contracts → Business logic → Persistence → Communication → Monitoring

## Remember

- Always use format: `## Task N: [Your Title]`
- Include TDD cycle (Red-Green-Refactor) for each task
- Fill reusability sections with actual findings or "None"
- Mark completed tasks with `[IMPLEMENTED]` in heading
- Add `**Completion**: [summary]` line under completed task headings

## Integration Checklist
- [ ] Existing functionality remains intact
- [ ] Shared code changes are backward compatible
- [ ] All integration points tested
- [ ] Documentation reflects changes
- [ ] Performance metrics maintained or improved