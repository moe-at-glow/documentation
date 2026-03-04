# Report and Track Defects

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P6-004 |
| **Owner** | Developer (fix), QA Lead (report/verify) |
| **Accountable** | QA Lead |
| **SLA** | Critical: 4 hours, High: 1 business day, Medium: current sprint, Low: next sprint/backlog |
| **Escalation** | Tech Lead (technical issues, reopen rate > 20%), Product Owner (severity/priority disputes) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Defect observed during testing (manual or automated)
- [ ] Access to project tracker for defect logging
- [ ] [Defect Report Template](../templates/defect-report-template.md) available

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Project tracker unavailable | STOP. Document defect offline. Submit when tracker is restored. | Tech Lead |
| Cannot determine if issue is defect or expected behavior | STOP. Consult Business Analyst or Product Owner for clarification | Product Owner |
| More than 3 critical defects in one sprint | STOP current testing. Initiate root cause analysis | Tech Lead |

---

## PROCEDURE

### Step 1: Reproduce the Defect

| Action | Owner | SLA |
|--------|-------|-----|
| Repeat the steps that caused the failure | QA Lead | 30 min |
| Verify issue occurs consistently | QA Lead | 15 min |
| Test with different test data to determine scope | QA Lead | 15 min |
| Determine if environment issue vs. code bug | QA Lead | 15 min |

- [ ] Defect reproduced at least twice
- [ ] Reproduction rate documented (e.g., "3 out of 5 attempts")
- [ ] Scope identified (single input, broad category, all inputs)

> **IF** issue is environment-related (wrong config, missing data) **THEN** fix environment, retest, do not log as code defect
> **ELSE IF** issue is intermittent **THEN** note reproduction rate in report, proceed to Step 2
> **ELSE** proceed to Step 2

### Step 2: Classify Severity

| Action | Owner | SLA |
|--------|-------|-----|
| Assign severity based on defect severity reference | QA Lead | 5 min |

| Severity | Definition | SLA | Escalation |
|----------|-----------|-----|------------|
| Critical | System unusable, data loss, security breach | 4 hours | Tech Lead + PM immediately |
| High | Major feature broken, no workaround | 1 business day | Tech Lead at triage |
| Medium | Feature broken but workaround exists | Current sprint | Standard triage |
| Low | Cosmetic or minor inconvenience | Next sprint/backlog | Standard triage |

- [ ] Severity assigned per [Defect Severity Reference](../references/defect-severity-reference.md)

> **IF** Critical **THEN** escalate to Tech Lead + PM immediately, do not wait for triage
> **ELSE IF** severity disputed **THEN** escalate to Product Owner for final decision
> **ELSE** proceed to Step 3

### Step 3: Write the Defect Report

| Action | Owner | SLA |
|--------|-------|-----|
| Complete [Defect Report Template](../templates/defect-report-template.md) with all required fields | QA Lead | 30 min |

Required fields:

- [ ] Title: clear, specific summary
- [ ] Severity: Critical / High / Medium / Low
- [ ] Environment: staging / test / local
- [ ] Steps to reproduce: exact, numbered, reproducible by anyone
- [ ] Expected result
- [ ] Actual result
- [ ] Test case reference (if applicable)

Attach where available:

- [ ] Screenshots / screen recordings
- [ ] API request/response payloads
- [ ] Error logs
- [ ] Affected component identified
- [ ] Related feature ticket linked

### Step 4: Submit the Defect

| Action | Owner | SLA |
|--------|-------|-----|
| Create defect in project tracker | QA Lead | 15 min |
| Set severity and priority | QA Lead | 5 min |
| Assign to developer or leave for triage | QA Lead | 5 min |
| Link to failing test case | QA Lead | 5 min |
| Link to related feature ticket | QA Lead | 5 min |

- [ ] Defect created in project tracker
- [ ] Severity set
- [ ] Linked to test case
- [ ] Linked to feature ticket (if applicable)

> **IF** Critical severity **THEN** assign directly to developer, notify Tech Lead immediately
> **ELSE** leave for triage

### Step 5: Triage

