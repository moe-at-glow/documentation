# Create Detailed Design

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P4-001 |
| **Owner** | Developer |
| **Accountable** | Tech Lead |
| **SLA** | 5 business days per component |
| **Escalation** | Tech Lead (technical), Product Owner (scope) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Approved Architecture Description Document available
- [ ] Component assigned and identified in the architecture
- [ ] SRS available with requirements mapped to this component
- [ ] Detailed Design Standard reviewed
- [ ] DDD Template obtained

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Architecture not approved | STOP. Wait for ADD approval before designing components | Tech Lead |
| Requirements ambiguous or conflicting | STOP. Request SRS clarification | Product Owner |
| Component boundaries unclear | STOP. Request architecture clarification | Tech Lead |
| Assigned component not in ADD | STOP. Verify component assignment | Tech Lead |

---

## PROCEDURE

### Step 1: Review Architecture Context

| Action | Owner | SLA |
|--------|-------|-----|
| Read ADD section for assigned component | Developer | 2 hours |
| Note component responsibility, owned data, and interfaces | Developer | 1 hour |
| Read all ADRs affecting this component | Developer | 1 hour |
| List SWR IDs assigned to this component | Developer | 30 min |

- [ ] Component responsibility documented
- [ ] Owned data identified
- [ ] Interfaces catalogued
- [ ] Relevant ADRs listed
- [ ] SWR IDs mapped to component

> **IF** ADR conflicts with SRS requirement **THEN** escalate to Tech Lead
> **ELSE IF** component has no assigned requirements **THEN** verify assignment with Tech Lead
> **ELSE** proceed to Step 2

### Step 2: Define Public Interface

| Action | Owner | SLA |
|--------|-------|-----|
| Document every method, endpoint, or event exposed to other components or users | Developer | 4 hours |
| Define request/response schemas per API Design Standard | Developer | 2 hours |

- [ ] All REST endpoints listed with method, URL, description
- [ ] All published events listed with payload schema
- [ ] All internal service methods listed with signatures
- [ ] Request/response schemas defined for each endpoint

> **IF** interface duplicates another component's endpoint **THEN** resolve ownership with Tech Lead
> **ELSE IF** interface requires data from another component **THEN** document dependency and coordinate with owning developer
> **ELSE** proceed to Step 3

### Step 3: Design Internal Structure

| Action | Owner | SLA |
|--------|-------|-----|
| Break component into internal modules | Developer | 3 hours |
| Define responsibility, public methods, and dependencies for each module | Developer | 2 hours |

- [ ] Module directory structure defined
- [ ] Each module has single responsibility documented (one sentence)
- [ ] Public methods with signatures defined per module
- [ ] Dependencies (imports/injections) listed per module
- [ ] Test file locations identified

> **IF** module has more than one responsibility **THEN** split into separate modules
> **ELSE IF** circular dependency detected **THEN** refactor to eliminate cycle
> **ELSE** proceed to Step 4

### Step 4: Design Data Model

| Action | Owner | SLA |
|--------|-------|-----|
| Identify entities from requirements | Developer | 1 hour |
| Define attributes with data types | Developer | 2 hours |
| Define relationships and foreign keys | Developer | 1 hour |
| Add required columns (id, created_at, updated_at) | Developer | 30 min |
| Define indexes for query patterns | Developer | 1 hour |
| Write CREATE TABLE statements | Developer | 1 hour |

- [ ] All entities identified
- [ ] All attributes defined with types and constraints
- [ ] Relationships defined with FK and ON DELETE behavior
- [ ] Standard columns present (id, created_at, updated_at, deleted_at)
- [ ] Indexes defined for all query patterns
- [ ] Database Design Standard followed

> **IF** component has no persistent data **THEN** skip this step, document rationale
> **ELSE IF** data model conflicts with another component's schema **THEN** resolve with Tech Lead
> **ELSE** proceed to Step 5

### Step 5: Design Business Logic

| Action | Owner | SLA |
|--------|-------|-----|
| State each business rule with requirement reference | Developer | 2 hours |
| Define algorithm or decision logic for each rule | Developer | 3 hours |
| Identify edge cases and boundary conditions | Developer | 2 hours |
| Define error conditions and handling per rule | Developer | 1 hour |

