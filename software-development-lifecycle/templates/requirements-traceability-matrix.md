# Requirements Traceability Matrix (RTM)

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P2-RTM |
| **When to Use** | Track every requirement from origin through design, code, and test |
| **Owner** | Business Analyst |
| **Reviewer** | QA Lead |
| **SLA** | Maintained continuously; reviewed at each phase gate |
| **Runbook** | [Derive Software Requirements](../runbooks/derive-software-requirements.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Coverage Metrics section is optional. Traceability Matrix columns may omit SYS and STK if not applicable.
> **IF** medium project (3-5 devs) **THEN** All sections required; Coverage Metrics updated at milestones only.
> **IF** large project (6+ devs) **THEN** Full template required. Coverage Metrics updated every sprint.

---

## [ ] Document Control

| Field | Value |
|-------|-------|
| Project | [Project Name] |
| Author | [Name] |
| Date | YYYY-MM-DD |
| Version | 1.0 |

---

## [ ] Traceability Matrix

| Req ID | Req Description | Source (BR) | Stakeholder (STK) | System (SYS) | Design Reference | Code Reference | Test Case ID | Test Result | Status |
|--------|----------------|-------------|-------------------|-------------|-----------------|---------------|-------------|-------------|--------|
| SWR-001 | [Brief description] | BR-XXX | STK-XXX | SYS-XXX | [Design doc section] | [Module/file] | TC-XXX | Pass/Fail/-- | Approved |
| SWR-002 | | | | | | | | | |
| SWR-003 | | | | | | | | | |

---

## [ ] Maintenance Guide

<!-- When to update each column -->

| Event | Action |
|-------|--------|
| New requirement added | Add row; fill Req ID, Description, Source, Status |
| Requirement modified | Update row; verify all links remain valid |
| Requirement retired | Set Status to "Retired"; do not delete the row |
| Design completed | Fill Design Reference column |
| Code implemented | Fill Code Reference column |
| Test case written | Fill Test Case ID column |
| Test executed | Fill Test Result column (Pass/Fail) |
| Change request approved | Update affected rows; add new rows as needed |

### [ ] Naming Conventions

| Column | Format | Example |
|--------|--------|---------|
| Req ID | SWR-XXX | SWR-042 |
| Source (BR) | BR-XXX | BR-012 |
| Stakeholder | STK-XXX | STK-087 |
| System | SYS-XXX | SYS-134 |
| Test Case ID | TC-XXX | TC-201 |

### [ ] Review Checkpoints

| Checkpoint | Reviewer | What to Check |
|-----------|----------|--------------|
| After requirements baseline | Business Analyst | All SWRs have Source (BR) links |
| After design review | Tech Lead | All SWRs have Design Reference |
| After code complete | Tech Lead | All SWRs have Code Reference |
| After test execution | QA Lead | All SWRs have Test Case ID and Test Result |
| Before release | Product Owner | All Must Have SWRs show Test Result = Pass |

---

## [ ] Coverage Metrics

| Metric | Formula | Current Value | Target |
|--------|---------|---------------|--------|
| Requirements with test cases | (SWRs with TC-XXX) / (Total SWRs) x 100 | __% | 100% (Must Have), 90% (Should Have) |
| Requirements tested | (SWRs with Test Result) / (Total SWRs) x 100 | __% | 100% before release |
| Requirements passing | (SWRs with Pass) / (SWRs with Test Result) x 100 | __% | 100% for Must Have |
| Orphan test cases | Test cases with no linked SWR | __ | 0 |
| Untraceable requirements | SWRs with no Source (BR) | __ | 0 |

---

## [ ] Summary

| Status | Count |
|--------|-------|
| Total Requirements | __ |
| Approved | __ |
| Implemented | __ |
| Verified (Tested) | __ |
| Passing | __ |
| Deferred | __ |
| Retired | __ |

---

## COMPLETION CHECKLIST

- [ ] All required sections filled
- [ ] Every SWR traces to at least one BR
- [ ] Reviewed by QA Lead
- [ ] Approved by Tech Lead
- [ ] Stored in project SharePoint / repository
- [ ] Coverage Metrics up to date

---

## CROSS-REFERENCES

| Artifact | Link |
|----------|------|
| Producing Runbook | [Derive Software Requirements](../runbooks/derive-software-requirements.md) |
| Business Requirements Document | [BRD Template](business-requirements-document.md) |
| Software Requirements Specification | [SRS Template](software-requirements-specification.md) |
| Change Request Form | [Change Request Form](change-request-form.md) |
