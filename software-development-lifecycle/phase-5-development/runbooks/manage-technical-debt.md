# Manage Technical Debt

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P5-004 |
| **Owner** | Developer |
| **Accountable** | Tech Lead |
| **SLA** | Identification: 1 day; Resolution: per sprint plan |
| **Escalation** | Tech Lead (prioritization disputes), Product Owner (capacity allocation) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Technical debt item identified from one of: code review, retrospective, bug investigation, dependency audit, performance monitoring, or new feature difficulty
- [ ] Access to [Technical Debt Register](../templates/technical-debt-register.md)
- [ ] Project tracker access for ticket creation

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Debt item is actually a bug (user-facing defect) | STOP. Log as bug, not technical debt. Follow bug fix process. | Tech Lead |
| Debt resolution requires architectural change with no DDD | STOP. Request design review before proceeding. | Tech Lead |
| Debt fix would consume >50% of sprint capacity | STOP. Seek Product Owner approval for capacity allocation. | Product Owner |

---

## PROCEDURE

### Step 1: Identify Technical Debt

| Action | Owner | SLA |
|--------|-------|-----|
| Capture debt item from discovery source | Developer | 1 hour |
| Document what the debt is and why it exists | Developer | 30 min |

| Source | When |
|--------|------|
| Code review | Reviewer identifies shortcuts or design issues |
| Sprint retrospective | Team discusses recurring pain points |
| Bug investigation | Root cause reveals structural issue |
| Dependency audit | `npm audit` or manual review finds outdated/vulnerable packages |
| Performance monitoring | Slow queries, high memory usage, timeout patterns |
| New feature difficulty | Simple feature requires disproportionate effort |

- [ ] Debt item captured with clear description
- [ ] Source of discovery documented

### Step 2: Classify the Debt

| Action | Owner | SLA |
|--------|-------|-----|
| Score impact (1-5) | Developer | 15 min |
| Score effort to fix (1-5) | Developer | 15 min |
| Calculate priority (Impact / Effort) | Developer | 5 min |

**Impact Scoring:**

| Score | Meaning |
|-------|---------|
| 1 | Cosmetic. No functional impact. |
| 2 | Minor inconvenience. Slows development slightly. |
| 3 | Moderate. Affects developer productivity or minor performance issue. |
| 4 | Significant. Causes bugs, security concerns, or major performance issues. |
| 5 | Critical. Blocks features, causes data loss risk, or has active security vulnerability. |

**Effort Scoring:**

| Score | Meaning |
|-------|---------|
| 1 | Less than 2 hours |
| 2 | Half day to 1 day |
| 3 | 2-3 days |
| 4 | 1 sprint (1-2 weeks) |
| 5 | Multiple sprints or requires architectural change |

- [ ] Impact score assigned (1-5)
- [ ] Effort score assigned (1-5)
- [ ] Priority calculated (Impact / Effort)

> **IF** Impact = 5 and relates to security vulnerability **THEN** escalate to Tech Lead immediately; treat as urgent
> **ELSE** proceed to Step 3

### Step 3: Record in Technical Debt Register

| Action | Owner | SLA |
|--------|-------|-----|
| Create entry in [Technical Debt Register](../templates/technical-debt-register.md) | Developer | 30 min |

| Field | Description |
|-------|-------------|
| ID | Unique identifier (TD-XXX) |
| Title | Short description |
| Description | What the debt is and why it exists |
| Category | Code, design, dependency, infrastructure, test |
| Impact score | 1-5 |
| Effort score | 1-5 |
| Priority | Impact / Effort |
| Affected components | Which modules or services |
| Date identified | When found |
| Identified by | Who found it |
| Status | Open |

- [ ] Entry created in Technical Debt Register with all fields populated

### Step 4: Decide on Action

| Action | Owner | SLA |
|--------|-------|-----|
| Determine action based on priority score | Tech Lead | 1 day |

| Priority Score | Action |
|---------------|--------|
| >= 3.0 | Schedule in current or next sprint |
| 1.5 - 2.9 | Add to backlog, schedule within 2-3 sprints |
| 1.0 - 1.4 | Add to backlog, address opportunistically |
| < 1.0 | Accept the debt. Document decision. Review quarterly. |

