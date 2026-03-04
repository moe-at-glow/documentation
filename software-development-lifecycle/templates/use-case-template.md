# Use Case Template

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P2-UCT |
| **When to Use** | Document a specific user interaction flow derived from business requirements |
| **Owner** | Business Analyst |
| **Reviewer** | Tech Lead |
| **SLA** | 2 business days per use case |
| **Runbook** | [Extract Business Requirements](../runbooks/extract-business-requirements.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Sections Alternative Flows, Exception Flows, Non-Functional Requirements, and Assumptions are optional. Main Flow is sufficient.
> **IF** medium project (3-5 devs) **THEN** All sections required; Open Issues optional if tracked in a backlog tool.
> **IF** large project (6+ devs) **THEN** Full template required.

---

## [ ] Use Case Summary

| Field | Value |
|-------|-------|
| Use Case ID | UC-XXX |
| Use Case Name | [Descriptive name, e.g., "Record Equipment Return"] |
| Version | 1.0 |
| Author | [Name] |
| Date | YYYY-MM-DD |
| Status | Draft / Reviewed / Approved |

---

## [ ] Actor(s)

| Actor | Type | Description |
|-------|------|-------------|
| [Primary actor] | Human / System | [Brief description of the actor] |
| [Secondary actor] | Human / System | [Brief description] |

---

## [ ] Description

<!-- 1-2 sentence summary of what this use case accomplishes -->

[Description here]

---

## [ ] Preconditions

1. [Condition that must be true before this use case starts]
2. [Another precondition]

---

## [ ] Postconditions

### [ ] Success

1. [State of the system after successful completion]
2. [Another postcondition]

### [ ] Failure

1. [State of the system if the use case fails]

---

## [ ] Main Flow

| Step | Actor | System |
|------|-------|--------|
| 1 | [Actor action] | |
| 2 | | [System response] |
| 3 | [Actor action] | |
| 4 | | [System response] |
| 5 | | [System response] |

---

## [ ] Alternative Flows

### [ ] AF-1: [Alternative scenario name]

**Trigger:** [When this alternative occurs, e.g., "At Step 3, if [condition]"]

| Step | Actor | System |
|------|-------|--------|
| 3a | [Alternative actor action] | |
| 3b | | [Alternative system response] |

[Returns to Main Flow at Step X / Ends use case]

---

## [ ] Exception Flows

### [ ] EF-1: [Exception scenario name]

**Trigger:** [When this exception occurs, e.g., "At Step 2, if [error condition]"]

| Step | Actor | System |
|------|-------|--------|
| 2a | | [System displays error message: "[message]"] |
| 2b | [Actor action to recover] | |

[Returns to Main Flow at Step X / Ends use case]

---

## [ ] Business Rules

| Rule ID | Description |
|---------|-------------|
| RULE-XXX | [Business rule that applies to this use case] |
| | |

---

## [ ] Related Requirements

| Requirement ID | Description |
|---------------|-------------|
| BR-XXX | [Related business requirement] |
| SWR-XXX | [Related software requirement] |
| | |

---

## [ ] Non-Functional Requirements

| Category | Requirement |
|----------|------------|
| Performance | [e.g., "Use case must complete within 5 seconds"] |
| Security | [e.g., "Actor must be authenticated with role X"] |
| Usability | [e.g., "Maximum 3 clicks to complete"] |

---

## [ ] Assumptions

1. [Assumption relevant to this use case]
2. [Another assumption]

---

## [ ] Open Issues

| ID | Issue | Owner | Status |
|----|-------|-------|--------|
| [1] | [Open question or unresolved decision] | [Name] | Open/Resolved |

---

## COMPLETION CHECKLIST

- [ ] All required sections filled
- [ ] Reviewed by Tech Lead
- [ ] Approved by Product Owner
- [ ] Stored in project SharePoint / repository
- [ ] Cross-referenced in RTM (if applicable)

---

## CROSS-REFERENCES

| Artifact | Link |
|----------|------|
| Producing Runbook | [Extract Business Requirements](../runbooks/extract-business-requirements.md) |
| Business Requirements Document | [BRD Template](business-requirements-document.md) |
| Software Requirements Specification | [SRS Template](software-requirements-specification.md) |
| Requirements Traceability Matrix | [RTM Template](requirements-traceability-matrix.md) |
