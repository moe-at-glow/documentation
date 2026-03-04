# Requirements Engineering Standard

Standard for requirements engineering at GlowPowerRental, aligned with ISO/IEC/IEEE 29148.

---

## Requirements Hierarchy

Requirements are decomposed through four levels. Each level refines the one above it.

```
Business Requirements (BR)
   |
   v
Stakeholder Requirements (STK)
   |
   v
System Requirements (SYS)
   |
   v
Software Requirements (SWR)
```

### Level Definitions

| Level | ID Format | Purpose | Owner | Approval Authority |
|-------|-----------|---------|-------|--------------------|
| Business Requirement | BR-XXX | Define what the business needs to achieve | Product Owner | Project Sponsor |
| Stakeholder Requirement | STK-XXX | Define what stakeholders need the system to do for them | Business Analyst | Product Owner |
| System Requirement | SYS-XXX | Define what the system must do to satisfy stakeholder needs | Business Analyst / Tech Lead | Tech Lead |
| Software Requirement | SWR-XXX | Define specific software behavior, constraints, and interfaces | Tech Lead / Developer | Tech Lead |

---

## Mandatory Requirement Attributes

Every requirement at every level must have the following attributes:

| Attribute | Description | Example |
|-----------|-------------|---------|
| ID | Unique identifier using level prefix | SWR-042 |
| Title | Short descriptive name | Late Fee Calculation |
| Description | Clear statement of the requirement | The system shall calculate late fees at 2% of daily rental rate per day overdue |
| Priority | MoSCoW classification | Must Have |
| Source | Origin of the requirement (stakeholder, regulation, etc.) | Operations Manager |
| Rationale | Why this requirement exists | Late returns cause revenue loss; automated calculation reduces manual errors |
| Acceptance Criteria | Measurable conditions for verification | Given a rental 3 days overdue at 100 SAR/day, the calculated fee is 6 SAR |
| Status | Current lifecycle state | Approved |
| Parent | ID of the parent requirement (except BR level) | SYS-018 |
| Version | Current version number | 1.2 |

---

## Requirement Lifecycle States

```
Draft --> Under Review --> Approved --> Implemented --> Verified --> Retired
                |                          |
                v                          v
            Rejected                   Deferred
```

| State | Definition | Who Transitions |
|-------|-----------|-----------------|
| Draft | Initial capture, not yet reviewed | Business Analyst |
| Under Review | Submitted for stakeholder review | Business Analyst |
| Approved | Accepted and baselined | Approval authority per level |
| Rejected | Determined to be invalid or unnecessary | Approval authority per level |
| Implemented | Code written to fulfill the requirement | Developer |
| Verified | Tested and confirmed to meet acceptance criteria | QA Lead |
| Deferred | Accepted but postponed to a future release | Product Owner |
| Retired | No longer applicable | Product Owner |

---

## Requirement ID Naming Convention

Format: `<LEVEL>-<NUMBER>`

| Level | Prefix | Range | Example |
|-------|--------|-------|---------|
| Business Requirement | BR | BR-001 to BR-999 | BR-042 |
| Stakeholder Requirement | STK | STK-001 to STK-999 | STK-087 |
| System Requirement | SYS | SYS-001 to SYS-999 | SYS-134 |
| Software Requirement | SWR | SWR-001 to SWR-999 | SWR-201 |

Rules:

- Numbers are assigned sequentially within each level.
- Numbers are never reused, even if a requirement is retired.
- Cross-project requirements use a project prefix: `<PROJECT>-<LEVEL>-<NUMBER>` (e.g., `FLEET-BR-001`).

---

## Requirement Quality Criteria

Every approved requirement must satisfy all six quality criteria:

| Criterion | Definition | Test |
|-----------|-----------|------|
| Unambiguous | Has exactly one interpretation | Can two readers independently reach the same understanding? |
| Testable | Can be verified through testing or inspection | Can you write a pass/fail test for it? |
| Traceable | Can be traced to its source and forward to design/test | Does it have a parent and can it link to implementation? |
| Feasible | Can be implemented within known constraints | Has the tech lead confirmed it is achievable? |
| Necessary | Removal would create a gap in meeting business objectives | Does it trace to a business requirement? |
| Consistent | Does not contradict any other requirement | Has it been checked against all related requirements? |

A requirement that fails any criterion must be reworked before it can move to **Approved** status.

---

## ISO 29148 Clause Mapping

| ISO 29148 Clause | GlowPowerRental Artifact |
|------------------|--------------------------|
| Clause 5: Stakeholder requirements definition | Stakeholder Analysis, BRD |
| Clause 6: System requirements analysis | System Requirements section of SRS |
| Clause 7: Software requirements specification | SRS |
| Clause 8: Information items | BRD, SRS, RTM |
