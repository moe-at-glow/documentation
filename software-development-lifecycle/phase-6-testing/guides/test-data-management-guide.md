# Test Data Management -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P6-002 |
| **Use When** | Creating, seeding, or cleaning up test data at any test level |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] No production data (real names, emails, PII) used in tests
- [ ] Each test creates its own data (no shared/global test data)
- [ ] Database truncation happens in `beforeEach`, not `afterEach`
- [ ] IDs use UUIDs or unique prefixes (no sequential 1, 2, 3)
- [ ] Dates are fixed values or mocked clock (no `new Date()` in assertions)
- [ ] Only minimal data needed for the test is seeded

---

## SELECTION CRITERIA / DECISION TABLE

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| Unit test needs a domain object | Use in-memory factory function with overrides | Hitting a real database |
| Integration test needs DB records | Use seed helper functions per test | Sharing seed data across tests |
| System test needs environment data | Use pre-loaded staging data sets | Using production database dumps |
| Test involves dates/times | Mock system clock with `jest.useFakeTimers()` | Using `new Date()` or current time |
| Test cleanup needed | `TRUNCATE ... CASCADE` in `beforeEach` | `DELETE FROM` (slower) or `afterEach` only |
| Tests run in parallel | Use UUIDs or unique prefixes for all IDs | Hardcoded sequential IDs |
| Performance testing needed | Use `seed-performance.sql` (10K+ records) | Standard seed with 100 records |
| System test setup | Use API calls to create data | Direct DB access bypassing application layer |

---

## QUICK-REFERENCE TABLE

### Test Data Values

| Data Type | Use | Do Not Use |
|-----------|-----|------------|
| Names | "Test Customer", "Jane Tester" | Real customer names |
| Emails | test-{uuid}@example.com | Real email addresses |
| Phones | +966500000000 | Real phone numbers |
| Amounts | Round numbers (100.00, 250.00) | Production financial data |
| Dates | Fixed dates (2026-01-01) | Current date/time |
| IDs | UUIDs or `test-` prefixed | Sequential IDs (1, 2, 3) |

### Staging Data Sets

| Data Set | Purpose | Contents |
|----------|---------|----------|
| `seed-minimal.sql` | Smoke tests | 10 customers, 20 equipment, 50 rentals |
| `seed-standard.sql` | Full system testing | 100 customers, 200 equipment, 500 rentals |
| `seed-performance.sql` | Performance testing | 10K customers, 50K equipment, 200K rentals |

### Data Strategy by Test Level

| Level | Data Source | Cleanup |
|-------|-----------|---------|
| Unit | In-memory factory functions | None needed |
| Integration | Database seed helpers | `TRUNCATE ... CASCADE` in `beforeEach` |
| System | Pre-loaded staging data sets (`npm run db:seed:staging`) | Reset between test runs |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| For background | Training | [training/testing-phase-overview.md](training/testing-phase-overview.md) |
| Test level selection | Quick Reference | [testing-pyramid-explained.md](testing-pyramid-explained.md) |
| Common pitfalls | Quick Reference | [common-testing-pitfalls.md](common-testing-pitfalls.md) |
