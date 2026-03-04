> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Detailed Design Document

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P4-001 |
| **When to Use** | Creating detailed design for each system component |
| **Owner** | Developer |
| **Reviewer** | Tech Lead |
| **SLA** | 3 business days per component |
| **Runbook** | ../runbooks/create-detailed-design.md |
| **Last Verified** | 2025-10-10 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Sections 7, 9 optional; Section 3 reduced to file list only
> **IF** medium project (3-5 devs) **THEN** All sections required; Section 9 can be abbreviated
> **IF** large project (6+ devs) **THEN** Full template required

**Selected:** Small project (1-2 devs)

---

## [x] Document Control

| Field | Value |
|-------|-------|
| Component Name | Calculation Engine / Project Engine |
| Version | 1.0 |
| Author | Rami Haddad |
| Date | 2025-10-10 |
| Related ADD Section | ADD Section 4.2 -- Core Domain Services |
| Related Requirements | SWR-010, SWR-011, SWR-012, SWR-020, SWR-021, SWR-022, SWR-023 |

---

# PART A -- Calculation Engine

---

## [x] 1. Component Overview

| Field | Value |
|-------|-------|
| Responsibility | Performs all electrical power calculations including single-phase and three-phase conversions, load aggregation, and critical-load analysis |
| Architecture Context | Called by the Loads API endpoints and the Project summary endpoints; reads from the `loads` table; returns computed values to the API layer |
| Technology | Python 3.11, Flask (internal module -- no direct routes) |
| Owned Data | None (stateless); reads `loads` table owned by Project Engine |

---

## [x] 2. Public Interface

| Method | Type | Description | Input | Output |
|--------|------|-------------|-------|--------|
| `calculateSinglePhase(amps, voltage, power_factor)` | Internal | Compute single-phase kW | amps: float, voltage: float (default 230), power_factor: float | dict: `{kw, kva}` |
| `calculateThreePhase(amps, voltage, power_factor)` | Internal | Compute three-phase kW | amps: float, voltage: float (default 400), power_factor: float | dict: `{kw, kva}` |
| `convertAmpsToKw(amps, voltage, power_factor, phase)` | Internal | Dispatch to single/three-phase calc | amps: float, voltage: float, power_factor: float, phase: str (`"single"` or `"three"`) | float: kW |
| `convertKwToKva(kw, power_factor)` | Internal | Convert kW to kVA | kw: float, power_factor: float | float: kVA |
| `calculateTotalLoad(project_id)` | Internal | Sum all loads for a project | project_id: int | dict: `{total_kw, total_kva, load_count}` |
| `calculateCriticalLoad(project_id)` | Internal | Sum only critical loads for a project | project_id: int | dict: `{critical_kw, critical_kva, critical_count}` |

---

## [x] 3. Internal Structure

```
src/
+-- services/
|   +-- calculation_engine.py      # PowerCalculator class
|   +-- __init__.py
+-- tests/
    +-- test_calculation_engine.py  # Unit tests for all calculation methods
```

### [x] Module Descriptions

| Module | Responsibility | Dependencies |
|--------|---------------|-------------|
| `calculation_engine.py` | Houses the `PowerCalculator` class with all calculation methods | `math` (stdlib), `models.load` (for DB queries in aggregate methods) |
| `test_calculation_engine.py` | Unit tests covering formulas, edge cases, and validation | `pytest`, `calculation_engine` |

---

## [x] 4. Data Model

The Calculation Engine is stateless. It reads from the `loads` table (owned by the Project Engine). See Part B and the Data Model Document for full DDL.

---

## [x] 5. Business Logic

### [x] Single-Phase Power Calculation

**Requirement:** SWR-010

**Algorithm:**
```
INPUT:  amps (A), voltage (V, default 230), power_factor (PF)
OUTPUT: { kw, kva }

1. VALIDATE amps > 0, 0 < PF <= 1.0, voltage > 0
2. kw = (amps * voltage * PF) / 1000
3. kva = kw / PF
4. ROUND kw and kva to 2 decimal places
5. RETURN { kw, kva }
```

