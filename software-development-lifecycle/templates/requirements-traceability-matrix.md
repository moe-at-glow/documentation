# Requirements Traceability Matrix (RTM)

**Template -- Copy and fill in for each project.**

---

## Document Control

| Field | Value |
|-------|-------|
| Project | [Project Name] |
| Author | [Name] |
| Date | YYYY-MM-DD |
| Version | 1.0 |

---

## Traceability Matrix

| Req ID | Req Description | Source (BR) | Stakeholder (STK) | System (SYS) | Design Reference | Code Reference | Test Case ID | Test Result | Status |
|--------|----------------|-------------|-------------------|-------------|-----------------|---------------|-------------|-------------|--------|
| SWR-001 | [Brief description] | BR-XXX | STK-XXX | SYS-XXX | [Design doc section] | [Module/file] | TC-XXX | Pass/Fail/-- | Approved |
| SWR-002 | | | | | | | | | |
| SWR-003 | | | | | | | | | |

---

## How to Maintain This Matrix

### When to Update

| Event | Action |
|-------|--------|
| New requirement added | Add a new row. Fill in Req ID, Description, Source, and Status. |
| Requirement modified | Update the affected row. Verify all links remain valid. |
| Requirement retired | Set Status to "Retired". Do not delete the row. |
| Design completed | Fill in Design Reference column for affected requirements. |
| Code implemented | Fill in Code Reference column for affected requirements. |
| Test case written | Fill in Test Case ID column for affected requirements. |
| Test executed | Fill in Test Result column (Pass/Fail). |
| Change request approved | Update affected rows. Add new rows for new requirements. |

### Naming Conventions

| Column | Format | Example |
|--------|--------|---------|
| Req ID | SWR-XXX | SWR-042 |
| Source (BR) | BR-XXX | BR-012 |
| Stakeholder | STK-XXX | STK-087 |
| System | SYS-XXX | SYS-134 |
| Test Case ID | TC-XXX | TC-201 |

### Review Checkpoints

| Checkpoint | Reviewer | What to Check |
|-----------|----------|--------------|
| After requirements baseline | Business Analyst | All SWRs have Source (BR) links |
| After design review | Tech Lead | All SWRs have Design Reference |
| After code complete | Tech Lead | All SWRs have Code Reference |
| After test execution | QA Lead | All SWRs have Test Case ID and Test Result |
| Before release | Product Owner | All Must Have SWRs show Test Result = Pass |

---

## Coverage Metrics

| Metric | Formula | Current Value | Target |
|--------|---------|---------------|--------|
| Requirements with test cases | (SWRs with TC-XXX) / (Total SWRs) x 100 | __% | 100% (Must Have), 90% (Should Have) |
| Requirements tested | (SWRs with Test Result) / (Total SWRs) x 100 | __% | 100% before release |
| Requirements passing | (SWRs with Pass) / (SWRs with Test Result) x 100 | __% | 100% for Must Have |
| Orphan test cases | Test cases with no linked SWR | __ | 0 |
| Untraceable requirements | SWRs with no Source (BR) | __ | 0 |

---

## Summary

| Status | Count |
|--------|-------|
| Total Requirements | __ |
| Approved | __ |
| Implemented | __ |
| Verified (Tested) | __ |
| Passing | __ |
| Deferred | __ |
| Retired | __ |
