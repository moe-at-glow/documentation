# Design Artifacts Checklist

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P4-001 |
| **Use When** | Determining which design artifacts are required for a component |
| **Last Updated** | 2026-03-04 |

---

## ARTIFACT REQUIREMENTS

| Artifact | Description | Owner | Required | Approval |
|----------|-------------|-------|----------|----------|
| Detailed Design Document (DDD) | Internal structure, business logic, error handling per component | Developer / Tech Lead | Yes (per component) | Tech Lead |
| API Specification | Endpoint definitions, schemas, error codes, auth requirements | Developer / Tech Lead | Yes (if component has REST API) | Tech Lead + API consumer |
| Data Model | Table definitions, relationships, indexes, constraints, migrations | Developer / Tech Lead | Yes (if component owns data) | Tech Lead / DBA |
| UI Wireframes | Layout, navigation, interaction flows | UX Designer / Developer | Yes (if user-facing) | Product Owner + Tech Lead |
| Sequence Diagrams | Runtime interaction flows for complex scenarios | Developer / Tech Lead | Yes (for 3+ component interactions) | Tech Lead |
| Design Review Record | Findings, decision, action items from review | Tech Lead | Yes | -- |
| Updated RTM | Design references added to traceability matrix | Business Analyst | Yes | Business Analyst |

---

## COMPLETION CHECKLIST

- [ ] DDD complete for every component being developed
- [ ] API specifications complete for all API-exposing components
- [ ] Data model complete with migration scripts structure
- [ ] UI wireframes complete for all user-facing features
- [ ] Sequence diagrams for complex multi-component interactions
- [ ] Design review conducted for each component
- [ ] Review findings addressed
- [ ] RTM updated with design references
- [ ] Design baseline established

---

## DECISION TREE

### Which artifacts does my component need?

```
IF component is being developed
  THEN DDD is REQUIRED

  IF component exposes a REST API
    THEN API Specification is REQUIRED
  ELSE
    API Specification is NOT REQUIRED

  IF component owns data (database tables)
    THEN Data Model is REQUIRED
  ELSE
    Data Model is NOT REQUIRED

  IF component has a user-facing interface
    THEN UI Wireframes are REQUIRED
  ELSE
    UI Wireframes are NOT REQUIRED

  IF component interacts with 3+ other components
    THEN Sequence Diagrams are REQUIRED
  ELSE
    Sequence Diagrams are NOT REQUIRED

THEN ALWAYS:
  - Design Review Record is REQUIRED
  - Updated RTM is REQUIRED
```

### Is the design phase complete?

```
IF all required artifacts are produced
  AND design review is conducted for each component
  AND all review findings are addressed
  AND RTM is updated with design references
  THEN establish design baseline → Phase complete
ELSE
  THEN identify missing artifacts → Complete them before proceeding
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Create Detailed Design | Runbook | ../runbooks/create-detailed-design.md |
| Design API Contracts | Runbook | ../runbooks/design-api-contracts.md |
| Design Data Models | Runbook | ../runbooks/design-data-models.md |
| Conduct Design Review | Runbook | ../runbooks/conduct-design-review.md |