**Edge Cases:**
| Case | Handling |
|------|---------|
| amps = 0 | Return `{ kw: 0.0, kva: 0.0 }` |
| power_factor = 1.0 (unity) | kW equals kVA; valid result |
| Very large amps (> 10000) | Accept but log a warning -- may indicate data entry error |

**Error Conditions:**
| Condition | Response |
|-----------|----------|
| amps < 0 | Raise `ValidationError("INVALID_AMPS", "Amps must be non-negative")` |
| power_factor <= 0 or > 1.0 | Raise `ValidationError("INVALID_PF", "Power factor must be between 0 (exclusive) and 1.0 (inclusive)")` |
| voltage <= 0 | Raise `ValidationError("INVALID_VOLTAGE", "Voltage must be positive")` |

### [x] Three-Phase Power Calculation

**Requirement:** SWR-011

**Algorithm:**
```
INPUT:  amps (A), voltage (V, default 400), power_factor (PF)
OUTPUT: { kw, kva }

1. VALIDATE amps > 0, 0 < PF <= 1.0, voltage > 0
2. kw = (amps * voltage * sqrt(3) * PF) / 1000
3. kva = kw / PF
4. ROUND kw and kva to 2 decimal places
5. RETURN { kw, kva }
```

**Edge Cases:**
| Case | Handling |
|------|---------|
| amps = 0 | Return `{ kw: 0.0, kva: 0.0 }` |
| voltage = 230 (non-standard three-phase) | Accept; system supports variable voltage |

**Error Conditions:**
Same as single-phase calculation.

### [x] Convert Amps to kW (Dispatcher)

**Requirement:** SWR-012

**Algorithm:**
```
INPUT:  amps, voltage, power_factor, phase ("single" or "three")
OUTPUT: kw (float)

1. VALIDATE phase is "single" or "three"
2. IF phase == "single" THEN call calculateSinglePhase(amps, voltage, power_factor).kw
3. IF phase == "three" THEN call calculateThreePhase(amps, voltage, power_factor).kw
4. RETURN kw
```

**Error Conditions:**
| Condition | Response |
|-----------|----------|
| phase not in ("single", "three") | Raise `ValidationError("INVALID_PHASE", "Phase must be 'single' or 'three'")` |

### [x] Convert kW to kVA

**Requirement:** SWR-012

**Algorithm:**
```
INPUT:  kw, power_factor
OUTPUT: kva (float)

1. VALIDATE kw >= 0, 0 < power_factor <= 1.0
2. kva = kw / power_factor
3. ROUND kva to 2 decimal places
4. RETURN kva
```

### [x] Calculate Total Load

**Requirement:** SWR-020

**Algorithm:**
```
INPUT:  project_id (int)
OUTPUT: { total_kw, total_kva, load_count }

1. QUERY all loads WHERE project_id = :project_id
2. IF no loads found RETURN { total_kw: 0.0, total_kva: 0.0, load_count: 0 }
3. FOR each load:
   a. effective_kw = load.power_kw * load.quantity
   b. effective_kva = load.power_kva * load.quantity
4. total_kw = SUM(effective_kw)
5. total_kva = SUM(effective_kva)
6. load_count = COUNT(loads)
7. ROUND totals to 2 decimal places
8. RETURN { total_kw, total_kva, load_count }
```

### [x] Calculate Critical Load

**Requirement:** SWR-021

**Algorithm:**
```
INPUT:  project_id (int)
OUTPUT: { critical_kw, critical_kva, critical_count }

1. QUERY all loads WHERE project_id = :project_id AND is_critical = 1
2. IF no critical loads found RETURN { critical_kw: 0.0, critical_kva: 0.0, critical_count: 0 }
3. FOR each load:
   a. effective_kw = load.power_kw * load.quantity
   b. effective_kva = load.power_kva * load.quantity
4. critical_kw = SUM(effective_kw)
5. critical_kva = SUM(effective_kva)
6. critical_count = COUNT(loads)
7. ROUND totals to 2 decimal places
8. RETURN { critical_kw, critical_kva, critical_count }
```

---

## [x] 6. Error Handling

