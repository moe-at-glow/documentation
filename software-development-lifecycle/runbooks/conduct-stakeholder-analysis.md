# Conduct Stakeholder Analysis

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P2-001 |
| **Owner** | Business Analyst |
| **Accountable** | Product Owner |
| **SLA** | 5 business days |
| **Escalation** | Product Owner |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Approved business case or project charter available
- [ ] Access to organizational chart confirmed
- [ ] Scheduled time with project sponsor secured
- [ ] Business Analyst and Product Owner assigned

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| No approved business case or project charter exists | STOP. Obtain approval before proceeding. | Product Owner |
| Project sponsor unavailable for sign-off within SLA | STOP. Reschedule or request delegate authority. | Product Owner |
| Organizational chart is outdated or unavailable | STOP. Request updated org chart from HR. | Product Owner |

---

## PROCEDURE

### Step 1: Identify All Stakeholders

| Action | Owner | SLA |
|--------|-------|-----|
| List every person or group with influence over or affected by the project | Business Analyst | 1 day |

- [ ] All internal stakeholder categories reviewed:

| Category | Examples |
|----------|---------|
| Executive | CEO, CTO, Project Sponsor |
| Department Heads | Operations Manager, Finance Manager, IT Manager |
| End Users | Rental desk staff, warehouse operators, field technicians |
| Support | IT operations, customer support |

- [ ] All external stakeholder categories reviewed:

| Category | Examples |
|----------|---------|
| Customers | Rental clients, corporate accounts |
| Regulators | Saudi Arabian standards bodies, local municipality |
| Partners | Equipment suppliers, logistics providers |
| Third Parties | Payment gateway providers, insurance companies |

> **IF** stakeholder group is unclear **THEN** consult Domain Expert for classification
> **ELSE IF** stakeholder spans multiple categories **THEN** list under primary category and cross-reference
> **ELSE** proceed to Step 2

### Step 2: Classify Stakeholders Using Power/Interest Grid

| Action | Owner | SLA |
|--------|-------|-----|
| Place each stakeholder on the Power/Interest grid | Business Analyst | 0.5 day |

- [ ] Each stakeholder assigned a Power level (High/Medium/Low)
- [ ] Each stakeholder assigned an Interest level (High/Medium/Low)
- [ ] Each stakeholder mapped to a quadrant strategy:

| Quadrant | Power | Interest | Strategy |
|----------|-------|----------|----------|
| Manage Closely | High | High | Engage actively, consult on decisions |
| Keep Satisfied | High | Low | Inform of major decisions only |
| Keep Informed | Low | High | Provide regular updates, address concerns |
| Monitor | Low | Low | Minimal communication, major milestones only |

> **IF** stakeholder has High Power and High Interest **THEN** schedule 1:1 interview in Phase 2
> **ELSE IF** stakeholder has High Power and Low Interest **THEN** include in executive summary distribution
> **ELSE** add to general communications list

### Step 3: Document Stakeholder Profiles

| Action | Owner | SLA |
|--------|-------|-----|
| Record all required fields for each stakeholder | Business Analyst | 1 day |

- [ ] Each profile contains all mandatory fields:

| Field | Description |
|-------|-------------|
| Stakeholder ID | Unique identifier (SH-001) |
| Name | Full name |
| Role / Title | Position in organization |
| Organization | Department or external company |
| Power Level | High / Medium / Low |
| Interest Level | High / Medium / Low |
| Classification | Manage Closely / Keep Satisfied / Keep Informed / Monitor |
| Key Concerns | Primary interests and worries |
| Communication Preference | Email / Meeting / Report / Dashboard |
| Contact Information | Email, phone |

### Step 4: Create Stakeholder Register

| Action | Owner | SLA |
|--------|-------|-----|
| Compile all profiles into register using template | Business Analyst | 0.5 day |

- [ ] [Stakeholder Analysis Template](../templates/stakeholder-analysis-template.md) used
- [ ] All stakeholder profiles entered
- [ ] No duplicate entries

### Step 5: Define Communication Plan

| Action | Owner | SLA |
|--------|-------|-----|
| Define communication method, frequency, content, and owner for each stakeholder group | Business Analyst | 0.5 day |

- [ ] Communication plan covers all stakeholder groups:

| Stakeholder Group | Method | Frequency | Content | Owner |
|--------------------|--------|-----------|---------|-------|
| Project Sponsor | 1:1 Meeting | Weekly | Status, risks, decisions needed | Project Manager |
| Department Heads | Status Report | Bi-weekly | Progress, upcoming changes | Business Analyst |
| End Users | Workshop / Demo | Per sprint | Feature walkthrough, feedback collection | Business Analyst |
| Regulators | Formal Report | As required | Compliance documentation | Compliance Officer |

> **IF** stakeholder has no defined communication channel **THEN** assign default channel based on classification quadrant
> **ELSE** proceed to Step 6

### Step 6: Obtain Sign-Off

| Action | Owner | SLA |
|--------|-------|-----|
| Present stakeholder register and communication plan to project sponsor | Business Analyst | 0.5 day |
| Review completeness and confirm no groups are missing | Product Owner | 0.5 day |
| Obtain written approval | Product Owner | 1 day |
| Distribute approved register to project team | Business Analyst | 0.5 day |

- [ ] Register presented to project sponsor
- [ ] Completeness confirmed -- no missing stakeholder groups
- [ ] Written approval obtained
- [ ] Approved register distributed to project team

> **IF** sponsor identifies missing stakeholders **THEN** return to Step 1 and add them
> **ELSE IF** sponsor requests classification changes **THEN** return to Step 2 and reclassify
> **ELSE** proceed to EXIT CRITERIA

---

## EXIT CRITERIA

- [ ] All internal stakeholder groups identified
- [ ] All external stakeholder groups identified
- [ ] Each stakeholder classified on Power/Interest grid
- [ ] Stakeholder profiles documented with all required fields
- [ ] Communication plan defined for each group
- [ ] Stakeholder register reviewed by project sponsor
- [ ] Sign-off obtained and recorded

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Stakeholder Register | [stakeholder-analysis-template.md](../templates/stakeholder-analysis-template.md) | Project documentation repository |
| Communication Plan | -- | Project documentation repository |
| Sponsor Sign-Off Record | -- | Project documentation repository |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Stakeholder Analysis Template | Template | [../templates/stakeholder-analysis-template.md](../templates/stakeholder-analysis-template.md) |
| Requirements Engineering Standard | Standard | [../standards/requirements-engineering-standard.md](../standards/requirements-engineering-standard.md) |
| SDLC Framework | Reference | [../standards/sdlc-framework.md](../standards/sdlc-framework.md) |
| Extract Business Requirements | Runbook | [extract-business-requirements.md](extract-business-requirements.md) |
