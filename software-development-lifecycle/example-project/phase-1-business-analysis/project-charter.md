> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Project Charter

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P1-002 |
| **When to Use** | To formally authorize a project by defining objectives, scope, constraints, roles, and governance |
| **Owner** | Business Analyst |
| **Reviewer** | Product Owner |
| **Approver** | Project Sponsor |
| **SLA** | 5 business days |
| **Runbook** | [Create Project Charter](../../phase-1-business-analysis/runbooks/create-project-charter.md) |
| **Last Verified** | 2026-03-05 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Project Name, Sponsor, Objectives, High-Level Scope, Key Roles, Project Scale, Success Criteria, Authorization required only
> **IF** medium project (3-5 devs) **THEN** All sections except Communication Plan (use informal channels)
> **IF** large project (6+ devs) **THEN** Full template required

> **This project is classified as Medium (4 developers). All sections are completed; Communication Plan is included voluntarily due to the mix of internal and external stakeholders.**

---

### [x] Project Name

| Field | Value |
|-------|-------|
| **Project Name** | Power Atlas |
| **Project ID** | PRJ-2026-007 |
| **Version** | 1.0 |
| **Date** | 2026-03-05 |

---

### [x] Project Sponsor

| Field | Value |
|-------|-------|
| **Name** | Ahmed Al-Rashid |
| **Title** | Vice President, Operations |
| **Department** | Operations |
| **Contact** | ahmed.alrashid@glowpowerrental.com / +966-50-XXX-4401 |

---

### [x] Product Owner

| Field | Value |
|-------|-------|
| **Name** | Fatima Hassan |
| **Title** | Rental Operations Manager |
| **Department** | Rental Operations |
| **Contact** | fatima.hassan@glowpowerrental.com / +966-50-XXX-5512 |

---

### [x] Business Analyst

| Field | Value |
|-------|-------|
| **Name** | Sarah Chen |
| **Title** | Senior Business Analyst |
| **Department** | Project Management Office |
| **Contact** | sarah.chen@glowpowerrental.com / +966-50-XXX-6623 |

---

### [x] Project Objectives

| # | Objective | Measurable Outcome | Priority |
|---|-----------|-------------------|----------|
| 1 | Standardize power calculations across all engineers | Single calculation engine with validated formulas replaces 8 individual Excel templates; 100% of new projects use Power Atlas within 3 months of launch | Must Have |
| 2 | Reduce project sizing time from hours to minutes | Average time from project creation to completed calculation report drops from 4-6 hours to under 30 minutes, measured by system telemetry | Must Have |
| 3 | Reduce calculation error rate to below 2% | Monthly QA audit of random 10% sample shows error rate below 2% (down from current 12%) | Must Have |
| 4 | Enable client self-service requirement submission | Public bilingual (AR/EN) requirements form captures at least 30% of new project requests without staff intervention | Should Have |
| 5 | Automate professional PDF report generation | Engineers generate branded, ZATCA-compliant calculation reports with one click; zero manual formatting required | Must Have |
| 6 | Provide interactive equipment layout builder | Engineers can create site equipment layouts with drag-and-drop generator, distribution board, and cable run placement on a canvas | Should Have |
| 7 | Reduce quote turnaround time to same-day | Time from client request to delivered quote PDF drops from 2-3 business days to under 24 hours | Must Have |

---

### [x] High-Level Scope

**In-Scope:**

| # | Item | Description |
|---|------|-------------|
| 1 | Power Calculation Engine | kW/kVA/Amps conversion supporting single-phase (220V) and three-phase (380V/400V/415V) systems; configurable power factor, demand factor, diversity factor; ambient temperature and altitude derating |
| 2 | Project Management | CRUD operations for projects; folder-based organization; client association; project sharing between team members; status workflow (Draft → Active → Completed → Archived) |
| 3 | Generator Sizing and Database | Rental fleet database (Caterpillar, Cummins, Perkins; 20kVA-2000kVA); automated selection based on calculated load; fuel consumption estimates; N+1 redundancy recommendations |
| 4 | Equipment Layout Builder | Interactive canvas (React/Konva.js) for placing generators, distribution boards, cable runs, and load points; snap-to-grid; export as PNG/SVG for report inclusion |
| 5 | PDF Report Generation | Automated report creation via ReportLab with cover page, load schedule table, generator recommendation, equipment layout image, terms and conditions; ZATCA-compliant header; bilingual support |
| 6 | Client Requirements Portal | Public-facing web form (no login required) with bilingual AR/EN interface; fields for site details, load list, timeline, budget range, and file attachments (up to 25MB) |
| 7 | Requirements Review Pipeline | Internal dashboard showing submitted requirements in kanban-style columns (New → Under Review → Quoted → Won → Lost); assignment to engineers; notes and follow-up date tracking |
| 8 | User Authentication and RBAC | Email/password authentication; four roles: Admin (full system access + user management), Engineer (projects + calculations + layouts), Sales (read-only projects + report download), Client (own submissions only) |

