# Requirements: [Feature Name]

> Note: Adapt sections to your project type. Remove/modify sections that don't apply.

## Overview
Brief description and business value

## Dependencies

### Feature Dependencies
This feature depends on the following other features:
- [feature-number-name]: [What functionality is needed and why]
- [feature-number-name]: [What functionality is needed and why]
- Write "None" if no dependencies

### Integration Points
- [External systems or APIs this feature connects to]
- [Shared components or services this feature uses]
- Write "None" if no integrations

### Dependency Notes
- [Any assumptions about dependency implementation status]
- [Risk mitigation if dependencies are delayed]
- [Alternative approaches if dependencies change]

## Functional Requirements (EARS)

### Core Functionality
- The system SHALL [primary functions]
- WHEN [trigger] THEN the system SHALL [response]
- WHILE [state] the system SHALL [behavior]

### User/System Interactions
- WHEN [action/event] THEN the system SHALL [response]
- IF [condition] THEN the system SHALL [behavior]

### Data Management (if applicable)
- The system SHALL [data operations]
- WHEN [data event] THEN the system SHALL [action]

### Integration Requirements (if applicable)
- The system SHALL [integrate with X]
- WHEN [external event] THEN the system SHALL [handle]

### Error Handling
- IF [error condition] THEN the system SHALL [recovery action]
- WHEN [failure] THEN the system SHALL [fallback behavior]

## Non-Functional Requirements

### Performance (adapt to project type)
- **Web Apps**: Core Web Vitals (LCP <2.5s, FID <100ms, CLS <0.1), bundle size <150KB gzipped
- **CLI Tools**: Startup time <1s, memory usage <50MB, command completion <200ms
- **Libraries**: Bundle size <100KB, tree-shakeable, zero runtime dependencies preferred
- **Mobile Apps**: App launch <3s, 60fps animations, battery-efficient, offline capable
- **Desktop Apps**: Launch time <2s, memory efficient, native performance feel
- **APIs/Services**: Response time <200ms p95, throughput as needed, horizontal scalability

### Security (adapt to project needs)
- Authentication: [if applicable]
- Authorization: [if applicable]
- Data protection: [if handling sensitive data]
- Input validation: [security approach]

### Reliability
- Availability target: [if applicable]
- Error recovery: [strategy]
- Data integrity: [if applicable]

### Usability (adapt to project type)
- **CLI Tools**: Clear commands, helpful output, good defaults, intuitive argument structure
- **Web/Mobile Apps**: Responsive design, intuitive navigation, accessibility (WCAG), fast interactions
- **Libraries/SDKs**: Clean API, comprehensive docs, predictable behavior, good error messages
- **Desktop Apps**: Native look/feel, keyboard shortcuts, standard patterns, good performance
- **Services/APIs**: Clear contracts, meaningful errors, good documentation, monitoring dashboards

### Compatibility (if applicable)
- Platform support: [target platforms]
- Version compatibility: [backward/forward compatibility]
- Integration compatibility: [third-party systems]

### Observability (adapt to project needs)
- **Web Apps**: Error tracking (Sentry), performance monitoring, user analytics
- **CLI Tools**: Structured logging, crash reports, usage telemetry (opt-in)
- **Libraries**: Debug information, clear error stack traces, development warnings
- **Mobile Apps**: Crash reporting, performance metrics, user flow analytics
- **Desktop Apps**: Error reporting, performance metrics, feature usage tracking
- **APIs/Services**: Structured logging, metrics (Prometheus), distributed tracing, health checks

## Constraints & Assumptions

### Technical Constraints
- [Existing system limitations]
- [Technology constraints]
- [Performance constraints]

### Business Constraints
- [Timeline, budget, resources]
- [Regulatory requirements]
- [Business rules]

### Assumptions
- [What we're assuming to be true]
- [Dependencies on other systems/teams]
- [Environmental assumptions]

## Acceptance Criteria
- [ ] All functional requirements satisfied
- [ ] Performance targets met (if defined)
- [ ] Security measures implemented (if applicable)
- [ ] Tests passing
- [ ] Documentation complete

## Out of Scope
- [Explicitly list what this feature does NOT include]
- [Future enhancements to consider later]