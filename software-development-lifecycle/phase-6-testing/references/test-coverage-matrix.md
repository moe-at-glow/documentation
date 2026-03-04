# Test Coverage Matrix

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P6-003 |
| **Use When** | Setting coverage targets, reviewing coverage reports, or identifying coverage gaps |
| **Last Updated** | 2026-03-04 |

---

## Unit Test Coverage Targets

| Code Category | Minimum Line Coverage | Minimum Branch Coverage |
|--------------|----------------------|------------------------|
| Business logic (services, calculators) | 80% | 70% |
| Critical paths (payments, fees, billing) | 90% | 85% |
| Utilities and helpers | 60% | 50% |
| Data validation | 80% | 75% |
| Controllers (HTTP layer) | Not required | Not required |
| Generated code, configuration | Excluded | Excluded |
| Type definitions, interfaces | Excluded | Excluded |

---

## Integration Test Coverage Targets

| Category | Coverage Requirement |
|----------|---------------------|
| API endpoints (happy path) | 100% of endpoints have at least one happy path test |
| API endpoints (error paths) | 100% of endpoints test 401 (auth). 80% test 400 (validation). |
| Database CRUD operations | 100% of create, read, update operations tested |
| Database constraints | Unique constraints and foreign keys tested |
| Pagination | 100% of list endpoints test pagination |
| Authorization (IDOR) | 100% of resource endpoints test cross-user access |

---

## System Test Coverage Targets

| Category | Coverage Requirement |
|----------|---------------------|
| Critical user journeys | 100% tested every release |
| High priority workflows | 100% tested every release |
| Medium priority workflows | 100% tested for major releases |
| Cross-module flows | All flows that span 2+ modules tested |
| Error recovery | System behavior tested for each external service failure |

---

## Coverage by Module

| Module | Unit (min) | Integration (endpoints) | System (journeys) |
|--------|-----------|------------------------|-------------------|
| Rentals | 80% | All CRUD + status transitions | Rental lifecycle |
| Billing | 90% | Invoice CRUD + calculation endpoints | Invoice + payment flow |
| Payments | 90% | Payment processing + refund | Payment lifecycle |
| Equipment | 80% | CRUD + status + telemetry | Equipment lifecycle |
| Customers | 80% | CRUD + search | Registration + profile |
| Auth | 80% | Login + token + password | Login + access control |
| IoT / Telemetry | 70% | Telemetry ingestion | Equipment tracking |
| Reporting | 60% | Report generation endpoints | Report workflows |

---

## Measuring Coverage

### Unit Test Coverage

```bash
# Generate coverage report
npm run test:coverage

# Output includes:
# - Statements: percentage of statements executed
# - Branches: percentage of if/else branches executed
# - Functions: percentage of functions called
# - Lines: percentage of lines executed
```

### Integration Test Coverage

| Metric | How to Measure |
|--------|---------------|
| Endpoint coverage | Count of tested endpoints / total endpoints |
| Error code coverage | Count of tested error responses / expected error responses |
| Auth coverage | Count of endpoints with auth tests / protected endpoints |

### System Test Coverage

| Metric | How to Measure |
|--------|---------------|
| Requirement coverage | SWR requirements with linked test cases / total SWR requirements |
| Journey coverage | User journeys with passing tests / total critical journeys |

---

## Coverage Enforcement

| Level | Enforcement |
|-------|------------|
| Unit | Jest `coverageThreshold` in `jest.config.ts`. CI fails if below threshold. |
| Integration | Manual review during test planning. Checklist in PR template. |
| System | Requirements Traceability Matrix (RTM) review. Gaps flagged in test plan. |

### Jest Coverage Configuration

```typescript
// jest.config.ts
export default {
  coverageThreshold: {
    global: {
      statements: 75,
      branches: 65,
      functions: 70,
      lines: 75,
    },
    './src/modules/billing/': {
      statements: 90,
      branches: 85,
      functions: 90,
      lines: 90,
    },
    './src/modules/payments/': {
      statements: 90,
      branches: 85,
      functions: 90,
      lines: 90,
    },
  },
};
```

---

## Coverage Gaps: What to Do

| Situation | Action |
|-----------|--------|
| Module below unit test threshold | Write more unit tests. Focus on untested branches. |
| Endpoint missing integration test | Add test for happy path + primary error case. |
| Requirement with no linked test | Create test case. Add to test plan. |
| Coverage decreasing over time | Require coverage check in PR. Reject PRs that reduce coverage. |

---

## DECISION TREE

```
What type of coverage are you evaluating?
  UNIT TEST -->
    IF module is payments or billing --> Target: 90% line, 85% branch
    ELSE IF module is IoT/Telemetry --> Target: 70% line
    ELSE IF module is Reporting --> Target: 60% line
    ELSE IF code is controllers/generated/types --> Excluded
    ELSE --> Target: 80% line, 70% branch

  INTEGRATION TEST -->
    IF endpoint has no happy path test --> Add one immediately
    IF endpoint has no auth test (401) --> Add one immediately
    IF endpoint has no validation test (400) --> Add to sprint backlog

  SYSTEM TEST -->
    IF critical user journey has no test --> Block release until covered
    IF high priority workflow has no test --> Block release until covered
    IF medium priority workflow has no test --> Required for major releases only

Is coverage below target?
  YES --> Is it a CI-enforced threshold?
    YES --> Fix before merge (CI will reject PR)
    NO  --> Flag in test plan, schedule coverage improvement
  NO  --> Proceed
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Execute Test Cycle | Runbook | ../runbooks/execute-test-cycle.md |
| Write Integration Tests | Runbook | ../runbooks/write-integration-tests.md |
| Write System Tests | Runbook | ../runbooks/write-system-tests.md |
| Report and Track Defects | Runbook | ../runbooks/report-and-track-defects.md |
| Perform Regression Testing | Runbook | ../runbooks/perform-regression-testing.md |
