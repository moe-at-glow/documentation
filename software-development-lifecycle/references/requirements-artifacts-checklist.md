# Requirements Artifacts Checklist

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P2-002 |
| **Use When** | Verifying all required artifacts are produced during requirements engineering |
| **Last Updated** | 2026-03-04 |

---

## Artifact Register

| Artifact | Description | Owner | Format | Required | ISO Reference |
|----------|-------------|-------|--------|----------|---------------|
| Project Charter | Defines project scope, objectives, constraints, and authority | Project Sponsor | Document | Yes | ISO 12207 - Agreement Processes |
| Stakeholder Register | List of all stakeholders with classification and contact info | Business Analyst | Spreadsheet / Document | Yes | ISO 29148 - Clause 5 |
| Communication Plan | Communication method and frequency per stakeholder group | Business Analyst | Document | Yes | ISO 29148 - Clause 5 |
| Business Requirements Document (BRD) | Formal record of business requirements with priorities and acceptance criteria | Business Analyst | Document | Yes | ISO 29148 - Clause 5 |
| Stakeholder Requirements Specification | Requirements from each stakeholder group's perspective | Business Analyst | Section within BRD | Yes | ISO 29148 - Clause 5 |
| Software Requirements Specification (SRS) | Complete software requirements: functional, non-functional, interface, data | Tech Lead | Document | Yes | ISO 29148 - Clause 7 |
| Use Case Document | Actor interactions with the system including main, alternate, and exception flows | Business Analyst | Document | Conditional | ISO 29148 - Clause 6 |
| Requirements Traceability Matrix (RTM) | Mapping from BR through SWR to design, code, and test cases | Business Analyst | Spreadsheet | Yes | ISO 29148 - Clause 8 |
| Requirements Validation Report | Evidence that requirements are complete, consistent, feasible, and testable | Business Analyst | Document | Yes | ISO 29148 - Clause 6 |
| Requirements Baseline Sign-off | Formal approval of the requirements baseline by authorized stakeholders | Project Sponsor | Signed document | Yes | ISO 12207 - Decision Management |

---

## Artifact Lifecycle

| Artifact | Created During | Updated During | Approved By |
|----------|---------------|----------------|-------------|
| Project Charter | Business Analysis | Not updated (baseline document) | Project Sponsor |
| Stakeholder Register | Stakeholder Analysis | When new stakeholders are identified | Product Owner |
| Communication Plan | Stakeholder Analysis | When stakeholder groups change | Product Owner |
| BRD | Business Requirements Extraction | After change request approval | Project Sponsor |
| SRS | Software Requirements Derivation | After change request approval | Tech Lead |
| Use Case Document | Requirements Analysis | After change request approval | Business Analyst |
| RTM | Requirements Derivation | Every phase (design, code, test) | Business Analyst |
| Validation Report | Requirements Validation | After re-validation | Business Analyst |
| Baseline Sign-off | Requirements Baseline | After change request approval (new baseline version) | Project Sponsor |

---

## Completion Checklist

- [ ] Project Charter
- [ ] Stakeholder Register
- [ ] Communication Plan
- [ ] BRD with all mandatory attributes per requirement
- [ ] SRS with functional and non-functional requirements
- [ ] Use Cases (if applicable)
- [ ] RTM with BR-to-SWR traceability
- [ ] Validation Report
- [ ] Baseline Sign-off

---

## DECISION TREE

### Is This Artifact Required?

```
IF artifact is Project Charter, Stakeholder Register, Communication Plan,
   BRD, SRS, RTM, Validation Report, or Baseline Sign-off
    THEN required = YES -- produce before phase gate

ELSE IF artifact is Use Case Document
    THEN check project type:
        IF system has user-facing interactions
            THEN required = YES
        ELSE
            THEN required = NO -- document rationale for exclusion

ELSE IF artifact is Stakeholder Requirements Specification
    THEN included as section within BRD -- not a separate deliverable
```

### Who Approves This Artifact?

```
IF artifact is Project Charter OR BRD OR Baseline Sign-off
    THEN approver = Project Sponsor

ELSE IF artifact is Stakeholder Register OR Communication Plan
    THEN approver = Product Owner

ELSE IF artifact is SRS
    THEN approver = Tech Lead

ELSE IF artifact is Use Case Document OR RTM OR Validation Report
    THEN approver = Business Analyst
```

### When to Update an Artifact After Baseline

```
IF a Change Request (CR) is approved by CCB
    THEN identify affected artifacts:
        IF CR changes business requirements
            THEN update BRD, RTM, and request new Baseline Sign-off
        IF CR changes software requirements
            THEN update SRS, RTM, and request new Baseline Sign-off
        IF CR introduces new stakeholders
            THEN update Stakeholder Register and Communication Plan
    THEN re-run validation on affected requirements
    THEN update Validation Report
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Requirements Engineering Standard | Standard | ../standards/requirements-engineering-standard.md |
| Requirements Traceability Standard | Standard | ../standards/requirements-traceability.md |
| Business Requirements Document | Template | ../templates/business-requirements-document.md |
| Software Requirements Specification | Template | ../templates/software-requirements-specification.md |
| Stakeholder Analysis Template | Template | ../templates/stakeholder-analysis-template.md |
| Use Case Template | Template | ../templates/use-case-template.md |
| Requirements Traceability Matrix | Template | ../templates/requirements-traceability-matrix.md |
| Change Request Form | Template | ../templates/change-request-form.md |
| Extract Business Requirements | Runbook | ../runbooks/extract-business-requirements.md |
| Derive Software Requirements | Runbook | ../runbooks/derive-software-requirements.md |
| Validate Requirements | Runbook | ../runbooks/validate-requirements.md |
| Manage Requirements Changes | Runbook | ../runbooks/manage-requirements-changes.md |
| RACI Matrix | Reference | ./raci-matrix.md |
| ISO Standards Quick Reference | Reference | ./iso-standards-quick-reference.md |
