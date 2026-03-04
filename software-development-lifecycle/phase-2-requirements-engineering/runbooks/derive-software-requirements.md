# Derive Software Requirements

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P2-003 |
| **Owner** | Business Analyst + Tech Lead |
| **Accountable** | Tech Lead |
| **SLA** | 10 business days |
| **Escalation** | Tech Lead |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Approved and baselined BRD (RB-P2-002 exit criteria met)
- [ ] Completed stakeholder analysis (RB-P2-001 exit criteria met)
- [ ] Tech Lead assigned and available
- [ ] Business Analyst assigned and available

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| BRD not approved or baselined | STOP. Complete RB-P2-002 first. | Product Owner |
| Tech Lead unavailable for 5+ business days | STOP. Request substitute or reschedule. | Tech Lead |
| More than 30% of BRs require clarification | STOP. Return to RB-P2-002 for BRD rework. | Product Owner |
| Architecture constraints undefined | STOP. Obtain architecture guidance before decomposition. | Tech Lead |

---

## PROCEDURE

### Step 1: Review Approved Business Requirements

| Action | Owner | SLA |
|--------|-------|-----|
| Read the baselined BRD | Business Analyst + Tech Lead | 0.5 day |
| List all Must Have and Should Have business requirements | Business Analyst | 0.5 day |
| Identify requirements needing clarification | Business Analyst | 0.5 day |

- [ ] Baselined BRD reviewed
- [ ] Must Have and Should Have requirements listed
- [ ] Ambiguous requirements identified and flagged

> **IF** requirements need clarification **THEN** resolve with Product Owner before proceeding
> **ELSE** proceed to Step 2

### Step 2: Identify System Boundaries and Interfaces

| Action | Owner | SLA |
|--------|-------|-----|
| Define system scope and all boundary elements | Tech Lead | 1 day |

- [ ] System scope defined
- [ ] All boundary elements documented:

| Boundary Element | Description |
|-----------------|-------------|
| System Scope | What the software system is responsible for |
| External Systems | Systems the software integrates with (payment gateway, ERP, IoT sensors) |
| User Interfaces | How users interact with the system (web app, mobile app, dashboard) |
| Data Interfaces | Data flowing in and out (API calls, file imports, sensor data) |
| Infrastructure | Servers, databases, message brokers the system depends on |

> **IF** boundary is unclear **THEN** consult Domain Expert and Product Owner for clarification
> **ELSE** proceed to Step 3

### Step 3: Decompose Business Requirements into Stakeholder Requirements

| Action | Owner | SLA |
|--------|-------|-----|
| For each BR, identify what each stakeholder group needs (STK-XXX) | Business Analyst | 2 days |

- [ ] Each BR decomposed into one or more stakeholder requirements
- [ ] Each STK requirement attributed to a specific stakeholder group
- [ ] STK IDs assigned (STK-XXX format)

> **IF** a BR cannot be decomposed into stakeholder requirements **THEN** flag and clarify with Product Owner
> **ELSE** proceed to Step 4

### Step 4: Decompose Stakeholder Requirements into System Requirements

| Action | Owner | SLA |
|--------|-------|-----|
| For each STK requirement, define what the system must do (SYS-XXX) | Business Analyst + Tech Lead | 2 days |

- [ ] Each STK requirement decomposed into one or more system requirements
- [ ] SYS IDs assigned (SYS-XXX format)
- [ ] System requirements are implementation-neutral

> **IF** a system requirement spans multiple subsystems **THEN** split into subsystem-specific requirements
> **ELSE** proceed to Step 5

### Step 5: Decompose System Requirements into Software Requirements

| Action | Owner | SLA |
|--------|-------|-----|
| For each SYS requirement, define specific software behavior (SWR-XXX) | Tech Lead | 2 days |

- [ ] Each SYS requirement decomposed into one or more software requirements
- [ ] SWR IDs assigned (SWR-XXX format)
- [ ] Each SWR specifies concrete, implementable behavior

> **IF** a SWR requires architecture decisions not yet made **THEN** escalate to Tech Lead for architecture review
> **ELSE IF** a SWR is too large for a single sprint **THEN** decompose further
> **ELSE** proceed to Step 6

### Step 6: Classify Each Requirement

| Action | Owner | SLA |
|--------|-------|-----|
| Assign classification attributes to every SWR | Business Analyst + Tech Lead | 1 day |

- [ ] Each SWR classified per:

| Attribute | Options |
|-----------|---------|
| Type | Functional / Non-Functional |
| NFR Category (if applicable) | Performance / Security / Usability / Reliability / Scalability / Maintainability / Compliance |
| Priority | Must Have / Should Have / Could Have / Won't Have |
| Risk | High / Medium / Low |
| Source | Stakeholder / Regulatory / Technical / Business |

- [ ] [Requirements Classification Standard](../standards/requirements-classification.md) followed

> **IF** classification is disputed between BA and Tech Lead **THEN** Product Owner makes final priority call; Tech Lead makes final type/risk call
> **ELSE** proceed to Step 7

### Step 7: Define Acceptance Criteria

| Action | Owner | SLA |
|--------|-------|-----|
| Write acceptance criteria for each SWR in Given/When/Then format | Business Analyst | 2 days |

- [ ] Every SWR has at least one acceptance criterion
- [ ] Given/When/Then format used
- [ ] Criteria are measurable (no subjective terms without quantification)

> **IF** acceptance criteria cannot be defined **THEN** flag SWR as untestable; rework the requirement
> **ELSE** proceed to Step 8

### Step 8: Establish Traceability Links

| Action | Owner | SLA |
|--------|-------|-----|
| Update Requirements Traceability Matrix with all links | Business Analyst | 1 day |

- [ ] RTM updated: SWR -> SYS -> STK -> BR links established
- [ ] Every SWR traces back to at least one BR
- [ ] No orphan SWRs (requirements without BR trace)
- [ ] [Requirements Traceability Matrix Template](../templates/requirements-traceability-matrix.md) used

> **IF** an SWR has no BR trace **THEN** flag as candidate for removal; confirm with Tech Lead
> **ELSE** proceed to Step 9

### Step 9: Obtain Peer Review and Tech Lead Approval

| Action | Owner | SLA |
|--------|-------|-----|
| Review all requirements for completeness and consistency | Business Analyst | 1 day |
| Review all requirements for technical feasibility | Tech Lead | 1 day |
| Resolve any issues identified | Business Analyst + Tech Lead | 1 day |
| Approve and sign off | Tech Lead | 0.5 day |
| Update all requirement statuses from Draft to Approved | Business Analyst | 0.5 day |

- [ ] BA completeness and consistency review done
- [ ] Tech Lead feasibility review done
- [ ] All issues resolved
- [ ] Tech Lead sign-off obtained
- [ ] All statuses updated to Approved

> **IF** Tech Lead identifies infeasible requirements **THEN** rework with BA; return to Step 5 for affected requirements
> **ELSE IF** BA identifies incomplete traceability **THEN** return to Step 8
> **ELSE** proceed to EXIT CRITERIA

---

## EXIT CRITERIA

- [ ] All approved business requirements reviewed
- [ ] System boundaries and interfaces defined
- [ ] Business requirements decomposed into stakeholder requirements
- [ ] Stakeholder requirements decomposed into system requirements
- [ ] System requirements decomposed into software requirements
- [ ] Each requirement classified (type, priority, risk, source)
- [ ] Acceptance criteria defined for all software requirements
- [ ] Traceability matrix updated with all links
- [ ] Peer review completed by Business Analyst
- [ ] Tech Lead review and sign-off obtained

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Software Requirements Specification (SRS) | [software-requirements-specification.md](../templates/software-requirements-specification.md) | Project documentation repository |
| Requirements Traceability Matrix (updated) | [requirements-traceability-matrix.md](../templates/requirements-traceability-matrix.md) | Project documentation repository |
| Peer Review Record | -- | Project documentation repository |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| SRS Template | Template | [../templates/software-requirements-specification.md](../templates/software-requirements-specification.md) |
| RTM Template | Template | [../templates/requirements-traceability-matrix.md](../templates/requirements-traceability-matrix.md) |
| Requirements Classification Standard | Standard | [../standards/requirements-classification.md](../standards/requirements-classification.md) |
| Requirements Engineering Standard | Standard | [../standards/requirements-engineering-standard.md](../standards/requirements-engineering-standard.md) |
| Requirements Traceability Standard | Standard | [../standards/requirements-traceability.md](../standards/requirements-traceability.md) |
| BRD Template | Template | [../templates/business-requirements-document.md](../templates/business-requirements-document.md) |
| Extract Business Requirements | Runbook | [extract-business-requirements.md](extract-business-requirements.md) |
| Validate Requirements | Runbook | [validate-requirements.md](validate-requirements.md) |
