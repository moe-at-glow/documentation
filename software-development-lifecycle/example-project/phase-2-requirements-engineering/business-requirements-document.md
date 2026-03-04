> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Business Requirements Document (BRD)

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P2-BRD |
| **When to Use** | Capture and formalize business needs before deriving software requirements |
| **Owner** | Business Analyst |
| **Reviewer** | Product Owner |
| **SLA** | 5 business days from stakeholder interviews complete |
| **Runbook** | [Extract Business Requirements](../../runbooks/extract-business-requirements.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Sections 6 (Business Rules), 8 (Dependencies), and 9 (Glossary) are optional. Stakeholder Summary may be inline (skip separate Stakeholder Analysis).
> **IF** medium project (3-5 devs) **THEN** All sections required; Glossary optional if domain is well-understood.
> **IF** large project (6+ devs) **THEN** Full template required.

**Power Atlas classification: Medium project (3 devs) -- All sections required; Glossary optional.**

---

## [x] Document Control

| Field | Value |
|-------|-------|
| Document Title | Power Atlas -- Business Requirements Document |
| Version | 1.2 |
| Status | Approved |
| Author | Hasan Hazime |
| Date Created | 2026-01-12 |
| Last Updated | 2026-02-20 |

### [x] Revision History

| Version | Date | Author | Description |
|---------|------|--------|-------------|
| 0.1 | 2026-01-12 | Hasan Hazime | Initial draft from stakeholder interviews |
| 0.2 | 2026-01-19 | Hasan Hazime | Added equipment layout and generator database requirements |
| 1.0 | 2026-01-28 | Hasan Hazime | Incorporated feedback from engineering team review |
| 1.1 | 2026-02-10 | Hasan Hazime | Added bilingual support and audit trail requirements |
| 1.2 | 2026-02-20 | Hasan Hazime | Final revisions; approved by sponsor |

### [x] Approvers

| Name | Role | Signature | Date |
|------|------|-----------|------|
| Khalid Al-Rashid | Project Sponsor (VP, Engineering Services) | Approved | 2026-02-18 |
| Hasan Hazime | Product Owner | Approved | 2026-02-19 |
| Omar Farouk | Tech Lead | Approved | 2026-02-20 |

---

## [x] 1. Executive Summary

GlowPowerRental provides temporary power solutions for events, construction sites, and industrial clients across the Middle East. Currently, power calculations are performed using inconsistent Excel spreadsheets maintained individually by engineers, leading to calculation errors, non-standard reports, and difficulty sharing project data between team members.

Power Atlas is a web-based power calculation and project management tool that replaces the Excel-based workflow with a centralized, standardized platform. Engineers will use it to perform kW/kVA/Amps calculations with configurable power factor, demand factor, and diversity factor parameters. The tool will include project management capabilities, a client requirements portal, professional PDF report generation, an equipment layout builder, and a searchable generator database.

The expected outcomes are a 60% reduction in calculation errors, a 40% reduction in report preparation time, and full standardization of the calculation methodology used across the engineering team. The client-facing requirements portal will reduce the email-based back-and-forth currently needed to gather project specifications by an estimated 50%.

---

## [x] 2. Business Objectives

| ID | Objective | Success Metric | Target |
|----|-----------|---------------|--------|
| OBJ-001 | Eliminate calculation errors from manual Excel processes | Calculation error rate per project | < 2% (down from ~12%) |
| OBJ-002 | Standardize power calculation methodology across all engineers | % of projects using standardized formulas | 100% within 3 months of launch |
| OBJ-003 | Reduce report preparation time | Average time from calculation to final PDF | < 15 minutes (down from ~45 minutes) |
| OBJ-004 | Enable client self-service for requirements gathering | % of requirements submitted via portal vs. email | > 70% within 6 months |
| OBJ-005 | Improve project data sharing and collaboration | Number of projects shared between engineers per month | Increase by 200% |

---

## [x] 3. Project Scope

### [x] In Scope

| Item | Description |
|------|-------------|
| Power Calculator | Single-phase and three-phase calculations with PF, demand factor, and diversity factor |
| Project Management | CRUD operations, folders, sharing, status tracking, client association |
| Client Requirements Portal | Public submission form, admin review pipeline, edit request workflow |
| PDF Report Generation | Professional reports with company letterhead, load lists, and generator selections |
| Equipment Layout Builder | Canvas-based drag-and-drop tool for generators, cables, panels, and distribution boards |
| Generator Database | Searchable catalog with filtering by kW, kVA, voltage, fuel type, and manufacturer |
| User Authentication | Registration, login, role-based access (Admin, Engineer, Client) |
| Bilingual Support | Arabic (RTL) and English (LTR) interface |
| Data Export | Export to Excel and PDF formats |

### [x] Out of Scope

| Item | Reason |
|------|--------|
| Inventory management integration | Separate system exists; integration planned for Phase 2 |
| Financial quoting and invoicing | Handled by existing ERP system |
| Real-time GPS tracking of generators | Separate IoT initiative |
| Native mobile applications | Web responsive design covers field use; native apps deferred |
| Multi-tenant SaaS deployment | Single-organization deployment for GlowPowerRental only |

---

## [x] 4. Stakeholder Summary

| ID | Name | Role | Interest Level | Influence Level | Key Concerns |
|----|------|------|---------------|-----------------|-------------|
| STK-001 | Khalid Al-Rashid | VP, Engineering Services (Sponsor) | High | High | ROI, adoption rate, calculation accuracy |
| STK-002 | Hasan Hazime | Product Owner / Lead Developer | High | High | Technical feasibility, maintainability, timeline |
| STK-003 | Omar Farouk | Senior Power Engineer | High | Medium | Calculation accuracy, formula correctness, usability |
| STK-004 | Layla Ibrahim | Engineering Team Lead | High | Medium | Standardization, training effort, reporting quality |
| STK-005 | Ahmed Nasser | Field Engineer | Medium | Low | Mobile responsiveness, offline capability, ease of use |
| STK-006 | Sara Al-Mutairi | Client Relations Manager | Medium | Medium | Client portal usability, bilingual support |
| STK-007 | External Clients | End users of client portal | Medium | Low | Simple requirements submission, status visibility |

Full stakeholder analysis: [Stakeholder Analysis](../phase-1-business-analysis/stakeholder-analysis.md)

---

## [x] 5. Business Requirements

| ID | Title | Description | Priority | Source | Rationale | Acceptance Criteria | Status |
|----|-------|-------------|----------|--------|-----------|-------------------|--------|
| BR-001 | Online Power Calculation | The business shall provide an online power calculation tool that replaces the current Excel-based process for computing kW, kVA, and Amps across single-phase and three-phase configurations | M | STK-001, STK-003 | Excel sheets are inconsistent across engineers, leading to errors and non-standard outputs | Engineers can perform all standard power calculations through the web interface; results match validated reference calculations within 0.1% tolerance | Approved |
| BR-002 | Standardized Calculation Methodology | The business shall enforce a single, approved calculation methodology (including power factor, demand factor, and diversity factor) across all engineers | M | STK-001, STK-004 | Different engineers use different formulas and assumptions, causing inconsistent client deliverables | All calculations use the same formulas; formula parameters are configurable per project but default to company standards | Approved |
| BR-003 | Project Management | The business shall provide project management capabilities with client association, folder organization, and status tracking | M | STK-002, STK-004 | No centralized project tracking exists; engineers maintain personal folders | Engineers can create, read, update, and delete projects; projects can be organized in folders and linked to clients | Approved |
| BR-004 | Client Self-Service Requirements | The business shall allow clients to submit power requirements through a self-service portal without requiring an account | M | STK-006, STK-007 | Requirements are currently gathered via email chains, causing delays and lost information | Clients can access a public form, submit requirements, and receive a confirmation; submissions enter an admin review queue | Approved |
| BR-005 | Professional PDF Reports | The business shall generate professional PDF reports with company letterhead containing project summaries, load lists, and generator selections | M | STK-001, STK-004 | Current reports are manually formatted in Excel/Word, taking significant time and lacking consistency | PDF reports are generated with one click; reports include letterhead, project summary, load breakdown, and generator recommendations | Approved |
| BR-006 | Equipment Layout Visualization | The business shall provide a visual equipment layout builder for creating site power distribution diagrams | S | STK-003, STK-005 | Engineers currently use separate CAD software or hand drawings; an integrated tool saves time | Users can place generators, panels, cables, and distribution boards on a canvas; layouts can be saved and exported | Approved |
| BR-007 | Generator Database | The business shall maintain a searchable generator database to assist engineers in selecting appropriate equipment | M | STK-003, STK-004 | Generator specifications are scattered across manufacturer PDFs and personal notes | Engineers can search and filter generators by capacity, voltage, fuel type, and manufacturer; database is admin-maintainable | Approved |
| BR-008 | Role-Based Access Control | The business shall enforce role-based access with distinct permissions for Admin, Engineer, and Client roles | M | STK-001, STK-002 | Different users need different levels of access to protect sensitive project data | Admins manage users and system settings; Engineers manage projects and calculations; Clients view their own submissions only | Approved |
| BR-009 | Bilingual Support | The business shall support both Arabic (RTL) and English (LTR) interfaces | S | STK-006, STK-007 | Client base includes Arabic-speaking and English-speaking users across the Middle East | Users can switch between Arabic and English; all UI elements, labels, and reports render correctly in both languages | Approved |
| BR-010 | Data Export | The business shall support exporting project data and reports in Excel and PDF formats | M | STK-004, STK-005 | Engineers need to share data with clients and stakeholders who may not have system access | Users can export load lists to Excel and full reports to PDF; exported files contain all relevant project data | Approved |
| BR-011 | Project Sharing | The business shall allow engineers to share projects with other engineers for collaboration and review | S | STK-004, STK-003 | Senior engineers need to review junior engineers' work; coverage during absences requires access sharing | Engineers can share projects with specific colleagues with view or edit permissions | Approved |
| BR-012 | Requirements Review Workflow | The business shall provide a structured review and approval workflow for client-submitted requirements | M | STK-006, STK-004 | Submitted requirements need engineering review before becoming active projects; no structured process exists | Admin/Engineers can review, approve, reject, or request edits on submitted requirements; status is tracked through the pipeline | Approved |
| BR-013 | Generator Availability Calculation | The business shall calculate real-time generator availability and recommend optimal generator configurations based on load requirements | S | STK-003, STK-001 | Engineers manually compare load totals against generator capacities; automating this saves time and reduces over/under-sizing | System recommends generators that meet the calculated load with appropriate safety margins; availability percentage is displayed | Approved |
| BR-014 | Audit Trail | The business shall maintain an audit trail of all project changes for accountability and regulatory compliance | S | STK-001, STK-002 | No record exists of who changed what and when; needed for dispute resolution and quality assurance | All project modifications are logged with user, timestamp, and change description; audit log is viewable by Admins | Approved |
| BR-015 | Mobile-Responsive Design | The business shall ensure the application is fully usable on tablets and mobile devices for field engineers | S | STK-005 | Field engineers need to access calculations and project data on-site using tablets | All core functions (calculations, project viewing, load lists) are accessible and usable on devices with screen widths >= 768px | Approved |

---

## [x] 6. Business Rules

| Rule ID | Description | Source | Affected Requirements |
|---------|-------------|--------|----------------------|
| RULE-001 | All power calculations must use IEC standard voltage references: 230V for single-phase, 400V for three-phase (50Hz regions) | STK-003, IEC 60038 | BR-001, BR-002 |
| RULE-002 | Default power factor shall be 0.8 unless overridden at the project level by an engineer | Company Standard | BR-001, BR-002 |
| RULE-003 | Generator sizing must include a minimum 20% safety margin above calculated load | Company Standard | BR-007, BR-013 |
| RULE-004 | Client-submitted requirements must be reviewed within 2 business days | STK-006 | BR-004, BR-012 |
| RULE-005 | PDF reports must include the GlowPowerRental logo, project reference number, date, and preparing engineer name | STK-001 | BR-005 |
| RULE-006 | User accounts must be locked after 5 consecutive failed login attempts | Security Policy | BR-008 |
| RULE-007 | All project data must be retained for a minimum of 5 years | Regulatory / Company Policy | BR-014 |
| RULE-008 | Demand factor defaults: Lighting 1.0, HVAC 0.8, General Power 0.6, unless overridden | Company Standard | BR-001, BR-002 |

---

## [x] 7. Assumptions and Constraints

### [x] Assumptions

| ID | Assumption | Impact if Wrong |
|----|-----------|-----------------|
| ASM-001 | Engineers have reliable internet access at the office and reasonable connectivity on-site | Offline capability would need to be added, significantly increasing scope |
| ASM-002 | The existing GlowPowerRental generator catalog data can be exported to seed the database | Manual data entry of 200+ generator models would delay launch by 2-3 weeks |
| ASM-003 | Users are familiar with basic web applications and need minimal training | Extensive training program would need to be developed |
| ASM-004 | The application will be deployed on GlowPowerRental's existing Linux server infrastructure | Alternative hosting would require additional procurement and setup |
| ASM-005 | The calculation formulas provided by the senior engineering team are correct and complete | Incorrect formulas would require a calculation audit before launch |

### [x] Constraints

| ID | Constraint | Type | Impact |
|----|-----------|------|--------|
| CON-001 | Budget capped at internal development cost (3 developers, 4 months) | Budget | Limits scope to core features; advanced features deferred to later releases |
| CON-002 | Must use Python/Flask backend to align with team expertise | Technical | Constrains technology choices but leverages existing skills |
| CON-003 | Must deploy on existing on-premises server (no cloud services) | Technical | Limits scalability options; must optimize for available hardware |
| CON-004 | Must support Arabic RTL layout from initial release | Technical | Increases frontend development effort by approximately 25% |
| CON-005 | Must not require client users to install any software or create accounts to submit requirements | Business | Public form approach needed; security considerations for unauthenticated access |

---

## [x] 8. Dependencies

| ID | Dependency | Type | Owner | Status |
|----|-----------|------|-------|--------|
| DEP-001 | Generator catalog data export from existing spreadsheets | Internal | Omar Farouk | Resolved |
| DEP-002 | Company letterhead and branding assets for PDF reports | Internal | Marketing Department | Resolved |
| DEP-003 | Approved calculation formulas and default parameters | Internal | Omar Farouk, Layla Ibrahim | Resolved |
| DEP-004 | Linux server provisioning with Python 3.11+ | Internal | IT Operations | Resolved |
| DEP-005 | Arabic translations for UI labels and report templates | Internal | Sara Al-Mutairi | Open |

---

## [x] 9. Glossary

| Term | Definition |
|------|-----------|
| kW | Kilowatt -- unit of real (active) power |
| kVA | Kilovolt-Ampere -- unit of apparent power |
| Power Factor (PF) | Ratio of real power to apparent power (0 to 1); indicates efficiency of power usage |
| Demand Factor | Ratio of maximum demand to total connected load; accounts for not all loads running simultaneously |
| Diversity Factor | Ratio of the sum of individual maximum demands to the maximum demand of the whole system |
| Single-Phase | AC power delivered via one energized conductor and one neutral; standard voltage 230V |
| Three-Phase | AC power delivered via three energized conductors; standard voltage 400V (line-to-line) |
| RTL | Right-to-Left text direction, used for Arabic language |
| LTR | Left-to-Right text direction, used for English language |

---

## [x] 10. Approval Sign-Off

| Name | Role | Decision (Approve/Reject) | Comments | Date |
|------|------|--------------------------|----------|------|
| Khalid Al-Rashid | Project Sponsor | Approve | Proceed with development; review scope at 8-week checkpoint | 2026-02-18 |
| Hasan Hazime | Product Owner | Approve | All requirements captured accurately | 2026-02-19 |
| Omar Farouk | Tech Lead | Approve | Feasible within constraints; layout builder is highest-risk item | 2026-02-20 |

---

## COMPLETION CHECKLIST

- [x] All required sections filled
- [x] Reviewed by Product Owner
- [x] Approved by Project Sponsor
- [x] Stored in project SharePoint / repository
- [x] Cross-referenced in RTM (if applicable)

---

## CROSS-REFERENCES

| Artifact | Link |
|----------|------|
| Producing Runbook | [Extract Business Requirements](../../runbooks/extract-business-requirements.md) |
| Stakeholder Analysis | [Stakeholder Analysis](../phase-1-business-analysis/stakeholder-analysis.md) |
| Software Requirements Specification | [SRS](software-requirements-specification.md) |
| Requirements Traceability Matrix | [RTM](requirements-traceability-matrix.md) |
| Use Cases | [Use Cases](use-cases.md) |