**Out-of-Scope:**

| # | Item | Rationale |
|---|------|-----------|
| 1 | IoT / Real-time Generator Monitoring | Requires hardware sensors, cellular connectivity, and real-time data pipeline; fundamentally different architecture; planned for separate Phase 2 initiative |
| 2 | ERP Integration (SAP/Oracle) | GlowPowerRental's ERP platform migration to SAP S/4HANA is scheduled for 2027; integrating with the current legacy system would be throwaway work |
| 3 | Native Mobile Application (iOS/Android) | Web application will be responsive and usable on tablets in the field; native app development doubles frontend effort for ~25 users; revisit when user base exceeds 100 |
| 4 | Maintenance Scheduling | Separate operational domain managed by maintenance department using UpKeep; overlapping functionality would create data consistency issues |
| 5 | Billing and Invoicing | Finance team uses Qoyod accounting software; duplicating invoicing logic risks reconciliation errors and violates single-source-of-truth for financial data |

---

### [x] Constraints

| Constraint Type | Description | Impact |
|----------------|-------------|--------|
| **Budget** | Total project budget capped at $150,000 (including $20K contingency). Funded from Operations capital budget FY2026. | Limits team size to 4 developers; no room for additional contractor resources beyond planned UI/UX engagement |
| **Timeline** | 6-month development window (April-September 2026) with production launch targeted for October 15, 2026. Hard deadline driven by Q4 client contract renewal presentations. | Scope must be prioritized ruthlessly; layout builder is first candidate for deferral if timeline slips |
| **Technology** | Must deploy on single DigitalOcean droplet (company standard for internal tools). No AWS/Azure/GCP. Python/Flask mandated by existing team skills. | Limits horizontal scaling options; must design for vertical scaling within droplet tier; no managed database services available |
| **Regulatory** | PDF reports must include ZATCA-compliant headers (company tax registration number, VAT number, sequential document numbering). Arabic language support required for client-facing outputs. | Adds RTL CSS complexity; report template must pass ZATCA format validation; requires Arabic content review by native speaker |
| **Staffing** | Development team of 4 drawn from existing staff (no new hires). Tech Lead (Mohammad Al-Farsi) also supports production systems at 20% allocation. | Effective development capacity is 3.8 FTEs; critical path items cannot all depend on Tech Lead |

---

### [x] Assumptions

| # | Assumption | Impact if Invalid | Validation Method |
|---|-----------|-------------------|-------------------|
| 1 | All 4 developers will be available full-time for the 6-month duration without competing project assignments | Timeline extends by 2-4 weeks per developer pulled; critical path features delayed | Confirmed allocation with department heads before project kickoff; documented in resource plan |
| 2 | Existing Excel calculation formulas from senior engineers are mathematically correct and can be used as the reference standard | Calculation engine built on incorrect formulas produces wrong results at scale; worse than current state | Cross-validate top 3 engineers' formulas against IEC 60364 standards and manufacturer datasheets in Week 1 |
| 3 | SQLite is sufficient for the expected data volume (~600 projects/year, ~25 concurrent users) | Performance degradation under concurrent writes; requires database migration mid-project | Load test with simulated 50 concurrent users against SQLite in Sprint 1; define migration trigger thresholds |
| 4 | Field engineers have reliable internet access at project sites for web application use | Application is unusable in the field; adoption drops; engineers revert to Excel | Survey field engineers on connectivity; if unreliable, implement offline-capable PWA features (adds ~3 weeks to scope) |
| 5 | DigitalOcean droplet with 4 vCPU / 8GB RAM can handle production workload including PDF generation | PDF generation under load causes server timeouts; degraded user experience | Benchmark ReportLab PDF generation at 10 concurrent reports on target hardware in Sprint 2 |
| 6 | Client requirements form will receive adequate submission volume without marketing push | Self-service target of 30% is not met; ROI for client portal component is reduced | Plan email campaign to top 50 clients at launch; include QR code linking to form on all printed quotations |

---

### [x] High-Level Milestones

