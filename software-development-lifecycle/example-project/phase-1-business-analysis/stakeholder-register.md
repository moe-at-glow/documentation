> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Stakeholder Register

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P1-003 |
| **When to Use** | To identify, classify, and plan communication for all project stakeholders |
| **Owner** | Business Analyst |
| **Reviewer** | Product Owner |
| **SLA** | 3 business days |
| **Runbook** | [Conduct Initial Stakeholder Identification](../../phase-1-business-analysis/runbooks/conduct-initial-stakeholder-identification.md) |
| **Last Verified** | 2026-03-05 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Stakeholder Register table required; Communication Plan table optional
> **IF** medium project (3-5 devs) **THEN** Both tables required; simplified Communication Plan (combine stakeholder groups)
> **IF** large project (6+ devs) **THEN** Full template required with detailed per-group communication plan

> **This project is classified as Medium (4 developers). Both Stakeholder Register and Communication Plan tables are completed with combined stakeholder groups.**

---

### [x] Project Information

| Field | Value |
|-------|-------|
| **Project Name** | Power Atlas |
| **Date** | 2026-03-05 |
| **Author** | Sarah Chen, Senior Business Analyst |
| **Version** | 1.0 |

---

### [x] Stakeholder Register

| ID | Name | Role / Title | Organization | Category | Power Level | Interest Level | Classification | Key Concerns | Communication Preference | Contact |
|----|------|-------------|--------------|----------|-------------|----------------|----------------|--------------|--------------------------|---------|
| SH-001 | Ahmed Al-Rashid | VP Operations | GlowPowerRental -- Operations | Internal | High | High | Manage Closely | ROI delivery within projected timeline; operational efficiency gains visible by Q4 2026 client renewals; budget adherence to $150K ceiling; risk that tool disrupts current workflows during transition period | Bi-weekly steering committee; monthly executive summary; immediate escalation via phone for budget/timeline issues | ahmed.alrashid@glowpowerrental.com / +966-50-XXX-4401 |
| SH-002 | Fatima Hassan | Rental Operations Manager | GlowPowerRental -- Rental Operations | Internal | High | High | Manage Closely | Tool must match real-world engineering workflows; field engineers must actually adopt it (not revert to Excel); Arabic support for client-facing outputs is critical for Saudi market; requirements pipeline must integrate with her existing sales tracking process | Daily standup attendance; weekly backlog grooming; sprint review demos; direct Slack channel | fatima.hassan@glowpowerrental.com / +966-50-XXX-5512 |
| SH-003 | Mohammad Al-Farsi | Tech Lead | GlowPowerRental -- Engineering | Internal | Medium | High | Keep Informed | Technical debt from rushed delivery; SQLite scalability limits; single-server reliability; code quality and maintainability post-launch; ability to support the system long-term with existing team; deployment complexity on DigitalOcean without managed services | Daily standup; architecture decision meetings; PR review notifications; technical design review sessions | mohammad.alfarsi@glowpowerrental.com / +966-50-XXX-7734 |
| SH-004 | Field Engineers (group of 8) | Electrical Engineers | GlowPowerRental -- Field Operations | Internal | Low | High | Keep Informed | Tool must be faster and easier than their current Excel templates, not slower; must work on tablets in the field with potentially spotty internet; must handle the calculation edge cases they encounter (altitude derating, parallel generator configurations, mixed single/three-phase loads); fear of being "monitored" through centralized system | Bi-weekly UAT sessions (2 representatives); training workshops (all 8); feedback forms after each UAT session; dedicated Slack channel for bug reports | Group contact: field.engineers@glowpowerrental.com |
| SH-005 | Sales Team (group of 5) | Sales Representatives | GlowPowerRental -- Sales | Internal | Low | High | Keep Informed | Need professional-looking PDF reports to send to clients immediately; must be able to generate quotes without deep technical knowledge; client requirements pipeline must give them visibility into incoming requests; report turnaround must be same-day to compete | Sprint review demos (1 representative); training session before launch; weekly status email | Group contact: sales@glowpowerrental.com |
| SH-006 | Khalid Nasser | Chief Financial Officer | GlowPowerRental -- Finance | Internal | High | Low | Keep Satisfied | Budget adherence; measurable ROI tracking; no surprise cost overruns; ZATCA compliance for any documents that could be considered commercial; total cost of ownership including ongoing maintenance must stay within projected $43K/year | Monthly steering committee; quarterly ROI tracking report; immediate notification of any projected budget overrun >10% | khalid.nasser@glowpowerrental.com / +966-50-XXX-8845 |
| SH-007 | Omar Ibrahim | IT Director | GlowPowerRental -- IT | Internal | Medium | High | Keep Informed | Server security and hardening on DigitalOcean; backup and disaster recovery procedures; SSL certificate management; DNS configuration for poweratlas.glowpowerrental.com; monitoring and alerting setup; no interference with existing production systems; compliance with company IT security policies | Architecture review meetings; deployment planning sessions; bi-weekly infrastructure status sync; incident escalation path | omar.ibrahim@glowpowerrental.com / +966-50-XXX-9956 |
| SH-008 | Corporate Clients (~120 active) | Facility Managers, Project Managers, Procurement Officers | External -- Various companies (Saudi Aramco, NEOM, Red Sea Global, etc.) | External | Medium | Medium | Keep Informed | Requirements form must be simple and not require registration; Arabic language support is essential; submitted data must be handled confidentially; response time after submission should be clearly communicated; PDF reports must look professional and include all technical details needed for their internal approvals | Launch announcement email; in-form instructions and confirmation messages; follow-up communication through sales team | Via individual sales representative contacts |
| SH-009 | ZATCA (Zakat, Tax and Customs Authority) | Government Regulator | External -- Saudi Government | External | High | Low | Keep Satisfied | Any commercial documents (quotations, reports with pricing) must comply with ZATCA e-invoicing Phase 2 requirements including QR code, tax registration number, VAT number, and sequential numbering; Arabic content must be present on regulated documents | Monitor ZATCA portal for regulation updates; compliance review of report templates before launch; engage compliance consultant if requirements change | Via compliance consultant; ZATCA e-invoicing portal |
| SH-010 | Equipment Suppliers (Caterpillar, Cummins, Perkins dealers) | Generator Manufacturers / Dealers | External -- Supplier companies | External | Low | Low | Monitor | Generator specification data in Power Atlas must be accurate and current; any public-facing generator recommendations should not misrepresent manufacturer specs; potential future interest in API integration for real-time spec updates | No proactive communication required; notify if spec data format changes; annual review of generator database accuracy | Via existing procurement relationship |

