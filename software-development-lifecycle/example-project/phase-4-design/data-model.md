> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Data Model Document

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P4-003 |
| **When to Use** | Defining database schema and data structures for each component |
| **Owner** | Developer |
| **Reviewer** | Tech Lead |
| **SLA** | 2 business days per component |
| **Runbook** | ../runbooks/design-data-models.md |
| **Last Verified** | 2025-10-10 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Seed Data and Denormalization Notes optional; ERD can be text description
> **IF** medium project (3-5 devs) **THEN** All sections required; Seed Data can list tables only without counts
> **IF** large project (6+ devs) **THEN** Full template required

**Selected:** Small project (1-2 devs)

---

## [x] Document Control

| Field | Value |
|-------|-------|
| Component | Power Atlas -- Full System Data Model |
| Author | Rami Haddad |
| Date | 2025-10-10 |
| Database | SQLite 3.x |

---

## [x] Entity Relationship Diagram

```
+-------------------+       +---------------------+       +-------------------+
| users             |       | projects            |       | loads             |
|-------------------|       |---------------------|       |-------------------|
| user_id      INT  |<--+   | project_id     INT  |<--+   | load_id      INT  |
| username     TEXT |   +---| user_id        INT  |   +---| project_id   INT  |
| email        TEXT |   |   | project_name   TEXT |       | load_name    TEXT |
| password_hash TEXT|   |   | prn            TEXT |       | load_type    TEXT |
| role         TEXT |   |   | client_id      INT  |---+   | quantity     INT  |
| is_active    INT  |   |   | voltage_level  TEXT |   |   | power_kw     REAL |
| created_at   TEXT |   |   | frequency      TEXT |   |   | power_kva    REAL |
| updated_at   TEXT |   |   | power_factor   REAL |   |   | current_a    REAL |
+-------------------+   |   | demand_factor  REAL |   |   | voltage_v    REAL |
                        |   | diversity_factor REAL|   |   | power_factor REAL |
+-------------------+   |   | project_data   TEXT |   |   | is_critical  INT  |
| sessions          |   |   | layout_data    TEXT |   |   | created_at   TEXT |
|-------------------|   |   | status         TEXT |   |   +-------------------+
| session_id   INT  |   |   | is_archived    INT  |   |
| user_id      INT  |---+   | folder_id      INT  |---+-+
| token        TEXT |   |   | created_at     TEXT |   | |
| created_at   TEXT |   |   | updated_at     TEXT |   | | +-------------------+
| expires_at   TEXT |   |   +---------------------+   | | | folders           |
| last_active  TEXT |   |                              | | |-------------------|
+-------------------+   |   +---------------------+   | +-| folder_id    INT  |
                        |   | generators          |   |   | user_id      INT  |
+-------------------+   |   |---------------------|   |   | folder_name  TEXT |
| notifications     |   |   | generator_id   INT  |   |   | parent_id    INT  |--+
|-------------------|   |   | project_id     INT  |---+   | created_at   TEXT |  |
| notification_id INT|  |   | name           TEXT |       +-------------------+  |
| user_id      INT  |--+   | capacity_kva   REAL |             ^                |
| message      TEXT |       | fuel_type      TEXT |             +----------------+
| is_read      INT  |       | quantity       INT  |
| created_at   TEXT |       | created_at     TEXT |
+-------------------+       +---------------------+

+------------------------+       +-----------------------+
| clients                |       | client_requirements   |
|------------------------|       |-----------------------|
| client_id         INT  |<------| requirement_id   INT  |
| client_name       TEXT |       | client_id        INT  |
| contact_email     TEXT |       | requirement_code TEXT  |
| contact_phone     TEXT |       | client_name      TEXT  |
| company           TEXT |       | client_email     TEXT  |
| created_at        TEXT |       | event_name       TEXT  |
+------------------------+       | event_date       TEXT  |
                                 | event_location   TEXT  |
+------------------------+       | estimated_power  REAL  |
| requirement_changes    |       | voltage_req      TEXT  |
|------------------------|       | description      TEXT  |
| change_id         INT  |       | status           TEXT  |
| requirement_id    INT  |------>| approved_by      INT   |
| changed_by        INT  |       | project_id       INT   |
| old_status        TEXT |       | created_at       TEXT  |
| new_status        TEXT |       | updated_at       TEXT  |
| notes             TEXT |       +-----------------------+
| created_at        TEXT |
+------------------------+

+------------------------+
| project_activity       |
|------------------------|
| activity_id       INT  |
| project_id        INT  |-------> projects.project_id
| user_id           INT  |-------> users.user_id
| action            TEXT |
| details           TEXT |
| created_at        TEXT |
+------------------------+
```