| Error Scenario | Detection | Response Code | Error Code | Recovery |
|---------------|----------|---------------|-----------|----------|
| Negative amps value | Input validation in PowerCalculator | 400 | INVALID_AMPS | Return error to client; do not persist |
| Power factor out of range | Input validation in PowerCalculator | 400 | INVALID_PF | Return error to client; do not persist |
| Invalid phase string | Input validation in convertAmpsToKw | 400 | INVALID_PHASE | Return error to client |
| Project not found (aggregate methods) | DB query returns no project | 404 | PROJECT_NOT_FOUND | Return error to client |
| Database connection failure | SQLAlchemy exception catch | 500 | INTERNAL_ERROR | Log error; return generic 500 |

---

## [x] 7. Logging and Observability

> Scaling gate: optional for small projects. Included for reference.

| Log Point | Level | Data |
|-----------|-------|------|
| Calculation request received | DEBUG | method name, input parameters |
| Validation failure | WARN | field name, invalid value, error code |
| Large amps warning (> 10000) | WARN | project_id, load_id, amps value |
| Aggregate calculation complete | INFO | project_id, total_kw, load_count |

---

## [x] 8. Security

| Concern | Approach |
|---------|----------|
| Authentication | Calculation methods are internal; called only from authenticated API routes (JWT required) |
| Authorization | Caller must own the project or have admin role; enforced at API layer |
| Input validation | All numeric inputs validated for type and range before calculation |
| Data protection | No PII involved in calculations; no sensitive data logged |

---

## [x] 9. Design Patterns Used

> Scaling gate: optional for small projects. Included briefly.

| Pattern | Where | Why |
|---------|-------|-----|
| Strategy | `convertAmpsToKw` dispatches to single or three-phase method | Avoids branching; allows adding new phase types (e.g., DC) without modifying dispatcher |
| Value Object | Calculation results returned as dicts with fixed keys | Immutable result sets; clear contracts between layers |

---

## [x] 10. Traceability

| SWR ID | Design Element | Test Approach |
|--------|---------------|--------------|
| SWR-010 | `PowerCalculator.calculateSinglePhase()` | Unit test with known input/output pairs |
| SWR-011 | `PowerCalculator.calculateThreePhase()` | Unit test with known input/output pairs |
| SWR-012 | `PowerCalculator.convertAmpsToKw()`, `convertKwToKva()` | Unit test dispatching and conversion |
| SWR-020 | `PowerCalculator.calculateTotalLoad()` | Integration test with seeded load data |
| SWR-021 | `PowerCalculator.calculateCriticalLoad()` | Integration test with mixed critical/non-critical loads |

---

# PART B -- Project Engine

---

## [x] 1. Component Overview

| Field | Value |
|-------|-------|
| Responsibility | Manages project lifecycle including CRUD operations, status transitions, folder organization, and project sharing |
| Architecture Context | Exposes `/api/projects` and `/api/folders` REST endpoints; owns the `projects`, `folders`, and `project_activity` tables; delegates power calculations to the Calculation Engine |
| Technology | Python 3.11, Flask, SQLAlchemy ORM |
| Owned Data | `projects`, `folders`, `project_activity` tables |

---

## [x] 2. Public Interface

| Method / Endpoint | Type | Description | Input | Output |
|------------------|------|-------------|-------|--------|
| `GET /api/projects` | REST | List projects for current user | Query: status, client_id, page, per_page | JSON array of project summaries |
| `POST /api/projects` | REST | Create a new project | Body: project_name, prn, client_id, voltage_level, frequency, power_factor, demand_factor, diversity_factor | JSON: created project |
| `GET /api/projects/:id` | REST | Get project detail | Path: project_id | JSON: full project with computed totals |
| `PUT /api/projects/:id` | REST | Update a project | Path: project_id; Body: updatable fields | JSON: updated project |
| `DELETE /api/projects/:id` | REST | Archive a project (soft delete) | Path: project_id | JSON: `{ message }` |
| `GET /api/folders` | REST | List folders for current user | Query: parent_id | JSON array of folders |
| `POST /api/folders` | REST | Create a folder | Body: folder_name, parent_id (nullable) | JSON: created folder |
| `PUT /api/folders/:id` | REST | Update folder | Path: folder_id; Body: folder_name | JSON: updated folder |
| `DELETE /api/folders/:id` | REST | Delete folder (must be empty) | Path: folder_id | JSON: `{ message }` |

---

## [x] 3. Internal Structure

