# Extract Business Requirements

Step-by-step procedure to elicit and document business requirements.

---

## Prerequisites

- Approved business case and project charter.
- Completed stakeholder analysis.
- Stakeholder availability confirmed.

---

## Procedure

### Step 1: Review Business Case and Project Charter

1. Read the business case. Identify stated objectives, scope, and constraints.
2. Read the project charter. Note success criteria, budget, and timeline.
3. List all business objectives. Each objective will map to one or more business requirements.

### Step 2: Schedule Elicitation Sessions

Plan the following sessions based on stakeholder classification:

| Session Type | When to Use | Duration | Participants |
|-------------|-------------|----------|-------------|
| Structured Interview | Key stakeholders (Manage Closely) | 45-60 min | Business Analyst + 1 stakeholder |
| Requirements Workshop | Cross-functional needs | 2-4 hours | Business Analyst + 3-8 stakeholders |
| Observation | Operational processes | 2-4 hours | Business Analyst observes end users |
| Document Review | Existing systems and regulations | Self-paced | Business Analyst |

Schedule interviews first, then workshops to validate consolidated findings.

### Step 3: Conduct Structured Interviews

Use this question framework:

**Current State:**
1. Describe your current process for [activity].
2. What tools or systems do you use today?
3. What works well in the current process?
4. What are the biggest pain points?

**Future State:**
5. What would the ideal process look like?
6. What capabilities are missing today?
7. What information do you need that you cannot easily access?

**Constraints:**
8. Are there regulatory or compliance requirements?
9. Are there deadlines or events driving the timeline?
10. Are there budget or resource constraints?

**Priorities:**
11. If you could change only one thing, what would it be?
12. What would happen if this project is not delivered?

Record all responses. Attribute each response to the stakeholder.

### Step 4: Facilitate Requirements Workshop

**Agenda:**

| Time | Activity |
|------|----------|
| 0:00 | Welcome, objectives, ground rules |
| 0:15 | Present consolidated interview findings |
| 0:30 | Group discussion: validate and expand findings |
| 1:00 | Identify and prioritize requirements (MoSCoW) |
| 1:30 | Break |
| 1:45 | Resolve conflicts between stakeholder needs |
| 2:15 | Review action items and next steps |
| 2:30 | Close |

**Ground rules:**
- One speaker at a time.
- All perspectives are valid.
- Focus on what the business needs, not how to build it.
- Decisions are documented immediately.
- Parking lot for out-of-scope items.

### Step 5: Analyze Existing Systems and Processes

1. Document the current as-is state for each relevant process.
2. Identify data inputs, outputs, and transformations.
3. Note integrations with external systems.
4. Record existing business rules.

### Step 6: Document Business Requirements

Write each business requirement using the BR-XXX format:

| Attribute | Value |
|-----------|-------|
| ID | BR-XXX |
| Title | [Short descriptive name] |
| Description | The business shall [capability statement] |
| Priority | Must Have / Should Have / Could Have / Won't Have |
| Source | [Stakeholder name or document reference] |
| Rationale | [Why this requirement exists] |
| Acceptance Criteria | [Measurable conditions] |
| Status | Draft |

Refer to the [Requirements Engineering Standard](../standards/requirements-engineering-standard.md) for attribute definitions.

### Step 7: Map Requirements to Business Objectives

Create a mapping table:

| Business Objective | Related Requirements |
|--------------------|---------------------|
| Reduce equipment downtime by 20% | BR-001, BR-003, BR-007 |
| Automate invoicing for late returns | BR-012, BR-014 |

Every business requirement must trace to at least one business objective. Requirements without a business objective are candidates for removal.

### Step 8: Review and Validate with Stakeholders

1. Distribute the draft BRD to all stakeholders identified in Step 3 and Step 4.
2. Allow 5 business days for review.
3. Collect written feedback.
4. Schedule a review meeting to resolve disagreements.
5. Update requirements based on feedback.

### Step 9: Obtain Formal Approval

1. Present the final BRD to the project sponsor and key stakeholders.
2. Walk through each Must Have requirement.
3. Confirm priorities and scope boundaries.
4. Obtain written sign-off from the project sponsor.
5. Baseline the BRD. All future changes follow the [change management process](manage-requirements-changes.md).

---

## Output Artifacts

- Business Requirements Document (BRD) -- use [BRD Template](../templates/business-requirements-document.md)
- Interview notes and recordings
- Workshop minutes
- Business objective to requirement mapping

---

## Checklist

- [ ] Business case and project charter reviewed
- [ ] All Manage Closely stakeholders interviewed
- [ ] At least one requirements workshop conducted
- [ ] Current processes documented (as-is state)
- [ ] All requirements written in BR-XXX format with all mandatory attributes
- [ ] Each requirement mapped to a business objective
- [ ] Requirements prioritized using MoSCoW
- [ ] Draft BRD reviewed by stakeholders
- [ ] Feedback incorporated
- [ ] Formal sign-off obtained from project sponsor
- [ ] BRD baselined
