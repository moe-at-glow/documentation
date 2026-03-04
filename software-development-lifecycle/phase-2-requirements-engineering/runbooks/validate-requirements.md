# Validate Requirements

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P2-004 |
| **Owner** | Business Analyst + Tech Lead + QA Lead |
| **Accountable** | Product Owner |
| **SLA** | 10 business days |
| **Escalation** | Product Owner |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Draft SRS with all software requirements documented (RB-P2-003 exit criteria met)
- [ ] Requirements Traceability Matrix populated
- [ ] All requirement authors available for review
- [ ] Key stakeholders available for review meeting
- [ ] QA Lead assigned and available

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Draft SRS not complete | STOP. Complete RB-P2-003 first. | Tech Lead |
| RTM not populated | STOP. Complete traceability links first. | Business Analyst |
| More than 50% of requirements fail validation checks | STOP. Return to RB-P2-003 for major rework. | Tech Lead |
| Key review attendees unavailable for 10+ business days | STOP. Request schedule intervention. | Product Owner |

---

## PROCEDURE

### Step 1: Check Completeness

| Action | Owner | SLA |
|--------|-------|-----|
| Review each BR in the BRD and confirm downstream traceability exists | Business Analyst | 1 day |
| Check RTM for gaps | Business Analyst | 0.5 day |
| Document all gaps found | Business Analyst | 0.5 day |

- [ ] Every BR has at least one SWR (no orphan business requirements)
- [ ] All non-functional categories addressed (Performance, Security, Usability, Reliability, Scalability)
- [ ] All system interfaces documented (every external system has interface requirements)
- [ ] All user roles have requirements (every actor has at least one use case or user story)

> **IF** gaps found **THEN** log gap details; continue to Step 2 (resolve in Step 6)
> **ELSE** proceed to Step 2

### Step 2: Check Consistency

| Action | Owner | SLA |
|--------|-------|-----|
| Group requirements by feature area | Business Analyst | 0.5 day |
| Review each group for conflicting statements | Business Analyst + Tech Lead | 1 day |
| Cross-check NFRs for compatibility | Tech Lead | 0.5 day |
| Flag all conflicts | Business Analyst | 0.5 day |

- [ ] No contradictory functional requirements (no two requirements define conflicting behavior for same scenario)
- [ ] Non-functional requirements are compatible (security controls do not make performance targets impossible)
- [ ] Priority assignments are consistent (no Should Have depending on a Could Have)

> **IF** conflicts found **THEN** log conflict details; continue to Step 3 (resolve in Step 6)
> **ELSE** proceed to Step 3

### Step 3: Check Feasibility

| Action | Owner | SLA |
|--------|-------|-----|
| Review all Must Have and Should Have requirements for implementability | Tech Lead | 1 day |

- [ ] Technology exists to implement each requirement
- [ ] Each requirement deliverable within project timeline
- [ ] No requirement exceeds known infrastructure constraints

> **IF** infeasible requirements found **THEN** flag for renegotiation with Product Owner; continue to Step 4
> **ELSE** proceed to Step 4

### Step 4: Check Testability

| Action | Owner | SLA |
|--------|-------|-----|
| Review every SWR for testability | QA Lead | 1 day |

- [ ] Every SWR has at least one acceptance criterion
- [ ] No subjective terms without quantification ("fast", "easy", "user-friendly")
- [ ] Test approach identified for each SWR (manual test, automated test, or inspection)
- [ ] Test data and test environments can be provisioned

> **IF** untestable requirements found **THEN** flag for rework; continue to Step 5
> **ELSE** proceed to Step 5

### Step 5: Conduct Requirements Review Meeting

| Action | Owner | SLA |
|--------|-------|-----|
| Schedule and facilitate review meeting | Business Analyst | 1 day |

**Attendees:** Project Sponsor, Product Owner, Business Analyst, Tech Lead, QA Lead, Domain Expert(s)

- [ ] Meeting agenda followed:

| Time | Activity |
|------|----------|
| 0:00 | State review objectives and ground rules |
| 0:10 | Present validation findings (Steps 1-4) |
| 0:30 | Walk through each flagged issue |
| 1:00 | Break |
| 1:10 | Resolve conflicts and ambiguities |
| 1:40 | Agree on action items and owners |
| 1:50 | Confirm requirements ready for baseline (or identify rework needed) |
| 2:00 | Close |

- [ ] All flagged issues presented
- [ ] Meeting minutes recorded
- [ ] Action items assigned with owners and deadlines

> **IF** rework needed **THEN** proceed to Step 6
> **ELSE IF** requirements ready for baseline **THEN** skip to Step 8
> **ELSE** proceed to Step 6

### Step 6: Resolve Conflicts and Ambiguities

