# Testing Artifacts Checklist

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P6-002 |
| **Use When** | Verifying all required testing artifacts are produced before phase gate |
| **Last Updated** | 2026-03-04 |

---

## Per Sprint Artifacts

| # | Artifact | Produced By | Reviewed By | Done |
|---|----------|-------------|-------------|------|
| 1 | Test Plan (scope, approach, schedule) | QA Engineer | QA Lead | - [ ] |
| 2 | Test Cases (steps + expected results) | QA Engineer | QA Lead | - [ ] |
| 3 | Integration Test Code (new/changed endpoints) | Developer | Code Reviewer | - [ ] |
| 4 | Test Execution Results (pass/fail per case) | QA Engineer | QA Lead | - [ ] |
| 5 | Defect Reports (severity + repro steps) | QA Engineer | Tech Lead | - [ ] |
| 6 | Test Summary Report (metrics + risk) | QA Engineer | QA Lead | - [ ] |

---

## Per Release Artifacts

| # | Artifact | Produced By | Reviewed By | Done |
|---|----------|-------------|-------------|------|
| 7 | Release Test Plan (all test levels) | QA Lead | Tech Lead | - [ ] |
| 8 | Regression Test Results (full suite) | QA Engineer | QA Lead | - [ ] |
| 9 | Performance Test Report (load, response times) | QA Engineer | Tech Lead | - [ ] |
| 10 | Security Test Report (vuln scan, OWASP) | QA Engineer / Security | Tech Lead | - [ ] |
| 11 | UAT Sign-Off (business acceptance) | Product Owner | -- | - [ ] |
| 12 | Release Test Summary (go/no-go recommendation) | QA Lead | Tech Lead + Product Owner | - [ ] |

---

## Artifact Quality Criteria

| Artifact | Quality Check |
|----------|--------------|
| Test Plan | Covers all new features and changed areas. Identifies risks. Defines entry/exit criteria. |
| Test Cases | Traceable to requirements. Clear steps. Expected results defined. Priority assigned. |
| Integration Tests | Cover happy path + error paths. Isolated. Run in CI. |
| Defect Reports | Reproducible steps. Severity classified. Environment documented. |
| Test Summary | Includes metrics (pass rate, defect count). Provides go/no-go recommendation. |
| Performance Report | Compares to defined benchmarks. Identifies bottlenecks. |
| Security Report | Covers OWASP Top 10. No critical/high findings open. |
| UAT Sign-Off | All acceptance criteria verified. Signed by Product Owner. |

---

## Phase Gate Verification

- [ ] Test plan executed completely
- [ ] All critical and high priority test cases passed
- [ ] All critical and high severity defects resolved and re-tested
- [ ] Regression tests passed
- [ ] Integration test suite passes in CI
- [ ] Performance benchmarks met (release cycles)
- [ ] Security scan clean (release cycles)
- [ ] Test summary report written and approved
- [ ] UAT sign-off obtained (release cycles)
- [ ] No known critical or high severity defects remain

---

## DECISION TREE

```
Is this a sprint boundary or a release boundary?
  SPRINT --> Verify artifacts #1-6 are complete
  RELEASE --> Verify artifacts #1-12 are complete

For each artifact:
  Does the artifact exist?
    NO  --> Produce it before proceeding
    YES --> Does it meet quality criteria (see table above)?
      NO  --> Revise and re-review
      YES --> Mark as done

Are all phase gate verification items checked?
  NO  --> Identify blockers. Resolve or escalate.
  YES --> Proceed to deployment phase.
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Execute Test Cycle | Runbook | ../runbooks/execute-test-cycle.md |
| Report and Track Defects | Runbook | ../runbooks/report-and-track-defects.md |
| Perform Regression Testing | Runbook | ../runbooks/perform-regression-testing.md |
| Write Integration Tests | Runbook | ../runbooks/write-integration-tests.md |
| Write System Tests | Runbook | ../runbooks/write-system-tests.md |
