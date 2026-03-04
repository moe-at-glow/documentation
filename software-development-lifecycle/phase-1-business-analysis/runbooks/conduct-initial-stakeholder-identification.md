# Conduct Initial Stakeholder Identification

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P1-004 |
| **Owner** | Business Analyst, Product Owner |
| **Accountable** | Product Owner |
| **SLA** | 3 business days |
| **Escalation** | Project Sponsor |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Business need or opportunity identified by stakeholder
- [ ] Business Needs Analysis initiated or completed (RB-P1-001)
- [ ] Access to organizational chart and department directory
- [ ] Product Owner available for stakeholder classification review

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Organizational chart or directory unavailable and cannot be obtained | STOP. Request access through Product Owner | Product Owner |
| Business need cancelled or put on indefinite hold | STOP. Archive work-in-progress and close | Project Sponsor |
| Key departments refuse to participate in identification exercise | STOP. Escalate for executive mandate | Project Sponsor |

---

## PROCEDURE

### Step 1: Review Organizational Chart

| Action | Owner | SLA |
|--------|-------|-----|
| Obtain and review current organizational chart to map reporting lines and functional areas | Business Analyst | 0.5 business days |

- [ ] Current organizational chart obtained (dated within last 6 months)
- [ ] Functional areas relevant to business need identified
- [ ] Reporting lines and decision authority mapped
- [ ] Cross-functional teams and shared services identified
- [ ] Organizational chart gaps or inaccuracies noted

> **IF** organizational chart is outdated (>6 months) **THEN** request updated version from HR or department heads
> **ELSE** proceed with current chart

### Step 2: Identify Internal Stakeholders -- Executive Level

| Action | Owner | SLA |
|--------|-------|-----|
| Identify executive stakeholders with decision authority or strategic oversight | Business Analyst | 0.5 business days |

- [ ] Executive sponsor identified (decision authority)
- [ ] C-suite or VP-level stakeholders with strategic interest identified
- [ ] Department heads whose teams are impacted identified
- [ ] Governance or steering committee members identified
- [ ] Each executive stakeholder recorded with: name, title, department, relevance to project

> **IF** executive stakeholder has delegated authority to a proxy **THEN** record both executive and proxy with delegation scope
> **ELSE** record executive as direct stakeholder

### Step 3: Identify Internal Stakeholders -- Department Level

| Action | Owner | SLA |
|--------|-------|-----|
| Identify department-level stakeholders including managers and team leads in affected areas | Business Analyst | 0.5 business days |

- [ ] Department managers in directly impacted areas identified
- [ ] Team leads for affected processes or systems identified
- [ ] IT/Engineering leads for affected technical systems identified

- [ ] HR stakeholders identified (if staffing or organizational impact)
- [ ] Legal/Compliance stakeholders identified (if regulatory impact)
- [ ] Each department stakeholder recorded with: name, title, department, relevance to project

> **IF** department is undergoing restructuring **THEN** identify both current and anticipated future stakeholders
> **ELSE** record current department stakeholders

### Step 4: Identify Internal Stakeholders -- End-User and Support Level

| Action | Owner | SLA |
|--------|-------|-----|
| Identify end-users, support staff, and operational personnel who will use or maintain the solution | Business Analyst | 0.5 business days |

- [ ] Primary end-user groups identified (by role, function, or location)
- [ ] Estimated user count per group documented
- [ ] Help desk and support team leads identified
- [ ] Training and change management contacts identified
- [ ] Operations and infrastructure team contacts identified
- [ ] Each stakeholder group recorded with: group name, representative contact, estimated size, relevance

> **IF** end-user population exceeds 50 individuals **THEN** identify representative user champions per group instead of all individuals
> **ELSE** list individual end-users where practical

### Step 5: Identify External Stakeholders

| Action | Owner | SLA |
|--------|-------|-----|
| Identify external parties with interest in or impact from the project | Business Analyst | 0.5 business days |

- [ ] Customer stakeholders identified (key accounts, customer segments, customer advisory board)
- [ ] Regulatory stakeholders identified (agencies, auditors, certification bodies)
- [ ] Partner stakeholders identified (integration partners, channel partners, strategic alliances)
- [ ] Vendor stakeholders identified (technology vendors, service providers, contractors)
- [ ] Each external stakeholder recorded with: organization, contact name, role, relationship type, relevance

> **IF** external stakeholders require NDA or contractual review before engagement **THEN** flag for Legal review and note constraint in stakeholder register
> **ELSE** record external stakeholders for standard engagement

