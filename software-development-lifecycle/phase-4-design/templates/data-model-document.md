# Data Model Document

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P4-003 |
| **When to Use** | Defining database schema and data structures for each component |
| **Owner** | Developer |
| **Reviewer** | Tech Lead |
| **SLA** | 2 business days per component |
| **Runbook** | ../runbooks/design-data-models.md |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Seed Data and Denormalization Notes optional; ERD can be text description
> **IF** medium project (3-5 devs) **THEN** All sections required; Seed Data can list tables only without counts
> **IF** large project (6+ devs) **THEN** Full template required

---

## [ ] Document Control

| Field | Value |
|-------|-------|
| Component | [Component name] |
| Author | [Name] |
| Date | YYYY-MM-DD |
| Database | PostgreSQL [version] |

---

## [ ] Entity Relationship Diagram

```
[ASCII ERD -- show tables and relationships]

+-------------------+     +-------------------+
| [table_1]         |     | [table_2]         |
|-------------------|     |-------------------|
| id          UUID  |<-+  | id          UUID  |
| [column]  [type]  |  +--| [fk]_id    UUID   |
| created_at TSTZ   |     | [column]  [type]  |
| updated_at TSTZ   |     | created_at TSTZ   |
+-------------------+     +-------------------+
```

---

## [ ] Table Definitions

### [ ] [table_name]

| Column | Type | Nullable | Default | Constraints | Description |
|--------|------|----------|---------|-------------|-------------|
| id | UUID | No | gen_random_uuid() | PRIMARY KEY | |
| [column] | [type] | Yes/No | [default] | [constraints] | [description] |
| created_at | TIMESTAMPTZ | No | NOW() | | Record creation time |
| updated_at | TIMESTAMPTZ | No | NOW() | | Last modification time |
| deleted_at | TIMESTAMPTZ | Yes | NULL | | Soft delete timestamp |

---

## [ ] Relationships

| From Table | To Table | Type | Foreign Key | On Delete |
|-----------|---------|------|-------------|-----------|
| [table] | [table] | Many-to-One | [fk_column] | RESTRICT/CASCADE |

---

## [ ] Indexes

| Name | Table | Columns | Type | Rationale |
|------|-------|---------|------|-----------|
| [idx_name] | [table] | [columns] | B-tree/Unique/GIN | [Why] |

---

## [ ] Constraints

```sql
ALTER TABLE [table]
  ADD CONSTRAINT [name] CHECK ([condition]);
```

---

## [ ] Migration Files

| Order | File | Description |
|-------|------|-------------|
| 001 | [filename].sql | [What it creates/changes] |

---

## [ ] Seed Data

| Table | Records | Purpose |
|-------|---------|---------|
| [table] | [count] | [Development/testing purpose] |

---

## [ ] Denormalization Notes

| Table | Column | Rationale |
|-------|--------|-----------|
| [table] | [column] | [Why denormalized] |

---

## COMPLETION CHECKLIST

- [ ] Document Control filled in with component name and database version
- [ ] Entity Relationship Diagram shows all tables and relationships
- [ ] Table Definitions include all columns with types, nullability, defaults, and constraints
- [ ] Relationships documented with foreign keys and delete behavior
- [ ] Indexes defined with rationale for each
- [ ] Check constraints and custom constraints documented
- [ ] Migration files listed in execution order
- [ ] Seed data requirements specified
- [ ] Denormalization decisions documented with rationale
- [ ] All tables include id, created_at, updated_at columns
- [ ] Peer reviewed by Tech Lead

---

## CROSS-REFERENCES

| Document | Relationship | Link |
|----------|-------------|------|
| Detailed Design Document | Parent component design referencing this data model | ./detailed-design-document.md |
| API Specification | API contracts that read/write this data | ./api-specification.md |
| Design Review Checklist | Review gate for data model design | ./design-review-checklist.md |
| Design Data Models Runbook | Step-by-step procedure | ../runbooks/design-data-models.md |
| Software Requirements Specification | Source requirements (SWR-XXX) | ../../phase-2-requirements-engineering/templates/software-requirements-specification.md |
