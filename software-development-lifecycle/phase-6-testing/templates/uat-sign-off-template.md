# UAT Sign-Off Template

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P6-005 |
| **When to Use** | User Acceptance Testing sign-off before production release |
| **Owner** | QA Lead |
| **Reviewer** | Tech Lead / Product Owner |
| **SLA** | 2 business days after UAT completion |
| **Runbook** | [Execute Test Cycle](../runbooks/execute-test-cycle.md) |
| **Last Verified** | 2026-03-04 |

---

## Scaling Decision Gate

| Factor | Minor Release (1-3 features) | Standard Release (4-10 features) | Major Release (> 10 features) |
|--------|-------------------------------|-----------------------------------|-------------------------------|
| Feature testing depth | Acceptance criteria only | Acceptance criteria + edge cases | Acceptance criteria + edge cases + exploratory |
| Business readiness items | Documentation + support | Documentation + support + training | Full readiness checklist |
| Approvals required | Product Owner | Product Owner + Tech Lead | Product Owner + Tech Lead + QA Lead + BA |
| Sign-off meeting | Async approval | 30-min review meeting | Formal sign-off meeting with demo |

---

## [ ] UAT Information

| Field | Value |
|-------|-------|
| Project | GlowPowerRental |
| Release | <!-- Release X.Y.Z --> |
| UAT Period | <!-- YYYY-MM-DD to YYYY-MM-DD --> |
| Environment | <!-- Staging URL --> |
| UAT Lead | <!-- Product Owner name --> |
| Date | <!-- YYYY-MM-DD --> |

---

## [ ] 1. Features Tested

| Feature | Ticket | Acceptance Criteria | Result |
|---------|--------|-------------------|--------|
| <!-- feature --> | TICKET-NNN | <!-- summary of criteria --> | <!-- Accepted / Rejected / Deferred --> |

---

## [ ] 2. Acceptance Criteria Verification

### [ ] Feature: <!-- Feature Name -->

| # | Acceptance Criterion | Verified? | Notes |
|---|---------------------|-----------|-------|
| 1 | <!-- criterion from ticket --> | <!-- Yes / No / Partial --> | <!-- observations --> |
| 2 | <!-- --> | <!-- --> | <!-- --> |
| 3 | <!-- --> | <!-- --> | <!-- --> |

<!-- Repeat for each feature -->

---

## [ ] 3. UAT Test Results

| Metric | Count |
|--------|-------|
| Total scenarios tested | <!-- N --> |
| Passed | <!-- N --> |
| Failed | <!-- N --> |
| Deferred | <!-- N --> |

---

## [ ] 4. Issues Found During UAT

| # | Description | Severity | Resolution |
|---|------------|----------|-----------|
| 1 | <!-- issue --> | <!-- Critical / High / Medium / Low --> | <!-- Fixed / Deferred / Accepted --> |

---

## [ ] 5. Known Limitations

| # | Limitation | Impact | Workaround |
|---|-----------|--------|-----------|
| 1 | <!-- --> | <!-- --> | <!-- --> |

---

## [ ] 6. Business Readiness

| Item | Ready? | Notes |
|------|--------|-------|
| User documentation updated | <!-- Yes / No / N/A --> | <!-- --> |
| Training completed | <!-- Yes / No / N/A --> | <!-- --> |
| Support team briefed | <!-- Yes / No / N/A --> | <!-- --> |
| Data migration verified | <!-- Yes / No / N/A --> | <!-- --> |
| Rollback plan reviewed | <!-- Yes / No / N/A --> | <!-- --> |

---

## [ ] 7. Sign-Off Decision

### [ ] Decision

- [ ] **ACCEPTED** -- The release meets acceptance criteria and is approved for production deployment.
- [ ] **CONDITIONALLY ACCEPTED** -- The release is approved with the conditions listed below.
- [ ] **REJECTED** -- The release does not meet acceptance criteria. Issues listed above must be resolved.

### [ ] Conditions (if conditionally accepted)

1. <!-- condition -->
2. <!-- condition -->

---

## [ ] 8. Approvals

| Role | Name | Decision | Signature | Date |
|------|------|----------|-----------|------|
| Product Owner | <!-- --> | <!-- Accepted / Rejected --> | <!-- --> | <!-- YYYY-MM-DD --> |
| Business Analyst | <!-- --> | <!-- Accepted / Rejected --> | <!-- --> | <!-- YYYY-MM-DD --> |
| Tech Lead | <!-- --> | <!-- Acknowledged --> | <!-- --> | <!-- YYYY-MM-DD --> |
| QA Lead | <!-- --> | <!-- Acknowledged --> | <!-- --> | <!-- YYYY-MM-DD --> |

---

**By signing this document, the undersigned confirm that the software has been tested against the defined acceptance criteria and the decision above reflects the assessment of the testing team and business stakeholders.**

---

## Completion Checklist

- [ ] UAT Information filled in with release and environment details
- [ ] All features listed with acceptance criteria results
- [ ] Each feature's acceptance criteria individually verified
- [ ] UAT test results tallied
- [ ] Issues found during UAT documented with resolution status
- [ ] Known limitations listed with workarounds
- [ ] Business readiness items assessed
- [ ] Sign-off decision selected (Accepted / Conditional / Rejected)
- [ ] Conditions listed if conditionally accepted
- [ ] All required approvals obtained with signatures and dates

---

## Cross-References

| Type | Document | Link |
|------|----------|------|
| Runbook | Execute Test Cycle | [../runbooks/execute-test-cycle.md](../runbooks/execute-test-cycle.md) |
| Template | Test Plan Template | [test-plan-template.md](test-plan-template.md) |
| Template | Test Summary Report Template | [test-summary-report-template.md](test-summary-report-template.md) |
| Template | Test Case Template | [test-case-template.md](test-case-template.md) |
| Template | Defect Report Template | [defect-report-template.md](defect-report-template.md) |
