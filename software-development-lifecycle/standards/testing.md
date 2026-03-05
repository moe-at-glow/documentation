# Testing Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-TEST-001 |
| **Compliance Level** | Mandatory |
| **Enforced By** | QA Lead / Tech Lead |
| **Verification Method** | CI Pipeline / Test Review / Coverage Reports |
| **Last Updated** | 2026-03-05 |

---

## 1. Purpose

This standard defines the testing requirements across all test levels -- unit, integration, system, performance, and security. It establishes what to test, how to test it, what coverage to target, and which tools to use. Every team member writing or reviewing tests must follow this document.

---

## 2. Testing Strategy

### Scaling Gate

| Project Size | Requirements |
|--------------|-------------|
| Small (1-2 devs) | Unit + integration required. System tests on critical journeys only. UAT optional. |
| Medium (3-5 devs) | All test levels required. Performance testing on critical paths. Exploratory testing recommended. |
| Large (6+ devs) | Full compliance with every section of this standard. |

### Risk-Based Test Prioritization

Test effort follows business risk. Revenue-impacting flows (payments, billing, late fees) get the highest coverage thresholds and the most test scenarios. Supporting features (reporting, convenience) get standard coverage.

### Test Execution Triggers

| Trigger | Tests Run |
|---------|-----------|
| Pre-push (local) | Unit tests |
| PR created/updated | Unit + integration in CI |
| Merge to develop | Unit + integration + smoke |
| Release branch created | Full regression suite |
| Pre-deploy to staging | System + performance tests |
| Post-deploy to production | Smoke tests only |

### Defect SLAs

| Severity | Fix Deadline |
|----------|-------------|
| Critical (system unusable, data loss, security breach) | 4 hours |
| High (major feature broken, no workaround) | 1 business day |
| Medium (feature broken, workaround exists) | Current sprint |
| Low (cosmetic, minor) | Next sprint or backlog |

See [defect severity definitions](../references/defect-severity.md) for classification guidance.

### Exit Criteria

- **Unit**: all pass, coverage meets thresholds, no skipped tests.
- **Integration**: all API/DB/event tests pass, no critical/high defects open.
- **System**: all critical journeys pass, performance benchmarks met, security scan clean.
- **UAT**: all acceptance criteria verified, Product Owner sign-off obtained.

---

## 3. Testing Pyramid

### Target Distribution

| Level | Proportion | Quantity | Max Time per Test | Suite Target |
|-------|-----------|----------|-------------------|-------------|
| Unit | ~70% | 200-500 tests | < 100ms | < 30 seconds |
| Integration | ~20% | 50-100 tests | < 5s | < 5 minutes |
| System / E2E | ~10% | 20-30 tests | < 30s | < 30 minutes |

**Rule**: test at the lowest level possible. Higher levels only for what cannot be tested below. If you have many system tests for one feature, push edge cases down to unit tests.

---

## 4. Unit Testing Standard

### Coverage Thresholds

| Code Category | Line Coverage | Branch Coverage |
|--------------|--------------|-----------------|
| Business logic (services, calculators) | >= 80% | >= 70% |
| Critical paths (payments, fees, billing) | >= 90% | >= 85% |
| Utilities and helpers | >= 60% | >= 50% |
| Data validation | >= 80% | >= 75% |
| Controllers (HTTP layer) | Not required | Not required |
| Generated code, config, type definitions | Excluded | Excluded |

### Test Naming Convention

- `describe` block: name of the unit (`LateFeeCalculator`)
- Nested `describe`: method name (`calculateFee`)
- `it` block: `should [expected behavior] when [condition]`

### AAA Pattern (Arrange-Act-Assert)

Every test follows this structure. One Act per test. One behavior per test. No exceptions.

### What to Test

- Business logic and calculations
- Edge cases (zero values, maximums)
- Error handling (invalid inputs, missing data, external failures)
- Boundary conditions (0 days overdue vs 1 day)
- State transitions (valid and invalid)
- Validation rules (required fields, format, business rules)

### What NOT to Test at Unit Level

- Framework internals (Express routing, ORM)
- Third-party library internals
- Trivial getters/setters with no logic
- Private methods directly -- test via public interface
- Database queries -- use integration tests

### Mocking Rules

**Mock these**: external services, database repositories, message brokers, HTTP clients, system clock.

**Never mock**: the unit under test, pure business logic, input data/fixtures, standard library functions.

### Test Isolation

- Tests must not depend on execution order.
- Reset mocks in `beforeEach` (`jest.clearAllMocks`).
- No external dependencies (database, network, filesystem) in unit tests.
- Each test creates its own data via factory functions.

---

## 5. Integration Testing Standard

### Scope

Integration tests verify that components work together through real infrastructure. Test the full stack: HTTP request -> controller -> service -> repository -> real database -> response.

### Integration Points to Cover