**Power/Interest Classification Matrix:**

| | Low Interest | High Interest |
|---|-------------|---------------|
| **High Power** | **Keep Satisfied:** Khalid Nasser (CFO), ZATCA | **Manage Closely:** Ahmed Al-Rashid (Sponsor), Fatima Hassan (PO) |
| **Low Power** | **Monitor:** Equipment Suppliers | **Keep Informed:** Mohammad Al-Farsi (Tech Lead), Field Engineers, Sales Team, Omar Ibrahim (IT Director), Corporate Clients |

---

### [x] Communication Plan

| Stakeholder Group | Method | Frequency | Content | Owner |
|-------------------|--------|-----------|---------|-------|
| Manage Closely -- Ahmed Al-Rashid, Fatima Hassan | 1:1 steering committee meeting (Teams); ad hoc phone calls for escalations | Bi-weekly (Sponsor); Daily standup + weekly grooming (PO) | Detailed project status, budget burn, risk register updates, scope decisions, go/no-go recommendations, sprint demo and acceptance | Sarah Chen (status reports); Fatima Hassan (steering deck) |
| Keep Satisfied -- Khalid Nasser (CFO), ZATCA | Executive summary email (CFO); compliance review document (ZATCA) | Monthly (CFO); As needed / at report template design milestone (ZATCA) | Budget vs. forecast, ROI tracking metrics, projected total cost of ownership, ZATCA compliance status of report templates | Sarah Chen (CFO reports); Mohammad Al-Farsi (ZATCA compliance review) |
| Keep Informed -- Mohammad Al-Farsi, Omar Ibrahim, Field Engineers, Sales Team, Corporate Clients | Daily standup (dev team); bi-weekly sprint review (all internal); bi-weekly UAT sessions (field engineers); launch announcement (clients) | Daily (dev team); Bi-weekly (sprint reviews + UAT); At launch (clients) | Technical progress and blockers, completed features demo, upcoming sprint plan, UAT feedback results, infrastructure readiness status, client portal launch instructions | Mohammad Al-Farsi (daily standup); Sarah Chen (sprint review); Fatima Hassan (UAT coordination, client communications) |
| Monitor -- Equipment Suppliers | Email notification | Annually or as needed | Generator database updates, spec data verification requests, notification of any public-facing spec changes | Fatima Hassan |

---

### [x] Stakeholder Change Log

| Date | Stakeholder ID | Change Description | Updated By |
|------|---------------|-------------------|------------|
| 2026-03-05 | All | Initial stakeholder register created based on project kickoff interviews and organizational chart review | Sarah Chen |
| 2026-03-05 | SH-004 | Confirmed 8 field engineers (previously estimated 6-10); identified Tariq Al-Dosari and Hana Osman as UAT representatives | Fatima Hassan |
| 2026-03-05 | SH-008 | Updated active client count from estimated 100 to confirmed 120 based on CRM export from sales team | Sarah Chen |

---

## COMPLETION CHECKLIST

- [x] All known stakeholders identified and registered
- [x] Power and interest levels assessed for each stakeholder
- [x] Classifications assigned using Power/Interest matrix
- [x] Key concerns documented for each stakeholder
- [x] Communication preferences captured
- [x] Communication plan defined for each stakeholder group
- [x] Reviewed by Product Owner

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Conduct Initial Stakeholder Identification | Runbook | [../../phase-1-business-analysis/runbooks/conduct-initial-stakeholder-identification.md](../../phase-1-business-analysis/runbooks/conduct-initial-stakeholder-identification.md) |
| Business Case | Example | [business-case.md](business-case.md) |
| Project Charter | Example | [project-charter.md](project-charter.md) |
