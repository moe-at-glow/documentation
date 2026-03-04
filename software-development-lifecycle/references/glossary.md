# Glossary

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P2-004 |
| **Use When** | Looking up requirements engineering terminology used at GlowPowerRental |
| **Last Updated** | 2026-03-04 |

---

## Terms

| Term | Definition | ISO Reference |
|------|-----------|---------------|
| Acceptance Criteria | Specific, measurable conditions that a requirement must satisfy to be accepted. Written in Given/When/Then format. | ISO 29148 |
| Baseline | An approved, version-controlled snapshot of requirements at a point in time. Changes to baselined requirements require formal change control. | ISO 12207 |
| BRD (Business Requirements Document) | A document that captures business requirements, objectives, scope, and stakeholder needs. | ISO 29148, Clause 5 |
| Business Requirement | A high-level statement of what the business needs to achieve. Prefixed BR-XXX. | ISO 29148, Clause 5 |
| CCB (Change Control Board) | A group authorized to approve or reject changes to baselined requirements. Comprised of Product Owner, Tech Lead, QA Lead, and Project Sponsor. | ISO 12207 |
| Change Request | A formal proposal to modify a baselined requirement. Assigned ID CR-XXX and processed through impact analysis and CCB review. | ISO 12207 |
| Decomposition | The process of breaking higher-level requirements into more detailed lower-level requirements (BR to STK to SYS to SWR). | ISO 29148 |
| Elicitation | The process of discovering requirements from stakeholders through interviews, workshops, observation, and other techniques. | ISO 29148, Clause 5 |
| Feasibility | Whether a requirement can be implemented within known technical, budget, and schedule constraints. | ISO 29148 |
| Functional Requirement | A requirement that specifies what the system must do (behavior, features, operations). | ISO 29148, Clause 7 |
| MoSCoW | A prioritization method: Must Have, Should Have, Could Have, Won't Have. | -- |
| Non-Functional Requirement (NFR) | A requirement that specifies how the system must perform (quality attributes: performance, security, usability, reliability, scalability, maintainability, compliance). | ISO 29148, Clause 7 |
| RACI | A responsibility assignment matrix: Responsible, Accountable, Consulted, Informed. | -- |
| RTM (Requirements Traceability Matrix) | A document that maps requirements from business origin through design, implementation, and testing. | ISO 29148, Clause 8 |
| Scope Creep | Uncontrolled expansion of project scope through unapproved requirement additions. | -- |
| Software Requirement | A specific statement of software behavior, constraints, or interfaces. Prefixed SWR-XXX. The most detailed level of requirement. | ISO 29148, Clause 7 |
| SRS (Software Requirements Specification) | A document containing all software requirements with attributes, acceptance criteria, and traceability. | ISO 29148, Clause 7 |
| Stakeholder | Any person or group with an interest in or influence over the system. | ISO 29148, Clause 5 |
| Stakeholder Requirement | A requirement from the perspective of a specific stakeholder group. Prefixed STK-XXX. | ISO 29148, Clause 5 |
| System Requirement | A requirement that specifies what the system must do to satisfy stakeholder needs. Prefixed SYS-XXX. | ISO 29148, Clause 6 |
| Traceability | The ability to trace a requirement from its origin (business need) through specification, design, implementation, and verification. | ISO 29148, Clause 8 |
| Use Case | A description of how an actor interacts with the system to achieve a goal, including main flow, alternate flows, and exception flows. | ISO 29148 |
| User Story | An informal requirement format: "As a [role], I want [capability], so that [business value]." Used in Agile execution. | -- |
| Validation | Confirmation that the system meets stakeholder needs and intended use (building the right product). | ISO 12207 |
| Verification | Confirmation that a work product meets its specified requirements (building the product right). | ISO 12207 |

---

## DECISION TREE

### What Type of Requirement Is This?

```
IF requirement describes a business objective or need
    THEN type = Business Requirement (BR-XXX)
    THEN document in BRD

ELSE IF requirement describes what a stakeholder group needs
    THEN type = Stakeholder Requirement (STK-XXX)
    THEN document in BRD (stakeholder requirements section)

ELSE IF requirement describes what the system must do at system level
    THEN type = System Requirement (SYS-XXX)
    THEN document in SRS (system requirements section)

ELSE IF requirement describes specific software behavior or constraints
    THEN type = Software Requirement (SWR-XXX)
    IF it specifies behavior, features, or operations
        THEN subtype = Functional Requirement
    ELSE IF it specifies quality attributes (performance, security, etc.)
        THEN subtype = Non-Functional Requirement
    THEN document in SRS (software requirements section)
```

### Requirement Change: Process or Scope Creep?

```
IF requirement is baselined
    IF change goes through formal Change Request (CR-XXX)
        AND impact analysis is performed
        AND CCB approves
        THEN legitimate change -- update artifacts
    ELSE
        THEN scope creep -- reject and route to Change Request process

ELSE IF requirement is not yet baselined
    THEN change can be incorporated directly by the artifact owner
```

### Verification vs. Validation?

```
IF checking that a work product conforms to its specification
    THEN activity = Verification ("building the product right")

ELSE IF checking that the system meets stakeholder needs and intended use
    THEN activity = Validation ("building the right product")
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Requirements Engineering Standard | Standard | ../standards/requirements-engineering-standard.md |
| Requirements Classification Standard | Standard | ../standards/requirements-classification.md |
| Requirements Traceability Standard | Standard | ../standards/requirements-traceability.md |
| From Business Need to Software Requirement | Guide | ../guides/from-business-need-to-software-requirement.md |
| Extract Business Requirements | Runbook | ../runbooks/extract-business-requirements.md |
| Derive Software Requirements | Runbook | ../runbooks/derive-software-requirements.md |
| Manage Requirements Changes | Runbook | ../runbooks/manage-requirements-changes.md |
| RACI Matrix | Reference | ./raci-matrix.md |
| Requirements Artifacts Checklist | Reference | ./requirements-artifacts-checklist.md |
| ISO Standards Quick Reference | Reference | ./iso-standards-quick-reference.md |
