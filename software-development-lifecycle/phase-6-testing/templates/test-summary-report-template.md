# Test Summary Report Template

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P6-004 |
| **When to Use** | Summarizing results at the end of a test cycle |
| **Owner** | QA Lead |
| **Reviewer** | Tech Lead / Product Owner |
| **SLA** | 1 business day after test cycle completion |
| **Runbook** | [Execute Test Cycle](../runbooks/execute-test-cycle.md) |
| **Last Verified** | 2026-03-04 |

---

## Scaling Decision Gate

| Factor | Sprint Test | Release Regression | Full Release + UAT |
|--------|-------------|--------------------|--------------------|
| Executive summary depth | 2-3 sentences | Paragraph + recommendation | Full summary + risk assessment |
| Coverage reporting | Overall percentages | Per-module breakdown | Per-module + requirements traceability |
| Performance section | Skip if not tested | Summary metrics only | Full metrics with trend comparison |
| Security section | Skip if not tested | Audit results only | Full OWASP review + pen test results |
| Approvals required | QA Lead | QA Lead + Tech Lead | QA Lead + Tech Lead + PO |

---

## [ ] Report Information

| Field | Value |
|-------|-------|
| Report ID | TSR-NNN |
| Project | GlowPowerRental |
| Sprint / Release | <!-- Sprint N / Release X.Y.Z --> |
| Test Cycle | <!-- Sprint test / Release regression / UAT --> |
| Author | <!-- QA Engineer name --> |
| Date | <!-- YYYY-MM-DD --> |
| Status | <!-- Draft / Final --> |

---

## [ ] 1. Executive Summary

<!-- 2-3 sentences summarizing the overall test results and recommendation -->

**Recommendation:** <!-- Go / No-Go / Conditional Go -->

---

## [ ] 2. Test Execution Summary

### [ ] Overall Results

| Metric | Count | Percentage |
|--------|-------|-----------|
| Total test cases planned | <!-- N --> | 100% |
| Executed | <!-- N --> | <!-- X% --> |
| Passed | <!-- N --> | <!-- X% --> |
| Failed | <!-- N --> | <!-- X% --> |
| Blocked | <!-- N --> | <!-- X% --> |
| Not executed | <!-- N --> | <!-- X% --> |

### [ ] Results by Priority

| Priority | Total | Passed | Failed | Blocked |
|----------|-------|--------|--------|---------|
| Critical | <!-- N --> | <!-- N --> | <!-- N --> | <!-- N --> |
| High | <!-- N --> | <!-- N --> | <!-- N --> | <!-- N --> |
| Medium | <!-- N --> | <!-- N --> | <!-- N --> | <!-- N --> |
| Low | <!-- N --> | <!-- N --> | <!-- N --> | <!-- N --> |

### [ ] Results by Test Type

| Type | Total | Passed | Failed |
|------|-------|--------|--------|
| Functional | <!-- N --> | <!-- N --> | <!-- N --> |
| Regression | <!-- N --> | <!-- N --> | <!-- N --> |
| Performance | <!-- N --> | <!-- N --> | <!-- N --> |
| Security | <!-- N --> | <!-- N --> | <!-- N --> |

---

## [ ] 3. Defect Summary

### [ ] Defects Found This Cycle

| Severity | Found | Fixed | Open | Deferred |
|----------|-------|-------|------|----------|
| Critical | <!-- N --> | <!-- N --> | <!-- N --> | <!-- N --> |
| High | <!-- N --> | <!-- N --> | <!-- N --> | <!-- N --> |
| Medium | <!-- N --> | <!-- N --> | <!-- N --> | <!-- N --> |
| Low | <!-- N --> | <!-- N --> | <!-- N --> | <!-- N --> |
| **Total** | **<!-- N -->** | **<!-- N -->** | **<!-- N -->** | **<!-- N -->** |

### [ ] Open Defects

| Defect ID | Title | Severity | Status | Notes |
|-----------|-------|----------|--------|-------|
| DEF-NNN | <!-- title --> | <!-- severity --> | <!-- status --> | <!-- impact or plan --> |

### [ ] Deferred Defects

| Defect ID | Title | Severity | Rationale for Deferral |
|-----------|-------|----------|----------------------|
| DEF-NNN | <!-- title --> | <!-- severity --> | <!-- why it can be deferred --> |

---

## [ ] 4. Coverage Summary

### [ ] Unit Test Coverage