- [ ] Action decision recorded in register

> **IF** priority >= 3.0 **THEN** proceed to Step 5 immediately
> **ELSE IF** priority 1.5 - 2.9 **THEN** add to backlog; proceed to Step 5 when sprint-planned
> **ELSE IF** priority 1.0 - 1.4 **THEN** add to backlog; proceed to Step 5 opportunistically
> **ELSE** document acceptance decision; skip to Exit Criteria

### Step 5: Plan the Fix

| Action | Owner | SLA |
|--------|-------|-----|
| Create ticket in project tracker | Developer | 30 min |
| Link ticket to Technical Debt Register entry | Developer | 5 min |
| Write acceptance criteria for "resolved" state | Developer | 30 min |
| Estimate work using standard estimation process | Developer | 15 min |

- [ ] Ticket created and linked to debt register entry
- [ ] Acceptance criteria define "resolved" state
- [ ] Effort estimated
- [ ] Included in sprint planning

### Step 6: Resolve the Debt

| Action | Owner | SLA |
|--------|-------|-----|
| Create branch: `refactor/TD-XXX-short-description` | Developer | 5 min |
| Write tests if none exist | Developer | 1-4 hours |
| Implement the fix | Developer | Per estimate |
| Run full test suite | Developer | 15 min |
| Create PR referencing debt item | Developer | 15 min |

- [ ] Branch created following naming convention
- [ ] Tests written/updated for affected code
- [ ] Fix implemented
- [ ] All existing tests still pass
- [ ] PR created referencing TD-XXX

> **IF** fix causes unrelated test failures **THEN** investigate; escalate to Tech Lead if scope expands
> **ELSE** follow standard [Implement Feature](./implement-feature.md) and [Conduct Code Review](./conduct-code-review.md) process

### Step 7: Update Register and Track Metrics

| Action | Owner | SLA |
|--------|-------|-----|
| Update register entry status to Resolved | Developer | 5 min |
| Report metrics in sprint retrospective | Tech Lead | Per sprint cadence |

| Metric | Target |
|--------|--------|
| Total open debt items | Trending down or stable |
| Critical/high debt items (impact 4-5) | Zero older than 2 sprints |
| Debt items resolved per sprint | At least 1-2 per sprint |
| New debt items per sprint | Awareness metric (no hard target) |

- [ ] Register entry updated to Resolved
- [ ] Metrics reviewed in sprint retrospective

**Sprint Allocation Reference:**

| Sprint Type | Debt Allocation |
|------------|----------------|
| Normal sprint | 10-20% of capacity |
| Debt-focused sprint | 50%+ of capacity (schedule quarterly if debt is growing) |
| Pre-release sprint | No debt work unless blocking release |

---

## EXIT CRITERIA

- [ ] Debt item identified and classified with impact/effort scores
- [ ] Entry recorded in Technical Debt Register
- [ ] Action decision made (schedule fix, backlog, or accept)
- [ ] If fixing: ticket created, fix implemented, tests pass, PR merged
- [ ] Register updated with final status (Resolved or Accepted)

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Technical Debt Register entry | [Technical Debt Register](../templates/technical-debt-register.md) | Project documentation |
| Fix ticket | N/A | Project tracker |
| Refactor PR (if resolved) | [PR Template](../templates/pull-request-template.md) | GitHub |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Technical Debt Register | Template | [../templates/technical-debt-register.md](../templates/technical-debt-register.md) |
| Pull Request Template | Template | [../templates/pull-request-template.md](../templates/pull-request-template.md) |
| Code Review Checklist | Template | [../templates/code-review-checklist.md](../templates/code-review-checklist.md) |
| Coding Standards | Standard | [../standards/coding-standards.md](../standards/coding-standards.md) |
| Implement Feature | Runbook | [./implement-feature.md](./implement-feature.md) |
| Conduct Code Review | Runbook | [./conduct-code-review.md](./conduct-code-review.md) |
