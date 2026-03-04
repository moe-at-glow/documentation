# Common Requirements Pitfalls

Requirements engineering mistakes encountered in practice and how to avoid them.

---

## 1. Ambiguous Requirements

**Bad requirement:** "The system should be fast."

**Why it is a problem:** "Fast" means different things to different people. Developers cannot implement it. QA cannot test it. Stakeholders will be disappointed regardless of the outcome.

**How to fix it:** Quantify. Define specific, measurable criteria.

**Good requirement:** "SWR-101: The rental search API shall return results within 200ms for the 95th percentile under a load of 200 concurrent users."

---

## 2. Gold Plating

**Bad requirement:** "SWR-102: The dashboard shall display rental data in 12 different chart types including 3D pie charts, treemaps, and Sankey diagrams."

**Why it is a problem:** Nobody asked for 12 chart types. The Business Analyst or developer added features they thought would be impressive. This increases scope, development time, and maintenance burden without delivering business value.

**How to fix it:** Every requirement must trace to a stakeholder need. If no stakeholder asked for it and no business objective requires it, remove it.

**Good requirement:** "SWR-102: The dashboard shall display overdue rental counts by equipment category as a bar chart and total late fee revenue as a summary card."

---

## 3. Missing Non-Functional Requirements

**Bad practice:** SRS contains 47 functional requirements and zero non-functional requirements.

**Why it is a problem:** The system works functionally but falls over under load, has no security controls, and is impossible to maintain. Non-functional failures are the most expensive to fix after deployment.

**How to fix it:** For every system, explicitly address: Performance, Security, Usability, Reliability, Scalability, Maintainability, and Compliance. Use the [Requirements Classification Standard](../standards/requirements-classification.md) as a checklist.

**Good practice:** Dedicate a section of the SRS to non-functional requirements with at least one requirement per category.

---

## 4. Assumed Requirements

**Bad practice:** Business Analyst assumes the system should support Arabic and English because GlowPowerRental operates in Saudi Arabia, but does not document it as a requirement.

**Why it is a problem:** Assumptions are invisible. Developers may build English-only. When the assumption surfaces during testing, rework is expensive (RTL layout, Arabic date formats, bidirectional text).

**How to fix it:** Document all assumptions explicitly. Convert assumptions into requirements or confirm they are out of scope.

**Good requirement:** "SWR-103: The user interface shall support Arabic (RTL) and English (LTR) with language selection. All date/time displays shall follow the user's locale."

---

## 5. Scope Creep

**Bad practice:** After the requirements baseline is approved, the Operations Manager mentions "it would also be nice to track equipment maintenance schedules" in a hallway conversation. The developer adds it without a change request.

**Why it is a problem:** Uncontrolled additions expand scope, delay delivery, and introduce untested features. Nobody approved the change, nobody updated the RTM, and nobody wrote test cases.

**How to fix it:** All changes after baseline go through the [change management process](../runbooks/manage-requirements-changes.md). No exceptions.

**Good practice:** Log a change request (CR-XXX), perform impact analysis, get CCB approval, then implement.

---

## 6. Stakeholder Omission

**Bad practice:** Requirements are gathered only from the Operations Manager and IT Lead. End users (rental desk staff) and customers are not consulted.

**Why it is a problem:** The system satisfies management reporting needs but is unusable for the people who operate it daily. End users create workarounds, shadow systems, or reject the software entirely.

**How to fix it:** Complete the stakeholder analysis before elicitation. Ensure all quadrants of the Power/Interest grid are represented.

**Good practice:** Interview at least one representative from every stakeholder group classified as "Manage Closely" or "Keep Informed."

---

## 7. Premature Solutioning

**Bad requirement:** "BR-044: The system shall use a React frontend with a Node.js backend connected to PostgreSQL via Prisma ORM."

**Why it is a problem:** This is a technology specification, not a business requirement. Business requirements define what the business needs, not how to build it. Specifying technology at the BR level constrains architecture decisions unnecessarily.

**How to fix it:** Separate the "what" from the "how." Technology choices belong in architecture and design phases.

**Good requirement:** "BR-044: The business shall have a web-based system accessible from standard browsers for managing equipment rentals, tracking returns, and generating reports."

---

## 8. Incomplete Acceptance Criteria

**Bad requirement:** "SWR-104: The system shall handle equipment returns." (No acceptance criteria.)

**Why it is a problem:** "Handle" is undefined. Does it mean record the return date? Update inventory? Calculate fees? Generate a receipt? Without acceptance criteria, the developer guesses, and QA has nothing to test against.

**How to fix it:** Every software requirement must have explicit acceptance criteria in Given/When/Then format.

**Good requirement:**
```
SWR-104: The system shall record equipment returns.

Acceptance Criteria:
Given: An active rental agreement for equipment X
When:  The operator records the return of equipment X
Then:  The return date is stored
  And: The rental status changes to "returned"
  And: The equipment status changes to "available"
  And: A return receipt is generated
```

---

## 9. Untestable Requirements

**Bad requirement:** "SWR-105: The system shall provide an intuitive user experience."

**Why it is a problem:** "Intuitive" is subjective. There is no objective test for intuitiveness. This requirement will be marked as "passed" or "failed" based on opinion, not evidence.

**How to fix it:** Replace subjective terms with measurable criteria.

**Good requirement:** "SWR-105: A new user with no prior training shall be able to complete an equipment booking within 3 minutes, measured from first interaction to booking confirmation."

---

## 10. Conflicting Requirements

**Bad practice:** Two requirements in the same SRS:
- "SWR-106: All API responses shall be encrypted using AES-256."
- "SWR-107: API response time shall not exceed 50ms for any endpoint."

**Why it is a problem:** AES-256 encryption adds processing overhead that may make the 50ms target impossible for large payloads. These requirements conflict but neither acknowledges the trade-off.

**How to fix it:** During validation (consistency check), cross-reference all non-functional requirements. When conflicts exist, resolve them explicitly with stakeholders and document the trade-off.

**Good practice:**
- "SWR-106: All API responses shall be transmitted over TLS 1.3."
- "SWR-107: API response time shall not exceed 200ms for the 95th percentile, including TLS overhead."

---

## Quick Reference: Pitfall Detection Checklist

| Check | Warning Sign |
|-------|-------------|
| Contains "should", "might", "could" without quantification | Ambiguity |
| No stakeholder requested it | Gold plating |
| SRS has no non-functional requirements section | Missing NFRs |
| Requirement has no documented source | Assumed requirement |
| Feature added without a change request after baseline | Scope creep |
| Only 1-2 stakeholder groups were interviewed | Stakeholder omission |
| Business requirement specifies technology | Premature solutioning |
| Requirement has no acceptance criteria | Incomplete criteria |
| Acceptance criteria use subjective terms | Untestable |
| Two requirements have incompatible targets | Conflict |
