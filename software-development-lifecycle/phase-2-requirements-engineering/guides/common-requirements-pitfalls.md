# Common Requirements Pitfalls -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P2-003 |
| **Use When** | Reviewing requirements for quality before baseline approval |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] No ambiguous terms ("fast", "intuitive", "user-friendly") without quantification
- [ ] Every requirement traces to a stakeholder need (no gold plating)
- [ ] SRS includes non-functional requirements (performance, security, usability, reliability, scalability, maintainability, compliance)
- [ ] All assumptions are documented as explicit requirements or confirmed out of scope
- [ ] No features added after baseline without a change request (CR-XXX)
- [ ] All stakeholder groups from Power/Interest grid were consulted
- [ ] No business requirement specifies technology choices
- [ ] Every SWR has Given/When/Then acceptance criteria
- [ ] No subjective terms in acceptance criteria
- [ ] Cross-referenced NFRs checked for conflicts and trade-offs documented

---

## SELECTION CRITERIA / DECISION TABLE

| Warning Sign | Pitfall | Recommended Action | Avoid |
|-------------|---------|-------------------|-------|
| Contains "should", "might", "could" without quantification | Ambiguity | Replace with measurable criteria (e.g., "within 200ms at 95th percentile, 200 concurrent users") | Vague modifiers without numbers |
| No stakeholder requested the feature | Gold plating | Remove or get explicit stakeholder sign-off | Adding features that seem impressive but lack business justification |
| SRS has zero NFR section | Missing NFRs | Add at least one requirement per NFR category; use Requirements Classification Standard as checklist | Assuming NFRs will be "handled later" |
| Requirement has no documented source | Assumed requirement | Document the assumption; convert to requirement or confirm out of scope | Leaving assumptions invisible |
| Feature added after baseline without CR | Scope creep | Log CR-XXX, perform impact analysis, get CCB approval | Informal additions via hallway conversations |
| Only 1-2 stakeholder groups interviewed | Stakeholder omission | Complete stakeholder analysis; interview all "Manage Closely" and "Keep Informed" groups | Building for management while ignoring end users |
| BR specifies technology stack | Premature solutioning | Rewrite BR as business need; move technology to architecture/SWR | "BR: Use React frontend with Node.js backend" |
| Requirement has no acceptance criteria | Incomplete criteria | Add Given/When/Then for every SWR | "The system shall handle returns" with no criteria |
| Acceptance criteria use subjective terms | Untestable | Replace with measurable criteria (time, count, percentage) | "Intuitive", "easy to use", "responsive" |
| Two requirements have incompatible targets | Conflicting requirements | Cross-reference NFRs; resolve trade-offs with stakeholders; document decisions | Ignoring conflicts between performance and security targets |

---

## QUICK-REFERENCE TABLE

| Pitfall | Bad Example | Good Example |
|---------|------------|-------------|
| Ambiguity | "The system should be fast" | "Rental search API returns results within 200ms at 95th percentile, 200 concurrent users" |
| Gold plating | "Dashboard displays 12 chart types including 3D pie charts" | "Dashboard displays overdue counts as bar chart and total revenue as summary card" |
| Missing NFRs | 47 functional requirements, zero NFRs | Dedicated SRS section with at least one requirement per NFR category |
| Assumed requirement | Assuming Arabic + English support without documenting it | "SWR-103: UI supports Arabic (RTL) and English (LTR) with language selection" |
| Scope creep | Developer adds maintenance tracking from hallway conversation | CR-XXX logged, impact analysis done, CCB approval obtained |
| Stakeholder omission | Only Operations Manager and IT Lead consulted | All Power/Interest grid quadrants represented |
| Premature solutioning | "BR: Use React + Node.js + PostgreSQL via Prisma" | "BR: Web-based system accessible from standard browsers" |
| Incomplete criteria | "System shall handle equipment returns" | Given/When/Then with return date stored, status updated, receipt generated |
| Untestable | "Provide intuitive user experience" | "New user completes booking within 3 minutes, no prior training" |
| Conflicting requirements | AES-256 encryption + 50ms response target (unacknowledged trade-off) | TLS 1.3 + 200ms at 95th percentile including TLS overhead |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Requirements Classification | Standard | [../standards/requirements-classification.md](../standards/requirements-classification.md) |
| Manage Requirements Changes | Runbook | [../runbooks/manage-requirements-changes.md](../runbooks/manage-requirements-changes.md) |
| For background | Training | [training/requirements-engineering-overview.md](training/requirements-engineering-overview.md) |
