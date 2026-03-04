# Common Testing Pitfalls -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P6-003 |
| **Use When** | Reviewing tests, debugging test failures, or onboarding QA process |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] Every happy-path test has at least one corresponding error-path test
- [ ] Mocks are on dependencies only -- assertions target YOUR code's behavior
- [ ] No flaky tests in the suite (fix immediately, never skip)
- [ ] Test suite runs within time targets (unit < 30s, integration < 5m)
- [ ] Every test case links to an SWR requirement
- [ ] Tests run against production-like environment config
- [ ] Zero skipped or ignored test failures
- [ ] Defect reports include steps to reproduce, request/response, and environment
- [ ] Tests assert on behavior/output, not internal implementation calls
- [ ] Core regression suite runs before every merge

---

## SELECTION CRITERIA / DECISION TABLE

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| Writing a new test for a feature | Write both happy-path and error-path tests | Testing only valid input |
| Mocking a dependency | Assert on your code's output/behavior using the mock | Asserting that the mock returned what you configured it to return |
| Test passes intermittently | Fix root cause: mock time, isolate state, remove external deps | Skipping or ignoring the test |
| Test suite exceeds time targets | Push tests down the pyramid; seed only needed data | Adding more system/integration tests |
| Requirement changes | Update RTM and all linked tests | Leaving stale tests in place |
| Tests pass locally, fail in staging | Match production config (DB version, Node version, env vars) via Docker | Hardcoding environment-specific values |
| A test fails in CI | Treat as a bug; investigate immediately | Saying "that test is always flaky" |
| Filing a defect | Use defect report template with full reproduction steps | Verbal or incomplete reports |
| Refactoring code (same behavior) | Tests should still pass without changes | Testing implementation details (internal method calls) |
| Deploying a bug fix | Run core regression suite before merge | Skipping regression ("we only changed one thing") |

---

## QUICK-REFERENCE TABLE

| Pitfall | One-Line Fix |
|---------|-------------|
| Happy path only | Write at least one error test per happy path test |
| Testing mocks | Assert on your code's behavior, not the mock's return |
| Flaky tests | Fix immediately. Mock time. Isolate state. |
| Slow suite | Push tests down the pyramid. Minimize data. |
| No traceability | Link every test to a requirement |
| Wrong environment | Match production config in test environments |
| Ignoring failures | Zero tolerance. Every failure is a bug. |
| Bad defect reports | Use the template. Include steps to reproduce. |
| Testing implementation | Test behavior and output, not internal calls |
| Skipping regression | Always run core regression before merge |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| For background | Training | [training/testing-phase-overview.md](training/testing-phase-overview.md) |
| Test level selection | Quick Reference | [testing-pyramid-explained.md](testing-pyramid-explained.md) |
| Test data setup | Quick Reference | [test-data-management-guide.md](test-data-management-guide.md) |
| Regression testing | Runbook | [../runbooks/perform-regression-testing.md](../runbooks/perform-regression-testing.md) |
| Defect report template | Template | [../templates/defect-report-template.md](../templates/defect-report-template.md) |
