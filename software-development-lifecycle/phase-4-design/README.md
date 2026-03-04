# Phase 4: Design

Translating architecture into implementable component-level specifications for GlowPowerRental projects.

All documents follow the **QRH (Quick Reference Handbook)** format. For background/educational content, see the `training/` subdirectory.

---

## Phase Summary

| Attribute | Detail |
|-----------|--------|
| Entry Criteria | Approved Architecture Description Document and ADRs |
| Exit Criteria | Approved Detailed Design Documents, API specifications, data models, UI wireframes, design review sign-off |
| Key Roles | Tech Lead (owns design), Senior Developer (contributes), UX Designer (UI), DBA (data model), QA Lead (testability review) |
| ISO Alignment | ISO/IEC/IEEE 12207 - Design Definition Process |

---

## Documentation

### Standards (compliance checklists)

| Document | Description |
|----------|-------------|
| [Detailed Design Standard](standards/detailed-design-standard.md) | Component-level design rules, SOLID principles, naming conventions |
| [API Design Standard](standards/api-design-standard.md) | RESTful API conventions, error formats, versioning |
| [Database Design Standard](standards/database-design-standard.md) | Naming, data types, normalization, migration standards |
| [UI Design Standard](standards/ui-design-standard.md) | Responsive design, accessibility, RTL/LTR, form design |

### Runbooks (QRH procedures)

| Document | Description |
|----------|-------------|
| [Create Detailed Design](runbooks/create-detailed-design.md) | Step-by-step design procedure |
| [Design API Contracts](runbooks/design-api-contracts.md) | Step-by-step API design procedure |
| [Design Data Models](runbooks/design-data-models.md) | Step-by-step data modeling procedure |
| [Conduct Design Review](runbooks/conduct-design-review.md) | Design review meeting procedure |

### Guides (quick references)

| Document | Description |
|----------|-------------|
| [Design Patterns Guide](guides/design-patterns-guide.md) | When and how to use design patterns |
| [From Architecture to Design](guides/from-architecture-to-design.md) | Transformation walkthrough |
| [Common Design Pitfalls](guides/common-design-pitfalls.md) | Mistakes and how to avoid them |

### Training Materials

| Document | Description |
|----------|-------------|
| [Design Phase Overview](guides/training/design-phase-overview.md) | Background on how design works and why it matters |

### References (decision aids)

| Document | Description |
|----------|-------------|
| [Design Artifacts Checklist](references/design-artifacts-checklist.md) | All required Phase 4 artifacts |
| [Design Patterns Quick Reference](references/design-patterns-quick-reference.md) | Pattern lookup table |
| [HTTP Status Codes Reference](references/http-status-codes-reference.md) | API status codes with usage guidance |

### Templates

| Document | Description |
|----------|-------------|
| [Detailed Design Document](templates/detailed-design-document.md) | DDD template |
| [API Specification](templates/api-specification.md) | API spec template |
| [Data Model Document](templates/data-model-document.md) | Data model documentation template |
| [Design Review Checklist](templates/design-review-checklist.md) | Review checklist template |

### PlantUML Diagram Templates (`diagrams/`)

All design diagrams **must** be created as PlantUML `.puml` files. Copy these templates and fill in your project details:

| Diagram | Template | Required |
|---------|----------|----------|
| Class Diagram | [class-diagram.puml](diagrams/class-diagram.puml) | All components |
| API Flow Diagram | [api-flow-diagram.puml](diagrams/api-flow-diagram.puml) | All API components |
| Data Flow Diagram | [data-flow-diagram.puml](diagrams/data-flow-diagram.puml) | All data-processing components |