| Action | Owner | SLA |
|--------|-------|-----|
| Triage new defects with QA Lead | Tech Lead | 1 business day |

| Decision | Criteria |
|----------|----------|
| Fix now | Critical or High severity. Blocks release or testing. |
| Fix this sprint | Medium severity. Can be fixed alongside other work. |
| Backlog | Low severity. Not blocking. |
| Won't fix | Not a bug (expected behavior), or cost exceeds impact. |
| Duplicate | Same issue already reported. Link to original. |
| Need more info | Report incomplete. Return to reporter. |

- [ ] All new defects triaged
- [ ] Each defect has a disposition decision
- [ ] "Fix now" defects assigned to developers

> **IF** Won't Fix **THEN** document rationale, notify reporter
> **ELSE IF** Need More Info **THEN** return to reporter with specific questions
> **ELSE IF** Duplicate **THEN** link to original defect, close as duplicate

### Step 6: Track Progress

| Action | Owner | SLA |
|--------|-------|-----|
| Monitor defect lifecycle status transitions | QA Lead | Daily |
| Verify SLA compliance per severity | QA Lead | Daily |

Defect lifecycle: `New > Triaged > Assigned > In Progress > Fixed > Re-test > Closed`

| Status | Set By | Meaning |
|--------|--------|---------|
| New | QA (reporter) | Just reported, not yet reviewed |
| Triaged | Tech Lead / QA Lead | Severity confirmed, decision made |
| Assigned | Tech Lead | Developer assigned to fix |
| In Progress | Developer | Fix being implemented |
| Fixed | Developer | Fix implemented and pushed |
| Re-test | QA | Ready for QA verification |
| Closed | QA | Fix verified, defect resolved |
| Reopened | QA | Fix did not work, issue persists |
| Won't Fix | Tech Lead | Decision to not fix, with rationale |
| Duplicate | QA / Tech Lead | Same as another defect (linked) |

- [ ] All defects progressing through lifecycle
- [ ] Critical defects within 4-hour SLA
- [ ] High defects within 1 business day SLA

> **IF** Critical defect not fixed within 4 hours **THEN** escalate to Tech Lead + PM
> **ELSE IF** defect reopen rate > 20% **THEN** escalate to Tech Lead for process review
> **ELSE** continue monitoring

### Step 7: Re-Test Fixed Defects

| Action | Owner | SLA |
|--------|-------|-----|
| Deploy fix to test environment | Developer / DevOps | 30 min |
| Execute original reproduction steps | QA Lead | 30 min |
| Verify expected result now occurs | QA Lead | 15 min |
| Run related regression tests | QA Lead | 1 hour |

- [ ] Fix deployed to test environment
- [ ] Original reproduction steps pass
- [ ] Expected result confirmed
- [ ] Related regression tests pass

> **IF** fix resolves defect and regression passes **THEN** close defect with verification note
> **ELSE IF** fix does not resolve defect **THEN** reopen with explanation of what still fails
> **ELSE IF** fix introduces new issue **THEN** log new defect, link to original

---

## EXIT CRITERIA

- [ ] Defect reproduced and confirmed
- [ ] Severity classified per defect severity reference
- [ ] Defect report complete with all required fields
- [ ] Steps to reproduce are clear and numbered
- [ ] Defect submitted to project tracker
- [ ] Triaged and assigned
- [ ] Fix verified through re-testing
- [ ] Related regression tests passed
- [ ] Defect closed with verification note

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Defect Report | [defect-report-template.md](../templates/defect-report-template.md) | Project tracker |
| Defect Metrics (per sprint/release) | N/A | Project tracker dashboard |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Defect Severity Reference | Reference | [../references/defect-severity-reference.md](../references/defect-severity-reference.md) |
| Defect Report Template | Template | [../templates/defect-report-template.md](../templates/defect-report-template.md) |
| Testing Strategy Standard | Standard | [../standards/testing-strategy-standard.md](../standards/testing-strategy-standard.md) |
| Test Case Template | Template | [../templates/test-case-template.md](../templates/test-case-template.md) |