### Step 6: Classify Stakeholders by Influence and Interest

| Action | Owner | SLA |
|--------|-------|-----|
| Categorize each stakeholder using the influence-interest matrix | Business Analyst, Product Owner | 0.5 business days |

- [ ] Each stakeholder scored on influence (High/Medium/Low)
- [ ] Each stakeholder scored on interest (High/Medium/Low)
- [ ] Stakeholders mapped to quadrants:
  - High Influence / High Interest = Manage Closely
  - High Influence / Low Interest = Keep Satisfied
  - Low Influence / High Interest = Keep Informed
  - Low Influence / Low Interest = Monitor
- [ ] Classification reviewed and validated with Product Owner
- [ ] Engagement strategy assigned per quadrant

> **IF** Product Owner disagrees with classification **THEN** discuss and reach consensus; document rationale for final classification
> **ELSE** proceed with agreed classification

### Step 7: Create Initial Stakeholder Register

| Action | Owner | SLA |
|--------|-------|-----|
| Compile all identified stakeholders into the formal stakeholder register | Business Analyst | 0.5 business days |

- [ ] Stakeholder register populated with all identified stakeholders
- [ ] Each entry includes: name, title, organization/department, contact info, role in project, influence level, interest level, engagement strategy
- [ ] Stakeholders grouped by category (Executive, Department, End-User/Support, External)
- [ ] Register formatted per stakeholder register template
- [ ] Register stored in designated repository with appropriate access controls

> **IF** stakeholder register contains sensitive information (compensation, political dynamics) **THEN** apply restricted access and share classification-appropriate version only
> **ELSE** share full register with project team

### Step 8: Define Communication Needs

| Action | Owner | SLA |
|--------|-------|-----|
| Document communication preferences and requirements for each stakeholder group | Product Owner | 0.5 business days |

- [ ] Communication preferences captured per stakeholder group (format, frequency, channel)
- [ ] Information needs identified per stakeholder group (what they need to know)
- [ ] Preferred communication channels documented (email, meeting, report, dashboard)
- [ ] Communication frequency defined per group (daily, weekly, bi-weekly, monthly, milestone-only)
- [ ] Language or accessibility requirements noted

> **IF** stakeholder groups have conflicting communication preferences **THEN** create separate communication streams per group
> **ELSE** apply standardized communication approach with group-specific adjustments

### Step 9: Validate with Project Sponsor

| Action | Owner | SLA |
|--------|-------|-----|
| Present stakeholder register to Project Sponsor for validation and completeness check | Business Analyst | 0.5 business days |

- [ ] Stakeholder register presented to Project Sponsor
- [ ] Sponsor confirms completeness (no missing stakeholders)
- [ ] Sponsor validates influence/interest classifications for executive stakeholders
- [ ] Sponsor identifies any political sensitivities or relationship dynamics to note
- [ ] Missing stakeholders added based on sponsor feedback
- [ ] Validation outcome documented (Approved / Additions required)
- [ ] Final register version stored in designated repository

> **IF** sponsor identifies additional stakeholders **THEN** add to register, classify, and re-validate within 1 business day
> **ELSE** proceed to exit criteria

---

## EXIT CRITERIA

- [ ] All internal stakeholder categories reviewed (executive, department, end-user/support)
- [ ] All external stakeholder categories reviewed (customers, regulators, partners, vendors)
- [ ] Stakeholders classified by influence and interest
- [ ] Initial stakeholder register created and populated per template
- [ ] Communication needs defined per stakeholder group
- [ ] Stakeholder register validated by Project Sponsor
- [ ] Register stored in designated repository

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Stakeholder Register | [Stakeholder Register Template](../templates/stakeholder-register-template.md) | `project-repo/phase-1/stakeholder-register/` |
| Influence-Interest Matrix | [Influence-Interest Matrix Template](../templates/influence-interest-matrix-template.md) | `project-repo/phase-1/stakeholder-register/` |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Business Needs Analysis | Runbook | [RB-P1-001](./conduct-business-needs-analysis.md) |
| Business Case Development | Runbook | [RB-P1-002](./develop-business-case.md) |
| Project Charter Creation | Runbook | [RB-P1-003](./create-project-charter.md) |
| Stakeholder Register Template | Template | [../templates/stakeholder-register-template.md](../templates/stakeholder-register-template.md) |
| Phase 1 Standards | Standard | [../standards/phase-1-standards.md](../standards/phase-1-standards.md) |