---

## [x] Table Definitions

### [x] users

| Column | Type | Nullable | Default | Constraints | Description |
|--------|------|----------|---------|-------------|-------------|
| user_id | INTEGER | No | AUTOINCREMENT | PRIMARY KEY | Unique user identifier |
| username | TEXT | No | -- | UNIQUE, length 3-50 | Login username |
| email | TEXT | No | -- | UNIQUE, valid email format | User email address |
| password_hash | TEXT | No | -- | -- | bcrypt hash (12 rounds) |
| role | TEXT | No | `'operator'` | CHECK(role IN ('admin','operator','readonly')) | User role |
| is_active | INTEGER | No | `1` | CHECK(is_active IN (0,1)) | Account active flag |
| failed_login_attempts | INTEGER | No | `0` | -- | Counter for failed logins |
| locked_until | TEXT | Yes | NULL | -- | ISO 8601 timestamp; account locked until this time |
| created_at | TEXT | No | `datetime('now')` | -- | Account creation time |
| updated_at | TEXT | No | `datetime('now')` | -- | Last modification time |

---

### [x] sessions

| Column | Type | Nullable | Default | Constraints | Description |
|--------|------|----------|---------|-------------|-------------|
| session_id | INTEGER | No | AUTOINCREMENT | PRIMARY KEY | Session identifier |
| user_id | INTEGER | No | -- | REFERENCES users(user_id) ON DELETE CASCADE | Owning user |
| token | TEXT | No | -- | UNIQUE | JWT token string |
| created_at | TEXT | No | `datetime('now')` | -- | Session start time |
| expires_at | TEXT | No | -- | -- | Absolute expiry (24 hours from creation) |
| last_active | TEXT | No | `datetime('now')` | -- | Last activity timestamp; inactivity timeout at 1 hour |

---

### [x] projects

| Column | Type | Nullable | Default | Constraints | Description |
|--------|------|----------|---------|-------------|-------------|
| project_id | INTEGER | No | AUTOINCREMENT | PRIMARY KEY | Project identifier |
| user_id | INTEGER | No | -- | REFERENCES users(user_id) | Project owner |
| project_name | TEXT | No | -- | length 1-200 | Project display name |
| prn | TEXT | Yes | NULL | UNIQUE (when not null) | Power Rental Number (PRN-YYYY-NNNN) |
| client_id | INTEGER | Yes | NULL | REFERENCES clients(client_id) ON DELETE SET NULL | Associated client |
| voltage_level | TEXT | No | `'400'` | -- | System voltage level (V) |
| frequency | TEXT | No | `'50'` | -- | System frequency (Hz) |
| power_factor | REAL | No | `0.8` | CHECK(power_factor > 0 AND power_factor <= 1.0) | Default power factor |
| demand_factor | REAL | No | `1.0` | CHECK(demand_factor > 0 AND demand_factor <= 1.0) | Demand factor |
| diversity_factor | REAL | No | `1.0` | CHECK(diversity_factor > 0 AND diversity_factor <= 1.0) | Diversity factor |
| project_data | TEXT | Yes | NULL | -- | JSON blob for miscellaneous project data |
| layout_data | TEXT | Yes | NULL | -- | JSON blob for visual layout configuration |
| status | TEXT | No | `'draft'` | CHECK(status IN ('draft','active','archived')) | Project lifecycle status |
| is_archived | INTEGER | No | `0` | CHECK(is_archived IN (0,1)) | Soft-delete archive flag |
| folder_id | INTEGER | Yes | NULL | REFERENCES folders(folder_id) ON DELETE SET NULL | Organizational folder |
| created_at | TEXT | No | `datetime('now')` | -- | Creation timestamp |
| updated_at | TEXT | No | `datetime('now')` | -- | Last modification timestamp |

---

### [x] loads

