# TDD Process

## Cycle (Per Task)
1. **RED**: Write failing test for acceptance criteria
2. **GREEN**: Minimal COMPLETE implementation (not mock)
3. **REFACTOR**: Improve without changing behavior
4. **VALIDATE**: Re-run test to confirm
5. **INTEGRATE**: Test with previous tasks (if N>1)

## Minimal = Simple but COMPLETE
✅ Simplest working production code
✅ Real database/API connections
✅ Actual business logic
❌ NOT stubs, mocks, or "later"

## Examples
| Task | Wrong | Right |
|------|-------|-------|
| Login | return true | Hash check + JWT |
| Upload | return '/fake' | S3/filesystem |
| Payment | return {paid:true} | Stripe integration |