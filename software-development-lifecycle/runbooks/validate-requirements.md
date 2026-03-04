# Validate Requirements

Step-by-step procedure for validating requirements before establishing the baseline.

---

## Prerequisites

- Draft SRS with all software requirements documented.
- Requirements Traceability Matrix populated.
- All requirement authors and key stakeholders available for review.

---

## Procedure

### Step 1: Check Completeness

Verify that all business needs are covered:

1. Review each business requirement in the BRD.
2. Confirm it has at least one stakeholder requirement, one system requirement, and one software requirement tracing to it.
3. Check the RTM for gaps (business requirements with no downstream trace).
4. Document any gaps found.

| Check | Pass Criteria |
|-------|--------------|
| Every BR has at least one SWR | No orphan business requirements |
| All non-functional categories addressed | Performance, Security, Usability, Reliability, Scalability covered |
| All system interfaces documented | Every external system has interface requirements |
| All user roles have requirements | Every actor has at least one use case or user story |

### Step 2: Check Consistency

Verify that no requirements contradict each other:

1. Group requirements by feature area.
2. Review each group for conflicting statements.
3. Cross-check non-functional requirements (e.g., a performance requirement vs. a security requirement that adds latency).
4. Flag all conflicts.

| Check | Pass Criteria |
|-------|--------------|
| No contradictory functional requirements | No two requirements define conflicting behavior for the same scenario |
| Non-functional requirements are compatible | Security controls do not make performance targets impossible |
| Priority assignments are consistent | A Should Have requirement does not depend on a Could Have requirement |

### Step 3: Check Feasibility

Verify that each requirement can be implemented:

1. Tech Lead reviews all Must Have and Should Have requirements.
2. For each requirement, confirm:
   - Technology exists to implement it.
   - It can be delivered within the project timeline.
   - It does not exceed known infrastructure constraints.
3. Flag infeasible requirements for renegotiation with Product Owner.

### Step 4: Check Testability

Verify that each requirement can be tested:

1. QA Lead reviews every software requirement.
2. For each requirement, confirm:
   - Acceptance criteria exist and are measurable.
   - A pass/fail test can be written.
   - Test data and test environments can be provisioned.
3. Flag untestable requirements for rework.

| Check | Pass Criteria |
|-------|--------------|
| Acceptance criteria present | Every SWR has at least one acceptance criterion |
| Criteria are measurable | No subjective terms ("fast", "easy", "user-friendly") without quantification |
| Test approach identified | Manual test, automated test, or inspection method defined |

### Step 5: Conduct Requirements Review Meeting

**Attendees:** Project Sponsor, Product Owner, Business Analyst, Tech Lead, QA Lead, Domain Expert(s).

**Agenda:**

| Time | Activity |
|------|----------|
| 0:00 | Review objectives and ground rules |
| 0:10 | Present validation findings (Steps 1-4) |
| 0:30 | Walk through each flagged issue |
| 1:00 | Break |
| 1:10 | Resolve conflicts and ambiguities |
| 1:40 | Agree on action items and owners |
| 1:50 | Confirm requirements ready for baseline (or identify rework needed) |
| 2:00 | Close |

### Step 6: Resolve Conflicts and Ambiguities

For each issue identified:

1. Document the conflict or ambiguity.
2. Identify affected stakeholders.
3. Facilitate discussion to reach agreement.
4. If no agreement, escalate to Product Owner for decision.
5. Record the resolution and rationale.

### Step 7: Update Requirements

1. Apply all resolutions from Step 6.
2. Rework any requirements flagged as untestable, infeasible, or ambiguous.
3. Update the RTM to reflect changes.
4. Re-run checks from Steps 1-4 on modified requirements.

### Step 8: Obtain Baseline Approval

1. Present the validated SRS to the approval authority.
2. Confirm all validation checks pass.
3. Obtain written sign-off from:
   - Product Owner (business validity)
   - Tech Lead (technical feasibility)
   - QA Lead (testability)
4. Record the baseline version number and date.

### Step 9: Establish Requirements Baseline

1. Mark the SRS version as the official baseline.
2. Mark all approved requirements as status: **Approved**.
3. Lock the baseline. All future changes follow the [change management process](manage-requirements-changes.md).
4. Distribute the baselined SRS to all project team members.

---

## Output Artifacts

- Requirements Validation Report
- Updated SRS (baselined version)
- Updated RTM
- Review meeting minutes
- Baseline sign-off record

---

## Validation Checklist

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
