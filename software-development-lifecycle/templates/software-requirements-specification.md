# Software Requirements Specification (SRS)

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P2-SRS |
| **When to Use** | Derive and document software requirements from an approved BRD |
| **Owner** | Business Analyst / Tech Lead |
| **Reviewer** | QA Lead |
| **SLA** | 10 business days from BRD baseline |
| **Runbook** | [Derive Software Requirements](../runbooks/derive-software-requirements.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Sections 3.2.3-3.2.5 (Usability/Reliability/Scalability), 3.3.2 (Hardware Interfaces), 3.3.4 (Communications Interfaces), and Appendices are optional.
> **IF** medium project (3-5 devs) **THEN** All Section 3 subsections required; Appendices optional if covered in separate documents.
> **IF** large project (6+ devs) **THEN** Full template required. Aligned with ISO/IEC/IEEE 29148.

---

## [ ] Document Control

| Field | Value |
|-------|-------|
| Document Title | [Project Name] -- Software Requirements Specification |
| Version | 1.0 |
| Status | Draft / Under Review / Approved / Baselined |
| Author | [Name] |
| Date Created | YYYY-MM-DD |
| Last Updated | YYYY-MM-DD |
| Related BRD | [BRD document reference and version] |

### [ ] Revision History

| Version | Date | Author | Description |
|---------|------|--------|-------------|
| 0.1 | YYYY-MM-DD | [Name] | Initial draft |
| | | | |

### [ ] Approvers

| Name | Role | Signature | Date |
|------|------|-----------|------|
| [Name] | Tech Lead | | |
| [Name] | Product Owner | | |
| [Name] | QA Lead | | |

---

## [ ] 1. Introduction

### [ ] 1.1 Purpose

<!-- State the purpose of this SRS and the software product it describes -->

[Purpose statement here]

### [ ] 1.2 Scope

<!-- Name the product, what it does, benefits, and objectives -->

[Scope statement here]

### [ ] 1.3 Definitions and Acronyms

| Term | Definition |
|------|-----------|
| [Term] | [Definition] |

### [ ] 1.4 References

| Document | Version | Date |
|----------|---------|------|
| [BRD title] | [Version] | [Date] |
| [Other reference] | | |

---

## [ ] 2. Overall Description

### [ ] 2.1 Product Perspective

<!-- How this software fits into the larger system; include a system context diagram -->

```
[System Context Diagram]

+-------------+       +-----------------+       +-------------+
| External    | <---> | [System Name]   | <---> | External    |
| System A    |       |                 |       | System B    |
+-------------+       +-----------------+       +-------------+
                            ^
                            |
                      +----------+
                      |  Users   |
                      +----------+
```

### [ ] 2.2 Product Functions

| Function | Description |
|----------|-------------|
| [Function name] | [Brief description] |

### [ ] 2.3 User Characteristics

| User Type | Description | Technical Proficiency | Frequency of Use |
|-----------|-------------|----------------------|-----------------|
| [User role] | [Description] | Low/Medium/High | Daily/Weekly/Monthly |

### [ ] 2.4 Constraints

| Constraint | Description |
|-----------|-------------|
| [Type] | [Constraint detail] |

### [ ] 2.5 Assumptions

| ID | Assumption |
|----|-----------|
| ASM-001 | [Assumption] |

---

## [ ] 3. Specific Requirements

### [ ] 3.1 Functional Requirements

<!-- Use MoSCoW priority: M=Must, S=Should, C=Could, W=Won't. Trace each SWR to a BR. -->

| ID | Title | Description | Priority | Source BR | Acceptance Criteria | Status |
|----|-------|-------------|----------|-----------|-------------------|--------|
| SWR-001 | [Short name] | The system shall [behavior] | M/S/C/W | BR-XXX | Given [context], When [action], Then [result] | Draft |
| SWR-002 | | | | | | |

### [ ] 3.2 Non-Functional Requirements

#### [ ] 3.2.1 Performance

| ID | Description | Priority | Acceptance Criteria | Status |
|----|-------------|----------|-------------------|--------|
| SWR-NFR-P001 | [Performance requirement] | M/S/C/W | [Measurable criteria] | Draft |

#### [ ] 3.2.2 Security

| ID | Description | Priority | Acceptance Criteria | Status |
|----|-------------|----------|-------------------|--------|
| SWR-NFR-S001 | [Security requirement] | M/S/C/W | [Measurable criteria] | Draft |

#### [ ] 3.2.3 Usability

| ID | Description | Priority | Acceptance Criteria | Status |
|----|-------------|----------|-------------------|--------|
| SWR-NFR-U001 | [Usability requirement] | M/S/C/W | [Measurable criteria] | Draft |

#### [ ] 3.2.4 Reliability

| ID | Description | Priority | Acceptance Criteria | Status |
|----|-------------|----------|-------------------|--------|
| SWR-NFR-R001 | [Reliability requirement] | M/S/C/W | [Measurable criteria] | Draft |

#### [ ] 3.2.5 Scalability

| ID | Description | Priority | Acceptance Criteria | Status |
|----|-------------|----------|-------------------|--------|
| SWR-NFR-SC001 | [Scalability requirement] | M/S/C/W | [Measurable criteria] | Draft |

### [ ] 3.3 Interface Requirements

#### [ ] 3.3.1 User Interfaces

| ID | Description | Priority | Status |
|----|-------------|----------|--------|
| SWR-UI-001 | [UI requirement] | M/S/C/W | Draft |

#### [ ] 3.3.2 Hardware Interfaces

| ID | Description | Priority | Status |
|----|-------------|----------|--------|
| SWR-HW-001 | [Hardware interface requirement] | M/S/C/W | Draft |

#### [ ] 3.3.3 Software Interfaces

| ID | Description | Protocol/Format | Priority | Status |
|----|-------------|----------------|----------|--------|
| SWR-SW-001 | [External system integration] | REST/MQTT/etc. | M/S/C/W | Draft |

#### [ ] 3.3.4 Communications Interfaces

| ID | Description | Priority | Status |
|----|-------------|----------|--------|
| SWR-COM-001 | [Communications requirement] | M/S/C/W | Draft |

### [ ] 3.4 Data Requirements

| ID | Description | Retention Period | Priority | Status |
|----|-------------|-----------------|----------|--------|
| SWR-DATA-001 | [Data requirement] | [Duration] | M/S/C/W | Draft |

---

## [ ] 4. Traceability to Business Requirements

| SWR ID | SYS ID | STK ID | BR ID |
|--------|--------|--------|-------|
| SWR-001 | SYS-XXX | STK-XXX | BR-XXX |
| | | | |

Full traceability: [Link to Requirements Traceability Matrix]

---

## [ ] 5. Appendices

### [ ] Appendix A: Use Cases

[Link to Use Case documents]

### [ ] Appendix B: Data Models

[Entity relationship diagrams or data dictionary]

### [ ] Appendix C: Wireframes

[Link to wireframes or mockups]

---

## COMPLETION CHECKLIST

- [ ] All required sections filled
- [ ] Every SWR traces to at least one BR
- [ ] Reviewed by QA Lead
- [ ] Approved by Tech Lead and Product Owner
- [ ] Stored in project SharePoint / repository
- [ ] Cross-referenced in RTM (if applicable)

---

## CROSS-REFERENCES

| Artifact | Link |
|----------|------|
| Producing Runbook | [Derive Software Requirements](../runbooks/derive-software-requirements.md) |
| Business Requirements Document | [BRD Template](business-requirements-document.md) |
| Requirements Traceability Matrix | [RTM Template](requirements-traceability-matrix.md) |
| Use Case Template | [Use Case Template](use-case-template.md) |
