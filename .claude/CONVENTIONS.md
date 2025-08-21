# Project Conventions

> This file documents the specific conventions for this project. The framework can auto-detect language and apply defaults if these fields contain placeholders.

## Language & Stack

<!-- Language will be auto-detected during command execution if placeholders remain -->
**Primary Language**: [e.g., TypeScript 5.3+ with strict mode]  <!-- Auto-detected from project files -->
**Runtime**: [e.g., Bun 1.0+, Node.js 20 LTS]
**Package Manager**: [e.g., Bun, pnpm 8+, yarn 4]
**Monorepo Tool**: [e.g., Turborepo, Nx, Rush, Lerna 7]
**Backend Framework**: [e.g., Hono, Elysia, Fastify 4, NestJS]
**Frontend Framework**: [e.g., Next.js 14 App Router, Remix, SvelteKit]

## Code Style

**Code Quality Tool**: [e.g., Biome (replaces ESLint+Prettier), oxlint]
**Type Checking**: [e.g., tsc --noEmit in CI, strict mode enabled]
**Formatter Config**: [e.g., 2 spaces, semicolons, single quotes]
**Pre-commit Hooks**: [e.g., Husky + lint-staged, Lefthook]
**Import Sorting**: [e.g., Biome import sorting, trivago/prettier-plugin-sort-imports]

### Naming Conventions

```
Files:
  Components: PascalCase.tsx       (UserProfile.tsx)
  Utilities: camelCase.ts          (dateUtils.ts)
  Tests: *.test.ts or *.spec.ts    (user.test.ts)
  Types: types.ts or *.types.ts    (user.types.ts)

Code:
  Variables: camelCase             (userId, userName)
  Constants: UPPER_SNAKE_CASE      (MAX_RETRY_COUNT)
  Functions: camelCase (verbs)      (getUserById, calculateTotal)
  Classes: PascalCase               (UserService, DataProcessor)
  Interfaces: PascalCase with I    (IUser, IAuthService)
  Enums: PascalCase                (UserRole, StatusCode)
  Booleans: is/has/should prefix   (isActive, hasPermission)
```

## Project Structure

```
src/
├── components/     # React components
├── pages/          # Next.js pages
├── services/       # Business logic
├── utils/          # Utility functions
├── types/          # TypeScript types
├── hooks/          # Custom React hooks
└── styles/         # Global styles
```

## Testing

**Test Runner**: [e.g., Vitest (Vite-native), Bun test, Jest 29]
**Component Testing**: [e.g., React Testing Library, Vue Test Utils, Testing Library]
**E2E Testing**: [e.g., Playwright, Cypress 13]
**Test Location**: [e.g., Alongside source as *.test.ts, separate __tests__ folders]
**Coverage Target**: [e.g., 80% statements, 70% branches, 100% critical paths]
**API Testing**: [e.g., Supertest, Hono testing utilities, MSW for mocking]

### Test Patterns

```typescript
// Test naming: "should [expected behavior] when [condition]"
import { describe, it, expect, beforeEach } from 'vitest';
import { renderHook, waitFor } from '@testing-library/react';

describe('User Service', () => {
  it('should return user data when valid ID provided', async () => {
    // Arrange
    const userId = '123';

    // Act
    const result = await getUserById(userId);

    // Assert
    expect(result).toEqual(expectedUser);
  });

  // Test error cases
  it('should handle invalid user ID gracefully', async () => {
    await expect(getUserById('invalid')).rejects.toThrow('Invalid user ID');
  });
});
```

## Git Workflow

**Branch Naming**: `feature/[ticket-number]-brief-description`
**Commit Format**: Conventional Commits (`feat:`, `fix:`, `docs:`, etc.)
**PR Reviews Required**: [e.g., 1 approval minimum]

### Commit Examples
```
feat: add user authentication flow
fix: resolve memory leak in data processor
docs: update API documentation
refactor: simplify error handling logic
```

## Error Handling

```typescript
// Custom error class with cause chain support
class AppError extends Error {
  constructor(
    message: string,
    public code: string,
    public statusCode: number,
    public cause?: unknown
  ) {
    super(message, { cause });
    this.name = 'AppError';
  }

  toJSON() {
    return {
      name: this.name,
      message: this.message,
      code: this.code,
      statusCode: this.statusCode,
      stack: this.stack
    };
  }
}

// Usage with Zod validation
import { z } from 'zod';

const userSchema = z.object({
  id: z.string().uuid(),
  email: z.string().email()
});

try {
  const user = userSchema.parse(data);
} catch (error) {
  throw new AppError('Validation failed', 'VALIDATION_ERROR', 400, error);
}
```