| Integration | Requirement |
|-------------|-------------|
| API endpoint + database | Full CRUD tested with real PostgreSQL |
| Service + external API | Mock server in CI; real sandbox in staging |
| Event producer + consumer | Publish and consume cycle verified |
| Service + cache | Reads, writes, and cache miss handling |

### Required Test Scenarios per Endpoint

- Happy path (200/201)
- Unauthenticated request (401)
- Unauthorized access / wrong user (403)
- Invalid input (400) with error details
- Database constraints (unique, FK, not-null)
- Pagination on list endpoints
- Error response format matches API standard

### Database Setup and Teardown

1. Use real PostgreSQL, same version as production.
2. Dedicated test database (`<project>_test`). Never use the dev database.
3. Run all migrations automatically before the suite starts.
4. Truncate all tables in `beforeEach` for fresh state.
5. Reset sequences in `beforeEach`.
6. Each test seeds only the data it needs via factory functions.

### Test Doubles for External Services

| Environment | Strategy |
|-------------|----------|
| CI pipeline | In-process mock servers (fast, deterministic) |
| Staging | Real sandbox/test instances |

Use contract-based stubs when an OpenAPI spec is defined.

### Scope Boundaries -- Do NOT Test Here

- Business logic edge cases (unit level)
- UI rendering (system/E2E level)
- Performance under load (performance test level)

### File Organization

- Location: `src/modules/<module>/__tests__/`
- Naming: `*.integration.test.ts`
- Command: `npm run test:integration` runs only integration tests

---

## 6. System Testing Standard

### Critical User Journeys (Must Pass Every Release)

- Customer rental lifecycle: browse -> request -> approve -> active -> return -> invoice
- Payment processing: generate invoice -> process payment -> update balance -> send receipt
- Late fee handling: overdue -> calculate fee -> add to invoice -> notify customer
- User authentication: register -> login -> access protected resources -> logout

### Cross-Module Flows

- Customer -> Rental -> Billing (end-to-end)
- Rental -> Return -> Late Fee Calculation -> Payment
- Invoice Generation -> Payment Processing

### Environment Requirements

| Component | Requirement |
|-----------|-------------|
| Application | Same Docker image as production |
| Database | PostgreSQL same version, anonymized data |
| Cache | Redis same version as production |
| External services | Sandbox/test instances (payment gateway, email, SMS) |
| Network | Staging isolated from production |

### Environment Readiness

Before running system tests: verify staging matches production config, all migrations are applied, test data is loaded and anonymized, external sandboxes are accessible, and environment variables are set.

### Test Case Format

Each test case must include: Test ID (SYS-TC-NNN), title, priority, preconditions, steps, expected result, and postconditions. Use the [test case template](../templates/test-case.md).

---

## 7. Performance Testing Standard

### Response Time Targets

| Operation | p95 | p99 |
|-----------|-----|-----|
| Health check | < 50ms | < 100ms |
| Single resource GET | < 200ms | < 500ms |
| List with pagination | < 500ms | < 1s |
| Create/update (POST, PUT, PATCH) | < 300ms | < 1s |
| Search with filters | < 500ms | < 1.5s |
| Report generation | < 2s | < 5s |

### Throughput Targets

| Metric | Normal Load | Peak Load |
|--------|------------|-----------|
| Concurrent users | 100 | 500 |
| Requests/second | 200 | 1,000 |
| Error rate | < 0.1% | < 1% |

### Resource Limits

CPU < 50% normal / < 80% peak. Memory < 60% normal / < 85% peak. DB connections < 50% pool normal / < 80% pool peak.

### Test Types

| Type | Duration | Load | When Required |
|------|----------|------|---------------|
| Load test | 30 min, 100 users, 70/30 read/write | Normal | All projects, pre-release |
| Stress test | 60 min, ramp to 1000+ users | Beyond normal | Medium+, pre-release |
| Spike test | Baseline 100 -> spike 500 -> recover | Sudden burst | Large, quarterly |
| Endurance (soak) | 4-8 hours, 50 users | Sustained moderate | Large, quarterly |

### Execution Triggers

Run load tests pre-release, after major DB changes, and when adding new endpoints. Run the full suite (load + stress + spike + endurance) quarterly for large projects.

---

## 8. Security Testing Standard

### OWASP Top 10 Coverage

| OWASP Category | What to Test |
|----------------|-------------|
| A01 Broken Access Control | Authorization enforcement, IDOR prevention |
| A02 Cryptographic Failures | Password hashing (bcrypt/argon2), data protection |
| A03 Injection | SQL injection, XSS, command injection via parameterized queries |
| A04 Insecure Design | Architecture review (Phase 3 artifact) |
| A05 Security Misconfiguration | Headers, CORS, error handling |
| A06 Vulnerable Components | `npm audit --production`, license scan |
| A07 Auth Failures | Login, brute force lockout (5 attempts), token validation |
| A08 Data Integrity Failures | Input validation, deserialization |
| A09 Logging Failures | No PII/tokens/passwords in logs |
| A10 SSRF | Server-side request validation |

