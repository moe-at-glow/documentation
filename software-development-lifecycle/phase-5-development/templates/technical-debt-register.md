# Technical Debt Register

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P5-003 |
| **When to Use** | Logging, scoring, or reviewing technical debt |
| **Owner** | Developer |
| **Reviewer** | Tech Lead |
| **SLA** | Log within 1 business day of identification; review every sprint retrospective |
| **Runbook** | [Manage Technical Debt Runbook](../runbooks/manage-technical-debt.md) |
| **Last Verified** | 2026-03-04 |

---

## Scaling Decision Gate

| Total Open Items | Action |
|------------------|--------|
| **< 10** | Review in retrospective, address opportunistically |
| **10-25** | Dedicate 10% of sprint capacity to debt reduction |
| **25-50** | Dedicate 20% of sprint capacity; escalate to Tech Lead |
| **> 50** | STOP. Schedule dedicated debt sprint before new features |

---

## [ ] Scoring Guide

### [ ] Impact (1-5)

| Score | Meaning |
|-------|---------|
| 1 | Cosmetic. No functional impact. |
| 2 | Minor inconvenience. Slightly slows development. |
| 3 | Moderate. Affects developer productivity or minor performance issue. |
| 4 | Significant. Causes bugs, security concerns, or major performance issues. |
| 5 | Critical. Blocks features, data loss risk, or active security vulnerability. |

### [ ] Effort (1-5)

| Score | Meaning |
|-------|---------|
| 1 | Less than 2 hours |
| 2 | Half day to 1 day |
| 3 | 2-3 days |
| 4 | 1 sprint (1-2 weeks) |
| 5 | Multiple sprints or architectural change |

### [ ] Priority

**Priority = Impact / Effort**

| Priority | Action |
|----------|--------|
| >= 3.0 | Schedule in current or next sprint |
| 1.5 - 2.9 | Backlog, schedule within 2-3 sprints |
| 1.0 - 1.4 | Backlog, address opportunistically |
| < 1.0 | Accept. Document. Review quarterly. |

---

## [ ] Status Values

| Status | Meaning |
|--------|---------|
| Open | Identified but not yet scheduled |
| Scheduled | Ticket created, assigned to a sprint |
| In Progress | Actively being resolved |
| Resolved | Fixed and verified |
| Accepted | Deliberately accepted. Will not fix. Reviewed quarterly. |

---

## [ ] Register

<!-- Copy a row template for each new entry -->

| ID | Title | Category | Impact | Effort | Priority | Status | Date Identified |
|----|-------|----------|--------|--------|----------|--------|-----------------|
| TD-001 | <!-- title --> | <!-- code/design/dependency/infrastructure/test --> | <!-- 1-5 --> | <!-- 1-5 --> | <!-- I/E --> | <!-- Open --> | <!-- YYYY-MM-DD --> |

---

## [ ] Entry Detail Template

<!-- Copy this block for each entry and fill in the details below the register table. -->

### TD-NNN: <!-- Title -->

| Field | Value |
|-------|-------|
| **ID** | TD-NNN |
| **Title** | <!-- Short description --> |
| **Category** | <!-- Code / Design / Dependency / Infrastructure / Test --> |
| **Impact** | <!-- 1-5 --> |
| **Effort** | <!-- 1-5 --> |
| **Priority** | <!-- Impact / Effort --> |
| **Status** | <!-- Open / Scheduled / In Progress / Resolved / Accepted --> |
| **Affected Components** | <!-- Which modules or services --> |
| **Date Identified** | <!-- YYYY-MM-DD --> |
| **Identified By** | <!-- Name --> |
| **Ticket** | <!-- TICKET-NNN (when scheduled) --> |
| **Resolved Date** | <!-- YYYY-MM-DD (when resolved) --> |

**Description:**

<!-- What is the debt? Why does it exist? What is the impact if not addressed? -->

**Proposed Resolution:**

<!-- How should this be fixed? What is the approach? -->

---

## [ ] Example Entry

### TD-001: N+1 Query in Rental List Endpoint

| Field | Value |
|-------|-------|
| **ID** | TD-001 |
| **Title** | N+1 query in rental list endpoint |
| **Category** | Code |
| **Impact** | 4 |
| **Effort** | 2 |
| **Priority** | 2.0 |
| **Status** | Scheduled |
| **Affected Components** | Rental Service, Rental Repository |
| **Date Identified** | 2026-02-15 |
| **Identified By** | Sara (code review) |
| **Ticket** | TICKET-234 |
| **Resolved Date** | -- |

**Description:**

The `GET /api/v1/rentals` endpoint loads all rentals, then for each rental makes a separate query to load the customer name. With 100 rentals, this produces 101 database queries. Response time degrades linearly with the number of rentals.

**Proposed Resolution:**

Replace the loop with a JOIN query in `RentalRepository.findAllWithCustomers()`. Use a single SQL query that joins `rentals` with `customers` and maps the result.

---

## [ ] Summary Metrics

| Metric | Value | Trend |
|--------|-------|-------|
| Total open items | <!-- N --> | <!-- up/down/stable --> |
| Critical items (impact 4-5) | <!-- N --> | <!-- up/down/stable --> |
| Items resolved this sprint | <!-- N --> | |
| Items added this sprint | <!-- N --> | |
| Oldest open item | <!-- TD-NNN (N days old) --> | |

---

## Completion Checklist

- [ ] New debt entry added to Register table
- [ ] Entry Detail block created with all fields populated
- [ ] Impact scored (1-5)
- [ ] Effort scored (1-5)
- [ ] Priority calculated (Impact / Effort)
- [ ] Status set correctly
- [ ] Affected components identified
- [ ] Proposed resolution documented
- [ ] Summary metrics updated
- [ ] Reviewed in sprint retrospective

---

## Cross-References

| Document | Path | Relationship |
|----------|------|--------------|
| Manage Technical Debt Runbook | [../runbooks/manage-technical-debt.md](../runbooks/manage-technical-debt.md) | Parent runbook |
| Pull Request Template | [pull-request-template.md](pull-request-template.md) | Debt may be identified during PR creation |
| Code Review Checklist | [code-review-checklist.md](code-review-checklist.md) | Debt often identified during code review |