**Logging Levels**:
- ERROR: System failures, unrecoverable errors
- WARN: Recoverable issues, degraded performance
- INFO: Important business events
- DEBUG: Development and troubleshooting

## API Conventions

**API Style**: [e.g., REST, tRPC for type-safety, GraphQL with Pothos]
**REST Endpoints**: [e.g., kebab-case `/api/user-profiles`, resource-based]
**Response Format**: [e.g., JSON:API spec, `{ data, error, meta }` structure]
**Type Safety**: [e.g., Zod schemas for validation, tRPC for end-to-end types]
**Authentication**: [e.g., JWT with refresh tokens, Session cookies, OAuth 2.0]
**Rate Limiting**: [e.g., Token bucket, sliding window, IP-based]
**Versioning**: [e.g., URL `/api/v1/`, Header-based, GraphQL schema evolution]
**Error Codes**: [e.g., Standard HTTP codes + custom application codes]

## Database Conventions

**Table Naming**: [e.g., snake_case plural `user_profiles`]
**Column Naming**: [e.g., snake_case `created_at`, camelCase for JSON columns]
**Primary Keys**: [e.g., UUID v7 (time-ordered), ULID, Snowflake IDs]
**Timestamps**: [e.g., `created_at`, `updated_at`, `deleted_at` for soft delete]
**Migrations**: [e.g., Drizzle Kit, Prisma Migrate, Kysely migrations]
**Indexes**: [e.g., Add indexes for all foreign keys and frequent WHERE clauses]
**Constraints**: [e.g., Use database-level constraints, not just application validation]

## Documentation

**Code Comments**: Only for complex logic or business rules
**API Docs**: [e.g., OpenAPI/Swagger at `/api/docs`]
**README**: Must include setup, development, and deployment sections

## Security Practices (OWASP Top 10 Compliance)

### Input Validation & Sanitization
- Zod schemas for all API inputs
- HTML sanitization with DOMPurify or similar
- File upload restrictions (type, size, scanning)
- SQL injection prevention via ORMs/query builders

### Authentication & Authorization
- Secure session management (httpOnly, secure, sameSite cookies)
- Password hashing with Argon2id or bcrypt (min cost 12)
- MFA/2FA support
- JWT with short expiry and refresh tokens
- Rate limiting on auth endpoints

### Data Protection
- Encryption at rest and in transit (TLS 1.3+)
- PII data masking in logs
- Secrets in environment variables or secret managers
- Database connection pooling with SSL

### Security Headers & Policies
- Content Security Policy (CSP)
- HSTS, X-Frame-Options, X-Content-Type-Options
- CORS with explicit allowed origins
- Subresource Integrity (SRI) for CDN assets

### Dependency & Infrastructure Security
- Automated dependency scanning (Snyk, Socket.dev)
- Container scanning in CI/CD
- Regular security updates (Dependabot)
- Infrastructure as Code security scanning
- Web Application Firewall (WAF) rules

## Performance Standards

### Core Web Vitals (Required)
- **LCP** (Largest Contentful Paint): < 2.5s
- **FID** (First Input Delay): < 100ms
- **CLS** (Cumulative Layout Shift): < 0.1
- **INP** (Interaction to Next Paint): < 200ms

### Application Metrics
- API response time: < 100ms p50, < 200ms p95
- Time to First Byte: < 200ms
- Bundle size: < 150KB gzipped (initial), < 300KB total
- Lighthouse score: > 95 (all categories)
- Database queries: < 50ms p95
- Memory usage: < 512MB per instance
- Cold start time: < 1s (serverless)

### Optimization Strategies
- Code splitting and lazy loading
- Image optimization (WebP/AVIF with fallbacks)
- Edge caching with proper cache headers
- Database query optimization and indexing
- Connection pooling and reuse
- Preloading and prefetching critical resources

## Language-Specific Best Practices

