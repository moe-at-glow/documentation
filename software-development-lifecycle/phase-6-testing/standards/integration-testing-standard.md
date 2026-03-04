# Integration Testing Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P6-002 |
| **Compliance Level** | Mandatory |
| **Enforced By** | QA Lead |
| **Verification Method** | Test Review / CI Pipeline |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Happy path + auth tests required per endpoint; database setup rules apply; external service mocking optional
> **IF** medium project (3-5 devs) **THEN** Full endpoint coverage (happy + error paths); pagination and validation tests required
> **IF** large project (6+ devs) **THEN** Full compliance required

---

## COMPLIANCE REQUIREMENTS

### Integration Points

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | API endpoint + database: test full stack (HTTP -> controller -> service -> repository -> real DB -> response) | All projects | [ ] Test inventory per endpoint | PR blocked |
| 2 | Service + external API: test with realistic mock or real sandbox | All projects | [ ] Test execution log | PR blocked |
| 3 | Event producer + consumer: test publish and consume cycle | All projects | [ ] Test execution log | PR blocked |
| 4 | Service + cache: test reads, writes, and cache miss handling | All projects | [ ] Test execution log | PR blocked |

### Database Setup

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 5 | Use real PostgreSQL, same version as production | All projects | [ ] Test environment config | Test suite invalid |
| 6 | Dedicated test database (`glowpower_test`); never use the development database | All projects | [ ] Database connection config | Test suite invalid |
| 7 | Truncate all tables in `beforeEach` for fresh state per test | All projects | [ ] Test code review | Test suite rework |
| 8 | Run all migrations automatically before test suite starts | All projects | [ ] Test setup code review | Test suite rework |
| 9 | Each test seeds only the data it needs via factory functions | All projects | [ ] Test code review | Test suite rework |
| 10 | Reset sequences in `beforeEach` | All projects | [ ] Test code review | Test suite rework |

### Required Test Scenarios

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 11 | Happy path for every API endpoint | All projects | [ ] Test inventory review | PR blocked |
| 12 | Authentication enforcement: unauthenticated requests return 401 | All projects | [ ] Test execution log | PR blocked |
| 13 | Authorization enforcement: users cannot access other users' data (403) | All projects | [ ] Test execution log | PR blocked |
| 14 | Input validation: invalid requests return 400 with error details | Medium+ projects | [ ] Test execution log | PR blocked |
| 15 | Database constraints: unique, foreign key, not-null verified | Medium+ projects | [ ] Test execution log | PR blocked |
| 16 | Pagination: all list endpoints return correct pages | Medium+ projects | [ ] Test execution log | PR blocked |
| 17 | Error responses: format matches API standard | All projects | [ ] Test execution log | PR blocked |

### Scope Boundaries (Do NOT Test at Integration Level)

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 18 | Business logic edge cases: test at unit level, not integration | All projects | [ ] Test review during PR | Rework requested |
| 19 | UI rendering: test at system/E2E level | All projects | [ ] Test review during PR | Rework requested |
| 20 | Performance under load: test at performance test level | All projects | [ ] Test review during PR | Rework requested |

### External Service Mocking

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 21 | CI pipeline: use in-process mock servers (fast, deterministic) | All projects | [ ] CI test config review | CI pipeline rework |
| 22 | Contract-based stubs when OpenAPI spec is defined | Medium+ projects | [ ] Contract file exists | Stub rework |
| 23 | Real sandbox/test environments: staging only, never in CI | All projects | [ ] CI config audit | CI pipeline rework |

### File Organization and Naming

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 24 | Integration tests located in `src/modules/<module>/__tests__/` | All projects | [ ] File structure review | Rework requested |
| 25 | Naming convention: `*.integration.test.ts` | All projects | [ ] File naming review | Rename required |
| 26 | Separate Jest config or test match pattern to run integration tests independently | All projects | [ ] Jest config review | Config rework |
| 27 | `npm run test:integration` command runs only integration tests | All projects | [ ] Package.json scripts review | Script must be added |

### Coverage Requirements

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 28 | Every endpoint: at least one happy path + one error test | All projects | [ ] Test inventory review | PR blocked |
| 29 | Auth-protected endpoints: 401 without token + 403 wrong role tested | All projects | [ ] Test execution log | PR blocked |
| 30 | All CRUD operations verified with real database | All projects | [ ] Test execution log | PR blocked |
| 31 | At least one invalid input test per endpoint | Medium+ projects | [ ] Test execution log | PR blocked |
| 32 | Pagination verified on all list endpoints | Medium+ projects | [ ] Test execution log | PR blocked |

### Common Mistakes (Anti-Patterns)

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 33 | No shared test state between tests; truncate in `beforeEach` | All projects | [ ] Test code review | Rework required |
| 34 | Never test in development DB; use dedicated test database | All projects | [ ] Database config audit | Immediate rework |
| 35 | Avoid excessive integration tests; test edge cases at unit level | All projects | [ ] Test review during PR | Rework requested |
| 36 | Test error paths (400, 401, 403, 404, 409), not only happy path | All projects | [ ] Test inventory review | PR blocked |
| 37 | Generate UUIDs or use sequences; no hardcoded test data IDs | All projects | [ ] Test code review | Rework required |

---

## COMPLIANCE CHECKLIST

- [ ] Every API endpoint has at least one happy path integration test
- [ ] Every API endpoint has at least one error path integration test
- [ ] Authentication enforcement tested (401 without token)
- [ ] Authorization enforcement tested (403 wrong user/role)
- [ ] Input validation tested (400 with error details)
- [ ] Database constraints tested (unique, FK, not-null)
- [ ] Pagination tested on all list endpoints
- [ ] Error response format matches API standard
- [ ] Real PostgreSQL used (same version as production)
- [ ] Dedicated test database configured (`glowpower_test`)
- [ ] Tables truncated in `beforeEach`; no shared state
- [ ] Migrations run automatically before suite
- [ ] External services mocked in CI with in-process mock servers
- [ ] Files named `*.integration.test.ts` in correct directory
- [ ] `npm run test:integration` command works independently
- [ ] No hardcoded test data IDs
- [ ] No business logic edge cases tested at integration level

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Write Integration Tests | Runbook | [../runbooks/write-integration-tests.md](../runbooks/write-integration-tests.md) |
| Execute Test Cycle | Runbook | [../runbooks/execute-test-cycle.md](../runbooks/execute-test-cycle.md) |
| Report and Track Defects | Runbook | [../runbooks/report-and-track-defects.md](../runbooks/report-and-track-defects.md) |
| Perform Regression Testing | Runbook | [../runbooks/perform-regression-testing.md](../runbooks/perform-regression-testing.md) |
| Test Case Template | Template | [../templates/test-case-template.md](../templates/test-case-template.md) |
| Defect Report Template | Template | [../templates/defect-report-template.md](../templates/defect-report-template.md) |
| Test Summary Report Template | Template | [../templates/test-summary-report-template.md](../templates/test-summary-report-template.md) |
| Defect Severity Reference | Reference | [../references/defect-severity-reference.md](../references/defect-severity-reference.md) |