| Column | Type | Nullable | Default | Constraints | Description |
|--------|------|----------|---------|-------------|-------------|
| load_id | INTEGER | No | AUTOINCREMENT | PRIMARY KEY | Load identifier |
| project_id | INTEGER | No | -- | REFERENCES projects(project_id) ON DELETE CASCADE | Parent project |
| load_name | TEXT | No | -- | length 1-200 | Load description |
| load_type | TEXT | No | -- | CHECK(load_type IN ('lighting','motor','hvac','appliance','it_equipment','other')) | Load category |
| quantity | INTEGER | No | `1` | CHECK(quantity >= 1 AND quantity <= 9999) | Number of identical loads |
| power_kw | REAL | Yes | NULL | CHECK(power_kw >= 0) | Power in kilowatts |
| power_kva | REAL | Yes | NULL | CHECK(power_kva >= 0) | Apparent power in kVA |
| current_a | REAL | Yes | NULL | CHECK(current_a >= 0) | Current in amps |
| voltage_v | REAL | No | `400.0` | CHECK(voltage_v > 0) | Operating voltage |
| power_factor | REAL | No | `0.8` | CHECK(power_factor > 0 AND power_factor <= 1.0) | Load power factor |
| is_critical | INTEGER | No | `0` | CHECK(is_critical IN (0,1)) | Critical load flag |
| created_at | TEXT | No | `datetime('now')` | -- | Creation timestamp |

---

### [x] clients

| Column | Type | Nullable | Default | Constraints | Description |
|--------|------|----------|---------|-------------|-------------|
| client_id | INTEGER | No | AUTOINCREMENT | PRIMARY KEY | Client identifier |
| client_name | TEXT | No | -- | length 1-200 | Company or individual name |
| contact_email | TEXT | Yes | NULL | Valid email format | Primary contact email |
| contact_phone | TEXT | Yes | NULL | length 7-20 | Primary contact phone |
| company | TEXT | Yes | NULL | length 1-200 | Parent company name |
| created_at | TEXT | No | `datetime('now')` | -- | Record creation time |
| updated_at | TEXT | No | `datetime('now')` | -- | Last modification time |

---

### [x] generators

| Column | Type | Nullable | Default | Constraints | Description |
|--------|------|----------|---------|-------------|-------------|
| generator_id | INTEGER | No | AUTOINCREMENT | PRIMARY KEY | Generator identifier |
| project_id | INTEGER | No | -- | REFERENCES projects(project_id) ON DELETE CASCADE | Parent project |
| name | TEXT | No | -- | length 1-200 | Generator designation |
| capacity_kva | REAL | No | -- | CHECK(capacity_kva > 0) | Generator capacity in kVA |
| fuel_type | TEXT | No | `'diesel'` | CHECK(fuel_type IN ('diesel','gas','hybrid')) | Fuel type |
| quantity | INTEGER | No | `1` | CHECK(quantity >= 1) | Number of units |
| created_at | TEXT | No | `datetime('now')` | -- | Creation timestamp |

---

### [x] folders

| Column | Type | Nullable | Default | Constraints | Description |
|--------|------|----------|---------|-------------|-------------|
| folder_id | INTEGER | No | AUTOINCREMENT | PRIMARY KEY | Folder identifier |
| user_id | INTEGER | No | -- | REFERENCES users(user_id) ON DELETE CASCADE | Folder owner |
| folder_name | TEXT | No | -- | length 1-100 | Folder display name |
| parent_id | INTEGER | Yes | NULL | REFERENCES folders(folder_id) ON DELETE CASCADE | Parent folder for nesting (max depth: 3) |
| created_at | TEXT | No | `datetime('now')` | -- | Creation timestamp |

---

### [x] client_requirements

| Column | Type | Nullable | Default | Constraints | Description |
|--------|------|----------|---------|-------------|-------------|
| requirement_id | INTEGER | No | AUTOINCREMENT | PRIMARY KEY | Requirement identifier |
| client_id | INTEGER | Yes | NULL | REFERENCES clients(client_id) | Linked client (set after matching) |
| requirement_code | TEXT | No | -- | UNIQUE | Tracking code: `PR{DDMMYYYY}-{seq}` |
| client_name | TEXT | No | -- | length 1-200 | Submitted client name |
| client_email | TEXT | No | -- | Valid email format | Submitted client email |
| client_phone | TEXT | Yes | NULL | -- | Submitted client phone |
| event_name | TEXT | No | -- | length 1-200 | Event or site name |
| event_date | TEXT | No | -- | ISO 8601 date | Event date |
| event_location | TEXT | No | -- | length 1-300 | Event location |
| estimated_power_kw | REAL | Yes | NULL | CHECK(estimated_power_kw >= 0) | Estimated power needed |
| voltage_requirement | TEXT | No | `'400'` | -- | Required voltage level |
| description | TEXT | Yes | NULL | max 5000 chars | Additional requirement details |
| status | TEXT | No | `'submitted'` | CHECK(status IN ('submitted','approved','rejected','edit_requested')) | Requirement status |
| approved_by | INTEGER | Yes | NULL | REFERENCES users(user_id) | Admin who approved/rejected |
| project_id | INTEGER | Yes | NULL | REFERENCES projects(project_id) | Linked project after approval |
| created_at | TEXT | No | `datetime('now')` | -- | Submission timestamp |
| updated_at | TEXT | No | `datetime('now')` | -- | Last status change |