- [ ] Each business rule linked to SWR ID
- [ ] Algorithm/logic documented for each rule
- [ ] Edge cases identified and handling defined
- [ ] Error conditions listed with responses
- [ ] Input/output types and formats specified

> **IF** business rule contradicts another rule **THEN** escalate to Product Owner
> **ELSE IF** edge case handling unclear **THEN** request clarification from Product Owner
> **ELSE** proceed to Step 6

### Step 6: Design Error Handling

| Action | Owner | SLA |
|--------|-------|-----|
| List all error scenarios for this component | Developer | 1 hour |
| Define detection, response, and recovery for each error | Developer | 2 hours |

- [ ] Every error scenario has detection method
- [ ] Every error scenario has HTTP status and error code
- [ ] Recovery strategy defined (retry, queue, none)
- [ ] Client errors vs server errors distinguished

> **IF** error requires cross-component coordination **THEN** document and coordinate with owning developer
> **ELSE** proceed to Step 7

### Step 7: Design Logging and Monitoring

| Action | Owner | SLA |
|--------|-------|-----|
| Define log points with level and data | Developer | 1 hour |
| Verify no sensitive data logged (passwords, tokens, PII) | Developer | 30 min |

- [ ] Log points defined for: request received, operation completed, external calls, errors, performance warnings
- [ ] Log levels assigned (INFO, DEBUG, ERROR, WARN)
- [ ] Sensitive data exclusions verified
- [ ] Monitoring thresholds defined

### Step 8: Design Security Considerations

| Action | Owner | SLA |
|--------|-------|-----|
| Define input validation approach | Developer | 1 hour |
| Define authorization checks | Developer | 1 hour |
| Verify SQL injection prevention | Developer | 30 min |
| Define data exposure controls | Developer | 30 min |

- [ ] Input validation at controller level
- [ ] Parameterized queries (no string concatenation)
- [ ] Role-based authorization per endpoint
- [ ] DTOs used to limit data exposure

### Step 9: Create Sequence Diagrams

| Action | Owner | SLA |
|--------|-------|-----|
| Identify interactions involving 3+ components | Developer | 30 min |
| Create sequence diagram for each complex interaction | Developer | 2 hours |

- [ ] All multi-component interactions identified
- [ ] Sequence diagram created for each

> **IF** no interactions involve 3+ components **THEN** skip, document rationale
> **ELSE** create diagrams and proceed

### Step 10: Document Design Patterns Used

| Action | Owner | SLA |
|--------|-------|-----|
| List each design pattern with location and justification | Developer | 1 hour |

- [ ] Each pattern mapped to file/module
- [ ] Justification documented for each pattern choice

### Step 11: Submit for Design Review

| Action | Owner | SLA |
|--------|-------|-----|
| Follow Conduct Design Review runbook | Developer | Per review SLA |

- [ ] DDD completed using template
- [ ] Design review initiated

---

## EXIT CRITERIA

- [ ] Detailed Design Document completed using DDD Template
- [ ] All public interfaces fully defined
- [ ] Internal module structure designed
- [ ] Data model designed with all required columns and indexes
- [ ] Business logic documented with edge cases
- [ ] Error handling designed for every scenario
- [ ] Logging and monitoring points defined
- [ ] Security considerations addressed
- [ ] Sequence diagrams created for complex interactions
- [ ] Design patterns documented
- [ ] Design review submitted
- [ ] RTM updated with design references

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Detailed Design Document | [DDD Template](../templates/detailed-design-document.md) | Project repository /docs/design/ |
| Updated RTM | -- | Project repository /docs/traceability/ |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Detailed Design Standard | Standard | [../standards/detailed-design-standard.md](../standards/detailed-design-standard.md) |
| API Design Standard | Standard | [../standards/api-design-standard.md](../standards/api-design-standard.md) |
| Database Design Standard | Standard | [../standards/database-design-standard.md](../standards/database-design-standard.md) |
| DDD Template | Template | [../templates/detailed-design-document.md](../templates/detailed-design-document.md) |
| Design Review Checklist | Template | [../templates/design-review-checklist.md](../templates/design-review-checklist.md) |
| Conduct Design Review | Runbook | [conduct-design-review.md](conduct-design-review.md) |
| Design API Contracts | Runbook | [design-api-contracts.md](design-api-contracts.md) |
| Design Data Models | Runbook | [design-data-models.md](design-data-models.md) |
