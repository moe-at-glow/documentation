# Manage Requirements Changes

Step-by-step procedure for handling requirement changes after baseline is established.

---

## Prerequisites

- Requirements baseline is established.
- Change Control Board (CCB) members identified: Product Owner, Tech Lead, QA Lead, Project Sponsor (for high-impact changes).

---

## Procedure

### Step 1: Receive Change Request

Any stakeholder may submit a change request. Accept change requests through:

- Formal submission using the [Change Request Form](../templates/change-request-form.md).
- Verbal requests must be converted to a written change request by the Business Analyst before processing.

### Step 2: Log Change Request

1. Assign a unique ID using format: `CR-XXX` (sequential numbering).
2. Record the following:

| Field | Value |
|-------|-------|
| CR ID | CR-XXX |
| Date Submitted | YYYY-MM-DD |
| Requestor | Name and role |
| Description | What is being requested |
| Affected Requirements | List of BR/STK/SYS/SWR IDs affected |
| Justification | Business reason for the change |
| Status | Submitted |

3. Acknowledge receipt to the requestor within 2 business days.

### Step 3: Perform Impact Analysis

Analyze the impact across five dimensions:

| Dimension | Questions to Answer |
|-----------|-------------------|
| Scope | Which requirements are affected? Are new requirements needed? Are existing requirements removed? |
| Schedule | Does this change the delivery timeline? Which sprints are affected? |
| Cost | Does this require additional resources, licenses, or infrastructure? |
| Risk | Does this introduce new technical or business risks? Does it affect system stability? |
| Technical | Does this require architecture changes? Does it affect existing integrations? |

Use the RTM to trace the impact from the affected requirement through design, code, and tests.

### Step 4: Present Impact Analysis to Change Control Board

1. Prepare a one-page impact summary.
2. Present to the CCB.
3. For each impact dimension, state the finding and recommendation.
4. Recommend one of: Approve, Reject, or Defer.

**CCB Decision Authority:**

| Impact Level | Decision Authority |
|-------------|-------------------|
| Low (single requirement, no schedule impact) | Product Owner alone |
| Medium (multiple requirements, minor schedule impact) | Product Owner + Tech Lead |
| High (architecture change, significant schedule/cost impact) | Full CCB including Project Sponsor |

### Step 5: Record Decision

| Decision | Action |
|----------|--------|
| Approved | Proceed to Step 6 |
| Rejected | Update CR status to Rejected. Notify requestor with rationale. Close the CR. |
| Deferred | Update CR status to Deferred. Record target release or review date. Notify requestor. |

### Step 6: Update Requirements Baseline (Approved Changes Only)

1. Modify affected requirements in the SRS.
2. Add new requirements if needed (assign new IDs).
3. Retire removed requirements (status: Retired, do not delete).
4. Update the baseline version number.
5. Record the change in the SRS revision history.

### Step 7: Update Traceability Matrix

1. Update all affected rows in the RTM.
2. Add new rows for new requirements.
3. Mark retired requirements.
4. Verify all traceability links are still valid.

### Step 8: Communicate Changes

Notify all affected parties:

| Audience | Communication |
|----------|--------------|
| Development Team | Updated SRS with highlighted changes, affected sprint items |
| QA Team | Updated RTM, new/modified test cases needed |
| Product Owner | Updated scope and priority |
| Requestor | Decision outcome and implementation plan |
| Project Sponsor | Summary of scope/schedule/cost impact (for High impact changes) |

### Step 9: Archive Change Request

1. Update CR status to Closed.
2. Record final decision, implementation date, and actual impact.
3. Store the CR with the project documentation.

---

## Change Request Form (Quick Reference)

```
CR-XXX
Date: YYYY-MM-DD
Requestor: [Name, Role]
Affected Requirements: [BR/SWR IDs]
Description: [What is being requested]
Justification: [Why]

Impact Analysis:
  Scope:    [Low / Medium / High] - [Details]
  Schedule: [Low / Medium / High] - [Details]
  Cost:     [Low / Medium / High] - [Details]
  Risk:     [Low / Medium / High] - [Details]
  Technical:[Low / Medium / High] - [Details]

Decision: [Approve / Reject / Defer]
Decision Date: YYYY-MM-DD
Decision Authority: [Name(s)]
Rationale: [Why this decision]
```

---

## Output Artifacts

- Change Request log (all CRs with status)
- Impact analysis documents
- Updated SRS (new baseline version)
- Updated RTM
- Communication records

---

## Checklist

- [ ] Change request received in writing
- [ ] CR logged with unique ID and all required fields
- [ ] Receipt acknowledged to requestor
- [ ] Impact analysis completed across all five dimensions
- [ ] Impact analysis presented to CCB
- [ ] Decision recorded with rationale
- [ ] Requirements baseline updated (if approved)
- [ ] Traceability matrix updated
- [ ] All affected parties notified
- [ ] Change request archived