```
src/
+-- routes/
|   +-- projects.py        # Flask blueprint for /api/projects
|   +-- folders.py         # Flask blueprint for /api/folders
+-- services/
|   +-- project_service.py # Business logic for project operations
|   +-- folder_service.py  # Business logic for folder operations
+-- models/
|   +-- project.py         # SQLAlchemy model for projects table
|   +-- folder.py          # SQLAlchemy model for folders table
|   +-- project_activity.py # SQLAlchemy model for project_activity table
+-- tests/
    +-- test_projects.py
    +-- test_folders.py
```

### [x] Module Descriptions

| Module | Responsibility | Dependencies |
|--------|---------------|-------------|
| `projects.py` (routes) | HTTP handling, request parsing, response formatting | `project_service`, Flask |
| `project_service.py` | Project CRUD, status transitions, authorization checks | `models.project`, `calculation_engine` |
| `folder_service.py` | Folder CRUD, hierarchy validation, empty-check on delete | `models.folder`, `models.project` |

---

## [x] 4. Data Model

See full DDL in the Data Model Document. Key tables:

```sql
CREATE TABLE projects (
  project_id INTEGER PRIMARY KEY AUTOINCREMENT,
  user_id INTEGER NOT NULL REFERENCES users(user_id),
  project_name TEXT NOT NULL,
  prn TEXT,
  client_id INTEGER REFERENCES clients(client_id),
  voltage_level TEXT DEFAULT '400',
  frequency TEXT DEFAULT '50',
  power_factor REAL DEFAULT 0.8,
  demand_factor REAL DEFAULT 1.0,
  diversity_factor REAL DEFAULT 1.0,
  project_data TEXT,          -- JSON blob for layout and misc data
  layout_data TEXT,           -- JSON blob for visual layout
  status TEXT NOT NULL DEFAULT 'draft' CHECK(status IN ('draft','active','archived')),
  is_archived INTEGER NOT NULL DEFAULT 0,
  folder_id INTEGER REFERENCES folders(folder_id),
  created_at TEXT NOT NULL DEFAULT (datetime('now')),
  updated_at TEXT NOT NULL DEFAULT (datetime('now'))
);
```

### [x] Indexes

| Index | Columns | Rationale |
|-------|---------|-----------|
| `idx_projects_user_id` | user_id | Filter projects by owner -- primary query pattern |
| `idx_projects_client_id` | client_id | Filter projects by client |
| `idx_projects_status` | status | Filter by project status |

---

## [x] 5. Business Logic

### [x] Project Status State Machine

**Requirement:** SWR-022

**State Diagram:**
```
                 activate()            archive()
  +-------+  -------------->  +--------+  ------------->  +----------+
  | draft |                   | active |                  | archived |
  +-------+  <--------------  +--------+                  +----------+
                reopen()
```

**Allowed Transitions:**
| From | To | Method | Conditions |
|------|----|--------|------------|
| draft | active | `activate()` | Project must have at least one load |
| active | archived | `archive()` | None; always allowed |
| active | draft | `reopen()` | Only project owner or admin |
| draft | archived | `archive()` | None; always allowed |
| archived | (none) | -- | Terminal state; no transitions out |

**Error Conditions:**
| Condition | Response |
|-----------|----------|
| Invalid transition (e.g., archived -> active) | Raise `InvalidStateTransition("Cannot transition from 'archived' to 'active'")` -- HTTP 409 |
| Activate without loads | Raise `ValidationError("Project must have at least one load before activation")` -- HTTP 422 |

### [x] Folder Hierarchy Logic

**Requirement:** SWR-023

**Rules:**
```
1. Folders belong to a single user (user_id on folders table)
2. Folders can be nested: parent_id references another folder_id
3. Maximum nesting depth: 3 levels (root -> child -> grandchild)
4. Folder names must be unique within the same parent for the same user
5. Deleting a folder requires it to be empty (no projects, no child folders)
6. Moving a project to a folder: update projects.folder_id
```

**Algorithm -- Create Folder:**
```
INPUT:  user_id, folder_name, parent_id (nullable)
OUTPUT: created folder

1. IF parent_id is not null:
   a. QUERY parent folder
   b. VERIFY parent folder exists AND belongs to user_id
   c. CALCULATE depth of parent
   d. IF parent depth >= 2 THEN REJECT (max depth 3)
2. VERIFY no sibling folder with same name for this user and parent_id
3. INSERT folder record
4. RETURN created folder
```

