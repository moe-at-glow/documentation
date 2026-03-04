# Conduct Architecture Review

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P3-002 |
| **Owner** | Tech Lead |
| **Accountable** | Tech Lead |
| **SLA** | 5 business days (end-to-end including follow-up) |
| **Escalation** | Project Sponsor (scope issues), Product Owner (priority conflicts) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Draft Architecture Description Document (ADD) complete with all viewpoints
- [ ] All ADRs written and in Proposed status
- [ ] ADD distributed to reviewers at least 5 business days before review meeting
- [ ] All required attendees confirmed

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| ADD missing one or more viewpoints | STOP. Return ADD to architect for completion. | Tech Lead |
| Fewer than 4 of 6 required attendees available | STOP. Reschedule review meeting. | Tech Lead |
| ADRs not written | STOP. Complete ADRs before scheduling review. | Tech Lead |
| ADD not distributed 5 days in advance | STOP. Redistribute and reschedule. | Tech Lead |

---

## PROCEDURE

### Step 1: Distribute Review Materials

| Action | Owner | SLA |
|--------|-------|-----|
| Distribute draft ADD, all ADRs, and review checklist to all attendees | Tech Lead | 1 hour |
| Request each reviewer to read ADD and prepare written questions/concerns | Tech Lead | At distribution |
| Collect pre-review feedback from all reviewers | Tech Lead | 2 days before meeting |
| Prepare responses to pre-review feedback | System Architect | 1 day before meeting |

Required attendees:

| Role | Purpose |
|------|---------|
| System Architect | Present and defend the architecture |
| Tech Lead | Evaluate feasibility and implementation impact |
| Product Owner | Confirm business requirements coverage |
| Infrastructure Engineer | Evaluate deployment feasibility and infrastructure needs |
| QA Lead | Evaluate testability and test infrastructure needs |
| Senior Developer(s) | Evaluate development view and technology choices |

- [ ] ADD distributed to all attendees
- [ ] Review checklist distributed
- [ ] All ADRs distributed
- [ ] Pre-review feedback collected
- [ ] Architect responses prepared

### Step 2: Conduct Review Meeting

| Action | Owner | SLA |
|--------|-------|-----|
| Open meeting: state objectives and review criteria | Tech Lead | 10 min |
| Present System Context View | System Architect | 15 min |
| Facilitate discussion on system boundaries | Tech Lead | 15 min |
| Present Logical View | System Architect | 20 min |
| Facilitate discussion on component decomposition and interfaces | Tech Lead | 20 min |
| Break | -- | 10 min |
| Present Process, Deployment, and Development Views | System Architect | 30 min |
| Facilitate discussion on runtime behavior, infrastructure, code organization | Tech Lead | 15 min |
| Walk through ADRs and key technology decisions | System Architect | 15 min |
| Facilitate discussion on quality attributes (performance, security, scalability) | Tech Lead | 15 min |
| Summarize findings, action items, and decision | Tech Lead | 15 min |

- [ ] All five viewpoints presented
- [ ] All ADRs reviewed
- [ ] All attendee questions addressed or recorded as action items

### Step 3: Evaluate Against Criteria

| Action | Owner | SLA |
|--------|-------|-----|
| Assess each evaluation criterion and record Pass/Fail | All reviewers | During meeting |

| Criterion | Pass/Fail |
|-----------|-----------|
| Conceptual Integrity -- consistent principles, uniform patterns | |
| Completeness -- all ASRs addressed, all external interfaces shown, all components defined | |
| Consistency with Requirements -- every requirement traces to an architecture element | |
| Feasibility -- buildable with available skills and timeline, mature technology choices | |
| Quality Attribute Coverage -- documented approach for performance, security, scalability, reliability | |
| Risk Identification -- risks identified and mitigated, single points of failure addressed | |
| Testability -- each component testable independently, test environments feasible | |
| Deployability -- deployment topology clear, automatable | |
| Maintainability -- components loosely coupled, data ownership clear | |

- [ ] All 9 criteria assessed
- [ ] Pass/Fail recorded for each criterion

