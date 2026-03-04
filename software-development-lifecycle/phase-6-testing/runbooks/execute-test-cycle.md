# Execute Test Cycle

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P6-001 |
| **Owner** | QA Lead |
| **Accountable** | QA Lead |
| **SLA** | 2-3 business days per sprint cycle; 5 business days per release cycle |
| **Escalation** | Tech Lead (technical issues), Product Owner (severity/priority disputes) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Code merged to `develop` with passing CI (Phase 5 exit criteria met)
- [ ] Test environment (staging) available and configured
- [ ] Test plan reviewed and approved
- [ ] Test data prepared and loaded

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Staging environment unreachable or unstable | STOP. Raise infra ticket and notify Tech Lead | Tech Lead |
| More than 3 critical defects found in smoke tests | STOP. Block test cycle and initiate emergency triage | Tech Lead + Product Owner |
| Test data corrupted or missing | STOP. Reset test data before proceeding | Tech Lead |
| CI pipeline broken on `develop` | STOP. Do not deploy to staging until CI is green | Tech Lead |

---

## PROCEDURE

### Step 1: Prepare the Test Environment

| Action | Owner | SLA |
|--------|-------|-----|
| Deploy latest `develop` (or release branch) to staging | QA Lead / DevOps | 30 min |
| Run database migrations on staging database | QA Lead / DevOps | 15 min |
| Load or reset test data to standard data set | QA Lead | 15 min |
| Verify all services are running via health checks | QA Lead | 15 min |
| Confirm external service sandboxes are accessible (payment gateway, email, SMS) | QA Lead | 15 min |

- [ ] `curl https://staging.glowpower.sa/api/v1/health` returns 200
- [ ] Database connectivity verified
- [ ] Redis connectivity verified
- [ ] MQTT broker connectivity verified
- [ ] External sandboxes responding

> **IF** any service health check fails **THEN** raise infra ticket, notify Tech Lead, do not proceed
> **ELSE** proceed to Step 2

### Step 2: Run Smoke Tests

| Action | Owner | SLA |
|--------|-------|-----|
| Execute smoke test suite against staging | QA Lead | 30 min |

| Test | Expected Result |
|------|----------------|
| Health check endpoint | 200 OK |
| Login with test credentials | JWT token returned |
| List rentals (authenticated) | 200 with rental data |
| Create a rental | 201 Created |
| View dashboard | 200 with data |

- [ ] All smoke tests pass

> **IF** any smoke test fails **THEN** STOP. Fix deployment issue before proceeding. Escalate to Tech Lead.
> **ELSE** proceed to Step 3

### Step 3: Execute Integration Tests

| Action | Owner | SLA |
|--------|-------|-----|
| Run full integration test suite: `npm run test:integration` | QA Lead | 1 hour |
| Review results and log failures as defects | QA Lead | 30 min |
| Check coverage report against requirements | QA Lead | 15 min |

- [ ] Integration test suite executed
- [ ] All failures logged as defects using [Defect Report Template](../templates/defect-report-template.md)
- [ ] Coverage meets integration test requirements

> **IF** coverage below threshold **THEN** flag to Tech Lead for developer action
> **ELSE** proceed to Step 4

### Step 4: Execute System Tests

| Action | Owner | SLA |
|--------|-------|-----|
| Open test plan for current sprint/release | QA Lead | 5 min |
| Execute test cases in priority order: Critical > High > Medium > Low | QA Lead | 4-8 hours |
| Record actual result for each test case | QA Lead | Continuous |

- [ ] All Critical test cases executed
- [ ] All High test cases executed
- [ ] Medium/Low test cases executed (time permitting)

For each test case:
> **IF** Pass **THEN** mark as Pass, proceed to next test
> **ELSE IF** Fail **THEN** log defect immediately using [Defect Report Template](../templates/defect-report-template.md), continue testing
> **ELSE IF** Blocked **THEN** document blocker, move to next test

### Step 5: Execute Regression Tests

| Action | Owner | SLA |
|--------|-------|-----|
| Run automated regression tests: `npm run test:regression` | QA Lead | 1 hour |
| Execute manual regression test cases from test plan | QA Lead | 2 hours |

- [ ] Automated regression tests executed
- [ ] Manual regression tests executed
- [ ] All regression failures logged as defects (minimum severity: High)

> **IF** regression failure found **THEN** log defect with severity >= High, notify Tech Lead
> **ELSE** proceed to Step 6

### Step 6: Execute Performance Tests (Release Cycles Only)

| Action | Owner | SLA |
|--------|-------|-----|
| Run load tests against staging | QA Lead | 2 hours |
| Compare results to performance targets | QA Lead | 30 min |

- [ ] Load test results within targets per [Performance Testing Standard](../standards/performance-testing-standard.md)
- [ ] Performance degradation logged as defects

> **IF** not a release cycle **THEN** skip to Step 8
> **ELSE** proceed to Step 7

### Step 7: Execute Security Tests (Release Cycles Only)