---

### [x] notifications

| Column | Type | Nullable | Default | Constraints | Description |
|--------|------|----------|---------|-------------|-------------|
| notification_id | INTEGER | No | AUTOINCREMENT | PRIMARY KEY | Notification identifier |
| user_id | INTEGER | No | -- | REFERENCES users(user_id) ON DELETE CASCADE | Recipient user |
| message | TEXT | No | -- | max 1000 chars | Notification message text |
| type | TEXT | No | `'info'` | CHECK(type IN ('info','warning','action_required')) | Notification category |
| reference_type | TEXT | Yes | NULL | -- | Related entity type (e.g., `project`, `requirement`) |
| reference_id | INTEGER | Yes | NULL | -- | Related entity ID |
| is_read | INTEGER | No | `0` | CHECK(is_read IN (0,1)) | Read flag |
| created_at | TEXT | No | `datetime('now')` | -- | Notification creation time |

---

### [x] requirement_changes

| Column | Type | Nullable | Default | Constraints | Description |
|--------|------|----------|---------|-------------|-------------|
| change_id | INTEGER | No | AUTOINCREMENT | PRIMARY KEY | Change record identifier |
| requirement_id | INTEGER | No | -- | REFERENCES client_requirements(requirement_id) ON DELETE CASCADE | Related requirement |
| changed_by | INTEGER | No | -- | REFERENCES users(user_id) | User who made the change |
| old_status | TEXT | No | -- | -- | Previous status |
| new_status | TEXT | No | -- | -- | New status |
| notes | TEXT | Yes | NULL | max 2000 chars | Change notes |
| created_at | TEXT | No | `datetime('now')` | -- | Change timestamp |

---

### [x] project_activity

| Column | Type | Nullable | Default | Constraints | Description |
|--------|------|----------|---------|-------------|-------------|
| activity_id | INTEGER | No | AUTOINCREMENT | PRIMARY KEY | Activity record identifier |
| project_id | INTEGER | No | -- | REFERENCES projects(project_id) ON DELETE CASCADE | Related project |
| user_id | INTEGER | No | -- | REFERENCES users(user_id) | User who performed the action |
| action | TEXT | No | -- | CHECK(action IN ('created','updated','activated','archived','reopened','load_added','load_removed','generator_added','generator_removed')) | Action type |
| details | TEXT | Yes | NULL | -- | JSON blob with action-specific details |
| created_at | TEXT | No | `datetime('now')` | -- | Activity timestamp |

---

## [x] Relationships

| From Table | To Table | Type | Foreign Key | On Delete |
|-----------|---------|------|-------------|-----------|
| projects | users | Many-to-One | projects.user_id -> users.user_id | RESTRICT |
| projects | clients | Many-to-One | projects.client_id -> clients.client_id | SET NULL |
| projects | folders | Many-to-One | projects.folder_id -> folders.folder_id | SET NULL |
| loads | projects | Many-to-One | loads.project_id -> projects.project_id | CASCADE |
| generators | projects | Many-to-One | generators.project_id -> projects.project_id | CASCADE |
| folders | users | Many-to-One | folders.user_id -> users.user_id | CASCADE |
| folders | folders | Many-to-One (self) | folders.parent_id -> folders.folder_id | CASCADE |
| sessions | users | Many-to-One | sessions.user_id -> users.user_id | CASCADE |
| client_requirements | clients | Many-to-One | client_requirements.client_id -> clients.client_id | SET NULL |
| client_requirements | users | Many-to-One | client_requirements.approved_by -> users.user_id | SET NULL |
| client_requirements | projects | Many-to-One | client_requirements.project_id -> projects.project_id | SET NULL |
| notifications | users | Many-to-One | notifications.user_id -> users.user_id | CASCADE |
| requirement_changes | client_requirements | Many-to-One | requirement_changes.requirement_id -> client_requirements.requirement_id | CASCADE |
| requirement_changes | users | Many-to-One | requirement_changes.changed_by -> users.user_id | RESTRICT |
| project_activity | projects | Many-to-One | project_activity.project_id -> projects.project_id | CASCADE |
| project_activity | users | Many-to-One | project_activity.user_id -> users.user_id | RESTRICT |

