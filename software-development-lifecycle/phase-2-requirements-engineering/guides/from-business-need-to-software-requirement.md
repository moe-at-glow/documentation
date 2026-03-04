# From Business Need to Software Requirement -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P2-002 |
| **Use When** | Decomposing a business need through the requirements hierarchy |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] Business requirement describes *what the business needs*, not technology or implementation
- [ ] All stakeholder groups identified (not just the requester)
- [ ] No levels skipped in decomposition (BR -> STK -> SYS -> SWR)
- [ ] Every lower-level requirement traces back to a parent
- [ ] No orphan requirements (SWR without SYS, SYS without STK)
- [ ] Non-functional requirements defined (performance, security, reliability, etc.)
- [ ] Every SWR has explicit Given/When/Then acceptance criteria
- [ ] Decomposition is one-to-many (not 1:1 mapping at every level)

---

## SELECTION CRITERIA / DECISION TABLE

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| Formalizing a business need | Write BR with: ID, Title, Description, Priority, Source, Rationale, Acceptance Criteria, Status | Specifying technology in the BR |
| Identifying stakeholder needs | Map each stakeholder group to what *they* need from the system | Consulting only the original requester |
| Defining system behavior | Write SYS requirements independent of technology choices | Jumping from STK directly to SWR |
| Writing software requirements | Define specific behavior with measurable acceptance criteria (Given/When/Then) | Leaving acceptance criteria blank or subjective |
| Requirement mixes levels | Split into separate requirements at appropriate levels | "Dashboard shows rentals with fees at 2% daily" (mixes STK + SWR) |
| 1:1 decomposition ratio | Re-analyze -- genuine decomposition produces multiple children per parent | Assuming one BR = one SWR |

---

## QUICK-REFERENCE TABLE

### Requirements Hierarchy

| Level | ID Pattern | Describes | Owner | Example |
|-------|-----------|-----------|-------|---------|
| Business Requirement | BR-XXX | What the business needs to achieve | Product Owner | "Automated late return tracking and fee invoicing" |
| Stakeholder Requirement | STK-XXX | What each stakeholder group needs from the system | Business Analyst | "Ops staff view overdue rentals on dashboard" |
| System Requirement | SYS-XXX | What the system must do (technology-independent) | BA / Tech Lead | "System shall compare return dates against agreement end dates" |
| Software Requirement | SWR-XXX | Specific software behavior and constraints | Tech Lead / Developer | "GET /api/v1/rentals/overdue returns all overdue agreements" |

### Traceability Chain (Example: BR-042)

| BR | STK | SYS | SWR |
|----|-----|-----|-----|
| BR-042 | STK-087 (Ops: dashboard) | SYS-134 (Flag overdue) | SWR-201 (API endpoint), SWR-202 (Daily job) |
| BR-042 | STK-087 (Ops: dashboard) | SYS-135 (Calculate fee) | SWR-203 (Fee formula), SWR-204 (Currency rounding) |
| BR-042 | STK-088 (Finance: invoices) | SYS-136 (Generate invoice) | SWR-205 (PDF generation), SWR-206 (Invoice storage) |
| BR-042 | STK-089 (Customers: notification) | SYS-137 (Send notification) | SWR-207 (Email), SWR-208 (SMS) |
| BR-042 | STK-090 (Mgmt: reports) | SYS-138 (Aggregate data) | (Defined during decomposition) |

### Decomposition Mistakes

| Mistake | Example | Fix |
|---------|---------|-----|
| Combining levels | "Dashboard shows overdue rentals with fees at 2% daily" | Separate: STK = what user sees; SWR = calculation logic |
| Technology in BR | "BR: Use PostgreSQL to track returns" | BR describes business need; technology belongs in SWR |
| 1:1 decomposition | Every BR maps to exactly one SWR | Genuine decomposition produces multiple children per parent |
| Missing NFRs | No performance/security/reliability requirements | Add NFRs at SWR level (e.g., "job completes in 5 min for 10K rentals") |
| Orphan requirements | SWR with no parent SYS | Every SWR traces to SYS -> STK -> BR |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Requirements Classification | Standard | [../standards/requirements-classification.md](../standards/requirements-classification.md) |
| For background | Training | [training/requirements-engineering-overview.md](training/requirements-engineering-overview.md) |
