# Database Design Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P4-003 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead |
| **Verification Method** | Design Review |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Naming conventions, required columns, data types required; audit trail optional
> **IF** medium project (3-5 devs) **THEN** Full compliance; denormalization documentation may be abbreviated
> **IF** large project (6+ devs) **THEN** Full compliance required

---

## COMPLIANCE REQUIREMENTS

### Naming Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| Table name | Plural, snake_case | rental_agreements, equipment_items, late_fee_invoices |
| Column name | snake_case | customer_name, return_date, daily_rate |
| Primary key | id | id (UUID or BIGINT) |
| Foreign key | {referenced_table_singular}_id | customer_id, equipment_id |
| Index name | idx_{table}_{column(s)} | idx_rental_agreements_customer_id |
| Unique constraint | uq_{table}_{column(s)} | uq_customers_email |
| Check constraint | chk_{table}_{description} | chk_rental_agreements_end_after_start |
| Foreign key constraint | fk_{table}_{referenced_table} | fk_rental_agreements_customers |

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | All database elements follow naming convention table above | All tables, columns, constraints, indexes | [ ] Naming audit against convention table | Reject migration |

### Required Columns

Every table must include:

| Column | Type | Default |
|--------|------|---------|
| id | UUID or BIGINT (auto-increment) | gen_random_uuid() or auto |
| created_at | TIMESTAMP WITH TIME ZONE | NOW() |
| updated_at | TIMESTAMP WITH TIME ZONE | NOW() (updated by trigger) |

| Use UUID | Use BIGINT |
|----------|-----------|
| Distributed systems or multi-database sync | Single database, sequential ordering matters |
| IDs exposed in URLs (harder to guess) | Internal-only IDs |
| Data merged across systems | High-volume tables where storage matters |

GlowPowerRental default: **UUID** for all new tables.

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 2 | Every table has id, created_at, updated_at columns | All tables | [ ] Required columns present | Reject migration |
| 3 | UUID used for all new tables unless BIGINT exception justified | All new tables | [ ] ID type validated | Reject migration |

### Soft Delete

| Column | Type | Behavior |
|--------|------|----------|
| deleted_at | TIMESTAMP WITH TIME ZONE, nullable | NULL = active, non-NULL = soft-deleted |

| Tables Requiring Soft Delete | Tables Where Hard Delete Is Acceptable |
|------------------------------|---------------------------------------|
| rental_agreements, customers, invoices, equipment_items | sessions, temporary tokens, cache entries |

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 4 | Soft-delete tables have deleted_at column | rental_agreements, customers, invoices, equipment_items | [ ] deleted_at column present | Reject migration |
| 5 | All queries on soft-delete tables filter `WHERE deleted_at IS NULL` unless explicitly querying deleted records | All queries on soft-delete tables | [ ] Query audit for deleted_at filter | Reject PR |

### Data Types

| Use Case | Data Type | Example |
|----------|-----------|---------|
| Monetary amounts | DECIMAL(12,2) | daily_rate DECIMAL(12,2) NOT NULL |
| Percentages | DECIMAL(5,4) | late_fee_rate DECIMAL(5,4) DEFAULT 0.0200 |
| Short text (known max) | VARCHAR(N) | email VARCHAR(255) |
| Long text (unknown length) | TEXT | notes TEXT |
| Boolean | BOOLEAN | is_overdue BOOLEAN DEFAULT FALSE |
| Date only | DATE | start_date DATE NOT NULL |
| Date and time | TIMESTAMP WITH TIME ZONE | created_at TIMESTAMPTZ |
| Enumerated values | VARCHAR with CHECK constraint | status VARCHAR(20) CHECK (status IN ('active','returned','overdue','cancelled')) |
| JSON metadata | JSONB | metadata JSONB DEFAULT '{}' |
| Binary/files | Store file in object storage, store URL in DB | document_url VARCHAR(500) |

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 6 | Never use FLOAT or DOUBLE for monetary amounts | All monetary columns | [ ] Monetary columns use DECIMAL | Reject migration |
| 7 | Data types match use-case table above | All columns | [ ] Data type audit | Reject migration |

### Indexing Strategy

