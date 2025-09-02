# Standards Reference

## Requirements
| Never | Always |
|-------|--------|
| "fast" | "<200ms p95" |
| "secure" | "JWT RS256 1hr expiry" |
| "user-friendly" | "displays error within 2s" |
| "good performance" | "1000 concurrent users" |
| "appropriate" | specific technology/metric |

## Design
| Never | Always |
|-------|--------|
| "details TBD" | complete specifications |
| "standard auth" | "JWT with refresh tokens" |
| "some database" | "PostgreSQL 15" |
| "appropriate errors" | specific error codes |

## Tasks
| Never | Always |
|-------|--------|
| mock/stub/placeholder | real implementation |
| "return fake data" | actual database query |
| "TODO: implement" | complete functionality |
| test with mocks | test real behavior |

## Code Quality
- NO any types → use unknown or specific
- NO bare except → catch specific errors
- NO mutable defaults → use None pattern
- ALWAYS handle null/undefined
- ALWAYS validate inputs
- ALWAYS close resources