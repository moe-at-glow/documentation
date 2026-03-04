> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Requirements Traceability Matrix (RTM)

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P2-RTM |
| **When to Use** | Track every requirement from origin through design, code, and test |
| **Owner** | Business Analyst |
| **Reviewer** | QA Lead |
| **SLA** | Maintained continuously; reviewed at each phase gate |
| **Runbook** | [Derive Software Requirements](../../phase-2-requirements-engineering/runbooks/derive-software-requirements.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Coverage Metrics section is optional. Traceability Matrix columns may omit SYS and STK if not applicable.
> **IF** medium project (3-5 devs) **THEN** All sections required; Coverage Metrics updated at milestones only.
> **IF** large project (6+ devs) **THEN** Full template required. Coverage Metrics updated every sprint.

**Power Atlas classification: Medium project (3 devs) -- All sections required; Coverage Metrics updated at milestones.**

---

## [x] Document Control

| Field | Value |
|-------|-------|
| Project | Power Atlas |
| Author | Hasan Hazime |
| Date | 2026-02-28 |
| Version | 1.1 |

---

## [x] Traceability Matrix

### Business Requirements to Software Requirements

| BR ID | BR Title | SWR IDs | Coverage |
|-------|----------|---------|----------|
| BR-001 | Online Power Calculation | SWR-001, SWR-002, SWR-003, SWR-004, SWR-005, SWR-006, SWR-012, SWR-013, SWR-014 | Full |
| BR-002 | Standardized Calculation Methodology | SWR-001, SWR-002, SWR-003, SWR-004, SWR-005 | Full |
| BR-003 | Project Management | SWR-007, SWR-008, SWR-010, SWR-011, SWR-012 | Full |
| BR-004 | Client Self-Service Requirements | SWR-015, SWR-016 | Full |
| BR-005 | Professional PDF Reports | SWR-026, SWR-027, SWR-031 | Full |
| BR-006 | Equipment Layout Visualization | SWR-028, SWR-029, SWR-030, SWR-031 | Full |
| BR-007 | Generator Database | SWR-019, SWR-020, SWR-021 | Full |
| BR-008 | Role-Based Access Control | SWR-022, SWR-023, SWR-024, SWR-025 | Full |
| BR-009 | Bilingual Support | SWR-NFR-U002, SWR-NFR-U003 | Full |
| BR-010 | Data Export | SWR-013, SWR-031, SWR-032 | Full |
| BR-011 | Project Sharing | SWR-009 | Full |
| BR-012 | Requirements Review Workflow | SWR-016, SWR-017, SWR-018 | Full |
| BR-013 | Generator Availability Calculation | SWR-021 | Full |
| BR-014 | Audit Trail | SWR-033, SWR-034 | Full |
| BR-015 | Mobile-Responsive Design | SWR-UI-001 | Full |

### Full Traceability Matrix (SWR-level detail)

| Req ID | Req Description | Source (BR) | Stakeholder (STK) | Design Reference | Code Reference | Test Case ID | Test Result | Status |
|--------|----------------|-------------|-------------------|-----------------|---------------|-------------|-------------|--------|
| SWR-001 | Single-phase kW calculation: kW = (Amps x 230V x PF) / 1000 | BR-001, BR-002 | STK-003 | DD-CALC-001 | calc/engine.py | TC-001, TC-002 | -- | Approved |
| SWR-002 | Three-phase kW calculation: kW = (Amps x 400V x sqrt(3) x PF) / 1000 | BR-001, BR-002 | STK-003 | DD-CALC-001 | calc/engine.py | TC-003, TC-004 | -- | Approved |
| SWR-003 | kVA calculation: kVA = kW / PF | BR-001, BR-002 | STK-003 | DD-CALC-001 | calc/engine.py | TC-005 | -- | Approved |
| SWR-004 | Demand factor application to individual loads | BR-001, BR-002 | STK-003, STK-004 | DD-CALC-002 | calc/engine.py | TC-006 | -- | Approved |
| SWR-005 | Diversity factor application to project total | BR-001, BR-002 | STK-003, STK-004 | DD-CALC-002 | calc/engine.py | TC-007 | -- | Approved |
| SWR-006 | Reverse calculation (kW to Amps, kVA to kW) | BR-001 | STK-003 | DD-CALC-003 | calc/engine.py | TC-008, TC-009 | -- | Approved |
| SWR-007 | Project CRUD with all required properties | BR-003 | STK-002, STK-004 | DD-PROJ-001 | projects/routes.py | TC-010, TC-011, TC-012, TC-013 | -- | Approved |
| SWR-008 | Project folder organization (up to 3 levels) | BR-003 | STK-004 | DD-PROJ-002 | projects/folders.py | TC-014 | -- | Approved |
| SWR-009 | Project sharing with View/Edit permissions | BR-011 | STK-003, STK-004 | DD-PROJ-003 | projects/sharing.py | TC-015, TC-016 | -- | Approved |
| SWR-010 | Project status tracking through defined states | BR-003 | STK-004 | DD-PROJ-004 | projects/routes.py | TC-017 | -- | Approved |
| SWR-011 | Client association with contact details | BR-003 | STK-006 | DD-PROJ-005 | clients/routes.py | TC-018, TC-019 | -- | Approved |
| SWR-012 | Load CRUD with type, quantity, power values, critical flag | BR-001, BR-003 | STK-003 | DD-LOAD-001 | loads/routes.py | TC-020, TC-021, TC-022 | -- | Approved |
| SWR-013 | Load summary table with calculated totals | BR-001, BR-010 | STK-003, STK-004 | DD-LOAD-002 | loads/summary.py | TC-023 | -- | Approved |
| SWR-014 | Critical load flagging and separate subtotal | BR-001 | STK-003 | DD-LOAD-003 | loads/summary.py | TC-024 | -- | Approved |
| SWR-015 | Public requirements submission form | BR-004 | STK-006, STK-007 | DD-REQ-001 | requirements/public.py | TC-025, TC-026 | -- | Approved |
| SWR-016 | Requirements admin review queue with filters | BR-004, BR-012 | STK-004, STK-006 | DD-REQ-002 | requirements/admin.py | TC-027, TC-028 | -- | Approved |
| SWR-017 | Review actions: approve, reject, request edits | BR-012 | STK-004, STK-006 | DD-REQ-003 | requirements/admin.py | TC-029, TC-030, TC-031 | -- | Approved |
| SWR-018 | Client edit response via unique link | BR-012 | STK-006, STK-007 | DD-REQ-004 | requirements/public.py | TC-032 | -- | Approved |
| SWR-019 | Generator catalog with all specification fields | BR-007 | STK-003 | DD-GEN-001 | generators/routes.py | TC-033, TC-034 | -- | Approved |
| SWR-020 | Generator search and filter by multiple criteria | BR-007 | STK-003 | DD-GEN-002 | generators/routes.py | TC-035, TC-036 | -- | Approved |
| SWR-021 | Generator recommendation with 20% safety margin | BR-007, BR-013 | STK-003 | DD-GEN-003 | generators/recommend.py | TC-037, TC-038 | -- | Approved |
| SWR-022 | User registration with password policy | BR-008 | STK-002 | DD-AUTH-001 | auth/routes.py | TC-039, TC-040 | -- | Approved |
| SWR-023 | Session-based authentication with 8-hour expiry | BR-008 | STK-002 | DD-AUTH-002 | auth/routes.py | TC-041, TC-042 | -- | Approved |
| SWR-024 | Account lockout after 5 failed attempts (30 min) | BR-008 | STK-002 | DD-AUTH-003 | auth/routes.py | TC-043 | -- | Approved |
| SWR-025 | Role-based permission enforcement | BR-008 | STK-001, STK-002 | DD-AUTH-004 | auth/decorators.py | TC-044, TC-045, TC-046 | -- | Approved |
| SWR-026 | PDF report content (letterhead, loads, generators) | BR-005 | STK-001, STK-004 | DD-RPT-001 | reports/generator.py | TC-047, TC-048 | -- | Approved |
| SWR-027 | PDF report formatting (A4, page numbers, TOC) | BR-005 | STK-004 | DD-RPT-002 | reports/generator.py | TC-049 | -- | Approved |
| SWR-028 | Layout builder canvas with zoom/pan/grid/undo | BR-006 | STK-003 | DD-LAY-001 | frontend/layout/ | TC-050, TC-051 | -- | Approved |
| SWR-029 | Draggable equipment library with standard symbols | BR-006 | STK-003 | DD-LAY-002 | frontend/layout/ | TC-052, TC-053 | -- | Approved |
| SWR-030 | Wire connections between equipment items | BR-006 | STK-003 | DD-LAY-003 | frontend/layout/ | TC-054 | -- | Approved |
| SWR-031 | Layout export as PNG/SVG and in PDF reports | BR-006, BR-005, BR-010 | STK-003, STK-004 | DD-LAY-004 | frontend/layout/, reports/ | TC-055, TC-056 | -- | Approved |
| SWR-032 | Excel export of load lists (.xlsx) | BR-010 | STK-004, STK-005 | DD-EXP-001 | exports/excel.py | TC-057 | -- | Approved |
| SWR-033 | Audit trail logging for all project modifications | BR-014 | STK-001, STK-002 | DD-AUD-001 | audit/logger.py | TC-058, TC-059 | -- | Approved |
| SWR-034 | Audit trail viewing with date/action filters | BR-014 | STK-001 | DD-AUD-002 | audit/routes.py | TC-060 | -- | Approved |
| SWR-NFR-P001 | Calculation response time < 200ms | BR-001 | STK-003 | DD-PERF-001 | -- | TC-NFR-001 | -- | Approved |
| SWR-NFR-P002 | PDF generation < 5 seconds for 100 loads | BR-005 | STK-004 | DD-PERF-002 | -- | TC-NFR-002 | -- | Approved |
| SWR-NFR-P003 | Dashboard load time < 2 seconds | BR-003 | STK-004 | DD-PERF-003 | -- | TC-NFR-003 | -- | Approved |
| SWR-NFR-P004 | Layout canvas >= 30 FPS with 50 items | BR-006 | STK-003 | DD-PERF-004 | -- | TC-NFR-004 | -- | Approved |
| SWR-NFR-S001 | bcrypt password hashing (cost factor 12) | BR-008 | STK-002 | DD-SEC-001 | auth/utils.py | TC-NFR-005 | -- | Approved |
| SWR-NFR-S002 | HTTPS enforcement in production | BR-008 | STK-002 | DD-SEC-002 | config/production.py | TC-NFR-006 | -- | Approved |
| SWR-NFR-S003 | CSRF protection on all state-changing requests | BR-008 | STK-002 | DD-SEC-003 | auth/middleware.py | TC-NFR-007 | -- | Approved |
| SWR-NFR-S004 | Input sanitization (XSS, SQL injection prevention) | BR-008 | STK-002 | DD-SEC-004 | -- | TC-NFR-008 | -- | Approved |
| SWR-NFR-U001 | WCAG 2.1 Level AA compliance | BR-015 | STK-005 | DD-UI-001 | -- | TC-NFR-009 | -- | Approved |
| SWR-NFR-U002 | Arabic RTL layout support | BR-009 | STK-006, STK-007 | DD-UI-002 | frontend/i18n/ | TC-NFR-010 | -- | Approved |
| SWR-NFR-U003 | Language switching without page reload | BR-009 | STK-006 | DD-UI-003 | frontend/i18n/ | TC-NFR-011 | -- | Approved |
| SWR-NFR-R001 | 99.5% uptime during business hours | BR-003 | STK-001 | DD-OPS-001 | -- | TC-NFR-012 | -- | Approved |
| SWR-NFR-R002 | Automated daily database backups (30-day retention) | BR-014 | STK-002 | DD-OPS-002 | scripts/backup.sh | TC-NFR-013 | -- | Approved |
| SWR-NFR-R003 | SQLite write contention handling with retry | BR-003 | STK-002 | DD-OPS-003 | db/connection.py | TC-NFR-014 | -- | Approved |
| SWR-NFR-SC001 | Support 100 concurrent users | BR-003 | STK-001 | DD-PERF-005 | -- | TC-NFR-015 | -- | Approved |
| SWR-NFR-SC002 | Support 10,000 projects / 500,000 loads | BR-003 | STK-001 | DD-PERF-006 | -- | TC-NFR-016 | -- | Approved |
| SWR-UI-001 | Responsive design (768px to 2560px) | BR-015 | STK-005 | DD-UI-004 | frontend/styles/ | TC-NFR-017 | -- | Approved |

---

## [x] Maintenance Guide

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

### [x] Naming Conventions

| Column | Format | Example |
|--------|--------|---------|
| Req ID | SWR-XXX or SWR-NFR-XYYY | SWR-007, SWR-NFR-P001 |
| Source (BR) | BR-XXX | BR-012 |
| Stakeholder | STK-XXX | STK-003 |
| Design Reference | DD-MOD-XXX | DD-CALC-001 |
| Test Case ID | TC-XXX or TC-NFR-XXX | TC-037, TC-NFR-001 |

### [x] Review Checkpoints

| Checkpoint | Reviewer | What to Check |
|-----------|----------|--------------|
| After requirements baseline | Hasan Hazime | All SWRs have Source (BR) links |
| After design review | Omar Farouk | All SWRs have Design Reference |
| After code complete | Omar Farouk | All SWRs have Code Reference |
| After test execution | Layla Ibrahim | All SWRs have Test Case ID and Test Result |
| Before release | Hasan Hazime | All Must Have SWRs show Test Result = Pass |

---

## [x] Coverage Metrics

| Metric | Formula | Current Value | Target |
|--------|---------|---------------|--------|
| Requirements with test cases | (SWRs with TC-XXX) / (Total SWRs) x 100 | 100% | 100% (Must Have), 90% (Should Have) |
| Requirements tested | (SWRs with Test Result) / (Total SWRs) x 100 | 0% | 100% before release |
| Requirements passing | (SWRs with Pass) / (SWRs with Test Result) x 100 | N/A | 100% for Must Have |
| Orphan test cases | Test cases with no linked SWR | 0 | 0 |
| Untraceable requirements | SWRs with no Source (BR) | 0 | 0 |

---

## [x] Summary

| Status | Count |
|--------|-------|
| Total Requirements | 49 |
| Approved | 49 |
| Implemented | 0 |
| Verified (Tested) | 0 |
| Passing | 0 |
| Deferred | 0 |
| Retired | 0 |

---

## COMPLETION CHECKLIST

- [x] All required sections filled
- [x] Every SWR traces to at least one BR
- [x] Reviewed by QA Lead
- [x] Approved by Tech Lead
- [x] Stored in project SharePoint / repository
- [x] Coverage Metrics up to date

---

## CROSS-REFERENCES

| Artifact | Link |
|----------|------|
| Producing Runbook | [Derive Software Requirements](../../phase-2-requirements-engineering/runbooks/derive-software-requirements.md) |
| Business Requirements Document | [BRD](business-requirements-document.md) |
| Software Requirements Specification | [SRS](software-requirements-specification.md) |
| Change Request Form | [Change Request Form](../../phase-2-requirements-engineering/templates/change-request-form.md) |
