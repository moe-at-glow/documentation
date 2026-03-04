# System Testing Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P6-005 |
| **Compliance Level** | Mandatory |
| **Enforced By** | QA Lead |
| **Verification Method** | Test Review / CI Pipeline |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Critical user journeys only; minimal test data set; automated regression on critical paths; manual exploratory optional
> **IF** medium project (3-5 devs) **THEN** Critical + high priority journeys; standard test data set; automated regression + manual exploratory
> **IF** large project (6+ devs) **THEN** Full compliance required

---

## COMPLIANCE REQUIREMENTS

### Critical User Journeys

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Customer rental lifecycle tested: browse -> request -> approve -> active -> return -> invoice | All projects | [ ] Test execution log | Release blocked |
| 2 | Payment processing tested: generate invoice -> process payment -> update balance -> send receipt | All projects | [ ] Test execution log | Release blocked |
| 3 | Late fee handling tested: overdue -> calculate fee -> add to invoice -> notify customer | All projects | [ ] Test execution log | Release blocked |
| 4 | Equipment management tested: add -> assign to rental -> track via IoT -> schedule maintenance | Medium+ projects | [ ] Test execution log | Release blocked |
| 5 | User authentication tested: register -> login -> access protected resources -> logout | All projects | [ ] Test execution log | Release blocked |
| 6 | Reporting tested: generate report -> filter by date/status -> export | Medium+ projects | [ ] Test execution log | Release blocked |

### Cross-Module Flows

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 7 | Customer -> Rental -> Billing flow tested end-to-end | All projects | [ ] Test execution log | Release blocked |
| 8 | Rental -> Return -> Late Fee Calculation -> Payment flow tested | All projects | [ ] Test execution log | Release blocked |
| 9 | Invoice Generation -> Payment Processing flow tested | All projects | [ ] Test execution log | Release blocked |

### Test Environment

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 10 | System tests run in staging environment | All projects | [ ] Environment audit | Tests invalid |
| 11 | Application: same Docker image as production | All projects | [ ] Image tag verification | Tests invalid |
| 12 | Database: PostgreSQL same version as production, with anonymized data | All projects | [ ] Environment config | Tests invalid |
| 13 | Cache: Redis same version as production | All projects | [ ] Environment config | Tests invalid |
| 14 | MQTT Broker: Mosquitto same version as production | Medium+ projects | [ ] Environment config | Tests invalid |
| 15 | External services: sandbox/test instances of payment gateway, email, SMS | All projects | [ ] Environment config | Tests invalid |
| 16 | Network: staging network isolated from production | All projects | [ ] Network audit | Immediate escalation |

### Environment Readiness

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 17 | Staging environment matches production configuration | All projects | [ ] Environment config diff | Tests blocked |
| 18 | Database schema current (all migrations applied) | All projects | [ ] Migration status check | Tests blocked |
| 19 | Test data loaded (anonymized production-like data) | All projects | [ ] Data load verification | Tests blocked |
| 20 | External service sandboxes accessible | All projects | [ ] Connectivity check | Tests blocked |
| 21 | Environment variables set for staging | All projects | [ ] Env var audit | Tests blocked |

### Test Case Design

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 22 | Each test case includes: Test ID (SYS-TC-NNN), Title, Priority, Preconditions, Steps, Expected Result, Postconditions | All projects | [ ] Test case review | Test case rework |
| 23 | Critical priority: revenue-impacting or data-integrity workflows | All projects | [ ] Priority classification review | Reclassification required |
| 24 | High priority: core business functionality | All projects | [ ] Priority classification review | Reclassification required |
| 25 | Medium priority: supporting functionality | Medium+ projects | [ ] Priority classification review | Accepted |
| 26 | Low priority: convenience features | Large projects | [ ] Priority classification review | Accepted |

### Test Data

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 27 | Production-like volume to surface pagination, performance, and edge case issues | All projects | [ ] Data volume audit | Re-run with correct data |
| 28 | Anonymized: no real customer names, emails, or financial data | All projects | [ ] Data anonymization audit | Immediate remediation |
| 29 | Consistent: same versioned, reproducible data set for all system tests | All projects | [ ] Data set version check | Data set correction |
| 30 | Resettable: can be reset to known state before each test cycle | All projects | [ ] Reset procedure verification | Procedure must be created |

