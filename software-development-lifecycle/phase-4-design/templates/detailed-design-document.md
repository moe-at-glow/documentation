# Detailed Design Document

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P4-001 |
| **When to Use** | Creating detailed design for each system component |
| **Owner** | Developer |
| **Reviewer** | Tech Lead |
| **SLA** | 3 business days per component |
| **Runbook** | ../runbooks/create-detailed-design.md |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Sections 7, 9 optional; Section 3 reduced to file list only
> **IF** medium project (3-5 devs) **THEN** All sections required; Section 9 can be abbreviated
> **IF** large project (6+ devs) **THEN** Full template required

---

## [ ] Document Control

| Field | Value |
|-------|-------|
| Component Name | [Component name] |
| Version | 1.0 |
| Author | [Name] |
| Date | YYYY-MM-DD |
| Related ADD Section | [Section reference in Architecture Description Document] |
| Related Requirements | [SWR-XXX, SWR-XXX] |

---

## [ ] 1. Component Overview

| Field | Value |
|-------|-------|
| Responsibility | [One sentence: what this component does] |
| Architecture Context | [How this component fits in the system -- which other components it interacts with] |
| Technology | [Language, framework, runtime] |
| Owned Data | [Database tables this component owns] |

---

## [ ] 2. Public Interface

| Method / Endpoint | Type | Description | Input | Output |
|------------------|------|-------------|-------|--------|
| [Method or URL] | REST / Event / Internal | [What it does] | [Parameters/body] | [Response/return] |

---

## [ ] 3. Internal Structure

```
[Directory structure of this component]

src/modules/[component]/
+-- [file].ts          # [Responsibility]
+-- [file].ts          # [Responsibility]
+-- __tests__/
    +-- [file].test.ts
```

### [ ] Module Descriptions

| Module | Responsibility | Dependencies |
|--------|---------------|-------------|
| [filename] | [What it does] | [What it imports] |

---

## [ ] 4. Data Model

```sql
CREATE TABLE [table_name] (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  -- [columns]
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

### [ ] Indexes

| Index | Columns | Rationale |
|-------|---------|-----------|
| [index_name] | [columns] | [Why this index exists] |

---

## [ ] 5. Business Logic

### [ ] [Rule/Algorithm Name]

**Requirement:** [SWR-XXX]

**Algorithm:**
```
[Step-by-step algorithm]
```

**Edge Cases:**
| Case | Handling |
|------|---------|
| [Edge case] | [How it is handled] |

**Error Conditions:**
| Condition | Response |
|-----------|----------|
| [Error condition] | [Error code and message] |

---

## [ ] 6. Error Handling

| Error Scenario | Detection | Response Code | Error Code | Recovery |
|---------------|----------|---------------|-----------|----------|
| [Scenario] | [How detected] | [HTTP status] | [Error code] | [Recovery action] |

---

## [ ] 7. Logging and Observability

| Log Point | Level | Data |
|-----------|-------|------|
| [When] | INFO/WARN/ERROR/DEBUG | [What is logged] |

---

## [ ] 8. Security

| Concern | Approach |
|---------|----------|
| Authentication | [How auth is handled] |
| Authorization | [Role requirements] |
| Input validation | [Validation approach] |
| Data protection | [Sensitive data handling] |

---

## [ ] 9. Design Patterns Used

| Pattern | Where | Why |
|---------|-------|-----|
| [Pattern name] | [Module/class] | [Problem it solves here] |

---

## [ ] 10. Traceability

| SWR ID | Design Element | Test Approach |
|--------|---------------|--------------|
| [SWR-XXX] | [Module/method] | [How it will be tested] |

---

## COMPLETION CHECKLIST

- [ ] Document Control filled in with correct component name and requirement references
- [ ] Component Overview describes responsibility and architecture context
- [ ] Public Interface lists all methods/endpoints with inputs and outputs
- [ ] Internal Structure shows directory layout and module descriptions
- [ ] Data Model includes DDL, indexes, and constraints
- [ ] Business Logic documents all algorithms and edge cases
- [ ] Error Handling covers all error scenarios with codes and recovery
- [ ] Logging and Observability defines log points and levels
- [ ] Security addresses authentication, authorization, validation, and data protection
- [ ] Design Patterns documented with rationale
- [ ] Traceability maps every SWR to a design element and test approach
- [ ] Peer reviewed by Tech Lead

---

## CROSS-REFERENCES

| Document | Relationship | Link |
|----------|-------------|------|
| Architecture Description Document | Parent architecture this component implements | ../architecture-description-document.md |
| API Specification | API contracts for this component | ./api-specification.md |
| Data Model Document | Full data model details | ./data-model-document.md |
| Design Review Checklist | Review gate for this document | ./design-review-checklist.md |
| Create Detailed Design Runbook | Step-by-step procedure | ../runbooks/create-detailed-design.md |
| Software Requirements Specification | Source requirements (SWR-XXX) | ../../phase-2-requirements-engineering/templates/software-requirements-specification.md |
