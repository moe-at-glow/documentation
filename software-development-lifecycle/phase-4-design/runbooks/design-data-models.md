# Design Data Models

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P4-003 |
| **Owner** | Developer |
| **Accountable** | Tech Lead |
| **SLA** | 3 business days per data domain |
| **Escalation** | Tech Lead (technical), Product Owner (scope) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Architecture defines which component owns which data
- [ ] SRS data requirements identified
- [ ] Database Design Standard reviewed
- [ ] Data Model Document Template obtained

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Data ownership unclear between components | STOP. Clarify ownership in architecture | Tech Lead |
| SRS data requirements incomplete | STOP. Request SRS update | Product Owner |
| Database Design Standard not available | STOP. Obtain standard before proceeding | Tech Lead |
| Target database technology not selected | STOP. Resolve technology decision via ADR | Tech Lead |

---

## PROCEDURE

### Step 1: Identify Entities

| Action | Owner | SLA |
|--------|-------|-----|
| Extract entities from SRS requirements and design documents | Developer | 2 hours |
| Map each entity to source requirement | Developer | 1 hour |

- [ ] All entities extracted from requirements
- [ ] Each entity mapped to source SWR ID
- [ ] Entity descriptions documented
- [ ] No duplicate entities across components

> **IF** entity appears to belong to another component **THEN** verify ownership with Tech Lead
> **ELSE IF** requirement does not map to any entity **THEN** create new entity or clarify requirement with Product Owner
> **ELSE** proceed to Step 2

### Step 2: Define Attributes

| Action | Owner | SLA |
|--------|-------|-----|
| List all attributes per entity with data types | Developer | 3 hours |
| Mark nullable, default, and constraints per attribute | Developer | 2 hours |
| Map each attribute to source requirement | Developer | 1 hour |

- [ ] Every attribute has column name, type, nullable flag, default, and constraints
- [ ] Naming follows Database Design Standard (snake_case)
- [ ] Source requirement mapped per attribute
- [ ] Standard columns included: id (UUID, PK), created_at (TIMESTAMPTZ), updated_at (TIMESTAMPTZ)
- [ ] Soft delete column included where applicable: deleted_at (TIMESTAMPTZ, nullable)

> **IF** attribute type is ambiguous **THEN** consult Database Design Standard for type guidance
> **ELSE IF** attribute duplicates data in another entity **THEN** evaluate normalization in Step 4
> **ELSE** proceed to Step 3

### Step 3: Define Relationships

| Action | Owner | SLA |
|--------|-------|-----|
| Define relationship type between entities (1:1, 1:N, M:N) | Developer | 1 hour |
| Define foreign key columns and ON DELETE behavior | Developer | 1 hour |

- [ ] All relationships defined with from/to entities
- [ ] Relationship type documented (Many-to-One, One-to-Many, Many-to-Many)
- [ ] Foreign key columns specified
- [ ] ON DELETE behavior specified (RESTRICT, CASCADE, SET NULL)

> **IF** Many-to-Many relationship exists **THEN** create junction table with composite key
> **ELSE IF** relationship crosses component boundaries **THEN** use ID reference only (no FK constraint), document in design
> **ELSE** proceed to Step 4

### Step 4: Normalize to 3NF

| Action | Owner | SLA |
|--------|-------|-----|
| Verify 1NF: no repeating groups | Developer | 30 min |
| Verify 2NF: no partial dependencies | Developer | 30 min |
| Verify 3NF: no transitive dependencies | Developer | 30 min |
| Document any intentional denormalization with rationale | Developer | 1 hour |

- [ ] 1NF verified
- [ ] 2NF verified
- [ ] 3NF verified
- [ ] All intentional denormalizations documented with business rationale

> **IF** denormalization needed for performance **THEN** document rationale, table, column, and source of truth
> **ELSE IF** normalization violation found **THEN** refactor schema to eliminate violation
> **ELSE** proceed to Step 5

### Step 5: Define Indexes

| Action | Owner | SLA |
|--------|-------|-----|
| Identify query patterns from requirements and API design | Developer | 1 hour |
| Define index per query pattern | Developer | 1 hour |
| Define unique indexes for business uniqueness constraints | Developer | 30 min |

