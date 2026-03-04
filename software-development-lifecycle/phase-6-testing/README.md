# Phase 6: Testing

Testing standards, procedures, and references for GlowPowerRental projects.

All documents follow the **QRH (Quick Reference Handbook)** format. For background/educational content, see the `training/` subdirectory.

---

## Purpose

The Testing phase verifies that implemented code meets the requirements defined in Phase 2, the architecture defined in Phase 3, and the detailed designs from Phase 4.

**Input:** Working code on `develop` branch with passing unit tests from Phase 5.

**Output:** Tested software with test reports, defect logs, and sign-off for deployment.

---

## Documents

### Standards (compliance checklists)

| Document | Description |
|----------|-------------|
| [Testing Strategy Standard](standards/testing-strategy-standard.md) | Test levels, types, environments, and exit criteria |
| [Integration Testing Standard](standards/integration-testing-standard.md) | API and service integration test requirements |
| [System Testing Standard](standards/system-testing-standard.md) | End-to-end system test requirements |
| [Performance Testing Standard](standards/performance-testing-standard.md) | Load, stress, and performance test requirements |
| [Security Testing Standard](standards/security-testing-standard.md) | Security and vulnerability testing requirements |

### Runbooks (QRH procedures)

| Document | Description |
|----------|-------------|
| [Execute Test Cycle](runbooks/execute-test-cycle.md) | Step-by-step procedure for running a complete test cycle |
| [Write Integration Tests](runbooks/write-integration-tests.md) | How to write and run integration tests |
| [Write System Tests](runbooks/write-system-tests.md) | How to write and run end-to-end system tests |
| [Report and Track Defects](runbooks/report-and-track-defects.md) | Defect reporting, classification, and lifecycle |
| [Perform Regression Testing](runbooks/perform-regression-testing.md) | When and how to run regression test suites |

### Guides (quick references)

| Document | Description |
|----------|-------------|
| [Test Data Management Guide](guides/test-data-management-guide.md) | Creating, managing, and isolating test data |
| [Testing Pyramid Explained](guides/testing-pyramid-explained.md) | Unit, integration, and system test balance |
| [Common Testing Pitfalls](guides/common-testing-pitfalls.md) | Mistakes to avoid during testing |

### Training Materials

| Document | Description |
|----------|-------------|
| [Testing Phase Overview](guides/training/testing-phase-overview.md) | Background on how testing fits into the SDLC |

### References (decision aids)

| Document | Description |
|----------|-------------|
| [Testing Artifacts Checklist](references/testing-artifacts-checklist.md) | All artifacts produced during testing |
| [Test Coverage Matrix](references/test-coverage-matrix.md) | Coverage targets by test level and code category |
| [Defect Severity Reference](references/defect-severity-reference.md) | Defect classification and SLA reference |
| [Testing Tools Reference](references/testing-tools-reference.md) | Tools used for testing at each level |

### Templates

| Document | Description |
|----------|-------------|
| [Test Plan Template](templates/test-plan-template.md) | Template for sprint or release test plans |
| [Test Case Template](templates/test-case-template.md) | Template for individual test cases |
| [Defect Report Template](templates/defect-report-template.md) | Template for defect/bug reports |
| [Test Summary Report Template](templates/test-summary-report-template.md) | Template for test cycle summary reports |
| [UAT Sign-Off Template](templates/uat-sign-off-template.md) | Template for user acceptance testing sign-off |

---

## Phase Entry Criteria

- [ ] Code is merged to `develop` and CI passes
- [ ] Unit tests pass with required coverage (Phase 5 exit criteria met)
- [ ] Test environment is available and configured
- [ ] Test data is prepared
- [ ] Test plan is reviewed and approved

## Phase Exit Criteria

- [ ] All planned test cases executed
- [ ] All critical and high-severity defects resolved
- [ ] Regression tests pass
- [ ] Performance benchmarks met
- [ ] Security scan passes with no critical/high findings
- [ ] Test summary report approved by QA Lead
- [ ] UAT sign-off obtained (for releases)
