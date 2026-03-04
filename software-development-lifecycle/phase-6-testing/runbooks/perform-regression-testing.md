# Perform Regression Testing

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P6-005 |
| **Owner** | QA Lead |
| **Accountable** | QA Lead |
| **SLA** | Smoke: 5 min, Core: 30 min, Full: 2-4 hours |
| **Escalation** | Tech Lead (regression failures), Product Owner (release-blocking decisions) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Code change merged and deployed to test environment
- [ ] Change type identified (feature, bug fix, refactor, migration, dependency update)
- [ ] Test environment healthy and accessible
- [ ] Previous regression test results available for comparison

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Test environment unstable or unreachable | STOP. Raise infra ticket | Tech Lead |
| Smoke tests fail (system not functional) | STOP. Roll back deployment or fix before regression | Tech Lead |
| More than 5 regression failures in a single run | STOP. Likely systemic issue. Initiate root cause analysis | Tech Lead |

---

## PROCEDURE

### Step 1: Determine Regression Scope

| Action | Owner | SLA |
|--------|-------|-----|
| Identify change type and map to regression scope | QA Lead | 30 min |

| Trigger | Scope |
|---------|-------|
| Feature merged to develop | Targeted regression (related features only) |
| Bug fix deployed | Targeted regression + the fixed area |
| Release branch created | Full regression suite |
| Major refactoring merged | Full regression suite |
| Database migration applied | Full regression suite |
| Dependency update (major version) | Full regression suite |

| Change | Regression Scope |
|--------|-----------------|
| Billing module change | Billing tests + rental tests |
| Auth module change | All modules |
| Database schema change | All modules using affected tables |
| API response format change | All API consumer tests |
| Shared utility change | All modules importing the utility |

- [ ] Change type identified
- [ ] Regression scope determined
- [ ] Scope documented

> **IF** unsure of scope **THEN** run the full suite (cost of missing a regression exceeds cost of extra tests)
> **ELSE** proceed with determined scope

### Step 2: Prepare the Environment

| Action | Owner | SLA |
|--------|-------|-----|
| Deploy latest code to test environment | QA Lead / DevOps | 30 min |
| Reset test data to standard data set | QA Lead | 15 min |
| Verify all services are healthy | QA Lead | 10 min |

- [ ] Latest code deployed
- [ ] Test data reset
- [ ] `curl https://staging.glowpower.sa/api/v1/health` returns 200
- [ ] All services healthy

> **IF** health check fails **THEN** STOP. Raise infra ticket, notify Tech Lead
> **ELSE** proceed to Step 3

### Step 3: Run Automated Regression Tests

| Action | Owner | SLA |
|--------|-------|-----|
| Run regression suite (full or targeted based on Step 1) | QA Lead | 30 min - 2 hours |

```bash
# Full regression suite
npm run test:regression

# Targeted regression (specific module)
npm run test:regression -- --testPathPattern="<module>"
```

Automated regression includes:
- All unit tests
- All integration tests
- Automated system tests for critical journeys

- [ ] Automated regression suite executed
- [ ] Results recorded
- [ ] Failures identified

> **IF** all automated tests pass **THEN** proceed to Step 4
> **ELSE IF** failures exist **THEN** document each failure, proceed to Step 4 while investigation begins

### Step 4: Execute Manual Regression Tests

| Action | Owner | SLA |
|--------|-------|-----|
| Open regression test case list | QA Lead | 5 min |
| Execute test cases based on determined scope | QA Lead | 1-2 hours |

Focus areas:
- [ ] Features adjacent to the changed area
- [ ] Features that share data with the changed area
- [ ] Critical paths regardless of change (smoke tests)

> **IF** scope is targeted **THEN** execute only related manual test cases
> **ELSE IF** scope is full **THEN** execute all manual regression test cases

### Step 5: Compare Results

| Action | Owner | SLA |
|--------|-------|-----|
| Compare current results against previous run | QA Lead | 30 min |

| Result | Action |
|--------|--------|
| All tests pass | Regression testing complete. Proceed. |
| New failure in changed area | Likely bug in new code. Log defect. Fix before proceeding. |
| New failure in unchanged area | Regression bug. Log as High severity defect. |
| Previously failing test now passes | Verify this is expected (side effect of the fix). Document. |
| Flaky test (intermittent failure) | Log as defect. Investigate root cause. Do not ignore. |

- [ ] All results compared to previous baseline
- [ ] New failures categorized
- [ ] Flaky tests identified

### Step 6: Handle Regression Failures

| Action | Owner | SLA |
|--------|-------|-----|
| Log defect for each regression failure (minimum severity: High) | QA Lead | 30 min per defect |
| Notify Tech Lead and developer who introduced the change | QA Lead | 15 min |
| Re-run full regression scope after fix is deployed | QA Lead | Per scope SLA |

- [ ] All regression failures logged as defects (severity >= High)
- [ ] Each defect includes: what was working before, what is broken now, which change likely caused it
- [ ] Developer who introduced change notified and assigned

> **IF** regression failure found **THEN** STOP release. Do not proceed until regression is resolved and re-tested.
> **ELSE** proceed to Step 7

Defect SLAs for regression failures:

| Severity | SLA | Escalation |
|----------|-----|------------|
| Critical | 4 hours | Tech Lead + PM immediately |
| High | 1 business day | Tech Lead at triage |

### Step 7: Update Regression Suite

| Action | Owner | SLA |
|--------|-------|-----|
| Review and update regression suite based on cycle results | QA Lead | 1 hour |

| Action | When |
|--------|------|
| Add new test cases | New feature added; its tests join regression |
| Remove test cases | Feature removed or replaced |
| Update test cases | Feature behavior changed intentionally |
| Mark flaky tests for investigation | Test fails intermittently |

- [ ] New test cases added for new features
- [ ] Obsolete test cases removed
- [ ] Modified test cases updated
- [ ] Flaky tests flagged for investigation

---

## EXIT CRITERIA

- [ ] Regression scope determined and documented
- [ ] Test environment prepared with latest code
- [ ] Automated regression tests executed
- [ ] Manual regression tests executed (if in scope)
- [ ] Results compared to previous run
- [ ] All regressions logged as High severity defects (minimum)
- [ ] Regression defects fixed and re-tested
- [ ] Regression suite updated with new/modified test cases

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Regression test results | Test runner output | CI artifacts / project tracker |
| Defect reports (regression failures) | [defect-report-template.md](../templates/defect-report-template.md) | Project tracker |
| Updated regression suite | Source code | Source repository |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Testing Strategy Standard | Standard | [../standards/testing-strategy-standard.md](../standards/testing-strategy-standard.md) |
| Performance Testing Standard | Standard | [../standards/performance-testing-standard.md](../standards/performance-testing-standard.md) |
| Defect Report Template | Template | [../templates/defect-report-template.md](../templates/defect-report-template.md) |
| Defect Severity Reference | Reference | [../references/defect-severity-reference.md](../references/defect-severity-reference.md) |
| Test Case Template | Template | [../templates/test-case-template.md](../templates/test-case-template.md) |
