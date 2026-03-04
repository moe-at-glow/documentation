# Defect Severity Reference

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P6-001 |
| **Use When** | Classifying defect severity and priority during test execution or triage |
| **Last Updated** | 2026-03-04 |

---

## Severity Levels

### Critical

| Criteria | Examples |
|----------|---------|
| System crash or hang | Application crashes on startup. Server returns 500 for all requests. |
| Data loss or corruption | Rental records deleted. Payment amounts modified incorrectly. |
| Security breach | Unauthorized access to customer data. SQL injection successful. |
| Financial error | Payment charged wrong amount. Invoice total incorrect. |
| Complete feature failure | Login does not work for any user. Cannot create any rental. |

**SLA:** Fix within 4 hours. Escalate immediately to Tech Lead and Project Manager.

### High

| Criteria | Examples |
|----------|---------|
| Core feature broken | Cannot return equipment. Late fee not calculated. |
| No workaround | No alternative way to accomplish the task. |
| Affects many users | All customers see wrong data. All new rentals fail validation. |
| Blocking other testing | Cannot test downstream features because this is broken. |

**SLA:** Fix within 1 business day. Must be resolved before release.

### Medium

| Criteria | Examples |
|----------|---------|
| Feature works incorrectly | Filter shows wrong results, but data is correct in detail view. |
| Workaround available | Export fails, but data can be retrieved via API. |
| Non-critical feature | Report formatting is wrong. Dashboard widget shows stale data. |
| Performance degradation | Page loads in 3 seconds instead of target 200ms. |

**SLA:** Fix within current sprint. Can release with known issue if documented.

### Low

| Criteria | Examples |
|----------|---------|
| Cosmetic | Alignment issue. Font inconsistency. Extra whitespace. |
| Minor UX | Button label unclear. Error message could be more helpful. |
| Edge case | Rare scenario produces unexpected but non-harmful behavior. |
| Documentation | API documentation has a typo. Help text is outdated. |

**SLA:** Fix in next sprint or add to backlog. Does not block release.

---

## Priority vs. Severity

| Severity | Priority | Example |
|----------|----------|---------|
| Critical | Urgent | Payment processes wrong amount -> Fix NOW |
| High | High | Cannot create rental -> Fix this sprint |
| Medium | Medium | Export broken (workaround exists) -> Fix when available |
| Low | Low | Typo in error message -> Fix in backlog |
| Low | High | CEO demo is tomorrow and logo is wrong -> Fix now despite low severity |
| Medium | Low | Rare edge case in archived data -> Fix eventually |

**Rule:** When severity and priority disagree, the **Product Owner** sets the priority.

---

## Defect Resolution SLA Summary

| Severity | Fix SLA | Release Blocker? | Escalation |
|----------|---------|-----------------|------------|
| Critical | 4 hours | Yes | Immediate: Tech Lead + PM |
| High | 1 business day | Yes | Same day: Tech Lead |
| Medium | Current sprint | No (with documentation) | Sprint planning |
| Low | Next sprint / backlog | No | Backlog grooming |

---

## DECISION TREE

```
Is the system completely unusable or is data being lost/corrupted?
  YES --> Critical
  NO  --> Continue

Is a major feature completely broken with no workaround?
  YES --> High
  NO  --> Continue

Is the feature broken but has a workaround, or is a non-critical feature affected?
  YES --> Medium
  NO  --> Continue

Is it cosmetic, a minor inconvenience, or a documentation issue?
  YES --> Low
```

---

## Defect Lifecycle States

```
New --> Triaged --> Assigned --> In Progress --> Fixed --> Re-test --> Closed
                       |                                      |
                       |                                      └--> Reopened
                       |
                       ├--> Won't Fix (with rationale)
                       ├--> Duplicate (linked to original)
                       └--> Need More Info (back to reporter)
```

| Transition | Who | Criteria |
|-----------|-----|---------|
| New -> Triaged | QA Lead / Tech Lead | Severity confirmed, reproducible |
| Triaged -> Assigned | Tech Lead | Developer identified |
| Assigned -> In Progress | Developer | Work started |
| In Progress -> Fixed | Developer | Fix pushed, ready for re-test |
| Fixed -> Re-test | QA | Fix deployed to test environment |
| Re-test -> Closed | QA | Fix verified, regression checked |
| Re-test -> Reopened | QA | Fix did not resolve the issue |

---

## Metrics

| Metric | Formula | Target |
|--------|---------|--------|
| Defect density | Defects found / KLOC (thousands of lines of code) | < 5 defects/KLOC |
| Defect fix rate | Defects fixed / Defects found per sprint | > 80% |
| Defect reopen rate | Defects reopened / Defects fixed | < 10% |
| Defect leakage | Production defects / Total defects found | < 5% |
| Mean time to fix (Critical) | Average hours from report to fix for Critical | < 4 hours |
| Mean time to fix (High) | Average hours from report to fix for High | < 8 hours |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Execute Test Cycle | Runbook | ../runbooks/execute-test-cycle.md |
| Report and Track Defects | Runbook | ../runbooks/report-and-track-defects.md |
| Perform Regression Testing | Runbook | ../runbooks/perform-regression-testing.md |
| Write Integration Tests | Runbook | ../runbooks/write-integration-tests.md |
| Write System Tests | Runbook | ../runbooks/write-system-tests.md |
