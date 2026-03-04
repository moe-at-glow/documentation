# Create Project Charter

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P1-003 |
| **Owner** | Business Analyst |
| **Accountable** | Project Sponsor |
| **SLA** | 5 business days |
| **Escalation** | Project Sponsor |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Business case approved by Project Sponsor (RB-P1-002 completed)
- [ ] Project Sponsor identified and available for sign-off
- [ ] Initial stakeholder identification completed (RB-P1-004 completed or in progress)
- [ ] Organizational project governance standards available

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Business case approval revoked or placed on hold | STOP. Halt charter development and await sponsor direction | Project Sponsor |
| Project Sponsor unavailable for >5 business days | STOP. Identify interim authority or pause charter creation | Product Owner |
| Organizational restructuring impacts project authority or funding | STOP. Reassess project viability with new leadership | Project Sponsor |
| Constraints render approved scope infeasible | STOP. Return to business case for scope revision | Project Sponsor |

---

## PROCEDURE

### Step 1: Define Project Objectives

| Action | Owner | SLA |
|--------|-------|-----|
| Translate business case goals into specific, measurable project objectives | Business Analyst | 0.5 business days |

- [ ] Business objectives extracted from approved business case
- [ ] Each objective stated in SMART format (Specific, Measurable, Achievable, Relevant, Time-bound)
- [ ] Objectives aligned with organizational strategic goals
- [ ] Maximum 5 primary objectives defined
- [ ] Objectives reviewed with Product Owner

> **IF** objectives conflict with each other **THEN** escalate to Product Owner for prioritization
> **ELSE** proceed with aligned objectives

### Step 2: Define High-Level Scope

| Action | Owner | SLA |
|--------|-------|-----|
| Document in-scope and out-of-scope items at the project level | Business Analyst | 0.5 business days |

- [ ] In-scope deliverables listed (systems, features, integrations, migrations)
- [ ] In-scope user groups and business processes identified
- [ ] Out-of-scope items explicitly listed with rationale for exclusion
- [ ] Scope boundaries consistent with approved business case
- [ ] Scope statement reviewed with Product Owner and Tech Lead

> **IF** Tech Lead identifies technical dependencies that expand scope **THEN** document and escalate to Product Owner for scope decision
> **ELSE** proceed with defined scope boundaries

### Step 3: Identify Constraints

| Action | Owner | SLA |
|--------|-------|-----|
| Document all known constraints that limit project execution options | Business Analyst | 1 business day |


- [ ] Timeline constraints documented (hard deadlines, regulatory dates, market windows)
- [ ] Technology constraints documented (platform mandates, integration requirements, legacy dependencies)
- [ ] Regulatory constraints documented (compliance requirements, data residency, audit obligations)
- [ ] Resource constraints documented (team availability, skill gaps, competing priorities)
- [ ] Each constraint classified as fixed (non-negotiable) or flexible (adjustable with approval)
- [ ] Constraints validated with Project Sponsor

> **IF** constraints make approved scope infeasible **THEN** trigger ABORT: return to business case for scope revision
> **ELSE** proceed with documented constraints

### Step 4: Define High-Level Milestones

| Action | Owner | SLA |
|--------|-------|-----|
| Establish major project milestones aligned with SDLC phases and business deadlines | Business Analyst | 0.5 business days |

- [ ] Phase gate milestones defined (one per SDLC phase)
- [ ] External deadline milestones defined (regulatory, contractual, market)
- [ ] Key deliverable milestones defined (MVP, beta, GA)
- [ ] Target dates assigned to each milestone (month/quarter level)
- [ ] Dependencies between milestones identified
- [ ] Milestone schedule reviewed with Product Owner and Tech Lead

> **IF** milestone dates conflict with resource availability **THEN** flag conflict and present options to Project Sponsor
> **ELSE** proceed with milestone schedule

### Step 5: Assign Key Roles

| Action | Owner | SLA |
|--------|-------|-----|
| Identify and assign individuals to key project roles per RACI matrix | Business Analyst | 1 business day |