---

## [x] Indexes

| Name | Table | Columns | Type | Rationale |
|------|-------|---------|------|-----------|
| idx_users_email | users | email | Unique | Login lookup by email; uniqueness enforcement |
| idx_users_username | users | username | Unique | Login lookup by username; uniqueness enforcement |
| idx_projects_user_id | projects | user_id | B-tree | Primary query: list projects by owner |
| idx_projects_client_id | projects | client_id | B-tree | Filter projects by client |
| idx_projects_status | projects | status | B-tree | Filter projects by status |
| idx_projects_folder_id | projects | folder_id | B-tree | List projects within a folder |
| idx_loads_project_id | loads | project_id | B-tree | Aggregate loads per project -- most frequent query |
| idx_loads_is_critical | loads | project_id, is_critical | Composite B-tree | Critical load queries filter by project + critical flag |
| idx_generators_project_id | generators | project_id | B-tree | List generators per project |
| idx_folders_user_id | folders | user_id | B-tree | List folders by owner |
| idx_folders_parent_id | folders | parent_id | B-tree | List child folders |
| idx_sessions_user_id | sessions | user_id | B-tree | Look up active sessions for a user |
| idx_sessions_token | sessions | token | Unique | Token validation lookup |
| idx_requirements_code | client_requirements | requirement_code | Unique | Public tracking code lookup |
| idx_requirements_status | client_requirements | status | B-tree | Filter requirements by status (admin dashboard) |
| idx_notifications_user_id | notifications | user_id, is_read | Composite B-tree | Unread notification count per user |
| idx_activity_project_id | project_activity | project_id | B-tree | Activity log per project |

---

## [x] Constraints

```sql
-- Users: role validation
ALTER TABLE users
  ADD CONSTRAINT chk_users_role CHECK (role IN ('admin', 'operator', 'readonly'));

-- Projects: status validation
ALTER TABLE projects
  ADD CONSTRAINT chk_projects_status CHECK (status IN ('draft', 'active', 'archived'));

-- Projects: numeric range validations
ALTER TABLE projects
  ADD CONSTRAINT chk_projects_pf CHECK (power_factor > 0 AND power_factor <= 1.0);
ALTER TABLE projects
  ADD CONSTRAINT chk_projects_df CHECK (demand_factor > 0 AND demand_factor <= 1.0);
ALTER TABLE projects
  ADD CONSTRAINT chk_projects_divf CHECK (diversity_factor > 0 AND diversity_factor <= 1.0);

-- Loads: load_type validation
ALTER TABLE loads
  ADD CONSTRAINT chk_loads_type CHECK (load_type IN ('lighting', 'motor', 'hvac', 'appliance', 'it_equipment', 'other'));

-- Loads: quantity range
ALTER TABLE loads
  ADD CONSTRAINT chk_loads_quantity CHECK (quantity >= 1 AND quantity <= 9999);

-- Loads: non-negative power values
ALTER TABLE loads
  ADD CONSTRAINT chk_loads_power_kw CHECK (power_kw IS NULL OR power_kw >= 0);
ALTER TABLE loads
  ADD CONSTRAINT chk_loads_power_kva CHECK (power_kva IS NULL OR power_kva >= 0);
ALTER TABLE loads
  ADD CONSTRAINT chk_loads_current CHECK (current_a IS NULL OR current_a >= 0);

-- Client requirements: status validation
ALTER TABLE client_requirements
  ADD CONSTRAINT chk_requirements_status CHECK (status IN ('submitted', 'approved', 'rejected', 'edit_requested'));

-- Generators: capacity must be positive
ALTER TABLE generators
  ADD CONSTRAINT chk_generators_capacity CHECK (capacity_kva > 0);

-- Folders: unique name per parent per user
CREATE UNIQUE INDEX uq_folders_name_parent_user
  ON folders(user_id, parent_id, folder_name);
```