### SAST (Static Analysis) -- CI Pipeline

- `npm audit --production` on every PR -- blocks on critical/high.
- ESLint security plugin on every PR.
- No GPL or restricted licenses in production dependencies.

### DAST (Dynamic Analysis)

- OWASP checklist review: every release (QA Engineer + Tech Lead).
- Penetration testing: quarterly or major release (security specialist).
- Security header verification: every deployment.

---

## 9. Test Data Management

### Core Rules

1. No production data (real names, emails, PII) in any test.
2. Each test creates its own data. No shared or global test data.
3. Database truncation in `beforeEach`, not `afterEach`.
4. Use UUIDs or unique prefixes for IDs. No hardcoded sequential IDs.
5. Fix dates to known values or mock the clock. No `new Date()` in assertions.
6. Seed only the minimal data needed for the test.

### Data Strategy by Test Level

| Level | Data Source | Cleanup |
|-------|-----------|---------|
| Unit | In-memory factory functions | None needed |
| Integration | Database seed helpers | `TRUNCATE ... CASCADE` in `beforeEach` |
| System | Pre-loaded staging data sets | Reset between test runs |

### Staging Data Sets

| Data Set | Purpose | Contents |
|----------|---------|----------|
| `seed-minimal.sql` | Smoke tests | 10 customers, 20 equipment, 50 rentals |
| `seed-standard.sql` | Full system testing | 100 customers, 200 equipment, 500 rentals |
| `seed-performance.sql` | Performance testing | 10K customers, 50K equipment, 200K rentals |

---

## 10. Coverage Matrix

### Unit Test Coverage by Module

| Module | Line Target | Notes |
|--------|------------|-------|
| Billing | 90% | Critical path |
| Payments | 90% | Critical path |
| Rentals | 80% | Business logic |
| Equipment | 80% | Business logic |
| Customers | 80% | Business logic |
| Auth | 80% | Business logic |
| IoT / Telemetry | 70% | Data ingestion |
| Reporting | 60% | Supporting feature |

### Integration Test Coverage

| Category | Target |
|----------|--------|
| API endpoints (happy path) | 100% of endpoints |
| API endpoints (auth - 401) | 100% of protected endpoints |
| API endpoints (validation - 400) | 80% of endpoints |
| Database CRUD operations | 100% of create/read/update |
| Database constraints | Unique + FK tested |
| Pagination | 100% of list endpoints |
| Authorization (IDOR) | 100% of resource endpoints |

### System Test Coverage

| Category | Target |
|----------|--------|
| Critical user journeys | 100% every release |
| High priority workflows | 100% every release |
| Medium priority workflows | 100% for major releases |
| Cross-module flows | All flows spanning 2+ modules |
| Error recovery | Each external service failure scenario |

Coverage is enforced via Jest `coverageThreshold` in CI for unit tests, manual review during test planning for integration tests, and Requirements Traceability Matrix review for system tests.

---

## 11. Testing Tools

| Tool | Purpose | When to Use |
|------|---------|-------------|
| Jest | Test runner, assertions, mocking | Unit and integration tests |
| Supertest | HTTP assertions for Express | Integration tests against API endpoints |
| ts-jest | TypeScript preprocessor | All TypeScript test files |
| Docker Compose | Spin up test database | Integration test environment |
| k6 | Scriptable load testing | Performance tests (load, stress, spike) |
| Artillery | YAML-config load testing | Simple performance test scenarios |
| npm audit | Dependency vulnerability scan | Every PR (CI pipeline) |
| ESLint security plugin | Static security analysis | Every PR (CI pipeline) |
| OWASP ZAP | Dynamic application security testing | Staging, penetration testing |
| Jest --coverage | Line/branch/function coverage | Coverage reporting and CI gates |
| Factory functions | Generate test objects in-memory | Unit and integration test data |
| Seed scripts | Load database test data | Integration and system tests |

### Key Commands

```bash
npm test                        # Unit tests
npm run test:coverage           # Unit tests with coverage
npm run test:integration        # Integration tests
npm run test:system             # System tests against staging
k6 run tests/performance/*.js   # Performance tests
npm audit --production          # Security dependency scan
```

---

## Related Documents

| Document | Link |
|----------|------|
| Test Plan Template | [../templates/test-plan.md](../templates/test-plan.md) |
| Test Case Template | [../templates/test-case.md](../templates/test-case.md) |
| Defect Report Template | [../templates/defect-report.md](../templates/defect-report.md) |
| Defect Severity Reference | [../references/defect-severity.md](../references/defect-severity.md) |
| Run Test Cycle Runbook | [../runbooks/run-test-cycle.md](../runbooks/run-test-cycle.md) |
| Test Summary Report Template | [../templates/test-summary-report.md](../templates/test-summary-report.md) |
| UAT Sign-Off Template | [../templates/uat-sign-off.md](../templates/uat-sign-off.md) |