> The framework automatically detects your project language and applies the appropriate standards below.
>
> **Auto-Detection**: If the Language & Stack section above contains placeholders, the framework will:
> 1. Detect language from project files (package.json → JS/TS, requirements.txt → Python, go.mod → Go, etc.)
> 2. Apply the corresponding language-specific standards from this section
> 3. Inform you when detection occurs: "ℹ️ Detected [language] project. Applying [language] standards."

### TypeScript/JavaScript Standards

#### Critical Rules (Must Follow)
1. **Type Safety**
   - Enable `strict: true` in tsconfig.json
   - Never use `any` - use `unknown` or specific types
   - Always handle `null` and `undefined` with `?.` and `??`
   - Use type guards instead of type assertions (`as`)

2. **Async/Promise Handling**
   ```typescript
   // ❌ Wrong
   async function getData() { fetch('/api'); }  // Missing await

   // ✅ Correct
   async function getData() {
     try {
       const data = await fetch('/api');
       return await data.json();
     } catch (error) {
       console.error('Failed:', error);
     }
   }
   ```

3. **Function Signatures**
   - Always specify return types explicitly
   - Type all parameters (no implicit `any`)
   - Use generics over `any` for flexibility

4. **Common Pitfalls to Avoid**
   ```typescript
   // ❌ Non-null assertion
   const value = someValue!.property;

   // ✅ Safe access
   const value = someValue?.property ?? defaultValue;

   // ❌ Type assertion without validation
   const user = data as User;

   // ✅ Type guard with validation
   if (isUser(data)) {
     const user = data; // Type is narrowed
   }
   ```

### Python Standards

#### Critical Rules (Must Follow)
1. **Type Hints** (Python 3.9+)
   ```python
   # ❌ Wrong
   def process_data(data):
       return data['value']

   # ✅ Correct
   from typing import Dict, Any, Optional

   def process_data(data: Dict[str, Any]) -> Optional[str]:
       return data.get('value')
   ```

2. **Error Handling**
   ```python
   # ❌ Wrong - bare except
   try:
       result = risky_operation()
   except:
       pass

   # ✅ Correct - specific exceptions
   try:
       result = risky_operation()
   except (ValueError, KeyError) as e:
       logger.error(f"Operation failed: {e}")
       raise
   ```

3. **Resource Management**
   ```python
   # ❌ Wrong - manual cleanup
   file = open('data.txt')
   content = file.read()
   file.close()

   # ✅ Correct - context manager
   with open('data.txt') as file:
       content = file.read()
   ```

4. **Common Pitfalls to Avoid**
   ```python
   # ❌ Mutable default argument
   def add_item(item, items=[]):
       items.append(item)
       return items

   # ✅ Correct default
   def add_item(item, items=None):
       if items is None:
           items = []
       items.append(item)
       return items
   ```

### Universal Code Quality Standards

Regardless of language, always:
- **Validate all inputs** before processing
- **Log errors with context** (never log sensitive data)
- **Write tests for error paths** not just happy paths
- **Use dependency injection** for testability
- **Document complex logic** with clear comments
- **Follow existing patterns** in the codebase
- **No hardcoded credentials** - use environment variables
- **Clean up resources** - close files, connections, streams

## Definition of Done

A task is complete when:
1. ✅ Code meets all acceptance criteria
2. ✅ Tests written with >80% coverage
3. ✅ Language-specific standards followed (see above)
4. ✅ No security vulnerabilities (OWASP scan clean)
5. ✅ Performance benchmarks met
6. ✅ Error handling and logging implemented
7. ✅ Code reviewed and approved
8. ✅ Documentation and API specs updated
9. ✅ No debug code (console.log, print statements)
10. ✅ Deployed to staging with feature flag
11. ✅ Monitoring and alerts configured
12. ✅ Accessibility standards met (WCAG 2.1 AA)

## Quick Commands

<!-- Test runner command MUST be specified for /pin:execute to work -->
**Test Runner**: [e.g., npm test, bun test, pytest, go test]  <!-- REQUIRED for execution phase -->

```bash
# Development (Bun)
bun dev                  # Start development server
bun test                 # Run tests with Bun test runner
bun run check            # Type check and lint with Biome
bun run build            # Build for production

# Database
bun db:generate          # Generate migrations
bun db:migrate           # Run migrations
bun db:seed              # Seed database
bun db:studio            # Open database GUI

# Production
bun start                # Start production server
bun run deploy           # Deploy to production
```

---

*Last Updated: [Date]*
*Maintained By: [Team/Person]*
