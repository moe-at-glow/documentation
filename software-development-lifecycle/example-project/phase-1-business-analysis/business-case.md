> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Business Case

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P1-001 |
| **When to Use** | To justify a proposed project by documenting costs, benefits, risks, and alternatives for stakeholder approval |
| **Owner** | Business Analyst |
| **Reviewer** | Product Owner |
| **Approver** | Project Sponsor |
| **SLA** | 5 business days |
| **Runbook** | [Develop Business Case](../../phase-1-business-analysis/runbooks/develop-business-case.md) |
| **Last Verified** | 2026-03-05 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Executive Summary, Problem/Opportunity Statement, Proposed Solution, Cost-Benefit Summary, Recommendation, Approval required only
> **IF** medium project (3-5 devs) **THEN** All sections except Alternatives Considered
> **IF** large project (6+ devs) **THEN** Full template required

> **This project is classified as Medium (4 developers). All sections except Alternatives Considered are completed.**

---

### [x] Executive Summary

| Field | Value |
|-------|-------|
| **Project Name** | Power Atlas |
| **Date** | 2026-03-05 |
| **Author** | Sarah Chen, Business Analyst |
| **Version** | 1.0 |
| **Summary** | GlowPowerRental engineers currently perform power calculations manually using inconsistent Excel spreadsheets, resulting in a 12% error rate, 4-6 hour project sizing cycles, and 2-3 day quote turnaround times. Power Atlas is a proposed centralized web application (poweratlas.glowpowerrental.com) that will standardize power calculations, automate PDF report generation, enable client self-service requirement submission, and provide an equipment layout builder -- delivering an estimated 290% ROI in Year 1 through productivity gains, error reduction, and improved client conversion. |

---

### [x] Problem / Opportunity Statement

| Field | Value |
|-------|-------|
| **Current State** | GlowPowerRental's 8 field engineers and 5 sales staff rely on individual Excel spreadsheets for power calculations (kW/kVA/Amps conversions, load scheduling, generator sizing). Each engineer maintains their own templates with different formulas, naming conventions, and output formats. There is no centralized repository of past projects, no standardized calculation methodology, and no way for clients to self-serve. Completed calculations are manually transcribed into Word documents for client delivery. Project data is siloed on individual laptops with no backup or version control. |
| **Impact of Inaction** | The 12% calculation error rate will persist, costing approximately $60K/year in rework and client goodwill. Engineers will continue spending 4-6 hours per project on manual calculations instead of billable work. Quote turnaround will remain at 2-3 days, during which competitors with faster response times capture an estimated 15% of leads. As the business scales from ~400 to a projected ~600 annual projects, manual processes will require additional headcount rather than organic growth. |
| **Opportunity** | A centralized power calculation platform can standardize engineering outputs, reduce calculation time by 90%, enable client self-service for requirement gathering, and generate professional PDF reports automatically. The Saudi rental power market is growing at 8% annually, and GlowPowerRental's ability to respond faster with higher accuracy directly impacts win rates. |
| **Affected Users/Customers** | 8 field engineers (primary daily users), 5 sales staff (quote generation), 3 operations managers (project oversight), ~120 active corporate clients (report recipients and requirement submitters), and external facility managers requesting ad-hoc power assessments. Total: ~25 internal users, ~200 external users. |
| **Urgency** | High -- Q4 2026 contract renewals with three major clients (Saudi Aramco facilities services, NEOM construction support, Red Sea Global events) require demonstrable process improvements. Competitors have begun offering digital quoting tools. |

---

### [x] Proposed Solution (High-Level)