| Add Index When | Example |
|---------------|---------|
| Column used in WHERE clauses frequently | idx_rental_agreements_status |
| Column used in JOIN conditions | idx_rental_agreements_customer_id |
| Column used in ORDER BY | idx_rental_agreements_created_at |
| Column has uniqueness constraint | uq_customers_email |
| Column combination queried together | idx_rental_agreements_status_customer_id |

| Do NOT Add Index When |
|----------------------|
| Table has fewer than 1,000 rows |
| Column is rarely queried |
| High write volume where index maintenance overhead matters |

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 8 | Indexes added for columns in WHERE, JOIN, ORDER BY clauses | Frequently queried columns | [ ] Index coverage reviewed | Rework migration |
| 9 | Composite index: most selective column first | Composite indexes | [ ] Column order validated | Rework migration |
| 10 | No unnecessary indexes on small tables (<1,000 rows) or rarely queried columns | All indexes | [ ] Index justification documented | Rework migration |

### Normalization

Baseline: Third Normal Form (3NF).

| Normal Form | Rule |
|-------------|------|
| 1NF | No repeating groups, atomic values |
| 2NF | No partial dependencies |
| 3NF | No transitive dependencies |

| Acceptable Denormalization | Justification Required |
|---------------------------|----------------------|
| Reporting/analytics (materialized views) | Avoids expensive JOINs on read-heavy reports |
| Snapshot data (e.g., customer_name on invoice) | Must show value at time of creation |
| Performance-critical read paths (cached counts) | Avoids COUNT on large tables |

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 11 | All tables normalized to 3NF minimum | All tables | [ ] Normalization validated | Reject migration |
| 12 | All denormalization decisions documented with rationale | Denormalized elements | [ ] Rationale documented | Reject migration |

### Migration Standards

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 13 | Versioned migrations with sequential number and timestamp: `001_create_rental_agreements.sql` | All migrations | [ ] Naming convention followed | Reject migration |
| 14 | Every migration includes UP (apply) script | All migrations | [ ] UP script present | Reject migration |
| 15 | Every migration includes DOWN (revert) script | All migrations | [ ] DOWN script present | Reject migration |
| 16 | Dropping columns/tables requires multi-step migration (deprecate then remove) | Destructive changes | [ ] Multi-step plan documented | Block deployment |
| 17 | Data migrations separate from schema migrations | All migrations | [ ] Separate migration files | Reject migration |
| 18 | Migrations tested: UP then DOWN on test database before production | All migrations | [ ] Test run completed | Block deployment |

### Audit Trail

Audit log table required for financial/compliance tables:

```sql
CREATE TABLE audit_log (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  table_name VARCHAR(100) NOT NULL,
  record_id UUID NOT NULL,
  action VARCHAR(10) NOT NULL CHECK (action IN ('INSERT','UPDATE','DELETE')),
  old_values JSONB,
  new_values JSONB,
  changed_by UUID NOT NULL,
  changed_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

Tables requiring audit: invoices, payments, rental_agreements, customer financial data.

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 19 | Audit log triggers enabled for financial/compliance tables | invoices, payments, rental_agreements, customer financial data | [ ] Audit triggers present | Block deployment |

---

## COMPLIANCE CHECKLIST

- [ ] All tables, columns, constraints, indexes follow naming conventions
- [ ] Every table has id, created_at, updated_at columns
- [ ] UUID used for all new tables (BIGINT exceptions justified)
- [ ] Soft-delete tables have deleted_at column
- [ ] All queries on soft-delete tables filter WHERE deleted_at IS NULL
- [ ] No FLOAT/DOUBLE used for monetary amounts
- [ ] Data types match standard use-case table
- [ ] Indexes present for WHERE, JOIN, ORDER BY columns
- [ ] Composite indexes ordered by selectivity
- [ ] All tables normalized to 3NF minimum
- [ ] Denormalization decisions documented with rationale
- [ ] Migrations versioned with sequential numbering
- [ ] Every migration has UP and DOWN scripts
- [ ] Destructive changes follow multi-step migration plan
- [ ] Data migrations separate from schema migrations
- [ ] Migrations tested (UP/DOWN) on test database
- [ ] Audit log triggers enabled for financial/compliance tables

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Design Data Models | Runbook | ../runbooks/design-data-models.md |
| Conduct Design Review | Runbook | ../runbooks/conduct-design-review.md |
| Data Model Document | Template | ../templates/data-model-document.md |
| Design Review Checklist | Template | ../templates/design-review-checklist.md |
