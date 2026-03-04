# Manage Requirements Changes

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P2-005 |
| **Owner** | Business Analyst |
| **Accountable** | Product Owner |
| **SLA** | 10 business days per change request |
| **Escalation** | Product Owner (Low/Medium), Project Sponsor (High) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Requirements baseline established (RB-P2-004 exit criteria met)
- [ ] Change Control Board (CCB) members identified: Product Owner, Tech Lead, QA Lead, Project Sponsor
- [ ] Change request received in writing or converted to writing

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| No requirements baseline exists | STOP. Complete RB-P2-004 first. | Product Owner |
| CCB members not identified or unavailable | STOP. Establish CCB membership before processing changes. | Product Owner |
| Change request lacks sufficient detail for impact analysis | STOP. Return to requestor for clarification. | Business Analyst |

---

## PROCEDURE

### Step 1: Receive Change Request

| Action | Owner | SLA |
|--------|-------|-----|
| Accept change request via formal submission using [Change Request Form](../templates/change-request-form.md) | Business Analyst | 0.5 day |

- [ ] Change request received in writing
- [ ] [Change Request Form](../templates/change-request-form.md) used

> **IF** request submitted verbally **THEN** convert to written CR using Change Request Form before processing
> **ELSE** proceed to Step 2

### Step 2: Log Change Request

| Action | Owner | SLA |
|--------|-------|-----|
| Assign unique CR-XXX ID (sequential numbering) | Business Analyst | 0.5 day |
| Record all required fields | Business Analyst | 0.5 day |
| Acknowledge receipt to requestor | Business Analyst | 2 business days |

- [ ] CR ID assigned (CR-XXX format)
- [ ] All fields recorded:

| Field | Value |
|-------|-------|
| CR ID | CR-XXX |
| Date Submitted | YYYY-MM-DD |
| Requestor | Name and role |
| Description | What is being requested |
| Affected Requirements | List of BR/STK/SYS/SWR IDs affected |
| Justification | Business reason for the change |
| Status | Submitted |

- [ ] Receipt acknowledged to requestor within 2 business days

### Step 3: Perform Impact Analysis

| Action | Owner | SLA |
|--------|-------|-----|
| Analyze impact across all five dimensions | Business Analyst + Tech Lead | 3 business days |
| Use RTM to trace impact through design, code, and tests | Business Analyst | During analysis |

- [ ] All five dimensions analyzed:

| Dimension | Questions Answered |
|-----------|-------------------|
| Scope | Which requirements affected? New requirements needed? Existing removed? |
| Schedule | Delivery timeline change? Which sprints affected? |
| Cost | Additional resources, licenses, or infrastructure required? |
| Risk | New technical or business risks? System stability impact? |
| Technical | Architecture changes required? Existing integrations affected? |

- [ ] RTM used to trace full impact chain
- [ ] Impact level determined (Low / Medium / High)

> **IF** impact analysis reveals dependencies on pending CRs **THEN** link CRs and process together
> **ELSE** proceed to Step 4

### Step 4: Present Impact Analysis to Change Control Board

| Action | Owner | SLA |
|--------|-------|-----|
| Prepare one-page impact summary | Business Analyst | 0.5 day |
| Present to CCB with finding and recommendation per dimension | Business Analyst | 1 day |
| Recommend: Approve, Reject, or Defer | Business Analyst | During presentation |

- [ ] One-page impact summary prepared
- [ ] CCB presentation delivered
- [ ] Recommendation stated

**CCB Decision Authority:**

| Impact Level | Decision Authority |
|-------------|-------------------|
| Low (single requirement, no schedule impact) | Product Owner alone |
| Medium (multiple requirements, minor schedule impact) | Product Owner + Tech Lead |
| High (architecture change, significant schedule/cost impact) | Full CCB including Project Sponsor |

> **IF** impact is High and Project Sponsor unavailable **THEN** defer decision until Sponsor available
> **ELSE** proceed to Step 5

### Step 5: Record Decision

