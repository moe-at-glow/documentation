# Extract Business Requirements

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P2-002 |
| **Owner** | Business Analyst |
| **Accountable** | Product Owner |
| **SLA** | 15 business days |
| **Escalation** | Product Owner |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Approved business case and project charter available
- [ ] Completed stakeholder analysis (RB-P2-001 exit criteria met)
- [ ] Stakeholder availability confirmed for elicitation sessions
- [ ] Business Analyst and Domain Expert assigned

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| No approved business case exists | STOP. Complete business case approval first. | Product Owner |
| Stakeholder analysis not completed | STOP. Execute RB-P2-001 first. | Product Owner |
| Key stakeholders (Manage Closely) unavailable for 10+ business days | STOP. Request schedule intervention. | Product Owner |
| Conflicting business objectives with no resolution path | STOP. Escalate for executive alignment. | Project Sponsor |

---

## PROCEDURE

### Step 1: Review Business Case and Project Charter

| Action | Owner | SLA |
|--------|-------|-----|
| Read the business case; identify stated objectives, scope, and constraints | Business Analyst | 0.5 day |
| Read the project charter; note success criteria, budget, and timeline | Business Analyst | 0.5 day |
| List all business objectives for requirement mapping | Business Analyst | 0.5 day |

- [ ] Business case reviewed
- [ ] Project charter reviewed
- [ ] All business objectives listed

> **IF** objectives are ambiguous or conflicting **THEN** schedule clarification session with Product Owner
> **ELSE** proceed to Step 2

### Step 2: Schedule Elicitation Sessions

| Action | Owner | SLA |
|--------|-------|-----|
| Plan sessions based on stakeholder classification | Business Analyst | 1 day |

- [ ] Sessions scheduled per this matrix:

| Session Type | When to Use | Duration | Participants |
|-------------|-------------|----------|-------------|
| Structured Interview | Key stakeholders (Manage Closely) | 45-60 min | Business Analyst + 1 stakeholder |
| Requirements Workshop | Cross-functional needs | 2-4 hours | Business Analyst + 3-8 stakeholders |
| Observation | Operational processes | 2-4 hours | Business Analyst observes end users |
| Document Review | Existing systems and regulations | Self-paced | Business Analyst |

- [ ] Interviews scheduled before workshops
- [ ] All Manage Closely stakeholders have interview slots

> **IF** stakeholder declines interview **THEN** escalate to Product Owner for intervention
> **ELSE** proceed to Step 3

### Step 3: Conduct Structured Interviews

| Action | Owner | SLA |
|--------|-------|-----|
| Interview all Manage Closely stakeholders using question framework | Business Analyst + Domain Expert | 5 days |
| Record all responses attributed to source stakeholder | Business Analyst | During interviews |

- [ ] Current State questions covered (process, tools, strengths, pain points)
- [ ] Future State questions covered (ideal process, missing capabilities, information gaps)
- [ ] Constraints questions covered (regulatory, timeline, budget)
- [ ] Priority questions covered (top change, impact of non-delivery)
- [ ] All responses recorded and attributed

> **IF** stakeholder raises out-of-scope items **THEN** log to parking lot for later review
> **ELSE IF** stakeholder identifies new stakeholders not in register **THEN** update stakeholder register per RB-P2-001
> **ELSE** proceed to Step 4

### Step 4: Facilitate Requirements Workshop

| Action | Owner | SLA |
|--------|-------|-----|
| Conduct workshop to validate and expand interview findings | Business Analyst | 1 day |

- [ ] Workshop agenda followed:

| Time | Activity |
|------|----------|
| 0:00 | State objectives and ground rules |
| 0:15 | Present consolidated interview findings |
| 0:30 | Facilitate group discussion: validate and expand findings |
| 1:00 | Identify and prioritize requirements (MoSCoW) |
| 1:30 | Break |
| 1:45 | Resolve conflicts between stakeholder needs |
| 2:15 | Review action items and next steps |
| 2:30 | Close |

- [ ] Ground rules enforced (one speaker, all perspectives valid, business needs focus, decisions documented, parking lot active)
- [ ] Workshop minutes recorded
- [ ] Action items assigned

> **IF** unresolved conflicts remain after workshop **THEN** schedule follow-up conflict resolution with Product Owner
> **ELSE** proceed to Step 5

### Step 5: Analyze Existing Systems and Processes

| Action | Owner | SLA |
|--------|-------|-----|
| Document current as-is state for each relevant process | Business Analyst | 2 days |
| Identify data inputs, outputs, and transformations | Business Analyst | During analysis |
| Note integrations with external systems | Business Analyst | During analysis |
| Record existing business rules | Business Analyst | During analysis |

- [ ] As-is state documented for each process
- [ ] Data flows mapped (inputs, outputs, transformations)
- [ ] External system integrations listed
- [ ] Business rules captured

### Step 6: Document Business Requirements