### Test Data Sets

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 31 | Minimal set (smoke tests): 10 customers, 20 equipment, 50 rentals | All projects | [ ] Data set audit | Data set correction |
| 32 | Standard set (full system testing): 100 customers, 200 equipment, 500 rentals | Medium+ projects | [ ] Data set audit | Data set correction |
| 33 | Load set (performance testing): 10,000 customers, 50,000 equipment, 200,000 rentals | Large projects | [ ] Data set audit | Data set correction |

### Manual System Test Execution

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 34 | QA Engineer follows test cases from test plan | All projects | [ ] Test execution records | Re-execution required |
| 35 | Actual results recorded for each step | All projects | [ ] Test execution records | Re-execution required |
| 36 | Defects logged for any deviation from expected results | All projects | [ ] Defect tracker | Defect must be logged |
| 37 | Test case marked as Pass / Fail / Blocked | All projects | [ ] Test execution records | Status must be recorded |

### Automated System Test Execution

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 38 | Regression and smoke tests automated | Medium+ projects | [ ] CI pipeline config | Automation backlog item |
| 39 | Automated tests run against staging URL with real authentication | Medium+ projects | [ ] Test execution log | Test rework |
| 40 | Automated tests verify full workflow (create -> activate -> return -> invoice) | Medium+ projects | [ ] Test code review | Test rework |

### Defect Handling

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 41 | Log defect using Defect Report Template | All projects | [ ] Defect tracker | Defect must be logged |
| 42 | Classify severity: Critical / High / Medium / Low | All projects | [ ] Defect severity field | Classification required |
| 43 | Link defect to failing test case | All projects | [ ] Defect-test link | Link must be added |
| 44 | Re-run failed test case after fix | All projects | [ ] Re-test execution log | Re-test required |

### Exit Criteria

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 45 | All critical priority test cases pass | All projects | [ ] Test summary report | Release blocked |
| 46 | All high priority test cases pass (or failures documented with accepted risk) | All projects | [ ] Test summary report | Release blocked |
| 47 | No critical or high severity defects remain open | All projects | [ ] Defect tracker | Release blocked |
| 48 | Medium severity defects documented with fix plan | All projects | [ ] Defect tracker | Release blocked |
| 49 | Performance benchmarks met | Medium+ projects | [ ] Performance test report | Release blocked |
| 50 | Security scan clean | All projects | [ ] Security scan report | Release blocked |
| 51 | Test summary report written and approved | All projects | [ ] Approved report artifact | Release blocked |

---

## COMPLIANCE CHECKLIST

- [ ] All critical user journeys have system tests (rental lifecycle, payment, late fees, auth)
- [ ] All cross-module flows tested end-to-end
- [ ] Staging environment matches production configuration
- [ ] Database schema current with all migrations applied
- [ ] Test data loaded, anonymized, and resettable
- [ ] External service sandboxes accessible
- [ ] Test cases follow standard format (SYS-TC-NNN with all required fields)
- [ ] Manual tests executed with results recorded per step
- [ ] Defects logged for all deviations with severity classification
- [ ] Automated regression/smoke tests running in CI
- [ ] All critical priority test cases pass
- [ ] All high priority test cases pass (or accepted risk documented)
- [ ] No critical/high severity defects open
- [ ] Medium defects have documented fix plans
- [ ] Performance benchmarks met
- [ ] Security scan clean
- [ ] Test summary report written and approved

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Write System Tests | Runbook | [../runbooks/write-system-tests.md](../runbooks/write-system-tests.md) |
| Execute Test Cycle | Runbook | [../runbooks/execute-test-cycle.md](../runbooks/execute-test-cycle.md) |
| Report and Track Defects | Runbook | [../runbooks/report-and-track-defects.md](../runbooks/report-and-track-defects.md) |
| Perform Regression Testing | Runbook | [../runbooks/perform-regression-testing.md](../runbooks/perform-regression-testing.md) |
| Write Integration Tests | Runbook | [../runbooks/write-integration-tests.md](../runbooks/write-integration-tests.md) |
| Test Plan Template | Template | [../templates/test-plan-template.md](../templates/test-plan-template.md) |
| Test Case Template | Template | [../templates/test-case-template.md](../templates/test-case-template.md) |
| Defect Report Template | Template | [../templates/defect-report-template.md](../templates/defect-report-template.md) |
| Test Summary Report Template | Template | [../templates/test-summary-report-template.md](../templates/test-summary-report-template.md) |
| UAT Sign-Off Template | Template | [../templates/uat-sign-off-template.md](../templates/uat-sign-off-template.md) |
| Defect Severity Reference | Reference | [../references/defect-severity-reference.md](../references/defect-severity-reference.md) |