---

## [x] Migration Files

| Order | File | Description |
|-------|------|-------------|
| 001 | `001_create_users.sql` | Create users table with role and lockout columns |
| 002 | `002_create_sessions.sql` | Create sessions table |
| 003 | `003_create_clients.sql` | Create clients table |
| 004 | `004_create_folders.sql` | Create folders table with self-referencing parent_id |
| 005 | `005_create_projects.sql` | Create projects table with all FK references |
| 006 | `006_create_loads.sql` | Create loads table |
| 007 | `007_create_generators.sql` | Create generators table |
| 008 | `008_create_client_requirements.sql` | Create client_requirements table |
| 009 | `009_create_notifications.sql` | Create notifications table |
| 010 | `010_create_requirement_changes.sql` | Create requirement_changes audit table |
| 011 | `011_create_project_activity.sql` | Create project_activity audit table |
| 012 | `012_create_indexes.sql` | Create all non-unique indexes |
| 013 | `013_seed_admin_user.sql` | Insert default admin user |

---

## [x] Seed Data

| Table | Records | Purpose |
|-------|---------|---------|
| users | 3 | Admin (rami.haddad), operator (sara.mansour), readonly (viewer.test) |
| clients | 5 | Sample clients: Al Habtoor Events, Dubai Expo Services, RAK Construction, Sharjah Municipality, ADNOC Logistics |
| projects | 4 | Sample projects in various statuses (2 draft, 1 active, 1 archived) |
| loads | 12 | Mix of lighting, motor, HVAC, and appliance loads across sample projects |
| generators | 3 | Diesel and gas generators assigned to the active project |
| folders | 3 | Root folder "2025 Events", child folder "Q4", grandchild folder "December" |

**Example Seed -- Admin User:**
```sql
INSERT INTO users (username, email, password_hash, role, is_active)
VALUES (
  'rami.haddad',
  'rami.haddad@glowpowerrental.com',
  '$2b$12$LJ3m5E4v2QrN8kG7xR9pUOZ1wYfB3hD6tK8mN0qS2vXcA4jE6iW9y',  -- bcrypt 12 rounds
  'admin',
  1
);
```

**Example Seed -- Sample Load:**
```sql
INSERT INTO loads (project_id, load_name, load_type, quantity, power_kw, power_kva, current_a, voltage_v, power_factor, is_critical)
VALUES (
  1,
  'Main Stage Lighting',
  'lighting',
  8,
  21.09,
  22.20,
  32.0,
  400.0,
  0.95,
  1
);
```

---

## [x] Denormalization Notes

| Table | Column | Rationale |
|-------|--------|-----------|
| client_requirements | client_name, client_email, client_phone | Denormalized from clients table because requirements can be submitted before a client record exists; preserves original submission data even if client record is later modified |
| projects | project_data (JSON) | Semi-structured data for UI-specific settings that do not warrant separate columns; avoids frequent schema migrations for non-critical fields |
| projects | layout_data (JSON) | Visual layout positions for the drag-and-drop canvas; schema is UI-driven and changes frequently |

---

## COMPLETION CHECKLIST

- [x] Document Control filled in with component name and database version
- [x] Entity Relationship Diagram shows all tables and relationships
- [x] Table Definitions include all columns with types, nullability, defaults, and constraints
- [x] Relationships documented with foreign keys and delete behavior
- [x] Indexes defined with rationale for each
- [x] Check constraints and custom constraints documented
- [x] Migration files listed in execution order
- [x] Seed data requirements specified
- [x] Denormalization decisions documented with rationale
- [x] All tables include id and created_at columns
- [x] Peer reviewed by Tech Lead

---

## CROSS-REFERENCES

| Document | Relationship | Link |
|----------|-------------|------|
| Detailed Design Document | Parent component design referencing this data model | ./detailed-design.md |
| API Specification | API contracts that read/write this data | ./api-specification.md |
| Design Review Checklist | Review gate for data model design | ./design-review-checklist.md |
| Design Data Models Runbook | Step-by-step procedure | ../../../phase-4-design/runbooks/design-data-models.md |
| Software Requirements Specification | Source requirements (SWR-XXX) | ../../phase-2-requirements-engineering/software-requirements-specification.md |
