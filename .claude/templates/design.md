# Design: [Feature Name]

> Note: Adapt sections to your architecture. Keep what's relevant, remove what's not.

## Technical Overview
- Architecture Approach: [aligned with project's architecture pattern]
- Technology Stack: [languages, frameworks, tools used]
- Key Design Decisions: [3-5 important choices made]

## System Architecture

### Component Structure
[Adapt based on project type:]
- For Web Apps: Frontend components, backend services, data layer
- For CLI Tools: Command structure, core logic, I/O handling
- For Libraries: Public API, internal modules, utilities
- For Mobile Apps: Views, controllers, models, platform services
- For Microservices: Service boundaries, communication, data ownership

### Data Flow
[How data moves through the feature]
- Input sources
- Processing steps
- Output destinations
- Error paths

### Integration Points
[How this feature connects with existing code]
- Existing modules/components used
- Interfaces/contracts defined
- External dependencies

## Data Design (if applicable)

### Data Structures
- Core data models/entities
- Data relationships
- Validation rules

### Storage Strategy (if applicable)
- Persistence approach
- Caching strategy
- Data lifecycle

## Interface Design

[Adapt based on project type:]

### For Web/Mobile Apps:
- User interface components
- State management
- Event handling
- Navigation flow

### For APIs/Services:
- Endpoints/methods
- Request/response formats
- Error responses
- Rate limiting

### For CLI Tools:
- Command structure
- Arguments and options
- Output formats
- Interactive elements

### For Libraries:
- Public API surface
- Method signatures
- Return types
- Error handling

## Security Design (if applicable)
- Authentication approach
- Authorization model
- Data protection measures
- Input validation strategy
- Security headers/configurations

## Performance & Scalability
- Performance optimizations
- Caching approach (if applicable)
- Resource management
- Scaling strategy (if applicable)

## Error Handling & Recovery
- Error types and categories
- Recovery strategies
- Fallback mechanisms
- User feedback

## Observability
- Logging approach
- Metrics to collect (if applicable)
- Debugging support
- Health checks (if applicable)

## Testing Strategy
- Unit test approach
- Integration test scenarios
- End-to-end tests (if applicable)
- Performance tests (if applicable)
- Security tests (if applicable)

## Deployment & Configuration (if applicable)
- Environment requirements
- Configuration management
- Feature flags (if applicable)
- Rollback strategy

## Dependencies & Risks

### Dependencies
- External libraries/packages
- System requirements
- Third-party services

### Risks & Mitigations
- Technical risks
- Performance risks
- Security risks
- Mitigation strategies

## Implementation Notes
- Development sequence
- Critical path items
- Parallel work opportunities
- Review/approval points

## Future Considerations
- Extensibility points
- Potential optimizations
- Technical debt items
- Enhancement opportunities