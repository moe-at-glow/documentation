# Test Plan Template

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P6-001 |
| **When to Use** | Creating sprint or release test plans |
| **Owner** | QA Lead |
| **Reviewer** | Tech Lead / Product Owner |
| **SLA** | 2 business days |
| **Runbook** | [Execute Test Cycle](../runbooks/execute-test-cycle.md) |
| **Last Verified** | 2026-03-04 |

---

## Scaling Decision Gate

| Factor | Small (< 20 TCs) | Medium (20-50 TCs) | Large (> 50 TCs) |
|--------|-------------------|---------------------|-------------------|
| Scope section depth | Summary list | Grouped by module | Full RTM required |
| Risk analysis | Top 3 risks | Full risk table | Risk workshop + table |
| Schedule detail | Milestone dates only | Activity-level dates | Daily task breakdown |
| Approvals required | QA Lead | QA Lead + Tech Lead | QA Lead + Tech Lead + PO |

---

## [ ] Test Plan Information

| Field | Value |
|-------|-------|
| Test Plan ID | TP-NNN |
| Project | GlowPowerRental |
| Sprint / Release | <!-- Sprint N / Release X.Y.Z --> |
| Author | <!-- Name --> |
| Date Created | <!-- YYYY-MM-DD --> |
| Approved By | <!-- QA Lead name --> |
| Status | <!-- Draft / Approved / In Progress / Completed --> |

---

## [ ] 1. Scope

### [ ] In Scope

| Ticket | Feature | Test Level |
|--------|---------|-----------|
| TICKET-NNN | <!-- feature description --> | <!-- Unit / Integration / System --> |

### [ ] Out of Scope

| Item | Reason |
|------|--------|
| <!-- --> | <!-- --> |

---

## [ ] 2. Test Approach

### [ ] Test Levels

| Level | Scope | Responsible |
|-------|-------|-------------|
| Unit | <!-- what will be unit tested --> | Developer |
| Integration | <!-- what will be integration tested --> | Developer / QA |
| System | <!-- what will be system tested --> | QA Engineer |
| UAT | <!-- what will be user acceptance tested --> | Product Owner |

### [ ] Test Types

- [ ] Functional testing
- [ ] Regression testing
- [ ] Performance testing
- [ ] Security testing
- [ ] Smoke testing
- [ ] Exploratory testing

---

## [ ] 3. Test Environment

| Component | Version / Configuration |
|-----------|------------------------|
| Application | <!-- branch or version --> |
| Node.js | <!-- version --> |
| PostgreSQL | <!-- version --> |
| Environment | <!-- local / test / staging --> |
| Test Data Set | <!-- minimal / standard / performance --> |

### [ ] Environment Setup Steps

1. <!-- Step 1 -->
2. <!-- Step 2 -->
3. <!-- Step 3 -->

---

## [ ] 4. Test Cases

### [ ] Critical Priority

| ID | Title | Requirement | Type | Status |
|----|-------|------------|------|--------|
| TC-001 | <!-- title --> | SWR-NNN | <!-- Functional / Regression --> | <!-- Not Run / Pass / Fail / Blocked --> |

### [ ] High Priority

| ID | Title | Requirement | Type | Status |
|----|-------|------------|------|--------|
| TC-NNN | <!-- title --> | SWR-NNN | <!-- type --> | <!-- status --> |

### [ ] Medium Priority

| ID | Title | Requirement | Type | Status |
|----|-------|------------|------|--------|
| TC-NNN | <!-- title --> | SWR-NNN | <!-- type --> | <!-- status --> |

### [ ] Low Priority

| ID | Title | Requirement | Type | Status |
|----|-------|------------|------|--------|
| TC-NNN | <!-- title --> | SWR-NNN | <!-- type --> | <!-- status --> |

---

## [ ] 5. Entry Criteria

- [ ] Code merged to develop / release branch
- [ ] CI pipeline passes (unit + integration tests)
- [ ] Test environment deployed and verified
- [ ] Test data loaded
- [ ] Test plan approved by QA Lead

---

## [ ] 6. Exit Criteria

- [ ] All critical and high priority test cases executed
- [ ] All critical and high severity defects resolved
- [ ] Regression tests pass
- [ ] Coverage meets thresholds
- [ ] Test summary report written

---

## [ ] 7. Risks and Mitigations

| Risk | Impact | Likelihood | Mitigation |
|------|--------|-----------|-----------|
| <!-- risk --> | <!-- High/Medium/Low --> | <!-- High/Medium/Low --> | <!-- mitigation --> |

---

## [ ] 8. Schedule

| Activity | Start Date | End Date | Responsible |
|----------|-----------|---------|-------------|
| Test plan review | <!-- --> | <!-- --> | QA Lead |
| Test environment setup | <!-- --> | <!-- --> | DevOps |
| Test execution | <!-- --> | <!-- --> | QA Engineer |
| Defect fixing | <!-- --> | <!-- --> | Developer |
| Re-testing | <!-- --> | <!-- --> | QA Engineer |
| Test summary report | <!-- --> | <!-- --> | QA Engineer |
| Sign-off | <!-- --> | <!-- --> | QA Lead / PO |

---

## [ ] 9. Approvals

| Role | Name | Date | Signature |
|------|------|------|-----------|
| QA Lead | <!-- --> | <!-- --> | <!-- --> |
| Tech Lead | <!-- --> | <!-- --> | <!-- --> |

---

## Completion Checklist

- [ ] Test Plan Information filled in completely
- [ ] Scope defined (in-scope and out-of-scope)
- [ ] Test approach and test types selected
- [ ] Test environment documented
- [ ] Test cases listed with priorities assigned
- [ ] Entry criteria defined and verifiable
- [ ] Exit criteria defined and measurable
- [ ] Risks identified with mitigations
- [ ] Schedule populated with dates and owners
- [ ] Approvals obtained from all required roles

---

## Cross-References

| Type | Document | Link |
|------|----------|------|
| Runbook | Execute Test Cycle | [../runbooks/execute-test-cycle.md](../runbooks/execute-test-cycle.md) |
| Template | Test Case Template | [test-case-template.md](test-case-template.md) |
| Template | Defect Report Template | [defect-report-template.md](defect-report-template.md) |
| Template | Test Summary Report Template | [test-summary-report-template.md](test-summary-report-template.md) |
| Template | UAT Sign-Off Template | [uat-sign-off-template.md](uat-sign-off-template.md) |