| Field | Value |
|-------|-------|
| **Solution Description** | Power Atlas is a web-based power calculation and project management platform accessible at poweratlas.glowpowerrental.com. It provides standardized power calculation engines (single-phase and three-phase, kW/kVA/Amps conversions with configurable power factors and efficiency derating), a project management layer with client association and folder organization, an interactive equipment layout builder (AutoCAD-like canvas for site plans), automated PDF report generation with ZATCA-compliant formatting, a public-facing client requirements form, and a requirements review pipeline for operations staff. |
| **Key Capabilities** | - Power calculator with kW/kVA/Amps conversion, single-phase and three-phase support, demand factor and diversity calculations<br>- Project management with CRUD operations, folder hierarchy, project sharing, and client association<br>- Generator database with manufacturer specs, fuel consumption curves, and altitude derating<br>- Interactive equipment layout builder using drag-and-drop canvas (React/Konva.js)<br>- PDF report generation with company branding, calculation breakdowns, and equipment recommendations<br>- Public client requirements form (bilingual Arabic/English) with file upload<br>- Requirements review pipeline with status tracking (New, Under Review, Quoted, Won, Lost)<br>- Role-based access control (Admin, Engineer, Sales, Client) |
| **Technology Approach** | Build (custom in-house development). Python/Flask backend with SQLite database, Vite/Tailwind CSS/vanilla JavaScript frontend, React/Konva.js for the layout builder component, ReportLab for PDF generation. Deployed on a DigitalOcean droplet with Nginx reverse proxy. |
| **Target Users** | Primary: Field engineers (daily power calculations and project management). Secondary: Sales team (quote generation and client communication), Operations managers (pipeline oversight and reporting), External clients (requirement submission via public portal). |

---

### [x] Scope

**In-Scope:**

| # | Item | Description |
|---|------|-------------|
| 1 | Power Calculation Engine | kW/kVA/Amps conversion with single-phase (220V) and three-phase (380V/400V/415V) support, configurable power factors (0.8 default), demand factors, diversity factors, ambient temperature derating, and altitude correction |
| 2 | Project Management | Create, read, update, delete projects; organize in folders; associate with clients; share between team members; track project status (Draft, Active, Completed, Archived) |
| 3 | Generator Sizing | Automated generator selection from a database of rental fleet inventory (Caterpillar, Cummins, Perkins models from 20kVA to 2000kVA); fuel consumption estimation; N+1 redundancy recommendations |
| 4 | Equipment Layout Builder | Interactive canvas for placing generators, distribution boards, cable runs, and load points on a site plan; export layout as image for inclusion in reports |
| 5 | PDF Report Generation | Automated generation of branded calculation reports with cover page, load schedule, generator recommendation, single-line diagram placeholder, equipment layout, and terms/conditions; ZATCA-compliant headers |
| 6 | Client Requirements Portal | Public-facing web form (bilingual AR/EN) for clients to submit project requirements including site details, load lists, timeline, and file attachments; no login required |
| 7 | Requirements Review Pipeline | Internal dashboard for operations staff to review submitted requirements, assign to engineers, track through stages (New → Under Review → Quoted → Won/Lost), with notes and follow-up dates |
| 8 | User Authentication and Roles | Email/password authentication with role-based access control: Admin (full access), Engineer (projects + calculations), Sales (read-only projects + reports), Client (own submissions only) |

**Out-of-Scope:**

| # | Item | Rationale |
|---|------|-----------|
| 1 | IoT / Real-time Generator Monitoring | Requires hardware integration and separate data pipeline; planned for Phase 2 after core platform is stable |
| 2 | ERP Integration (SAP/Oracle) | GlowPowerRental's ERP migration is scheduled for 2027; integration would target a moving platform |
| 3 | Native Mobile Application | Web application is responsive and sufficient for field use; native app ROI does not justify cost at current user count |
| 4 | Maintenance Scheduling | Separate operational domain with different stakeholders; existing maintenance system (UpKeep) is adequate |
| 5 | Billing and Invoicing | Handled by finance team in existing accounting software (Qoyod); duplication would create reconciliation issues |

---

### [x] Cost Estimate

**Development Costs:**

| Category | Description | Estimate |
|----------|-------------|----------|
| Internal Labor | 4 developers x 6 months x $5,000/month average blended rate | $120,000 |
| External Labor | UI/UX design contractor for layout builder and report templates (2 months) | $8,000 |
| Training | Team upskilling on ReportLab, Konva.js, and Arabic RTL implementation (online courses + workshops) | $2,000 |
| **Development Subtotal** | | **$130,000** |

**Infrastructure Costs:**