| Module | Statements | Branches | Functions | Lines | Target Met? |
|--------|-----------|----------|-----------|-------|------------|
| Billing | <!-- X% --> | <!-- X% --> | <!-- X% --> | <!-- X% --> | <!-- Yes/No --> |
| Rentals | <!-- X% --> | <!-- X% --> | <!-- X% --> | <!-- X% --> | <!-- Yes/No --> |
| Equipment | <!-- X% --> | <!-- X% --> | <!-- X% --> | <!-- X% --> | <!-- Yes/No --> |
| Overall | <!-- X% --> | <!-- X% --> | <!-- X% --> | <!-- X% --> | <!-- Yes/No --> |

### [ ] Requirements Coverage

| Category | Total Requirements | Covered by Tests | Coverage |
|----------|-------------------|-----------------|----------|
| Critical | <!-- N --> | <!-- N --> | <!-- X% --> |
| High | <!-- N --> | <!-- N --> | <!-- X% --> |
| Medium | <!-- N --> | <!-- N --> | <!-- X% --> |
| Overall | <!-- N --> | <!-- N --> | <!-- X% --> |

---

## [ ] 5. Performance Results (if applicable)

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| Response time (p95) | <!-- target --> | <!-- actual --> | <!-- Pass/Fail --> |
| Throughput (req/s) | <!-- target --> | <!-- actual --> | <!-- Pass/Fail --> |
| Error rate | <!-- target --> | <!-- actual --> | <!-- Pass/Fail --> |
| CPU utilization | <!-- target --> | <!-- actual --> | <!-- Pass/Fail --> |
| Memory utilization | <!-- target --> | <!-- actual --> | <!-- Pass/Fail --> |

---

## [ ] 6. Security Results (if applicable)

| Check | Result | Notes |
|-------|--------|-------|
| npm audit (critical/high) | <!-- Pass/Fail --> | <!-- details --> |
| OWASP Top 10 review | <!-- Pass/Fail --> | <!-- details --> |
| Authentication tests | <!-- Pass/Fail --> | <!-- details --> |
| Authorization tests | <!-- Pass/Fail --> | <!-- details --> |
| Security headers | <!-- Pass/Fail --> | <!-- details --> |

---

## [ ] 7. Risks and Issues

| Risk / Issue | Impact | Mitigation |
|-------------|--------|-----------|
| <!-- risk --> | <!-- impact --> | <!-- mitigation --> |

---

## [ ] 8. Recommendation

| Criteria | Status |
|----------|--------|
| All critical test cases passed | <!-- Yes / No --> |
| All high test cases passed | <!-- Yes / No --> |
| No critical defects open | <!-- Yes / No --> |
| No high defects open | <!-- Yes / No --> |
| Coverage targets met | <!-- Yes / No --> |
| Performance targets met | <!-- Yes / No / N/A --> |
| Security clean | <!-- Yes / No / N/A --> |

**Final Recommendation:** <!-- Go / No-Go / Conditional Go (with conditions) -->

---

## [ ] 9. Approvals

| Role | Name | Date | Decision |
|------|------|------|----------|
| QA Lead | <!-- --> | <!-- --> | <!-- Approve / Reject --> |
| Tech Lead | <!-- --> | <!-- --> | <!-- Approve / Reject --> |
| Product Owner | <!-- --> | <!-- --> | <!-- Approve / Reject --> |

---

## Completion Checklist

- [ ] Report Information filled in with correct cycle details
- [ ] Executive summary written with clear recommendation
- [ ] Test execution results tallied (overall, by priority, by type)
- [ ] Defect summary completed (found, fixed, open, deferred)
- [ ] Open and deferred defects listed with rationale
- [ ] Unit test coverage reported per module
- [ ] Requirements coverage reported per category
- [ ] Performance results documented (or marked N/A)
- [ ] Security results documented (or marked N/A)
- [ ] Risks and issues identified
- [ ] Go/No-Go recommendation stated with criteria assessment
- [ ] Approvals obtained from all required roles

---

## Cross-References

| Type | Document | Link |
|------|----------|------|
| Runbook | Execute Test Cycle | [../runbooks/execute-test-cycle.md](../runbooks/execute-test-cycle.md) |
| Template | Test Plan Template | [test-plan-template.md](test-plan-template.md) |
| Template | Defect Report Template | [defect-report-template.md](defect-report-template.md) |
| Template | UAT Sign-Off Template | [uat-sign-off-template.md](uat-sign-off-template.md) |
| Template | Test Case Template | [test-case-template.md](test-case-template.md) |
