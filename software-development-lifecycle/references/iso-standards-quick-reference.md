# ISO Standards Quick Reference

Quick reference for the three ISO standards underlying GlowPowerRental's SDLC framework.

---

## ISO/IEC/IEEE 12207 -- Software Life Cycle Processes

Defines the processes for software lifecycle management.

**Key processes relevant to requirements:**

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

Defines processes and artifacts for requirements engineering.

**Key clauses:**

| Clause | Title | What It Mandates | GlowPowerRental Artifact |
|--------|-------|-----------------|--------------------------|
| Clause 4 | Concepts | Requirements engineering fundamentals | Standards documents |
| Clause 5 | Stakeholder Requirements Definition | Process for identifying stakeholders and defining their requirements | Stakeholder Register, BRD |
| Clause 6 | System Requirements Analysis | Process for analyzing and specifying system requirements | System Requirements section of SRS |
| Clause 7 | Software Requirements Specification | Structure and content of an SRS document | SRS |
| Clause 8 | Information Items | Required documentation artifacts | BRD, SRS, RTM |

**Key concepts from 29148:**

| Concept | Definition |
|---------|-----------|
| Requirement | A statement that identifies a capability, characteristic, or quality factor of a system |
| Stakeholder requirement | Requirement from the perspective of a user or other stakeholder |
| System requirement | Requirement that specifies what the system must do |
| Software requirement | Requirement that specifies what the software component must do |
| Traceability | Ability to trace a requirement from origin through implementation to verification |

---

## ISO/IEC/IEEE 42010 -- Architecture Description

Defines how to document system architecture.

**Relevance to requirements:**

| Concept | How It Relates to Requirements |
|---------|-------------------------------|
| Architecture concerns | Stakeholder concerns drive both requirements and architecture viewpoints |
| Viewpoints | Different stakeholder perspectives are captured as both requirements and architecture views |
| Architecture decisions | Architecture decisions may create new technical requirements |
| System context | System boundary definition informs requirement scope |

**Key elements:**

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