| Category | Description | Estimate |
|----------|-------------|----------|
| Cloud/Hosting | DigitalOcean droplet (4 vCPU, 8GB RAM, 160GB SSD) for production | $350/month |
| Environments | Staging droplet (2 vCPU, 4GB RAM) for QA and demo | $100/month |
| Tools/Services | Domain registration, SSL (Let's Encrypt -- free), Backblaze B2 backup storage, UptimeRobot monitoring | $50/month |
| **Infrastructure Subtotal** | | **$500/month ($6,000/year)** |

**Licensing Costs:**

| Category | Description | Estimate |
|----------|-------------|----------|
| Software Licenses | ReportLab Plus license for commercial PDF generation with advanced features | $1,200/year |
| API/Service Fees | SendGrid email API (40K emails/month tier for notifications and report delivery) | $800/year |
| **Licensing Subtotal** | | **$2,000/year** |

**Ongoing Costs (Annual):**

| Category | Description | Estimate |
|----------|-------------|----------|
| Maintenance | 0.5 FTE developer for bug fixes, patches, minor enhancements (post-launch) | $30,000/year |
| Support | L1 support handled by operations team (existing staff, no incremental cost) | $0/year |
| Operations | Server monitoring, backup verification, security patches (IT team, 2 hrs/week) | $5,000/year |
| **Ongoing Subtotal** | | **$35,000/year** |

| **Total One-Time Cost** | **$130,000** |
|--------------------------|-----------|
| **Total Annual Recurring Cost** | **$43,000/year** |

---

### [x] Benefit Analysis

**Revenue Impact:**

| Benefit | Description | Estimated Value | Timeframe |
|---------|-------------|-----------------|-----------|
| Faster Quote Turnaround | Reducing quote delivery from 2-3 days to same-day enables capturing leads that currently go to competitors. At ~400 projects/year with average contract value of $15K, a 15% improvement in conversion rate on the 30% of leads currently lost to slow response. | $90,000/year | Month 3 post-launch (ramp to full by Month 6) |
| Professional Report Quality | Branded, consistent PDF reports improve client confidence and support premium pricing. Estimated 3% price improvement on contracts. | $18,000/year | Month 6 post-launch |

**Cost Savings:**

| Benefit | Description | Estimated Value | Timeframe |
|---------|-------------|-----------------|-----------|
| Engineer Productivity | Reducing project sizing from 4-6 hours to ~30 minutes per project. At 8 engineers handling ~50 projects/year each at $45/hr blended cost: (4.5 hrs saved x 400 projects x $45/hr) | $81,000/year | Month 1 post-launch |
| Eliminated Manual Reporting | Engineers currently spend ~1.5 hours per project formatting Word/Excel reports. Automated PDF generation eliminates this entirely. (1.5 hrs x 400 projects x $45/hr) | $27,000/year | Month 1 post-launch |
| Client Self-Service | Public requirements form auto-captures 30% of incoming project requests (currently all via phone/email requiring manual data entry by sales). Saves 1 FTE equivalent in sales coordination time. | $45,000/year | Month 4 post-launch |

**Efficiency Gains:**

| Benefit | Description | Estimated Value | Timeframe |
|---------|-------------|-----------------|-----------|
| Standardized Calculations | Single calculation engine eliminates methodology variations between engineers; consistent outputs regardless of who performs the work | 100% methodology consistency (currently ~60%) | Month 1 post-launch |
| Project Reusability | Engineers can clone and modify similar past projects instead of starting from scratch; estimated 40% of projects are similar to previous work | 40% reduction in calculation time for repeat project types | Month 2 post-launch |
| Centralized Project History | All projects stored centrally with search; no more lost spreadsheets on individual laptops; instant access to historical data for client follow-ups | Elimination of ~20 hrs/month spent searching for past project files | Month 1 post-launch |

**Risk Reduction:**

| Benefit | Description | Estimated Value | Timeframe |
|---------|-------------|-----------------|-----------|
| Calculation Error Reduction | Standardized formulas and validated inputs reduce error rate from 12% to <2%. At 400 projects/year, each error costs ~$1,250 in rework, client penalty, and reputation damage. (40 errors avoided x $1,250) | $50,000/year in avoided rework costs | Month 1 post-launch |
| Data Loss Prevention | Centralized storage with automated backups eliminates risk of project data loss from individual laptop failures. Two incidents in past 18 months cost ~$15K each in reconstruction effort. | $10,000/year in avoided data recovery | Month 1 post-launch |
| Audit Trail | System logs all calculation inputs, outputs, and modifications. Supports ZATCA audit requirements and client dispute resolution. | Qualitative -- regulatory compliance | Month 1 post-launch |

---

### [x] Cost-Benefit Summary

| Metric | Value |
|--------|-------|
| **Total Investment (Year 1)** | $173,000 (Development $130K + Infrastructure $6K + Licensing $2K + Ongoing $35K) |
| **Total Annual Benefits** | $321,000/year (Revenue $108K + Cost Savings $153K + Risk Reduction $60K) |
| **Net Present Value (NPV)** | $612,000 over 3 years (at 10% discount rate) |
| **Return on Investment (ROI)** | 290% Year 1 (Benefits of $321K on Year 1 cost base of $173K, net benefit $148K, adjusted for ramp) |
| **Payback Period** | 6.5 months post-launch |
| **Break-Even Point** | Month 13 from project start (Month 7 post-launch, accounting for 6-month development) |

---

### [x] Risk Assessment

| # | Risk | Probability | Impact | Risk Score | Mitigation Strategy | Owner |
|---|------|-------------|--------|------------|---------------------|-------|
| 1 | Low user adoption by field engineers who prefer existing Excel workflows | High | High | Critical | Involve 2 field engineers in UAT from Sprint 2; run parallel operation period (2 months); provide on-site training sessions; ensure mobile-responsive UI for field tablet use | Fatima Hassan |
| 2 | Excel migration -- existing project data in 8 different spreadsheet formats cannot be cleanly imported | Medium | Medium | Medium | Build CSV import utility with flexible column mapping; accept that historical data migration will be best-effort (~80% automated, 20% manual); prioritize active projects first | Mohammad Al-Farsi |
| 3 | Arabic RTL layout complexity causes UI bugs and delays development timeline | Medium | Medium | Medium | Use established RTL CSS frameworks (Tailwind RTL plugin); engage native Arabic speaker for QA; test RTL from Sprint 1 rather than retrofitting | Mohammad Al-Farsi |
| 4 | Single-server deployment becomes a single point of failure under load | Low | High | Medium | Implement automated daily backups to Backblaze B2; document recovery runbook with <2 hour RTO; plan horizontal scaling path for Year 2 if user count exceeds 100 concurrent | Omar Ibrahim |
| 5 | Scope creep as stakeholders request ERP integration, mobile app, or IoT features during development | High | Medium | High | Maintain strict scope boundary document reviewed at each sprint; all change requests go through formal change control with impact assessment; defer to Phase 2 backlog | Sarah Chen |
| 6 | ZATCA compliance requirements for report formatting change during development | Low | Medium | Low | Monitor ZATCA e-invoicing portal for updates; design report templates with configurable header/footer sections; engage compliance consultant for initial template review | Ahmed Al-Rashid |
| 7 | Key developer turnover during 6-month development period | Medium | High | High | Ensure all code is well-documented with CI/CD pipeline from day 1; no single-person knowledge silos; cross-train on all modules; competitive retention packages during project | Mohammad Al-Farsi |

**Risk Scoring Matrix:**

| | Low Impact | Medium Impact | High Impact |
|---|-----------|---------------|-------------|
| **High Probability** | Medium | High | Critical |
| **Medium Probability** | Low | Medium | High |
| **Low Probability** | Low | Low | Medium |

---

### [x] Success Metrics / KPIs

| # | Metric/KPI | Baseline | Target | Measurement Method | Measurement Frequency |
|---|-----------|----------|--------|--------------------|-----------------------|
| 1 | Average calculation time per project | 4-6 hours (manual Excel) | < 30 minutes | System telemetry: time from project creation to report generation | Monthly |
| 2 | Calculation error rate | 12% (based on QA audit of 50 recent projects) | < 2% | Monthly QA audit of 10% random sample of completed projects vs. manual verification | Monthly |
| 3 | Client self-service submission rate | 0% (all requirements via phone/email) | > 30% of new project requests | Count of requirements submitted via portal vs. total new projects | Monthly |
| 4 | Quote turnaround time | 2-3 business days | < 24 hours (same business day) | Time from client request receipt to quote PDF delivery | Weekly |
| 5 | System adoption rate | 0 active users | 100% of engineering and sales staff (13 users) actively using within 3 months of launch | Weekly active user count from application logs | Weekly |
| 6 | Monthly active projects in system | 0 | > 35 projects/month (matching current ~400/year throughput) | Count of projects with status changes in rolling 30-day window | Monthly |

---

### [x] Timeline (High-Level Milestones)

| # | Milestone | Target Date | Dependencies |
|---|-----------|-------------|--------------|
| 1 | Business Analysis and Requirements Complete | 2026-04-15 | Stakeholder interviews complete; existing Excel templates collected and analyzed |
| 2 | System Architecture and Design Complete | 2026-05-15 | Requirements approved; technology stack confirmed; DigitalOcean environment provisioned |
| 3 | Core Calculator and Project Management MVP | 2026-07-15 | Backend API complete; database schema finalized; basic UI functional |
| 4 | Layout Builder, PDF Reports, and Client Portal | 2026-08-31 | MVP stable; Konva.js integration complete; ReportLab templates approved |
| 5 | UAT, Arabic RTL, and Data Migration | 2026-09-30 | All features code-complete; test data migrated; field engineer test group onboarded |
| 6 | Production Launch | 2026-10-15 | UAT sign-off; production environment hardened; training sessions delivered; monitoring active |

---

### [x] Recommendation

| Field | Value |
|-------|-------|
| **Recommended Option** | Build Power Atlas as a custom web application using Python/Flask, deployed on DigitalOcean |
| **Justification** | Custom build is recommended over COTS alternatives because: (1) no existing product combines power calculation, layout building, and Arabic bilingual client portal in a single platform; (2) the $130K development cost is recovered within 6.5 months of launch through productivity gains alone; (3) custom build allows tight integration with GlowPowerRental's specific generator fleet data and calculation methodologies; (4) total cost of ownership over 3 years ($259K) is less than half the cost of the nearest commercial alternative (EtapPowerCalc at $180K/year licensing). The 290% Year 1 ROI and $612K 3-year NPV strongly justify the investment. |
| **Conditions / Dependencies** | (1) Dedicated allocation of 4 developers for 6 months without competing project assignments; (2) Active participation of at least 2 field engineers in bi-weekly UAT sessions starting from Month 3; (3) IT team provision of DigitalOcean production and staging environments by project start; (4) Product Owner (Fatima Hassan) available for weekly backlog grooming and sprint reviews. |
| **Next Steps** | 1. Obtain sponsor approval and budget authorization<br>2. Complete stakeholder register and communication plan<br>3. Begin Phase 2 requirements engineering with field engineer interviews<br>4. Provision development and staging environments on DigitalOcean<br>5. Collect and catalog all existing Excel calculation templates from 8 engineers |

---

### [x] Approval

| Role | Name | Signature | Date | Decision |
|------|------|-----------|------|----------|
| Project Sponsor | Ahmed Al-Rashid | _A. Al-Rashid_ | 2026-03-05 | Approved |
| Product Owner | Fatima Hassan | _F. Hassan_ | 2026-03-05 | Approved |
| CFO (Budget Authority) | Khalid Nasser | _K. Nasser_ | 2026-03-05 | Approved |

**Comments / Conditions of Approval:**

Ahmed Al-Rashid: "Approved with the condition that monthly budget burn reports are provided to my office. Priority must be given to the core calculator and PDF report features -- the layout builder can be descoped to Phase 2 if timeline is at risk. Ensure Arabic RTL is not an afterthought."

Khalid Nasser: "Budget approved at $150K ceiling (including $20K contingency). Any spend beyond $150K requires re-approval. Quarterly ROI tracking reports required starting Month 1 post-launch."

---

## COMPLETION CHECKLIST

- [x] All required sections filled
- [x] Cost estimates validated with Finance
- [x] Benefits quantified with supporting data
- [x] Risk assessment reviewed with stakeholders
- [x] Success metrics are measurable and time-bound
- [x] Reviewed by Product Owner
- [x] Approved by Project Sponsor

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Develop Business Case | Runbook | [../../phase-1-business-analysis/runbooks/develop-business-case.md](../../phase-1-business-analysis/runbooks/develop-business-case.md) |
| Project Charter | Example | [project-charter.md](project-charter.md) |
| Stakeholder Register | Example | [stakeholder-register.md](stakeholder-register.md) |
