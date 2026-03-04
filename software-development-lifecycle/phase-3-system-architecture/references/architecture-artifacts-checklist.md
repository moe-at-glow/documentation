# Architecture Artifacts Checklist

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P3-001 |
| **Use When** | Verifying completeness of Phase 3 deliverables before architecture review gate |
| **Last Updated** | 2026-03-04 |

---

## Artifact Register

| Artifact | Description | Owner | Format | Required | ISO Reference |
|----------|-------------|-------|--------|----------|---------------|
| Architecture Description Document (ADD) | Complete architecture documentation with all viewpoints | System Architect / Tech Lead | Markdown document | Yes | ISO 42010 |
| System Context Diagram | Boundary of the system and all external interactions | Tech Lead | ASCII or diagram tool | Yes | ISO 42010 - Context |
| Component Diagram | Internal modules/services, responsibilities, and interfaces | Tech Lead | ASCII or diagram tool | Yes | ISO 42010 - Logical View |
| Deployment Diagram | Infrastructure topology, server specs, network layout | Tech Lead | ASCII or diagram tool | Yes | ISO 42010 - Deployment View |
| Process/Sequence Diagrams | Runtime behavior for top 5 critical scenarios | Tech Lead | ASCII or diagram tool | Yes (large/medium), Optional (small) | ISO 42010 - Process View |
| Development View | Repository structure, module boundaries, build pipeline | Tech Lead | Markdown document | Yes (large/medium), Optional (small) | ISO 42010 - Development View |
| Architecture Decision Records (ADRs) | Documented decisions with context, alternatives, and rationale | Tech Lead | Markdown (one per decision) | Yes | ISO 42010 - Rationale |
| Technology Stack Document | All technologies with versions, purpose, and justification | Tech Lead | Table in ADD or separate document | Yes | ISO 42010 |
| Architecture Review Record | Findings, decision, and action items from the review | System Architect | Markdown document | Yes (large/medium), Optional (small) | ISO 12207 |
| Updated RTM | Architecture references added to traceability matrix | Business Analyst | Spreadsheet | Yes | ISO 29148 |

---

## Completion Checklist

| Artifact | Status |
|----------|--------|
| [ ] Architecture Description Document with all viewpoints | |
| [ ] System Context Diagram | |
| [ ] Component Diagram | |
| [ ] Deployment Diagram | |
| [ ] Process diagrams for top 5 scenarios | |
| [ ] Development view | |
| [ ] ADRs for all significant decisions (minimum 5) | |
| [ ] Technology stack documented | |
| [ ] Architecture review conducted | |
| [ ] Architecture review record filed | |
| [ ] RTM updated with architecture references | |
| [ ] Architecture approval obtained | |

---

## DECISION TREE

### Which artifacts are required for my project size?

```
IF project size = Large or Medium
  THEN all artifacts in the register are REQUIRED
  THEN proceed to completion checklist — every row must be checked

IF project size = Small
  THEN the following are REQUIRED:
    - Architecture Description Document (ADD)
    - System Context Diagram
    - Component Diagram
    - Deployment Diagram
    - ADRs (minimum 5)
    - Technology Stack Document
    - Updated RTM
  THEN the following are OPTIONAL:
    - Process/Sequence Diagrams
    - Development View
    - Architecture Review Record
```

### Is the checklist complete enough for review gate?

```
IF all "Required = Yes" artifacts have Status = Done
  AND all ADRs are written (minimum 5)
  AND RTM is updated
  THEN submit for architecture review

IF any "Required = Yes" artifact is missing
  THEN DO NOT submit — complete missing artifacts first

IF project is Small AND only optional artifacts are missing
  THEN document justification for omission
  THEN submit for architecture review
```

### Who owns a missing artifact?

```
IF artifact owner = "Tech Lead"
  THEN Tech Lead creates the artifact
  THEN System Architect reviews

IF artifact owner = "System Architect"
  THEN System Architect creates the artifact

IF artifact owner = "Business Analyst"
  THEN Business Analyst updates the RTM
  THEN Tech Lead verifies architecture references are correct
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Create Architecture Description | Runbook | ../runbooks/create-architecture-description.md |
| Conduct Architecture Review | Runbook | ../runbooks/conduct-architecture-review.md |
| Write Architecture Decision Record | Runbook | ../runbooks/write-architecture-decision-record.md |
