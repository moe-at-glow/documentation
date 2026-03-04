# Testing Strategy Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P6-001 |
| **Compliance Level** | Mandatory |
| **Enforced By** | QA Lead |
| **Verification Method** | Test Review / CI Pipeline |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Unit + Integration tests required; System tests limited to critical journeys only; UAT optional
> **IF** medium project (3-5 devs) **THEN** All test levels required; Exploratory testing recommended; Performance testing on critical paths
> **IF** large project (6+ devs) **THEN** Full compliance required

---

## COMPLIANCE REQUIREMENTS

### Test Levels

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Unit tests execute in local environment during Phase 5 | All projects | [ ] CI pipeline confirms unit test pass | PR blocked until resolved |
| 2 | Integration tests execute in Test (CI) environment after merge to develop | All projects | [ ] CI pipeline confirms integration test pass | Merge reverted |
| 3 | System tests execute in Staging environment per sprint/release | Medium+ projects | [ ] QA sign-off on test cycle | Release blocked |
| 4 | UAT executes in Staging environment before release | Medium+ projects | [ ] Product Owner sign-off | Release blocked |

### Testing Pyramid Ratios

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 5 | Unit tests: many (hundreds), < 100ms each | All projects | [ ] Test suite timing report | Refactor slow tests |
| 6 | Integration tests: moderate (dozens), < 5s each | All projects | [ ] Test suite timing report | Refactor slow tests |
| 7 | System tests: few (tens), < 30s each | Medium+ projects | [ ] Test suite timing report | Refactor slow tests |
| 8 | Test at the lowest level possible; higher levels only for what cannot be tested below | All projects | [ ] Test review during PR | Rework requested |

### Unit Test Coverage (Phase 5)

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 9 | Business logic (services, calculators): >= 80% line coverage | All projects | [ ] Coverage report in CI | PR blocked |
| 10 | Critical paths (payments, fee calculation): >= 90% line coverage | All projects | [ ] Coverage report in CI | PR blocked |
| 11 | Utilities and helpers: >= 60% line coverage | All projects | [ ] Coverage report in CI | PR blocked |
| 12 | Controllers (HTTP layer): coverage not required (covered by integration tests) | All projects | [ ] N/A | N/A |

### Integration Test Coverage

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 13 | Every API endpoint tested for happy path + primary error case | All projects | [ ] Test inventory review | PR blocked |
| 14 | All CRUD operations tested with real database | All projects | [ ] Test execution log | PR blocked |
| 15 | External service integrations tested with mocks/stubs in CI, real services in staging | All projects | [ ] CI + staging test reports | Release blocked |
| 16 | All event producers and consumers tested | All projects | [ ] Test inventory review | PR blocked |

### System Test Coverage

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 17 | All critical user journeys covered (create rental, process payment, return equipment) | Medium+ projects | [ ] Test plan review | Release blocked |
| 18 | All cross-module flows covered (rental -> billing -> payment) | Medium+ projects | [ ] Test plan review | Release blocked |
| 19 | Error recovery tested (system behavior when external services fail) | Large projects | [ ] Test plan review | Release blocked |

### Environment Rules

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 20 | Never test against production data directly; use anonymized copies in staging | All projects | [ ] Environment audit | Immediate escalation |
| 21 | Test environments must match production config (same DB version, same Node.js version) | All projects | [ ] Environment config diff | Deployment blocked |
| 22 | Test data is ephemeral: created before test, destroyed after | All projects | [ ] Test teardown verification | Test suite rework |
| 23 | No shared test state: tests must not depend on other tests' data | All projects | [ ] Test isolation review | Test suite rework |

