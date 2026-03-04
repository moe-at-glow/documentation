# Write Integration Tests

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P6-002 |
| **Owner** | QA Lead |
| **Accountable** | QA Lead |
| **SLA** | 2-3 business days per module |
| **Escalation** | Tech Lead (technical issues), Business Analyst (requirements clarification) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Feature implementation complete with passing unit tests
- [ ] Test database available (`glowpower_test`)
- [ ] API specification for endpoints under test is finalized
- [ ] Integration testing standard reviewed: [integration-testing-standard.md](../standards/integration-testing-standard.md)

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| API specification not finalized or conflicting | STOP. Clarify spec with Business Analyst before writing tests | Business Analyst |
| Test database unavailable or corrupted | STOP. Raise infra ticket | Tech Lead |
| Feature implementation incomplete or unstable | STOP. Return to developer for stabilization | Tech Lead |

---

## PROCEDURE

### Step 1: Identify Test Cases per Endpoint

| Action | Owner | SLA |
|--------|-------|-----|
| Map each API endpoint to required integration test cases | QA Lead | 2 hours |

| Category | Test Cases Needed |
|----------|------------------|
| Happy path | Valid request returns expected response |
| Authentication | Request without token returns 401 |
| Authorization | Request for another user's data returns 403 |
| Validation | Invalid input returns 400 with error details |
| Not found | Non-existent resource returns 404 |
| Conflict | Duplicate or conflicting operation returns 409 |
| Database constraints | Violations return appropriate errors |

- [ ] All endpoints identified for integration testing
- [ ] Test case matrix completed per endpoint

> **IF** endpoint behavior unclear **THEN** consult API specification and Business Analyst
> **ELSE** proceed to Step 2

### Step 2: Set Up Test Infrastructure

| Action | Owner | SLA |
|--------|-------|-----|
| Create or update integration test file in `src/modules/<module>/__tests__/<module>.integration.test.ts` | QA Lead | 1 hour |
| Configure test database setup/teardown in `beforeAll`/`afterAll` | QA Lead | 30 min |
| Configure per-test data reset in `beforeEach` | QA Lead | 30 min |

- [ ] Test file created with correct path convention
- [ ] `beforeAll`: test database created, app initialized
- [ ] `afterAll`: database destroyed
- [ ] `beforeEach`: all tables truncated

> **IF** shared test infrastructure already exists **THEN** reuse existing `createTestDatabase` and `createApp` helpers
> **ELSE** create infrastructure following project test patterns

### Step 3: Write Seed Helpers

| Action | Owner | SLA |
|--------|-------|-----|
| Create factory functions in `src/test/seeds.ts` for required entities | QA Lead | 1 hour |

- [ ] Seed helper created for each entity under test
- [ ] Each seed helper accepts overrides parameter
- [ ] Each seed helper returns the created entity

> **IF** seed helper already exists for entity **THEN** reuse existing helper, extend if needed
> **ELSE** create new seed helper following existing pattern

### Step 4: Write Happy Path Tests

| Action | Owner | SLA |
|--------|-------|-----|
| Write happy path test for each endpoint using Arrange-Act-Assert pattern | QA Lead | 2 hours |

- [ ] Each happy path test seeds required data (Arrange)
- [ ] Each happy path test calls the endpoint (Act)
- [ ] Each happy path test asserts response status and body (Assert)
- [ ] Each happy path test asserts database state after the call

> **IF** happy path test fails **THEN** verify feature implementation is correct before proceeding; raise defect if code is at fault
> **ELSE** proceed to Step 5

### Step 5: Write Error Path Tests

| Action | Owner | SLA |
|--------|-------|-----|
| Write tests for each error scenario: 400, 401, 403, 404, 409 | QA Lead | 3 hours |

- [ ] 400 Validation: missing required fields tested
- [ ] 400 Business rule violations tested (e.g., equipment not available)
- [ ] 401 Unauthorized: no token / invalid token tested
- [ ] 403 Forbidden: cross-user access tested
- [ ] 404 Not found: non-existent resource tested
- [ ] 409 Conflict: duplicate operations tested (if applicable)
- [ ] Error response format matches API standard

### Step 6: Write Authorization Tests

| Action | Owner | SLA |
|--------|-------|-----|
| Write IDOR prevention tests for each endpoint that accesses user-specific data | QA Lead | 1 hour |

- [ ] User A cannot access User B's resources (GET)
- [ ] User A cannot modify User B's resources (PUT/PATCH/DELETE)
- [ ] Role-based restrictions enforced (e.g., customer vs. admin)

### Step 7: Write Pagination Tests

| Action | Owner | SLA |
|--------|-------|-----|
| Write pagination tests for each list endpoint | QA Lead | 1 hour |

- [ ] Default pagination returns correct page size
- [ ] `page` and `per_page` parameters work correctly
- [ ] Response meta includes `total`, `page`, `per_page`, `total_pages`
- [ ] Empty result set returns correct structure

### Step 8: Run and Verify

| Action | Owner | SLA |
|--------|-------|-----|
| Run integration tests: `npm run test:integration` | QA Lead | 30 min |
| Run with coverage: `npm run test:integration -- --coverage` | QA Lead | 30 min |
| Verify test isolation by running in random order | QA Lead | 15 min |

- [ ] All tests pass
- [ ] Coverage meets integration test requirements
- [ ] No shared state between tests (random order passes)

> **IF** tests fail **THEN** fix test or raise defect against feature code
> **ELSE IF** coverage below threshold **THEN** add additional test cases
> **ELSE** proceed to Step 9

### Step 9: Add to CI Pipeline

| Action | Owner | SLA |
|--------|-------|-----|
| Verify integration tests run in CI workflow (`.github/workflows/ci.yml`) | QA Lead | 15 min |
| Confirm CI passes with new tests | QA Lead | 30 min |

- [ ] Integration tests execute in CI on every PR
- [ ] CI passes with all new tests

> **IF** CI not configured for integration tests **THEN** add integration test job to CI workflow, escalate to Tech Lead
> **ELSE** procedure complete

---

## EXIT CRITERIA

- [ ] All endpoints identified and covered by integration tests
- [ ] Test database setup and teardown configured
- [ ] Seed helpers created for all required test data
- [ ] Happy path tested for each endpoint
- [ ] Error paths tested (400, 401, 403, 404, 409)
- [ ] Authorization tested (IDOR prevention)
- [ ] Pagination tested on list endpoints
- [ ] Response format matches API standard
- [ ] Tests are isolated (no shared state)
- [ ] Tests pass in CI pipeline

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Integration test files | `src/modules/<module>/__tests__/<module>.integration.test.ts` | Source repository |
| Seed helpers | `src/test/seeds.ts` | Source repository |
| Coverage report | Generated by test runner | CI artifacts |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Integration Testing Standard | Standard | [../standards/integration-testing-standard.md](../standards/integration-testing-standard.md) |
| Testing Strategy Standard | Standard | [../standards/testing-strategy-standard.md](../standards/testing-strategy-standard.md) |
| Test Case Template | Template | [../templates/test-case-template.md](../templates/test-case-template.md) |
| Defect Report Template | Template | [../templates/defect-report-template.md](../templates/defect-report-template.md) |
| Defect Severity Reference | Reference | [../references/defect-severity-reference.md](../references/defect-severity-reference.md) |