- [ ] Index defined for each foreign key column
- [ ] Index defined for each filtered/sorted column in list endpoints
- [ ] Composite indexes defined for multi-column query patterns
- [ ] Unique indexes defined for business uniqueness constraints
- [ ] Index naming follows Database Design Standard

> **IF** query pattern requires full-text search **THEN** define GIN/GiST index, document configuration
> **ELSE IF** table expected to exceed 1M rows **THEN** evaluate partitioning strategy, escalate to Tech Lead
> **ELSE** proceed to Step 6

### Step 6: Define Constraints

| Action | Owner | SLA |
|--------|-------|-----|
| Define CHECK constraints for value validation | Developer | 1 hour |
| Define UNIQUE constraints for business rules | Developer | 30 min |
| Write constraint SQL statements | Developer | 1 hour |

- [ ] CHECK constraints defined for value ranges and allowed values
- [ ] UNIQUE constraints defined for business uniqueness rules
- [ ] FK constraints defined with proper ON DELETE
- [ ] NOT NULL constraints applied to required fields
- [ ] Constraint naming follows Database Design Standard

### Step 7: Design Migration Scripts

| Action | Owner | SLA |
|--------|-------|-----|
| Create versioned migration file structure | Developer | 1 hour |
| Write UP and DOWN sections per migration | Developer | 2 hours |

- [ ] Migration files numbered sequentially
- [ ] Tables created in dependency order (referenced tables first)
- [ ] Each migration has UP (apply) and DOWN (rollback) sections
- [ ] DOWN section correctly reverses UP section

> **IF** migration modifies existing table **THEN** verify backward compatibility, document breaking changes
> **ELSE** proceed to Step 8

### Step 8: Design Seed Data

| Action | Owner | SLA |
|--------|-------|-----|
| Define seed data records per table for dev/test | Developer | 2 hours |
| Verify seed data covers edge cases | Developer | 1 hour |

- [ ] Seed data defined for every table
- [ ] Record count sufficient for testing (pagination, filtering)
- [ ] Seed data covers status variations (active, returned, overdue, cancelled)
- [ ] Seed data referential integrity maintained

### Step 9: Submit for Review

| Action | Owner | SLA |
|--------|-------|-----|
| Submit data model to Tech Lead for review | Developer | 1 hour |
| Verify all SRS data requirements covered | Tech Lead | 1 business day |
| Verify naming follows Database Design Standard | Tech Lead | 1 business day |
| Verify indexes support identified query patterns | Tech Lead | 1 business day |
| Approve data model | Tech Lead | 1 business day |

- [ ] Data model submitted for review
- [ ] All SRS data requirements covered
- [ ] Naming follows Database Design Standard
- [ ] Indexes support query patterns
- [ ] Data model approved by Tech Lead

> **IF** review identifies blocking issues **THEN** fix and resubmit
> **ELSE IF** review identifies minor issues **THEN** fix, no re-review required
> **ELSE** data model approved

---

## EXIT CRITERIA

- [ ] All entities identified from requirements
- [ ] All attributes defined with data types and constraints
- [ ] All relationships defined with foreign keys and delete behavior
- [ ] Normalized to 3NF (denormalization documented if any)
- [ ] Standard columns present (id, created_at, updated_at)
- [ ] Indexes defined for all query patterns
- [ ] Constraints defined (CHECK, UNIQUE, FK, NOT NULL)
- [ ] Migration scripts structured with UP/DOWN
- [ ] Seed data designed for dev/test
- [ ] Reviewed and approved by Tech Lead

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Data Model Document | [Data Model Document Template](../templates/data-model-document.md) | Project repository /docs/design/data/ |
| Migration Scripts | -- | Project repository /migrations/ |
| Seed Data Scripts | -- | Project repository /seeds/ |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Database Design Standard | Standard | [../standards/database-design-standard.md](../standards/database-design-standard.md) |
| Data Model Document Template | Template | [../templates/data-model-document.md](../templates/data-model-document.md) |
| Create Detailed Design | Runbook | [create-detailed-design.md](create-detailed-design.md) |
| Design API Contracts | Runbook | [design-api-contracts.md](design-api-contracts.md) |
| Conduct Design Review | Runbook | [conduct-design-review.md](conduct-design-review.md) |