### Test Execution Frequency

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 24 | Pre-commit (local): linter on staged files | All projects | [ ] Git hook configuration | Hook must be installed |
| 25 | Pre-push (local): unit tests | All projects | [ ] Git hook configuration | Hook must be installed |
| 26 | PR created/updated: unit + integration tests in CI | All projects | [ ] CI pipeline config | PR blocked |
| 27 | Merge to develop: unit + integration + smoke tests in CI | All projects | [ ] CI pipeline config | Merge blocked |
| 28 | Release branch created: full regression suite | Medium+ projects | [ ] CI pipeline config | Release blocked |
| 29 | Pre-deployment to staging: full system + performance tests | Medium+ projects | [ ] Deployment pipeline config | Deployment blocked |
| 30 | Post-deployment to production: smoke tests only | All projects | [ ] Deployment pipeline config | Rollback triggered |

### Defect Management SLAs

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 31 | Critical (system unusable, data loss, security breach): fix within 4 hours | All projects | [ ] Defect tracker SLA report | Escalation to management |
| 32 | High (major feature broken, no workaround): fix within 1 business day | All projects | [ ] Defect tracker SLA report | Escalation to Tech Lead |
| 33 | Medium (feature broken, workaround exists): fix within current sprint | All projects | [ ] Sprint review | Carry to next sprint with justification |
| 34 | Low (cosmetic, minor inconvenience): fix in next sprint or backlog | All projects | [ ] Backlog review | Accepted |

### Exit Criteria

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 35 | Unit tests: all pass, coverage meets thresholds, no skipped tests | All projects | [ ] CI report | Phase 5 exit blocked |
| 36 | Integration tests: all API/DB/event tests pass, no critical/high defects open | All projects | [ ] CI report + defect tracker | Release blocked |
| 37 | System tests: all critical journeys pass, performance benchmarks met, security scan clean, no critical/high defects open | Medium+ projects | [ ] QA sign-off | Release blocked |
| 38 | UAT: all acceptance criteria verified by Product Owner, sign-off document signed, no critical/high defects open | Medium+ projects | [ ] UAT sign-off document | Release blocked |

---

## COMPLIANCE CHECKLIST

- [ ] All four test levels (Unit, Integration, System, UAT) are planned and scheduled
- [ ] Testing pyramid ratios followed (many unit, moderate integration, few system)
- [ ] Unit test coverage meets thresholds: 80% business logic, 90% critical paths, 60% utilities
- [ ] Every API endpoint has happy path + error integration test
- [ ] All CRUD operations tested with real database
- [ ] All event producers/consumers tested
- [ ] Critical user journeys have system tests
- [ ] Cross-module flows have system tests
- [ ] Test environments match production configuration
- [ ] No tests run against production data
- [ ] Test data is ephemeral with no shared state
- [ ] CI pipeline enforces test execution at all trigger points
- [ ] Defect SLAs documented and tracked
- [ ] Exit criteria met for each test level before phase transition

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Execute Test Cycle | Runbook | [../runbooks/execute-test-cycle.md](../runbooks/execute-test-cycle.md) |
| Write Integration Tests | Runbook | [../runbooks/write-integration-tests.md](../runbooks/write-integration-tests.md) |
| Write System Tests | Runbook | [../runbooks/write-system-tests.md](../runbooks/write-system-tests.md) |
| Report and Track Defects | Runbook | [../runbooks/report-and-track-defects.md](../runbooks/report-and-track-defects.md) |
| Perform Regression Testing | Runbook | [../runbooks/perform-regression-testing.md](../runbooks/perform-regression-testing.md) |
| Test Plan Template | Template | [../templates/test-plan-template.md](../templates/test-plan-template.md) |
| Test Case Template | Template | [../templates/test-case-template.md](../templates/test-case-template.md) |
| Defect Report Template | Template | [../templates/defect-report-template.md](../templates/defect-report-template.md) |
| Test Summary Report Template | Template | [../templates/test-summary-report-template.md](../templates/test-summary-report-template.md) |
| UAT Sign-Off Template | Template | [../templates/uat-sign-off-template.md](../templates/uat-sign-off-template.md) |
| Defect Severity Reference | Reference | [../references/defect-severity-reference.md](../references/defect-severity-reference.md) |