| Action | Owner | SLA |
|--------|-------|-----|
| Document each conflict or ambiguity | Business Analyst | 0.5 day |
| Identify affected stakeholders per issue | Business Analyst | 0.5 day |
| Facilitate discussion to reach agreement | Business Analyst | 1 day |
| Record resolution and rationale | Business Analyst | 0.5 day |

- [ ] Each issue documented
- [ ] Affected stakeholders identified
- [ ] Agreement reached for each issue
- [ ] Resolution and rationale recorded

> **IF** no agreement reached **THEN** escalate to Product Owner for final decision
> **ELSE** proceed to Step 7

### Step 7: Update Requirements

| Action | Owner | SLA |
|--------|-------|-----|
| Apply all resolutions from Step 6 | Business Analyst | 1 day |
| Rework requirements flagged as untestable, infeasible, or ambiguous | Business Analyst + Tech Lead | 1 day |
| Update RTM to reflect changes | Business Analyst | 0.5 day |
| Re-run checks from Steps 1-4 on modified requirements | Business Analyst + Tech Lead + QA Lead | 1 day |

- [ ] All resolutions applied
- [ ] Flagged requirements reworked
- [ ] RTM updated
- [ ] Validation checks re-run on modified requirements
- [ ] All re-run checks pass

> **IF** re-run checks fail **THEN** return to Step 6 for affected requirements
> **ELSE** proceed to Step 8

### Step 8: Obtain Baseline Approval

| Action | Owner | SLA |
|--------|-------|-----|
| Present validated SRS to approval authority | Business Analyst | 0.5 day |
| Confirm all validation checks pass | Business Analyst | During presentation |
| Obtain written sign-off from Product Owner (business validity) | Product Owner | 1 day |
| Obtain written sign-off from Tech Lead (technical feasibility) | Tech Lead | 1 day |
| Obtain written sign-off from QA Lead (testability) | QA Lead | 1 day |
| Record baseline version number and date | Business Analyst | 0.5 day |

- [ ] Validated SRS presented
- [ ] All validation checks confirmed passing
- [ ] Product Owner sign-off obtained
- [ ] Tech Lead sign-off obtained
- [ ] QA Lead sign-off obtained
- [ ] Baseline version number and date recorded

> **IF** approver requests changes during sign-off **THEN** return to Step 7
> **ELSE** proceed to Step 9

### Step 9: Establish Requirements Baseline

| Action | Owner | SLA |
|--------|-------|-----|
| Mark SRS version as official baseline | Business Analyst | 0.5 day |
| Set all approved requirements to status: Approved | Business Analyst | 0.5 day |
| Lock the baseline | Business Analyst | 0.5 day |
| Distribute baselined SRS to all project team members | Business Analyst | 0.5 day |

- [ ] SRS version marked as official baseline
- [ ] All requirements set to Approved status
- [ ] Baseline locked (all future changes follow [change management process](manage-requirements-changes.md))
- [ ] Baselined SRS distributed to project team

---

## EXIT CRITERIA

- [ ] Completeness check passed (all BRs traced to SWRs)
- [ ] Consistency check passed (no contradictions)
- [ ] Feasibility check passed (all requirements achievable)
- [ ] Testability check passed (all requirements have measurable acceptance criteria)
- [ ] Requirements review meeting conducted
- [ ] All conflicts and ambiguities resolved
- [ ] Requirements updated based on review outcomes
- [ ] Validation checks re-run on modified requirements
- [ ] Baseline approval obtained (Product Owner, Tech Lead, QA Lead)
- [ ] Baseline established and distributed

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Requirements Validation Report | -- | Project documentation repository |
| Updated SRS (baselined version) | [software-requirements-specification.md](../templates/software-requirements-specification.md) | Project documentation repository |
| Updated RTM | [requirements-traceability-matrix.md](../templates/requirements-traceability-matrix.md) | Project documentation repository |
| Review Meeting Minutes | -- | Project documentation repository |
| Baseline Sign-Off Record | -- | Project documentation repository |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| SRS Template | Template | [../templates/software-requirements-specification.md](../templates/software-requirements-specification.md) |
| RTM Template | Template | [../templates/requirements-traceability-matrix.md](../templates/requirements-traceability-matrix.md) |
| Requirements Engineering Standard | Standard | [../standards/requirements-engineering-standard.md](../standards/requirements-engineering-standard.md) |
| Requirements Traceability Standard | Standard | [../standards/requirements-traceability.md](../standards/requirements-traceability.md) |
| Derive Software Requirements | Runbook | [derive-software-requirements.md](derive-software-requirements.md) |
| Manage Requirements Changes | Runbook | [manage-requirements-changes.md](manage-requirements-changes.md) |