| Action | Owner | SLA |
|--------|-------|-----|
| Record CCB decision with rationale | Business Analyst | 0.5 day |

- [ ] Decision recorded

> **IF** decision is Approved **THEN** proceed to Step 6
> **ELSE IF** decision is Rejected **THEN** update CR status to Rejected; notify requestor with rationale; skip to Step 9
> **ELSE IF** decision is Deferred **THEN** update CR status to Deferred; record target release or review date; notify requestor; skip to Step 9

### Step 6: Update Requirements Baseline (Approved Changes Only)

| Action | Owner | SLA |
|--------|-------|-----|
| Modify affected requirements in the SRS | Business Analyst | 1 day |
| Add new requirements with new IDs if needed | Business Analyst | During modification |
| Retire removed requirements (status: Retired -- do not delete) | Business Analyst | During modification |
| Update baseline version number | Business Analyst | 0.5 day |
| Record change in SRS revision history | Business Analyst | 0.5 day |

- [ ] Affected requirements modified in SRS
- [ ] New requirements added with new IDs (if applicable)
- [ ] Removed requirements set to Retired status (not deleted)
- [ ] Baseline version number incremented
- [ ] SRS revision history updated

### Step 7: Update Traceability Matrix

| Action | Owner | SLA |
|--------|-------|-----|
| Update all affected rows in RTM | Business Analyst | 0.5 day |
| Add new rows for new requirements | Business Analyst | During update |
| Mark retired requirements in RTM | Business Analyst | During update |
| Verify all traceability links remain valid | Business Analyst | 0.5 day |

- [ ] All affected RTM rows updated
- [ ] New rows added for new requirements
- [ ] Retired requirements marked
- [ ] All traceability links verified valid

### Step 8: Communicate Changes

| Action | Owner | SLA |
|--------|-------|-----|
| Notify all affected parties per communication matrix | Business Analyst | 1 day |

- [ ] All audiences notified:

| Audience | Communication |
|----------|--------------|
| Development Team | Updated SRS with highlighted changes, affected sprint items |
| QA Team | Updated RTM, new/modified test cases needed |
| Product Owner | Updated scope and priority |
| Requestor | Decision outcome and implementation plan |
| Project Sponsor | Summary of scope/schedule/cost impact (High impact changes only) |

### Step 9: Archive Change Request

| Action | Owner | SLA |
|--------|-------|-----|
| Update CR status to Closed | Business Analyst | 0.5 day |
| Record final decision, implementation date, and actual impact | Business Analyst | 0.5 day |
| Store CR with project documentation | Business Analyst | 0.5 day |

- [ ] CR status set to Closed
- [ ] Final decision, implementation date, and actual impact recorded
- [ ] CR archived with project documentation

---

## EXIT CRITERIA

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

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Change Request Log (all CRs with status) | [change-request-form.md](../templates/change-request-form.md) | Project documentation repository |
| Impact Analysis Document | -- | Project documentation repository |
| Updated SRS (new baseline version) | [software-requirements-specification.md](../templates/software-requirements-specification.md) | Project documentation repository |
| Updated RTM | [requirements-traceability-matrix.md](../templates/requirements-traceability-matrix.md) | Project documentation repository |
| Communication Records | -- | Project documentation repository |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Change Request Form | Template | [../templates/change-request-form.md](../templates/change-request-form.md) |
| SRS Template | Template | [../templates/software-requirements-specification.md](../templates/software-requirements-specification.md) |
| RTM Template | Template | [../templates/requirements-traceability-matrix.md](../templates/requirements-traceability-matrix.md) |
| Requirements Engineering Standard | Standard | [../standards/requirements-engineering-standard.md](../standards/requirements-engineering-standard.md) |
| Requirements Traceability Standard | Standard | [../standards/requirements-traceability.md](../standards/requirements-traceability.md) |
| Validate Requirements | Runbook | [validate-requirements.md](validate-requirements.md) |
| Derive Software Requirements | Runbook | [derive-software-requirements.md](derive-software-requirements.md) |