- [ ] Project Sponsor confirmed (name, title, authority level)
- [ ] Product Owner assigned (name, availability commitment)
- [ ] Business Analyst assigned (name, allocation percentage)
- [ ] Tech Lead assigned (name, allocation percentage)
- [ ] QA Lead identified (name or TBD with assignment date)
- [ ] Operations Lead identified (name or TBD with assignment date)
- [ ] Domain Expert(s) identified (names, areas of expertise)
- [ ] Role assignments confirmed with each individual's manager
- [ ] RACI matrix populated for Phase 1 activities

> **IF** key role cannot be filled **THEN** document gap and escalate to Project Sponsor for staffing decision
> **ELSE** proceed with confirmed role assignments

### Step 6: Define Communication Approach

| Action | Owner | SLA |
|--------|-------|-----|
| Establish project communication framework including channels, frequency, and audience | Business Analyst | 0.5 business days |

- [ ] Stakeholder communication needs identified (from stakeholder register)
- [ ] Status reporting frequency defined (weekly, bi-weekly, monthly per audience)
- [ ] Meeting cadence established (standup, steering committee, sponsor check-in)
- [ ] Communication channels defined (email, chat, project tool, meetings)
- [ ] Escalation path documented (level 1 through level 3)
- [ ] Decision-making process documented (who decides, how, and when)

> **IF** stakeholders require different communication formats or frequencies **THEN** create tiered communication plan by stakeholder group
> **ELSE** apply standard communication framework

### Step 7: Draft Project Charter

| Action | Owner | SLA |
|--------|-------|-----|
| Compile all elements into the formal project charter document using the approved template | Business Analyst | 1 business day |

- [ ] Project name and identifier assigned
- [ ] Project objectives section completed
- [ ] High-level scope section completed (in-scope and out-of-scope)
- [ ] Constraints section completed
- [ ] Milestone schedule included
- [ ] Key roles and responsibilities section completed
- [ ] Communication approach section completed
- [ ] Approval and sign-off section included with signature blocks
- [ ] Document formatted per project charter template
- [ ] Draft reviewed by Product Owner before sponsor presentation

> **IF** Product Owner requests material changes **THEN** revise and re-review within 1 business day
> **ELSE** proceed to sponsor sign-off

### Step 8: Obtain Sponsor Sign-Off

| Action | Owner | SLA |
|--------|-------|-----|
| Present project charter to Project Sponsor for formal authorization | Business Analyst | 1 business day |

- [ ] Charter review meeting scheduled with Project Sponsor
- [ ] Charter presented with summary of objectives, scope, constraints, and milestones
- [ ] Sponsor questions and concerns addressed
- [ ] Sponsor decision recorded (Signed / Revise / Reject)
- [ ] Formal sign-off obtained (signature, digital approval, or written confirmation)
- [ ] Signed charter distributed to all key roles
- [ ] Charter stored in designated repository

> **IF** sponsor requests revisions **THEN** revise and resubmit within 2 business days
> **ELSE IF** sponsor rejects **THEN** document rejection rationale, communicate to stakeholders, and escalate to Product Owner
> **ELSE** proceed to exit criteria

---

## EXIT CRITERIA

- [ ] Project charter completed per template with all sections populated
- [ ] Project objectives defined in SMART format
- [ ] Scope boundaries defined (in-scope and out-of-scope)
- [ ] Constraints identified and classified
- [ ] High-level milestones defined with target dates
- [ ] Key roles assigned and confirmed
- [ ] Communication approach defined
- [ ] Charter signed by Project Sponsor
- [ ] Signed charter distributed and stored in designated repository

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Project Charter | [Project Charter Template](../templates/project-charter-template.md) | `project-repo/phase-1/project-charter/` |
| RACI Matrix | [RACI Matrix Template](../templates/raci-matrix-template.md) | `project-repo/phase-1/project-charter/` |
| Milestone Schedule | [Milestone Schedule Template](../templates/milestone-schedule-template.md) | `project-repo/phase-1/project-charter/` |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Business Needs Analysis | Runbook | [RB-P1-001](./conduct-business-needs-analysis.md) |
| Business Case Development | Runbook | [RB-P1-002](./develop-business-case.md) |
| Initial Stakeholder Identification | Runbook | [RB-P1-004](./conduct-initial-stakeholder-identification.md) |
| Project Charter Template | Template | [../templates/project-charter-template.md](../templates/project-charter-template.md) |
| Phase 1 Standards | Standard | [../standards/phase-1-standards.md](../standards/phase-1-standards.md) |