### Step 4: Evaluate Quality Attribute Scenarios

| Action | Owner | SLA |
|--------|-------|-----|
| Evaluate one scenario per critical quality attribute (Performance, Security, Scalability, Reliability) | All reviewers | During meeting |

For each scenario, record:
- [ ] Scenario described (stimulus, expected response)
- [ ] Architecture response documented
- [ ] Verdict recorded (Adequate / Needs improvement)

> **IF** verdict is "Needs improvement" **THEN** record as Concern or Blocker in Step 5
> **ELSE** proceed

### Step 5: Document Findings

| Action | Owner | SLA |
|--------|-------|-----|
| Categorize all findings into Blocker, Concern, or Observation | Tech Lead | 1 hour post-meeting |

| Category | Definition | Required Action |
|----------|-----------|-----------------|
| Blocker | Fundamental flaw preventing requirements from being met | Must fix before approval |
| Concern | Issue to address but does not block approval | Must address before Phase 4 |
| Observation | Suggestion for improvement, not required | Architect decides |

- [ ] All findings categorized
- [ ] Each finding has assigned owner and due date

### Step 6: Record Decision

| Action | Owner | SLA |
|--------|-------|-----|
| Record formal review decision | Tech Lead | Immediately after Step 5 |

| Decision | Criteria |
|----------|----------|
| Approved | Zero blockers, all evaluation criteria pass |
| Approved with Conditions | Zero blockers, 1-3 concerns with defined resolution timeline |
| Rework Required | One or more blockers exist |

- [ ] Decision recorded

> **IF** Approved **THEN** proceed to Step 7 (post-review)
> **ELSE IF** Approved with Conditions **THEN** proceed to Step 7; track conditions as action items
> **ELSE** return to architect for rework; schedule re-review (1 hour, blockers only)

### Step 7: Complete Post-Review Follow-Up

| Action | Owner | SLA |
|--------|-------|-----|
| Address all blockers and concerns | System Architect | 3 business days |
| Redistribute updated ADD | Tech Lead | 1 day after fixes |
| Schedule focused re-review if rework was required (1 hour, blockers only) | Tech Lead | Within 2 business days |
| Update all ADR statuses from Proposed to Accepted | Tech Lead | 1 hour |
| Distribute approved ADD to full project team | Tech Lead | 1 day |

- [ ] All blockers resolved
- [ ] All concerns resolved or tracked
- [ ] Updated ADD redistributed (if applicable)
- [ ] Re-review completed (if rework was required)
- [ ] All ADR statuses changed to Accepted
- [ ] Approved ADD distributed to full project team

---

## EXIT CRITERIA

- [ ] Review meeting conducted with all required attendees
- [ ] All 9 evaluation criteria assessed with Pass/Fail
- [ ] Quality attribute scenarios evaluated
- [ ] All findings documented and categorized
- [ ] Formal decision recorded (Approved / Approved with Conditions / Rework)
- [ ] All blockers and concerns resolved
- [ ] ADR statuses updated to Accepted
- [ ] Approved ADD distributed to project team

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Architecture Review Record (findings, decision, action items) | -- | `architecture/reviews/` |
| Updated ADD (if conditions or rework applied) | [ADD Template](../templates/architecture-description-document.md) | `architecture/` |
| Approved ADRs (status changed to Accepted) | [ADR Template](../templates/architecture-decision-record.md) | `architecture/decisions/` |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Architecture Description Standard | Standard | [../standards/architecture-description-standard.md](../standards/architecture-description-standard.md) |
| ADR Standard | Standard | [../standards/architecture-decision-records-standard.md](../standards/architecture-decision-records-standard.md) |
| ADD Template | Template | [../templates/architecture-description-document.md](../templates/architecture-description-document.md) |
| ADR Template | Template | [../templates/architecture-decision-record.md](../templates/architecture-decision-record.md) |
| Create Architecture Description | Runbook | [create-architecture-description.md](create-architecture-description.md) |
| Write Architecture Decision Record | Runbook | [write-architecture-decision-record.md](write-architecture-decision-record.md) |