| # | Milestone | Target Date | Exit Criteria |
|---|-----------|-------------|---------------|
| 1 | Phase 1: Business Analysis Complete | 2026-03-31 | Business case approved; project charter signed; stakeholder register complete; all stakeholder interviews conducted |
| 2 | Phase 2: Requirements Complete | 2026-04-15 | SRS document approved; all user stories written and estimated; data model defined; API contract drafted; requirements traceability matrix complete |
| 3 | Phase 3: Architecture and Design Complete | 2026-05-15 | Architecture decision records finalized; database schema approved; UI wireframes signed off; API specification complete; deployment architecture documented |
| 4 | Phase 4: Core Development Complete (Calculator + Projects + Auth) | 2026-07-15 | Power calculation engine passes validation against 20 reference projects; project CRUD operational; authentication and RBAC functional; unit test coverage >80% |
| 5 | Phase 5: Full Development Complete (Layout + PDF + Portal + Pipeline) | 2026-08-31 | All features code-complete; layout builder functional with export; PDF reports generate correctly in AR/EN; client portal accepting submissions; pipeline dashboard operational |
| 6 | Phase 6: Testing and UAT Complete | 2026-09-30 | All critical and high-severity bugs resolved; UAT sign-off from 2 field engineers, 1 sales rep, and Product Owner; performance benchmarks met; security scan clean; Arabic RTL reviewed |
| 7 | Production Launch | 2026-10-15 | Production environment deployed and monitored; DNS configured for poweratlas.glowpowerrental.com; training sessions delivered to all user groups; data migration complete; rollback plan tested |

---

### [x] Key Roles and Responsibilities

| Role | Name | Responsibilities | Availability |
|------|------|-----------------|--------------|
| Project Sponsor | Ahmed Al-Rashid | Strategic direction; budget approval; escalation resolution; executive stakeholder communication; go/no-go decisions at phase gates | 10% (bi-weekly steering meetings + ad hoc escalations) |
| Product Owner | Fatima Hassan | Requirements prioritization; backlog grooming; sprint review acceptance; user story approval; UAT coordination with field engineers; Arabic content review | 50% (daily standups + weekly grooming + sprint reviews) |
| Business Analyst | Sarah Chen | Requirements elicitation and documentation; stakeholder interviews; user story writing; process mapping; acceptance criteria definition; traceability matrix | 100% (dedicated to project) |
| Tech Lead | Mohammad Al-Farsi | Architecture decisions; code reviews; technical mentoring; database design; deployment pipeline; performance optimization; production support handoff | 80% (20% allocated to existing production systems) |
| Senior Developer | Nadia Al-Qahtani | Backend development (Flask API, SQLite, ReportLab PDF engine); generator database; calculation engine implementation; API testing | 100% (dedicated to project) |
| Frontend Developer | Rami Haddad | Vite/Tailwind UI implementation; React/Konva.js layout builder; Arabic RTL support; responsive design; client portal frontend | 100% (dedicated to project) |
| Full-Stack Developer | Yusuf Ibrahim | Authentication/RBAC; requirements pipeline; project management CRUD; data migration utilities; integration testing | 100% (dedicated to project) |
| QA Lead | Layla Mansour | Test planning; test case development; functional testing; regression testing; UAT support; Arabic language QA; performance testing | 50% (shared with another project until Sprint 4, then 100%) |

---

### [x] Communication Plan

| Audience | Method | Frequency | Content | Owner |
|----------|--------|-----------|---------|-------|
| Development Team | Daily standup (15 min, Microsoft Teams) | Daily (9:00 AM AST) | Yesterday's progress, today's plan, blockers | Mohammad Al-Farsi |
| Product Owner + BA | Sprint planning / backlog grooming (Teams) | Weekly (Sunday 10:00 AM AST) | Story prioritization, acceptance criteria review, scope questions | Sarah Chen |
| Project Stakeholders | Sprint review demo + written status report | Bi-weekly (end of each sprint) | Completed features demo, velocity metrics, upcoming sprint plan, risks and issues | Sarah Chen |
| Sponsor + CFO | Steering committee meeting | Monthly (first Thursday) | Budget burn, timeline status, risk register updates, escalations, go/no-go decisions | Fatima Hassan |
| Field Engineers (UAT group) | Hands-on testing session + feedback form | Bi-weekly (starting Sprint 4) | New feature walkthrough, usability feedback, bug reporting, workflow validation | Fatima Hassan |
| All Staff | Company-wide update email | Monthly | Project progress highlights, launch timeline, training schedule | Ahmed Al-Rashid |

**Escalation Path:**

| Level | Escalation Trigger | Escalate To | Response SLA |
|-------|-------------------|-------------|--------------|
| 1 | Task blocked > 1 day; technical decision needed | Mohammad Al-Farsi (Tech Lead) | 4 hours |
| 2 | Sprint goal at risk; scope/timeline conflict; resource conflict | Fatima Hassan (Product Owner) | 1 business day |
| 3 | Budget overrun > 10%; timeline slip > 2 weeks; critical technical risk materialized | Ahmed Al-Rashid (Sponsor) | 2 business days |

