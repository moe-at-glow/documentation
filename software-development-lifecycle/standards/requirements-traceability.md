# Requirements Traceability Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P2-004 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Business Analyst / QA Lead |
| **Verification Method** | RTM audit at each phase gate checkpoint |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Traceability via Jira epic-to-story-to-PR links acceptable; formal RTM not required; coverage metrics tracked informally
> **IF** medium project (3-5 devs) **THEN** Formal RTM required; all coverage metrics tracked; reviews at baseline and release readiness
> **IF** large project (6+ devs) **THEN** Full compliance required; reviews at every checkpoint

---

## COMPLIANCE REQUIREMENTS

### Traceability Matrix Structure

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | RTM contains column: Requirement ID | All traced requirements | [ ] Verify column present with valid IDs | RTM corrected before gate review |
| 2 | RTM contains column: Requirement Description | All traced requirements | [ ] Verify column present and populated | RTM corrected before gate review |
| 3 | RTM contains column: Source | All traced requirements | [ ] Verify column present and populated | RTM corrected before gate review |
| 4 | RTM contains column: Parent Requirement | All traced requirements | [ ] Verify column present with valid parent IDs | RTM corrected before gate review |
| 5 | RTM contains column: Design Reference | All traced requirements | [ ] Verify column present (populated after Phase 4) | RTM corrected before gate review |
| 6 | RTM contains column: Code Reference | All traced requirements | [ ] Verify column present (populated after Phase 5) | RTM corrected before gate review |
| 7 | RTM contains column: Test Case ID | All traced requirements | [ ] Verify column present (populated after Phase 6) | RTM corrected before gate review |
| 8 | RTM contains column: Test Result | All traced requirements | [ ] Verify column present (populated during Phase 6) | RTM corrected before gate review |
| 9 | RTM contains column: Status | All traced requirements | [ ] Verify column present with valid lifecycle state | RTM corrected before gate review |

### Traceability Directions

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 10 | Forward traceability maintained: BR --> STK --> SYS --> SWR --> Design --> Code --> Test | All requirements | [ ] Trace sample requirements forward through all artifacts | Gaps filled before release |
| 11 | Backward traceability maintained: Test --> Code --> Design --> SWR --> SYS --> STK --> BR | All test cases | [ ] Trace sample test cases backward to business requirements | Orphan tests flagged for justification or removal |

### RTM Update Triggers

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 12 | New requirement added: add row to RTM, link to parent | All new requirements | [ ] Verify new requirements appear in RTM within same sprint | RTM updated before next gate review |
| 13 | Requirement modified: update RTM row, verify all links still valid | Modified requirements | [ ] Verify RTM row updated and links revalidated | RTM updated before next gate review |
| 14 | Requirement deleted or retired: mark row as retired with reason | Retired requirements | [ ] Verify retired rows marked with reason | RTM updated before next gate review |
| 15 | Design created or updated: link design reference to requirement | Design artifacts | [ ] Verify design reference column populated | RTM updated before Phase 4 gate |
| 16 | Code implemented: link code reference to requirement | Code artifacts | [ ] Verify code reference column populated | RTM updated before Phase 5 gate |
| 17 | Test case created: link test case ID to requirement | Test artifacts | [ ] Verify test case ID column populated | RTM updated before Phase 6 gate |
| 18 | Test executed: update test result column | Test results | [ ] Verify test result column updated | RTM updated before release readiness |
| 19 | Change request approved: update affected rows, add new rows if needed | Change requests | [ ] Verify RTM reflects all approved changes | RTM updated before next gate review |

### Coverage Metrics

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 20 | Requirements Coverage: 100% of Must Have requirements have linked test cases | Must Have requirements | [ ] Calculate and verify coverage percentage | Release blocked until 100% achieved |
| 21 | Requirements Coverage: 90% of Should Have requirements have linked test cases | Should Have requirements | [ ] Calculate and verify coverage percentage | Gap documented; Product Owner accepts risk |
| 22 | Forward Traceability Completeness: 100% of Must Have requirements traceable BR to test case | Must Have requirements | [ ] Trace all Must Have requirements end-to-end | Release blocked until 100% achieved |
| 23 | Backward Traceability Completeness: 100% of test cases trace to a requirement (no orphan tests) | All test cases | [ ] Audit for test cases without requirement links | Orphan tests justified or removed |
| 24 | Implementation Coverage: 100% of approved requirements have linked code references before release | All approved requirements | [ ] Verify code reference column populated for all approved | Release blocked until 100% achieved |

### Traceability Review Checkpoints

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 25 | Requirements baseline: BA and Product Owner verify all requirements have parent links | Phase 2 gate | [ ] Review conducted and documented | Phase 2 gate blocked |
| 26 | Design review: Tech Lead verifies all requirements have design references | Phase 4 gate | [ ] Review conducted and documented | Phase 4 gate blocked |
| 27 | Code review: Tech Lead and Developer verify all requirements have code references | Phase 5 gate | [ ] Review conducted and documented | Phase 5 gate blocked |
| 28 | Test readiness review: QA Lead verifies all requirements have test cases | Phase 6 entry | [ ] Review conducted and documented | Test execution blocked |
| 29 | Release readiness review: Product Owner and QA Lead verify all metrics meet thresholds | Phase 7 gate | [ ] Review conducted and documented | Release blocked |

### RTM Governance

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 30 | One authoritative copy of RTM exists (single source of truth) | All projects | [ ] Verify single master location identified | Duplicates removed; master designated |
| 31 | RTM changes are version-controlled | All projects | [ ] Verify version history available | Version control implemented |
| 32 | RTM is accessible to all project team members | All projects | [ ] Verify team access permissions | Access granted |

---

## COMPLIANCE CHECKLIST

- [ ] RTM created with all nine required columns
- [ ] Forward traceability maintained (BR --> STK --> SYS --> SWR --> Design --> Code --> Test)
- [ ] Backward traceability maintained (no orphan tests)
- [ ] RTM updated on every trigger event (new/modified/retired requirements, design, code, test, change requests)
- [ ] Requirements Coverage: 100% Must Have, 90% Should Have have linked test cases
- [ ] Forward Traceability Completeness: 100% Must Have requirements traced end-to-end
- [ ] Backward Traceability Completeness: 100% test cases trace to requirements
- [ ] Implementation Coverage: 100% approved requirements have code references before release
- [ ] Traceability review conducted at each checkpoint (baseline, design, code, test readiness, release readiness)
- [ ] Single authoritative RTM copy maintained, version-controlled, and team-accessible

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| SDLC Framework Standard | Standard | ../standards/sdlc-framework.md |
| Requirements Engineering Standard | Standard | ../standards/requirements-engineering-standard.md |
| Requirements Classification Standard | Standard | ../standards/requirements-classification.md |
| Validate Requirements | Runbook | ../runbooks/validate-requirements.md |
| Manage Requirements Changes | Runbook | ../runbooks/manage-requirements-changes.md |
