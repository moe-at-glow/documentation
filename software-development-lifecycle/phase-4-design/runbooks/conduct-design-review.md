# Conduct Design Review

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P4-004 |
| **Owner** | Developer |
| **Accountable** | Tech Lead |
| **SLA** | 5 business days (3 days pre-read + 2 days review/disposition) |
| **Escalation** | Tech Lead (technical), Product Owner (scope) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Detailed Design Document complete for the component
- [ ] API specification complete (if component exposes APIs)
- [ ] Data model complete (if component owns data)
- [ ] Design Review Checklist template obtained
- [ ] All reviewers identified and available

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| DDD incomplete or missing sections | STOP. Return to designer for completion | Tech Lead |
| Required reviewer unavailable within SLA | STOP. Reschedule or assign delegate | Tech Lead |
| Architecture has changed since design started | STOP. Assess impact on design | Tech Lead |
| Scope change invalidates design | STOP. Re-scope before reviewing | Product Owner |

---

## PROCEDURE

### Step 1: Distribute Review Materials

| Action | Owner | SLA |
|--------|-------|-----|
| Distribute DDD, API spec, data model, and design review checklist to all reviewers | Developer | 1 hour |
| Confirm receipt from all reviewers | Developer | 1 business day |

Required reviewers:

| Reviewer | Focus Area |
|----------|------------|
| Tech Lead | Architecture adherence, patterns, feasibility, naming conventions |
| Senior Developer | Implementation complexity, testability, maintainability |
| QA Lead | Testability, edge case coverage, acceptance criteria alignment |
| Frontend Developer (if API) | API usability, response format, error handling |

- [ ] DDD distributed to all reviewers
- [ ] API specification distributed (if applicable)
- [ ] Data model distributed (if applicable)
- [ ] Design Review Checklist distributed
- [ ] All reviewers confirmed receipt
- [ ] Review meeting scheduled minimum 3 business days after distribution

> **IF** reviewer cannot attend **THEN** assign delegate with same focus area, get Tech Lead approval
> **ELSE IF** documents updated after distribution **THEN** redistribute and reset 3-day pre-read period
> **ELSE** proceed to Step 2

### Step 2: Conduct Review Meeting

| Action | Owner | SLA |
|--------|-------|-----|
| Present component overview and context | Developer | 10 min |
| Walk through public interface | Developer | 10 min |
| Walk through internal structure and business logic | Developer | 15 min |
| Walk through data model | Developer | 10 min |
| Walk through error handling and edge cases | Developer | 10 min |
| Review against Design Review Checklist | All Reviewers | 10 min |
| Discuss findings and action items | All Reviewers | 10 min |
| Record decision | Tech Lead | 10 min |

- [ ] All agenda items covered
- [ ] All reviewers provided input
- [ ] Findings documented with severity (blocking, major, minor)
- [ ] Action items assigned with owner and due date
- [ ] Meeting duration: 1 to 1.5 hours per component

> **IF** meeting exceeds 1.5 hours **THEN** table remaining items, schedule follow-up within 2 business days
> **ELSE** proceed to Step 3

### Step 3: Evaluate Using Design Review Checklist

| Action | Owner | SLA |
|--------|-------|-----|
| Complete every item in the Design Review Checklist | All Reviewers | During meeting |
| Record pass/fail/NA per checklist item | Tech Lead | During meeting |

- [ ] Every checklist item evaluated
- [ ] Each item marked pass, fail, or N/A
- [ ] Failed items documented as findings

### Step 4: Record Decision

| Action | Owner | SLA |
|--------|-------|-----|
| Determine review outcome based on findings | Tech Lead | End of meeting |

| Decision | Criteria | Next Action |
|----------|----------|-------------|
| Approved | All checklist items pass. Zero blocking issues. | Proceed to Step 5 (post-review) |
| Approved with conditions | Minor items to address. No blocking issues. | Proceed to Step 5, fix items in parallel |
| Rework required | Blocking issues found. | Return to designer, re-review after fixes |

- [ ] Decision recorded with rationale
- [ ] All reviewers acknowledge decision

> **IF** decision is "Approved" **THEN** proceed to Step 5
> **ELSE IF** decision is "Approved with conditions" **THEN** proceed to Step 5, track conditions as action items
> **ELSE IF** decision is "Rework required" **THEN** designer addresses blocking findings, re-submit for review (return to Step 1)

### Step 5: Complete Post-Review Actions

| Action | Owner | SLA |
|--------|-------|-----|
| Address all findings from review | Developer | 2 business days |
| Verify fixes for blocking and major findings | Tech Lead | 1 business day |
| Mark approved design as baseline | Tech Lead | 1 hour |
| Update RTM with design references | Developer | 2 hours |

- [ ] All findings addressed
- [ ] Blocking/major fixes verified by Tech Lead
- [ ] Design marked as baseline
- [ ] RTM updated with design document references

> **IF** fixes introduce new concerns **THEN** schedule follow-up review for affected sections only
> **ELSE** design review complete

---

## EXIT CRITERIA

- [ ] All review documents distributed and pre-read period completed
- [ ] Review meeting conducted with all required reviewers
- [ ] Every Design Review Checklist item evaluated
- [ ] All findings documented with severity, owner, and due date
- [ ] Decision recorded (Approved / Approved with conditions / Rework required)
- [ ] All findings addressed by designer
- [ ] Fixes verified by Tech Lead
- [ ] Design baselined
- [ ] RTM updated with design references

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Completed Design Review Checklist | [Design Review Checklist](../templates/design-review-checklist.md) | Project repository /docs/reviews/ |
| Review Findings Log | -- | Project repository /docs/reviews/ |
| Updated RTM | -- | Project repository /docs/traceability/ |
| Baselined Design Documents | -- | Project repository /docs/design/ |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Detailed Design Standard | Standard | [../standards/detailed-design-standard.md](../standards/detailed-design-standard.md) |
| API Design Standard | Standard | [../standards/api-design-standard.md](../standards/api-design-standard.md) |
| Database Design Standard | Standard | [../standards/database-design-standard.md](../standards/database-design-standard.md) |
| Design Review Checklist | Template | [../templates/design-review-checklist.md](../templates/design-review-checklist.md) |
| DDD Template | Template | [../templates/detailed-design-document.md](../templates/detailed-design-document.md) |
| Create Detailed Design | Runbook | [create-detailed-design.md](create-detailed-design.md) |
| Design API Contracts | Runbook | [design-api-contracts.md](design-api-contracts.md) |
| Design Data Models | Runbook | [design-data-models.md](design-data-models.md) |
