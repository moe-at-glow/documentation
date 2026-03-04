# Requirements Traceability Standard

Standard for maintaining requirements traceability at GlowPowerRental.

---

## Purpose

Traceability ensures every requirement can be traced from its business origin through design, implementation, and testing. It answers:

- Where did this requirement come from?
- What design and code implement it?
- What tests verify it?
- What is the impact if this requirement changes?

---

## Traceability Directions

### Forward Traceability

Traces from source to implementation and verification.

```
Business Requirement (BR)
   --> Stakeholder Requirement (STK)
      --> System Requirement (SYS)
         --> Software Requirement (SWR)
            --> Design Component
               --> Code Module
                  --> Test Case
```

Use forward traceability to answer: "Is every requirement implemented and tested?"

### Backward Traceability

Traces from implementation back to source.

```
Test Case
   --> Code Module
      --> Design Component
         --> Software Requirement (SWR)
            --> System Requirement (SYS)
               --> Stakeholder Requirement (STK)
                  --> Business Requirement (BR)
```

Use backward traceability to answer: "Why does this code exist? What business need does it serve?"

---

## Traceability Matrix Structure

| Column | Description |
|--------|-------------|
| Requirement ID | Unique identifier (BR/STK/SYS/SWR) |
| Requirement Description | Brief summary |
| Source | Origin (stakeholder, regulation, business need) |
| Parent Requirement | ID of the parent-level requirement |
| Design Reference | Design document section or component |
| Code Reference | Module, class, or file implementing the requirement |
| Test Case ID | ID of the test case that verifies the requirement |
| Test Result | Pass / Fail / Not Executed |
| Status | Requirement lifecycle state |

---

## When Traceability Must Be Updated

| Event | Traceability Action |
|-------|-------------------|
| New requirement added | Add row to RTM, link to parent requirement |
| Requirement modified | Update RTM row, verify all links still valid |
| Requirement deleted or retired | Mark row as retired, note reason |
| Design created or updated | Link design reference to requirement |
| Code implemented | Link code reference to requirement |
| Test case created | Link test case ID to requirement |
| Test executed | Update test result column |
| Change request approved | Update affected rows, add new rows if needed |

---

## Coverage Metrics

| Metric | Definition | Threshold |
|--------|-----------|-----------|
| Requirements Coverage | Percentage of requirements with at least one linked test case | 100% for Must Have, 90% for Should Have |
| Forward Traceability Completeness | Percentage of requirements traceable from BR to test case | 100% for Must Have requirements |
| Backward Traceability Completeness | Percentage of test cases traceable back to a requirement | 100% (no orphan tests) |
| Implementation Coverage | Percentage of approved requirements with linked code references | 100% before release |

---

## Traceability Review

The traceability matrix is reviewed at these checkpoints:

| Checkpoint | Reviewer | Focus |
|-----------|----------|-------|
| Requirements baseline | Business Analyst, Product Owner | All requirements have parent links |
| Design review | Tech Lead | All requirements have design references |
| Code review | Tech Lead, Developer | All requirements have code references |
| Test readiness review | QA Lead | All requirements have test cases |
| Release readiness review | Product Owner, QA Lead | All metrics meet thresholds |

---

## Tools

The traceability matrix is maintained in a spreadsheet or requirements management tool. Regardless of tool:

- One authoritative copy exists (single source of truth).
- Changes are version-controlled.
- The matrix is accessible to all project team members.
