# ISO Standards Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P2-003 |
| **Use When** | Identifying which ISO standard, clause, or process applies to a given SDLC activity or artifact |
| **Last Updated** | 2026-03-04 |

---

## ISO/IEC/IEEE 12207 -- Software Life Cycle Processes

| Process | Description | GlowPowerRental Phase |
|---------|-------------|----------------------|
| Stakeholder Needs and Requirements Definition | Identify stakeholders and define their needs | Business Analysis, Requirements Engineering |
| System/Software Requirements Definition | Analyze and define system and software requirements | Requirements Engineering |
| Architecture Definition | Define system architecture based on requirements | System Architecture |
| Verification | Confirm work products meet requirements | Testing |
| Validation | Confirm system meets stakeholder needs | Testing |
| Decision Management | Manage decisions through phase gates | All phases |
| Configuration Management | Control versions of work products | All phases |

---

## ISO/IEC/IEEE 29148 -- Requirements Engineering

### Key Clauses

| Clause | Title | What It Mandates | GlowPowerRental Artifact |
|--------|-------|-----------------|--------------------------|
| Clause 4 | Concepts | Requirements engineering fundamentals | Standards documents |
| Clause 5 | Stakeholder Requirements Definition | Process for identifying stakeholders and defining their requirements | Stakeholder Register, BRD |
| Clause 6 | System Requirements Analysis | Process for analyzing and specifying system requirements | System Requirements section of SRS |
| Clause 7 | Software Requirements Specification | Structure and content of an SRS document | SRS |
| Clause 8 | Information Items | Required documentation artifacts | BRD, SRS, RTM |

### Key Concepts

| Concept | Definition |
|---------|-----------|
| Requirement | A statement that identifies a capability, characteristic, or quality factor of a system |
| Stakeholder requirement | Requirement from the perspective of a user or other stakeholder |
| System requirement | Requirement that specifies what the system must do |
| Software requirement | Requirement that specifies what the software component must do |
| Traceability | Ability to trace a requirement from origin through implementation to verification |

---

## ISO/IEC/IEEE 42010 -- Architecture Description

### Relevance to Requirements

| Concept | How It Relates to Requirements |
|---------|-------------------------------|
| Architecture concerns | Stakeholder concerns drive both requirements and architecture viewpoints |
| Viewpoints | Different stakeholder perspectives are captured as both requirements and architecture views |
| Architecture decisions | Architecture decisions may create new technical requirements |
| System context | System boundary definition informs requirement scope |

### Key Elements

| Element | Description | GlowPowerRental Artifact |
|---------|-------------|--------------------------|
| System of Interest | The system being described | System boundary definition in SRS |
| Stakeholders | People with concerns about the system | Stakeholder Register |
| Concerns | Interests relevant to the system | Requirements source material |
| Architecture Viewpoints | Conventions for constructing views | Architecture Description Document |
| Architecture Views | Representations of the system from a viewpoint | Architecture diagrams |
| Architecture Decisions | Rationale for architecture choices | ADRs |

---

## ISO Clause to GlowPowerRental Artifact Mapping

| ISO Standard | Clause/Process | GlowPowerRental Artifact |
|-------------|----------------|--------------------------|
| ISO 12207 | Stakeholder Needs Definition | Stakeholder Register, Stakeholder Analysis |
| ISO 12207 | Requirements Definition | BRD, SRS |
| ISO 12207 | Decision Management | Phase gate review records |
| ISO 12207 | Configuration Management | Version-controlled documents |
| ISO 29148 | Clause 5 | Stakeholder Register, BRD |
| ISO 29148 | Clause 6 | SRS (system requirements section) |
| ISO 29148 | Clause 7 | SRS (software requirements section) |
| ISO 29148 | Clause 8 | BRD, SRS, RTM |
| ISO 42010 | Stakeholders | Stakeholder Register |
| ISO 42010 | Concerns | Requirements source traceability |
| ISO 42010 | Architecture Decisions | ADRs |

---

## ISO Clause to SDLC Phase Mapping

| SDLC Phase | ISO 12207 | ISO 29148 | ISO 42010 |
|------------|-----------|-----------|-----------|
| 1. Business Analysis | Stakeholder Needs Definition | Clause 5 (partial) | Stakeholders, Concerns |
| 2. Requirements Engineering | Requirements Definition | Clauses 5, 6, 7, 8 | Concerns |
| 3. System Architecture | Architecture Definition | -- | Viewpoints, Views, Decisions |
| 4. Design | Design Definition | -- | -- |
| 5. Development | Implementation | -- | -- |
| 6. Testing | Verification, Validation | -- | -- |
| 7. Deployment | Transition | -- | -- |
| 8. Operations | Operation, Maintenance | -- | -- |

---

## DECISION TREE

### Which Standard Applies?

```
IF activity involves identifying stakeholders or eliciting needs
    THEN ISO 12207 (Stakeholder Needs Definition) + ISO 29148 Clause 5

ELSE IF activity involves writing or reviewing requirements documents
    IF document is BRD or Stakeholder Requirements
        THEN ISO 29148 Clause 5
    ELSE IF document is SRS (system-level requirements)
        THEN ISO 29148 Clause 6
    ELSE IF document is SRS (software-level requirements)
        THEN ISO 29148 Clause 7
    ELSE IF document is RTM or other information item
        THEN ISO 29148 Clause 8

ELSE IF activity involves architecture definition or decisions
    THEN ISO 42010
    IF architecture decisions create new requirements
        THEN also ISO 29148 Clause 6 or 7

ELSE IF activity involves phase gate review or approval
    THEN ISO 12207 (Decision Management)

ELSE IF activity involves version control of work products
    THEN ISO 12207 (Configuration Management)

ELSE IF activity involves testing or verification
    THEN ISO 12207 (Verification + Validation)
```

### Which Artifact Satisfies This Clause?

```
IF clause is ISO 29148 Clause 5
    THEN produce: Stakeholder Register + BRD

ELSE IF clause is ISO 29148 Clause 6
    THEN produce: SRS (system requirements section)

ELSE IF clause is ISO 29148 Clause 7
    THEN produce: SRS (software requirements section)

ELSE IF clause is ISO 29148 Clause 8
    THEN produce: BRD + SRS + RTM

ELSE IF clause is ISO 12207 Decision Management
    THEN produce: Phase gate review records + Baseline Sign-off

ELSE IF clause is ISO 42010 Architecture Decisions
    THEN produce: ADRs
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Requirements Engineering Standard | Standard | ../standards/requirements-engineering-standard.md |
| Requirements Classification Standard | Standard | ../standards/requirements-classification.md |
| Requirements Traceability Standard | Standard | ../standards/requirements-traceability.md |
| SDLC Framework | Standard | ../../standards/sdlc-framework.md |
| Architecture Description Standard | Standard | ../../phase-3-system-architecture/standards/architecture-description-standard.md |
| Architecture Decision Records Standard | Standard | ../../phase-3-system-architecture/standards/architecture-decision-records-standard.md |
| Requirements Artifacts Checklist | Reference | ./requirements-artifacts-checklist.md |
| Glossary | Reference | ./glossary.md |
| RACI Matrix | Reference | ./raci-matrix.md |
| Validate Requirements | Runbook | ../runbooks/validate-requirements.md |