| Action | Owner | SLA |
|--------|-------|-----|
| Write each requirement in BR-XXX format with all mandatory attributes | Business Analyst | 3 days |

- [ ] Each requirement contains all attributes:

| Attribute | Value |
|-----------|-------|
| ID | BR-XXX |
| Title | [Short descriptive name] |
| Description | The business shall [capability statement] |
| Priority | Must Have / Should Have / Could Have / Won't Have |
| Source | [Stakeholder name or document reference] |
| Rationale | [Why this requirement exists] |
| Acceptance Criteria | [Measurable conditions] |
| Status | Draft |

- [ ] All requirements follow [Requirements Engineering Standard](../standards/requirements-engineering-standard.md)
- [ ] [BRD Template](../templates/business-requirements-document.md) used

> **IF** requirement has no clear source **THEN** trace back to interview/workshop notes or remove
> **ELSE IF** requirement has no measurable acceptance criteria **THEN** rework before proceeding
> **ELSE** proceed to Step 7

### Step 7: Map Requirements to Business Objectives

| Action | Owner | SLA |
|--------|-------|-----|
| Create mapping table linking each BR to business objectives | Business Analyst | 0.5 day |

- [ ] Every BR traces to at least one business objective
- [ ] No orphan requirements (BRs without business objective)

> **IF** a BR has no business objective mapping **THEN** flag as candidate for removal; confirm with Product Owner
> **ELSE** proceed to Step 8

### Step 8: Review and Validate with Stakeholders

| Action | Owner | SLA |
|--------|-------|-----|
| Distribute draft BRD to all interviewed stakeholders | Business Analyst | 0.5 day |
| Collect written feedback | Business Analyst | 5 business days |
| Schedule review meeting to resolve disagreements | Business Analyst | 1 day |
| Update requirements based on feedback | Business Analyst | 1 day |

- [ ] Draft BRD distributed to all stakeholders from Steps 3 and 4
- [ ] 5 business day review period allowed
- [ ] Written feedback collected
- [ ] Review meeting held for disagreements
- [ ] Requirements updated per feedback

> **IF** stakeholder feedback introduces new requirements **THEN** apply Steps 6-7 to new requirements
> **ELSE IF** stakeholder feedback contradicts existing requirements **THEN** facilitate resolution meeting with Product Owner
> **ELSE** proceed to Step 9

### Step 9: Obtain Formal Approval

| Action | Owner | SLA |
|--------|-------|-----|
| Present final BRD to project sponsor and key stakeholders | Business Analyst | 0.5 day |
| Walk through each Must Have requirement | Business Analyst | During presentation |
| Confirm priorities and scope boundaries | Product Owner | During presentation |
| Obtain written sign-off from project sponsor | Product Owner | 1 day |
| Baseline the BRD | Business Analyst | 0.5 day |

- [ ] Final BRD presented
- [ ] All Must Have requirements walked through
- [ ] Priorities and scope boundaries confirmed
- [ ] Written sign-off obtained from project sponsor
- [ ] BRD baselined (all future changes follow [change management process](manage-requirements-changes.md))

> **IF** sponsor requests changes during sign-off **THEN** return to Step 6, apply changes, re-validate
> **ELSE** proceed to EXIT CRITERIA

---

## EXIT CRITERIA

- [ ] Business case and project charter reviewed
- [ ] All Manage Closely stakeholders interviewed
- [ ] At least one requirements workshop conducted
- [ ] Current processes documented (as-is state)
- [ ] All requirements written in BR-XXX format with all mandatory attributes
- [ ] Each requirement mapped to a business objective
- [ ] Requirements prioritized using MoSCoW
- [ ] Draft BRD reviewed by stakeholders
- [ ] Feedback incorporated
- [ ] Formal sign-off obtained from project sponsor
- [ ] BRD baselined

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Business Requirements Document (BRD) | [business-requirements-document.md](../templates/business-requirements-document.md) | Project documentation repository |
| Interview Notes and Recordings | -- | Project documentation repository |
| Workshop Minutes | -- | Project documentation repository |
| Business Objective to Requirement Mapping | -- | Within BRD |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| BRD Template | Template | [../templates/business-requirements-document.md](../templates/business-requirements-document.md) |
| Requirements Engineering Standard | Standard | [../standards/requirements-engineering-standard.md](../standards/requirements-engineering-standard.md) |
| Stakeholder Analysis Template | Template | [../templates/stakeholder-analysis-template.md](../templates/stakeholder-analysis-template.md) |
| Conduct Stakeholder Analysis | Runbook | [conduct-stakeholder-analysis.md](conduct-stakeholder-analysis.md) |
| Manage Requirements Changes | Runbook | [manage-requirements-changes.md](manage-requirements-changes.md) |
| Derive Software Requirements | Runbook | [derive-software-requirements.md](derive-software-requirements.md) |
