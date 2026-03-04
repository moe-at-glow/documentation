# Conduct Code Review

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P5-003 |
| **Owner** | Developer (Reviewer) |
| **Accountable** | Tech Lead |
| **SLA** | 4 hours from PR submission to first review |
| **Escalation** | Tech Lead (technical disagreements), Product Owner (scope/requirement disputes) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Pull request submitted with completed [PR template](../templates/pull-request-template.md)
- [ ] PR description includes: what changed, why, and how it was tested
- [ ] CI pipeline passing on the PR branch
- [ ] Reviewer is not the PR author

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| PR description missing or incomplete | STOP. Request author to complete PR template. | Tech Lead |
| CI pipeline failing on PR branch | STOP. Return to author to fix build. | Tech Lead |
| No related design document exists for significant changes | STOP. Request DDD before reviewing. | Tech Lead |
| Reviewer has conflict of interest | STOP. Assign alternate reviewer. | Tech Lead |

---

## PROCEDURE

### Step 1: Read PR Description and Linked Ticket

| Action | Owner | SLA |
|--------|-------|-----|
| Read PR title, description, and linked ticket | Reviewer | 15 min |
| Verify PR description completeness | Reviewer | 5 min |

- [ ] PR title is clear and descriptive
- [ ] What changed is documented
- [ ] Why it changed is documented
- [ ] How it was tested is documented
- [ ] Linked ticket identified

> **IF** PR description is incomplete **THEN** request author to update before proceeding
> **ELSE** proceed to Step 2

### Step 2: Review Related Design Document

| Action | Owner | SLA |
|--------|-------|-----|
| Open related DDD or API spec | Reviewer | 10 min |
| Note expected behavior, data model, and error handling | Reviewer | 15 min |

- [ ] Design document located and reviewed
- [ ] Expected behavior noted
- [ ] Data model understood
- [ ] Error handling expectations identified

> **IF** no design document exists for a minor change **THEN** review against ticket acceptance criteria only
> **ELSE IF** no design document exists for a significant change **THEN** STOP. Escalate to Tech Lead.
> **ELSE** proceed to Step 3

### Step 3: Review the Diff

| Action | Owner | SLA |
|--------|-------|-----|
| Review test files first | Reviewer | 20 min |
| Review implementation files against tests and design | Reviewer | 30 min |
| Review configuration and infrastructure changes | Reviewer | 15 min |

- [ ] Tests reviewed first (understand expected behavior)
- [ ] Implementation matches test expectations and design
- [ ] Configuration/migration/CI changes reviewed

### Step 4: Check Against Review Criteria

| Action | Owner | SLA |
|--------|-------|-----|
| Evaluate code against [Code Review Checklist](../templates/code-review-checklist.md) | Reviewer | 30 min |

**Correctness:**
- [ ] Code does what the design specifies
- [ ] All edge cases from the design handled
- [ ] Acceptance criteria from the SRS satisfied

**Security:**
- [ ] Input validation at boundaries
- [ ] Parameterized queries (no SQL injection)
- [ ] Auth checks on protected endpoints
- [ ] No secrets in code

**Performance:**
- [ ] No N+1 queries
- [ ] Pagination on list endpoints
- [ ] Appropriate use of indexes

**Testability:**
- [ ] Unit tests present and meaningful
- [ ] Tests cover happy path and error cases
- [ ] Coverage meets threshold

**Standards:**
- [ ] Naming follows conventions
- [ ] Error handling follows standard pattern
- [ ] Logging follows guidelines

> **IF** critical security issue found **THEN** mark as blocking and escalate to Tech Lead immediately
> **ELSE IF** blocking issues found **THEN** request changes with clear explanation
> **ELSE** proceed to Step 5

### Step 5: Write Review Feedback

| Action | Owner | SLA |
|--------|-------|-----|
| Write comments with severity prefix | Reviewer | 20 min |
| Provide alternatives for blocking issues | Reviewer | 10 min |

- [ ] Blocking feedback prefixed with `[blocking]`
- [ ] Suggestions prefixed with `[suggestion]` or `[nit]`
- [ ] Each comment explains "why" (not just "fix this")
- [ ] Alternatives offered for blocking issues

### Step 6: Submit Review Decision

| Action | Owner | SLA |
|--------|-------|-----|
| Select review decision and submit | Reviewer | 5 min |

| Decision | When to Use |
|----------|-------------|
| **Approve** | No blocking issues. Code is ready to merge. |
| **Request Changes** | One or more blocking issues. Must be fixed before merge. |
| **Comment** | Questions or observations only. Not blocking. |

- [ ] Review decision submitted

> **IF** Approve **THEN** notify author; procedure complete
> **ELSE IF** Request Changes **THEN** proceed to Step 7
> **ELSE** notify author; await response

### Step 7: Follow Up on Requested Changes

| Action | Owner | SLA |
|--------|-------|-----|
| Verify blocking feedback was addressed | Reviewer | 2 hours |
| Re-review changed code | Reviewer | 30 min |
| Approve when all blocking issues resolved | Reviewer | 5 min |

- [ ] All blocking comments resolved
- [ ] Changed code re-reviewed
- [ ] Final approval submitted

> **IF** author disagrees with blocking feedback **THEN** discuss; escalate to Tech Lead if unresolved
> **ELSE** approve when satisfied

---

## EXIT CRITERIA

- [ ] All files in PR reviewed
- [ ] Code Review Checklist completed (correctness, security, performance, testability, standards)
- [ ] All feedback written with clear severity
- [ ] Review decision submitted
- [ ] All blocking issues resolved (if any)
- [ ] Final approval given

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Review comments | N/A | GitHub PR |
| Review decision (Approve/Request Changes) | N/A | GitHub PR |
| Completed code review checklist | [Code Review Checklist](../templates/code-review-checklist.md) | GitHub PR |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Code Review Checklist | Template | [../templates/code-review-checklist.md](../templates/code-review-checklist.md) |
| Pull Request Template | Template | [../templates/pull-request-template.md](../templates/pull-request-template.md) |
| Code Review Standard | Standard | [../standards/code-review-standard.md](../standards/code-review-standard.md) |
| Coding Standards | Standard | [../standards/coding-standards.md](../standards/coding-standards.md) |
| Implement Feature | Runbook | [./implement-feature.md](./implement-feature.md) |