| Action | Owner | SLA |
|--------|-------|-----|
| Run `npm audit` and review results | QA Lead | 30 min |
| Verify security headers on all endpoints | QA Lead | 30 min |
| Run authentication and authorization test cases | QA Lead | 1 hour |
| Review OWASP Top 10 checklist | QA Lead | 1 hour |

- [ ] `npm audit` shows no critical/high vulnerabilities
- [ ] Security headers present on all endpoints
- [ ] Auth test cases pass
- [ ] OWASP Top 10 checklist reviewed
- [ ] Security findings logged using security finding format

### Step 8: Review Defects

| Action | Owner | SLA |
|--------|-------|-----|
| Compile all defects found during test cycle | QA Lead | 30 min |
| Review defect list with Tech Lead and Product Owner | QA Lead | 1 hour |
| Classify each defect by severity | QA Lead + Tech Lead | 30 min |

| Severity | Action |
|----------|--------|
| Critical | Must fix before release. Block the release. SLA: 4 hours. |
| High | Must fix before release. SLA: 1 business day. |
| Medium | Fix if time allows. Can release with known issue if documented. SLA: current sprint. |
| Low | Add to backlog. Can release. SLA: next sprint. |

- [ ] All defects classified and triaged
- [ ] Critical/High defects assigned to developers

> **IF** Critical defect not fixed within 4 hours **THEN** escalate to Tech Lead + PM immediately
> **ELSE IF** severity/priority dispute **THEN** escalate to Product Owner

### Step 9: Re-Test Fixed Defects

| Action | Owner | SLA |
|--------|-------|-----|
| Re-deploy fixes to staging | QA Lead / DevOps | 30 min |
| Re-run specific failed test cases | QA Lead | 2 hours |
| Run targeted regression on fixed areas | QA Lead | 1 hour |
| Update defect status to Verified/Closed | QA Lead | 15 min |

- [ ] All fixed defects re-tested
- [ ] Targeted regression passed
- [ ] Defect statuses updated

> **IF** fix does not resolve defect **THEN** reopen defect, reassign to developer
> **ELSE** mark defect as Verified/Closed

### Step 10: Write Test Summary Report

| Action | Owner | SLA |
|--------|-------|-----|
| Complete [Test Summary Report Template](../templates/test-summary-report-template.md) | QA Lead | 2 hours |

- [ ] Total test cases documented: planned vs. executed vs. passed vs. failed vs. blocked
- [ ] Defect summary: found, fixed, remaining
- [ ] Coverage summary completed
- [ ] Risk assessment completed
- [ ] Go/No-Go recommendation documented

### Step 11: Obtain Sign-Off

| Action | Owner | SLA |
|--------|-------|-----|
| Obtain QA sign-off | QA Lead | After all critical/high defects resolved |
| Obtain UAT sign-off | Product Owner | After acceptance criteria verified |
| Obtain release approval | Tech Lead + Product Owner | After all sign-offs obtained |

- [ ] QA sign-off obtained
- [ ] UAT sign-off obtained
- [ ] Release approval granted

> **IF** any sign-off withheld **THEN** document reasons, schedule remediation, re-enter cycle at applicable step
> **ELSE** test cycle complete

---

## EXIT CRITERIA

- [ ] Staging environment deployed and verified
- [ ] Smoke tests pass
- [ ] Integration tests executed and results recorded
- [ ] System tests executed (all critical/high priority)
- [ ] Regression tests executed
- [ ] Performance tests executed (release cycles)
- [ ] Security tests executed (release cycles)
- [ ] All critical/high defects resolved and re-tested
- [ ] Test summary report written
- [ ] QA sign-off obtained
- [ ] UAT sign-off obtained (if applicable)
- [ ] Release approval granted

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Test Summary Report | [test-summary-report-template.md](../templates/test-summary-report-template.md) | Project tracker / release folder |
| Defect Reports | [defect-report-template.md](../templates/defect-report-template.md) | Project tracker |
| UAT Sign-Off | [uat-sign-off-template.md](../templates/uat-sign-off-template.md) | Project tracker / release folder |
| Test Execution Results | Per test plan | Project tracker |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Testing Strategy Standard | Standard | [../standards/testing-strategy-standard.md](../standards/testing-strategy-standard.md) |
| Performance Testing Standard | Standard | [../standards/performance-testing-standard.md](../standards/performance-testing-standard.md) |
| Security Testing Standard | Standard | [../standards/security-testing-standard.md](../standards/security-testing-standard.md) |
| Defect Severity Reference | Reference | [../references/defect-severity-reference.md](../references/defect-severity-reference.md) |
| Test Plan Template | Template | [../templates/test-plan-template.md](../templates/test-plan-template.md) |
| Defect Report Template | Template | [../templates/defect-report-template.md](../templates/defect-report-template.md) |
| Test Summary Report Template | Template | [../templates/test-summary-report-template.md](../templates/test-summary-report-template.md) |
| UAT Sign-Off Template | Template | [../templates/uat-sign-off-template.md](../templates/uat-sign-off-template.md) |