**Algorithm -- Delete Folder:**
```
INPUT:  user_id, folder_id
OUTPUT: success message

1. QUERY folder WHERE folder_id = :folder_id AND user_id = :user_id
2. IF not found RETURN 404
3. CHECK no child folders reference this folder_id as parent_id
4. CHECK no projects reference this folder_id
5. IF children or projects exist RETURN 409 ("Folder is not empty")
6. DELETE folder
7. RETURN success
```

### [x] Project Sharing Model

**Requirement:** SWR-024

**Rules:**
```
1. Projects are owned by a single user (projects.user_id)
2. Admins (role = 'admin') can view and edit all projects
3. Standard users can only view and edit their own projects
4. No explicit sharing table in v1 -- sharing is role-based only
5. Future: a project_shares table can add user-to-user sharing
```

---

## [x] 6. Error Handling

| Error Scenario | Detection | Response Code | Error Code | Recovery |
|---------------|----------|---------------|-----------|----------|
| Project not found | DB query returns None | 404 | PROJECT_NOT_FOUND | Return error |
| Folder not found | DB query returns None | 404 | FOLDER_NOT_FOUND | Return error |
| Invalid status transition | State machine check | 409 | INVALID_STATE_TRANSITION | Return error with allowed transitions |
| Duplicate project name for user | Unique constraint violation | 409 | DUPLICATE_PROJECT_NAME | Return error |
| Folder not empty on delete | Child count check | 409 | FOLDER_NOT_EMPTY | Return error with child count |
| Folder max depth exceeded | Depth calculation | 422 | MAX_DEPTH_EXCEEDED | Return error |
| Unauthorized access | user_id mismatch and not admin | 403 | FORBIDDEN | Return error |

---

## [x] 8. Security

| Concern | Approach |
|---------|----------|
| Authentication | All project/folder endpoints require valid JWT Bearer token |
| Authorization | Owner check: `project.user_id == current_user.user_id` or `current_user.role == 'admin'` |
| Input validation | `project_name` max 200 chars; `prn` validated against pattern; numeric fields range-checked |
| Data protection | `project_data` JSON may contain client details -- never logged; response filtering removes internal fields |

---

## [x] 10. Traceability

| SWR ID | Design Element | Test Approach |
|--------|---------------|--------------|
| SWR-020 | `GET /api/projects` with total load computation | Integration test: create project with loads, verify totals |
| SWR-022 | Project status state machine in `project_service.py` | Unit test: all valid transitions; all invalid transitions return 409 |
| SWR-023 | Folder hierarchy in `folder_service.py` | Unit test: nesting depth, unique names, delete non-empty |
| SWR-024 | Authorization checks in `project_service.py` | Integration test: admin vs. standard user access |

---

## COMPLETION CHECKLIST

- [x] Document Control filled in with correct component name and requirement references
- [x] Component Overview describes responsibility and architecture context
- [x] Public Interface lists all methods/endpoints with inputs and outputs
- [x] Internal Structure shows directory layout and module descriptions
- [x] Data Model includes DDL, indexes, and constraints
- [x] Business Logic documents all algorithms and edge cases
- [x] Error Handling covers all error scenarios with codes and recovery
- [x] Logging and Observability defines log points and levels
- [x] Security addresses authentication, authorization, validation, and data protection
- [x] Design Patterns documented with rationale
- [x] Traceability maps every SWR to a design element and test approach
- [x] Peer reviewed by Tech Lead

---

## CROSS-REFERENCES

| Document | Relationship | Link |
|----------|-------------|------|
| Architecture Description Document | Parent architecture this component implements | ../../phase-3-system-architecture/architecture-description-document.md |
| API Specification | API contracts for this component | ./api-specification.md |
| Data Model Document | Full data model details | ./data-model.md |
| Design Review Checklist | Review gate for this document | ./design-review-checklist.md |
| Software Requirements Specification | Source requirements (SWR-XXX) | ../phase-2-requirements-engineering/software-requirements-specification.md |