---

### [x] Project Scale

| Field | Value |
|-------|-------|
| **Team Size** | 4 developers (1 Tech Lead, 1 Senior Backend, 1 Frontend, 1 Full-Stack) + 1 QA (part-time) |
| **Classification** | Medium (3-5 devs) |
| **Estimated Duration** | 6 months (April - September 2026, with October launch) |
| **Estimated Effort** | 24 person-months development + 3 person-months QA + 6 person-months BA/PO = 33 person-months total |

**Scaling Implications per SDLC Framework:**

| Area | Small | Medium (This Project) | Large |
|------|-------|--------|-------|
| Documentation | Lightweight | **Standard -- Full requirements, architecture docs, test plans** | Comprehensive |
| Reviews | Peer review | **Formal review -- PR reviews by Tech Lead, sprint review demos** | Review board |
| Testing | Unit + integration | **+ E2E -- Unit, integration, E2E, UAT, Arabic RTL testing** | + Performance + Security |
| Governance | Minimal gates | **Standard gates -- Phase gate reviews at each milestone** | Full gate reviews |

---

### [x] Success Criteria

| # | Criterion | Metric | Target | Measurement Method |
|---|----------|--------|--------|--------------------|
| 1 | Power calculations are significantly faster than manual process | Average project calculation time | < 30 minutes (down from 4-6 hours) | Application telemetry: timestamp delta between project creation and first report generation |
| 2 | Calculation accuracy meets engineering standards | Error rate in completed calculations | < 2% (down from 12%) | Monthly QA audit: random sample of 10% of completed projects cross-checked against manual calculation |
| 3 | All engineering and sales staff actively use the platform | System adoption rate | 100% of target users (13 internal) active within 90 days of launch | Weekly active user count from application access logs |
| 4 | Clients self-submit requirements through the portal | Self-service submission rate | > 30% of new project requests via portal | Portal submissions / total new projects per month |
| 5 | Quote delivery time meets same-day target | Quote turnaround time | < 24 hours from request to delivered PDF | Timestamp delta: requirement received → report PDF sent to client |
| 6 | System performs reliably under normal load | Application uptime | > 99.5% uptime (excluding scheduled maintenance) | UptimeRobot monitoring; monthly uptime report |

---

### [x] Authorization

| Field | Value |
|-------|-------|
| **Sponsor Name** | Ahmed Al-Rashid |
| **Sponsor Signature** | _A. Al-Rashid_ |
| **Date** | 2026-03-05 |
| **Decision** | Authorized |

**Conditions of Authorization:**

1. Budget ceiling of $150,000 (including $20K contingency) is firm. Any projected overrun must be escalated to Sponsor and CFO before additional spend is committed.
2. Monthly budget burn reports must be submitted to Sponsor and CFO by the 5th business day of each month.
3. If timeline slips beyond 2 weeks, the Equipment Layout Builder (Scope Item #4) will be descoped to Phase 2 to protect the October 15 launch date.
4. Arabic RTL support must be implemented incrementally from Sprint 1 -- it is not acceptable to defer all Arabic work to the end.
5. A formal go/no-go decision will be made at the UAT milestone (September 30, 2026) before production deployment proceeds.

**Distribution List:**

| # | Name | Role | Date Distributed |
|---|------|------|-----------------|
| 1 | Ahmed Al-Rashid | VP Operations (Sponsor) | 2026-03-05 |
| 2 | Fatima Hassan | Rental Operations Manager (Product Owner) | 2026-03-05 |
| 3 | Sarah Chen | Senior Business Analyst | 2026-03-05 |
| 4 | Mohammad Al-Farsi | Tech Lead | 2026-03-05 |
| 5 | Khalid Nasser | CFO | 2026-03-05 |
| 6 | Omar Ibrahim | IT Director | 2026-03-05 |

---

## COMPLETION CHECKLIST

- [x] All required sections filled
- [x] Project objectives are measurable
- [x] Scope boundaries clearly defined
- [x] All constraints identified and documented
- [x] Assumptions validated where possible
- [x] Key roles assigned with confirmed availability
- [x] Project scale classification confirmed
- [x] Reviewed by Product Owner
- [x] Approved by Project Sponsor

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Create Project Charter | Runbook | [../../phase-1-business-analysis/runbooks/create-project-charter.md](../../phase-1-business-analysis/runbooks/create-project-charter.md) |
| Business Case | Example | [business-case.md](business-case.md) |
| Stakeholder Register | Example | [stakeholder-register.md](stakeholder-register.md) |
