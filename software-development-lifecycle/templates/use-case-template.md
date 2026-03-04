# Use Case Template

**Template -- Copy and fill in for each use case.**

---

## Use Case Summary

| Field | Value |
|-------|-------|
| Use Case ID | UC-XXX |
| Use Case Name | [Descriptive name, e.g., "Record Equipment Return"] |
| Version | 1.0 |
| Author | [Name] |
| Date | YYYY-MM-DD |
| Status | Draft / Reviewed / Approved |

---

## Actor(s)

| Actor | Type | Description |
|-------|------|-------------|
| [Primary actor] | Human / System | [Brief description of the actor] |
| [Secondary actor] | Human / System | [Brief description] |

---

## Description

[1-2 sentence summary of what this use case accomplishes.]

---

## Preconditions

1. [Condition that must be true before this use case starts]
2. [Another precondition]

---

## Postconditions

### Success

1. [State of the system after successful completion]
2. [Another postcondition]

### Failure

1. [State of the system if the use case fails]

---

## Main Flow

| Step | Actor | System |
|------|-------|--------|
| 1 | [Actor action] | |
| 2 | | [System response] |
| 3 | [Actor action] | |
| 4 | | [System response] |
| 5 | | [System response] |

---

## Alternative Flows

### AF-1: [Alternative scenario name]

**Trigger:** [When this alternative occurs, e.g., "At Step 3, if [condition]"]

| Step | Actor | System |
|------|-------|--------|
| 3a | [Alternative actor action] | |
| 3b | | [Alternative system response] |

[Returns to Main Flow at Step X / Ends use case]

---

## Exception Flows

### EF-1: [Exception scenario name]

**Trigger:** [When this exception occurs, e.g., "At Step 2, if [error condition]"]

| Step | Actor | System |
|------|-------|--------|
| 2a | | [System displays error message: "[message]"] |
| 2b | [Actor action to recover] | |

[Returns to Main Flow at Step X / Ends use case]

---

## Business Rules

| Rule ID | Description |
|---------|-------------|
| RULE-XXX | [Business rule that applies to this use case] |
| | |

---

## Related Requirements

| Requirement ID | Description |
|---------------|-------------|
| BR-XXX | [Related business requirement] |
| SWR-XXX | [Related software requirement] |
| | |

---

## Non-Functional Requirements

| Category | Requirement |
|----------|------------|
| Performance | [e.g., "Use case must complete within 5 seconds"] |
| Security | [e.g., "Actor must be authenticated with role X"] |
| Usability | [e.g., "Maximum 3 clicks to complete"] |

---

## Assumptions

1. [Assumption relevant to this use case]
2. [Another assumption]

---

## Open Issues

| ID | Issue | Owner | Status |
|----|-------|-------|--------|
| [1] | [Open question or unresolved decision] | [Name] | Open/Resolved |
