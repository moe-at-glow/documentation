# Detailed Design Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P4-001 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead |
| **Verification Method** | Design Review |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Sections: Component Overview, Public Interface, Data Model, Error Handling only
> **IF** medium project (3-5 devs) **THEN** All sections required; Design Decisions may be abbreviated
> **IF** large project (6+ devs) **THEN** Full compliance required

---

## COMPLIANCE REQUIREMENTS

### DDD Required Sections

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | DDD must include Component Overview (name, responsibility, architectural context) | All components | [ ] Section present and complete | Block design approval |
| 2 | DDD must include Public Interface (all methods/endpoints exposed) | All components | [ ] All public methods documented | Block design approval |
| 3 | DDD must include Internal Structure (classes, modules, functions, relationships) | All components | [ ] Structure diagram or description present | Block design approval |
| 4 | DDD must include Data Model (tables, entities, relationships owned) | All components | [ ] ER diagram or table definitions present | Block design approval |
| 5 | DDD must include Business Logic (algorithms, state machines, decision rules) | All components | [ ] Logic documented for each requirement | Block design approval |
| 6 | DDD must include Error Handling (detection, reporting, recovery) | All components | [ ] Error scenarios enumerated | Block design approval |
| 7 | DDD must include Logging and Observability (log levels, metrics) | All components | [ ] Logging strategy documented | Block design approval |
| 8 | DDD must include Security (auth, authorization, input validation) | All components | [ ] Security controls specified | Block design approval |
| 9 | DDD must include Dependencies (external services, libraries, internal components) | All components | [ ] Dependency list complete | Block design approval |
| 10 | DDD must include Design Decisions (patterns used, rationale) | All components | [ ] Decisions recorded with rationale | Block design approval |

### SOLID Principles

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 11 | Single Responsibility: each class/module has one reason to change | All classes/modules | [ ] Review class responsibilities | Rework design |
| 12 | Open/Closed: open for extension, closed for modification | Extension points | [ ] Strategy/plugin patterns used where applicable | Rework design |
| 13 | Liskov Substitution: subtypes substitutable for base types | All inheritance | [ ] Review subtype contracts | Rework design |
| 14 | Interface Segregation: clients do not depend on unused methods | All interfaces | [ ] Review interface granularity | Rework design |
| 15 | Dependency Inversion: depend on abstractions, not concretions | All service dependencies | [ ] Review dependency direction | Rework design |

### Additional Design Principles

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 16 | DRY: extract shared logic; prefer duplication over wrong abstraction | All code | [ ] No copy-pasted logic across components | Rework design |
| 17 | KISS: choose simplest approach satisfying the requirement | All designs | [ ] No over-engineered solutions | Rework design |
| 18 | YAGNI: do not design for hypothetical future requirements | All designs | [ ] Every element traces to SRS requirement | Rework design |
| 19 | Fail Fast: validate inputs at boundary, throw immediately on invariant violation | All boundaries | [ ] Input validation at entry points | Rework design |

### Naming Conventions -- Code Elements

| Element | Convention | Example |
|---------|-----------|---------|
| Class/Interface (JS/TS) | PascalCase | RentalService, LateFeeCalculator |
| Function/Method | camelCase | calculateLateFee, getRentalById |
| Variable | camelCase | rentalAgreement, daysOverdue |
| Constant | SCREAMING_SNAKE_CASE | MAX_RENTAL_DURATION_DAYS, LATE_FEE_PERCENTAGE |
| File (module) | kebab-case | rental-service.ts, late-fee-calculator.ts |
| Test file | [module].test.ts or [module].spec.ts | rental-service.test.ts |
| Type/Interface (TS) | PascalCase, prefix I optional | RentalAgreement, IRentalRepository |

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 20 | All code elements follow naming convention table above | All code | [ ] Naming audit during review | Reject PR |

### Design Quality Criteria

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 21 | Completeness: every requirement assigned to component has a design element | All components | [ ] Requirements traceability matrix checked | Block design approval |
| 22 | Consistency: design follows architecture conventions and patterns | All components | [ ] Patterns match architecture doc | Block design approval |
| 23 | Testability: each public method testable in isolation with mocks | All public methods | [ ] Test strategy described | Block design approval |
| 24 | Traceability: every design element traces to one or more SWRs | All design elements | [ ] SWR references present | Block design approval |
| 25 | Feasibility: implementable with available technology and team skills | All designs | [ ] Tech stack validated | Block design approval |
| 26 | Simplicity: simplest approach that satisfies requirements | All designs | [ ] No unnecessary complexity | Block design approval |

---

## COMPLIANCE CHECKLIST

- [ ] DDD contains all 10 required sections
- [ ] SOLID principles applied and documented
- [ ] DRY/KISS/YAGNI/Fail Fast principles followed
- [ ] All code elements follow naming conventions
- [ ] Every requirement has a corresponding design element
- [ ] Every design element traces to an SWR
- [ ] Each public method is testable in isolation
- [ ] Design patterns match architecture conventions
- [ ] Design is implementable with current tech stack
- [ ] Design decisions include rationale
- [ ] Database elements reference Database Design Standard
- [ ] API elements reference API Design Standard

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Create Detailed Design | Runbook | ../runbooks/create-detailed-design.md |
| Conduct Design Review | Runbook | ../runbooks/conduct-design-review.md |
| Detailed Design Document | Template | ../templates/detailed-design-document.md |
| Design Review Checklist | Template | ../templates/design-review-checklist.md |
| Database Design Standard | Standard | database-design-standard.md |
| API Design Standard | Standard | api-design-standard.md |
