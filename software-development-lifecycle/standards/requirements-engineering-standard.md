# Requirements Engineering Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P2-002 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Business Analyst / Tech Lead |
| **Verification Method** | Requirements baseline review, RTM audit, attribute completeness check |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** User stories with acceptance criteria acceptable in lieu of formal BRD; SRS equivalent required; RTM may be Jira epic-to-story links
> **IF** medium project (3-5 devs) **THEN** BRD, SRS, and RTM required; validation may be single review session
> **IF** large project (6+ devs) **THEN** Full compliance required

---

## COMPLIANCE REQUIREMENTS

### Requirements Hierarchy

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Requirements decompose through four levels: BR --> STK --> SYS --> SWR | All projects | [ ] Verify each requirement has correct level prefix and parent link | Requirement rejected at baseline review |
| 2 | Business Requirements use format BR-XXX | All projects | [ ] Audit requirement IDs against naming convention | Requirement IDs corrected before baseline |
| 3 | Stakeholder Requirements use format STK-XXX | All projects | [ ] Audit requirement IDs against naming convention | Requirement IDs corrected before baseline |
| 4 | System Requirements use format SYS-XXX | All projects | [ ] Audit requirement IDs against naming convention | Requirement IDs corrected before baseline |
| 5 | Software Requirements use format SWR-XXX | All projects | [ ] Audit requirement IDs against naming convention | Requirement IDs corrected before baseline |
| 6 | Numbers assigned sequentially, never reused | All projects | [ ] Check for gaps or duplicates in ID sequence | IDs reassigned; retired IDs documented |
| 7 | Cross-project requirements use prefix: PROJECT-LEVEL-NUMBER | Multi-project | [ ] Verify project prefix present on shared requirements | Prefix added before cross-project reference |

### Level Ownership and Approval

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 8 | BR owned by Product Owner, approved by Project Sponsor | All projects | [ ] Check approval signatures on BR-level requirements | Requirement cannot enter Approved state |
| 9 | STK owned by Business Analyst, approved by Product Owner | All projects | [ ] Check approval signatures on STK-level requirements | Requirement cannot enter Approved state |
| 10 | SYS owned by Business Analyst / Tech Lead, approved by Tech Lead | All projects | [ ] Check approval signatures on SYS-level requirements | Requirement cannot enter Approved state |
| 11 | SWR owned by Tech Lead / Developer, approved by Tech Lead | All projects | [ ] Check approval signatures on SWR-level requirements | Requirement cannot enter Approved state |

### Mandatory Requirement Attributes

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 12 | Every requirement has a unique ID using level prefix | All requirements | [ ] Audit for missing or duplicate IDs | Requirement blocked from review |
| 13 | Every requirement has a Title | All requirements | [ ] Audit for missing titles | Requirement blocked from review |
| 14 | Every requirement has a Description (clear statement) | All requirements | [ ] Audit for missing descriptions | Requirement blocked from review |
| 15 | Every requirement has MoSCoW Priority | All requirements | [ ] Audit for missing priority | Requirement blocked from review |
| 16 | Every requirement has a Source | All requirements | [ ] Audit for missing source | Requirement blocked from review |
| 17 | Every requirement has a Rationale | All requirements | [ ] Audit for missing rationale | Requirement blocked from review |
| 18 | Every requirement has Acceptance Criteria | All requirements | [ ] Audit for missing acceptance criteria | Requirement blocked from review |
| 19 | Every requirement has a Status (lifecycle state) | All requirements | [ ] Audit for missing status | Requirement blocked from review |
| 20 | Every requirement (except BR) has a Parent ID | STK, SYS, SWR | [ ] Audit for missing parent links | Requirement blocked from review |
| 21 | Every requirement has a Version number | All requirements | [ ] Audit for missing version | Requirement blocked from review |

### Requirement Quality Criteria

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 22 | Requirement is Unambiguous (one interpretation) | All approved requirements | [ ] Two independent readers reach same understanding | Rework before Approved status |
| 23 | Requirement is Testable (pass/fail test possible) | All approved requirements | [ ] Confirm a pass/fail test can be written | Rework before Approved status |
| 24 | Requirement is Traceable (source and forward links) | All approved requirements | [ ] Verify parent link exists and implementation can link | Rework before Approved status |
| 25 | Requirement is Feasible (implementable within constraints) | All approved requirements | [ ] Tech lead confirms achievability | Rework before Approved status |
| 26 | Requirement is Necessary (traces to business need) | All approved requirements | [ ] Verify trace to a business requirement | Rework before Approved status |
| 27 | Requirement is Consistent (no contradictions) | All approved requirements | [ ] Cross-check against all related requirements | Rework before Approved status |

### Lifecycle State Transitions

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 28 | Valid states: Draft, Under Review, Approved, Rejected, Implemented, Verified, Deferred, Retired | All requirements | [ ] Audit for invalid states | State corrected |
| 29 | Only Business Analyst transitions to Draft and Under Review | All requirements | [ ] Check transition author | Unauthorized transition reverted |
| 30 | Only approval authority per level transitions to Approved or Rejected | All requirements | [ ] Check approval authority | Unauthorized approval reverted |
| 31 | Only Developer transitions to Implemented | All requirements | [ ] Check transition author | Unauthorized transition reverted |
| 32 | Only QA Lead transitions to Verified | All requirements | [ ] Check transition author | Unauthorized transition reverted |
| 33 | Only Product Owner transitions to Deferred or Retired | All requirements | [ ] Check transition author | Unauthorized transition reverted |

---

## COMPLIANCE CHECKLIST

- [ ] Requirements hierarchy follows four-level decomposition (BR --> STK --> SYS --> SWR)
- [ ] All requirement IDs follow naming convention (LEVEL-NUMBER)
- [ ] All ten mandatory attributes populated for every requirement
- [ ] Every non-BR requirement has a valid parent link
- [ ] All approved requirements pass six quality criteria (unambiguous, testable, traceable, feasible, necessary, consistent)
- [ ] Lifecycle state transitions performed only by authorized roles
- [ ] Requirements baseline review conducted with stakeholder sign-off
- [ ] ISO 29148 clause mapping satisfied (Clauses 5-8)

---

## ISO 29148 Clause Mapping

| ISO 29148 Clause | GlowPowerRental Artifact |
|------------------|--------------------------|
| Clause 5: Stakeholder requirements definition | Stakeholder Analysis, BRD |
| Clause 6: System requirements analysis | System Requirements section of SRS |
| Clause 7: Software requirements specification | SRS |
| Clause 8: Information items | BRD, SRS, RTM |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| SDLC Framework Standard | Standard | ../standards/sdlc-framework.md |
| Requirements Classification Standard | Standard | ../standards/requirements-classification.md |
| Requirements Traceability Standard | Standard | ../standards/requirements-traceability.md |
| Extract Business Requirements | Runbook | ../runbooks/extract-business-requirements.md |
| Derive Software Requirements | Runbook | ../runbooks/derive-software-requirements.md |
| Validate Requirements | Runbook | ../runbooks/validate-requirements.md |
| Manage Requirements Changes | Runbook | ../runbooks/manage-requirements-changes.md |
