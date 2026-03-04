> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Component Diagram -- Power Atlas

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P3-003 |
| **When to Use** | Documenting the internal structure, responsibilities, and interactions of system components |
| **Owner** | Tech Lead |
| **Reviewer** | System Architect |
| **SLA** | 3 business days |
| **Runbook** | [Create Architecture Description](../../phase-3-system-architecture/runbooks/create-architecture-description.md) |
| **Last Verified** | 2026-03-05 |

---

## SCALING GATE

> **Applied:** Small project (1-2 devs) -- Component Description Table required with all components listed. Example section not applicable (this is the example).

---

## [x] Component Diagram

```
+======================================================================+
|                        Nginx (Reverse Proxy)                          |
|  - TLS termination (Let's Encrypt)                                    |
|  - Rate limiting (60 req/min per IP)                                  |
|  - Static file serving (/public/*, /layout-builder/*)                 |
|  - Proxy: /api/* --> Flask :8000                                      |
+====+============+============+=============+============+=============+
     |            |            |             |            |
     | /api/auth  | /api/      | /api/       | /api/      | /api/
     |            | projects   | requirements| reports    | (static)
     v            | loads      |             |            v
+---------+       | clients    |             |      +-----------+
| Auth    |       | generators |             |      | Frontend  |
| Module  |       | folders    |             |      | (Vite +   |
|         |       v            v             v      | Tailwind  |
| login   | +-----------+ +-----------+ +---------+ | + JS)     |
| register| | Project   | | Require-  | | Report  | |           |
| logout  | | Engine    | | ments     | | Gener-  | | 9 HTML    |
| sessions| |           | | Pipeline  | | ator    | | pages     |
| roles   | | projects  | |           | |         | +-----------+
|         | | loads     | | submit    | | PDF via |       |
| Owns:   | | clients   | | review    | | Report- |       v
| users   | | generators| | approve   | | Lab     | +-----------+
| sessions| | folders   | | reject    | |         | | Layout    |
+---------+ | activity  | | notify    | | Owns:   | | Builder   |
     |      |           | |           | | (none,  | |           |
     |      | Owns:     | | Owns:     | | state-  | | React 18  |
     |      | projects  | | client_   | | less)   | | TypeScript|
     |      | loads     | | require-  | |         | | Konva.js  |
     |      | clients   | | ments     | | Runs on | | Zustand   |
     |      | generators| | require-  | | port    | |           |
     |      | folders   | | ment_     | | 5020    | | Owns:     |
     |      | project_  | | changes   | +---------+ | (none,    |
     |      | generators| | notifica- |      |      | client-   |
     |      | project_  | | tions     |      |      | side      |
     |      | activity  | +-----------+      |      | state)    |
     |      +-----------+      |             |      +-----------+
     |           |              |             |           |
     |           |  +-----------+             |           |
     |           |  |                         |           |
     |           v  v                         v           |
     |      +----+--+---+              +------+------+    |
     |      | Calc.     |              | PDF Server  |    |
     |      | Engine    |              | (ReportLab) |    |
     |      |           |              |             |    |
     |      | power math|              | Port 5020   |    |
     |      | diversity |              | Templates   |    |
     |      | factors   |              | Cover pages |    |
     |      | unit conv.|              | Load sched. |    |
     |      | generator |              | Single-line |    |
     |      | sizing    |              | diagrams    |    |
     |      |           |              |             |    |
     |      | Owns:     |              | Owns:       |    |
     |      | (none,    |              | (none,      |    |
     |      | stateless)|              | stateless)  |    |
     |      +-----------+              +------+------+    |
     |                                        |           |
     v                                        v           |
+====+========================================+========+  |
|                  Database Layer                       |  |
|  SQLite (WAL mode) -- /database/power_atlas.db       |  |
|                                                       |  |
|  Tables:                                              |  |
|  +----------+ +----------+ +----------+ +----------+  |  |
|  | users    | | projects | | loads    | | clients  |  |  |
|  +----------+ +----------+ +----------+ +----------+  |  |
|  +----------+ +----------+ +----------+ +----------+  |  |
|  | genera-  | | folders  | | project_ | | sessions |  |  |
|  | tors     | |          | | genera-  | |          |  |  |
|  +----------+ +----------+ | tors     | +----------+  |  |
|  +----------+ +----------+ +----------+ +----------+  |  |
|  | client_  | | notifica-| | require- | | project_ |  |  |
|  | require- | | tions    | | ment_    | | activity |  |  |
|  | ments    | |          | | changes  | |          |  |  |
|  +----------+ +----------+ +----------+ +----------+  |  |
+======================================================+  |
                                                           |
           REST calls from Layout Builder -----------------+
           (GET/POST /api/projects/*, /api/generators/*)
```

---

## [x] Inter-Component Relationships

```
+----------------+         +----------------+         +------------------+
|                | auth    |                | reads   |                  |
| Auth Module    +-------->+ Project Engine +-------->+ Calculation      |
| (validates JWT |  check  | (passes load   | (power  | Engine           |
|  on every      |         |  data to calc) | math)   | (returns totals, |
|  API request)  |         |                |         |  sizing recs)    |
+-------+--------+         +-------+--------+         +------------------+
        |                          |
        | auth check               | project data
        v                          v
+-------+--------+         +-------+--------+
|                |         |                |
| Requirements   |         | Report         |
| Pipeline       |         | Generator      |
| (validates     |         | (fetches       |
|  client/engr   |         |  project data, |
|  roles)        |         |  sends to PDF  |
|                |         |  Server :5020) |
+-------+--------+         +-------+--------+
        |                          |
        | read/write               | read (project data)
        v                          | write (none)
+-------+--------+                 |
|                |<----------------+
| Database Layer |
| (SQLite)       |<----------------+
|                |                 |
+----------------+    Layout Builder fetches
                      project/generator data
                      via REST API (through
                      Project Engine)
```

### Relationship Summary

| From | To | Type | Description |
|------|----|------|-------------|
| Nginx | Auth Module | HTTP proxy | Routes `/api/auth/*` requests |
| Nginx | Project Engine | HTTP proxy | Routes `/api/projects/*`, `/api/loads/*`, `/api/clients/*`, `/api/generators/*`, `/api/folders/*` requests |
| Nginx | Requirements Pipeline | HTTP proxy | Routes `/api/requirements/*`, `/api/notifications/*` requests |
| Nginx | Report Generator | HTTP proxy | Routes `/api/reports/*` requests |
| Nginx | Frontend | Static serving | Serves HTML, JS, CSS files directly |
| Nginx | Layout Builder | Static serving | Serves React SPA bundle at `/layout-builder/` |
| Auth Module | Database Layer | SQL queries | Reads/writes `users`, `sessions` tables |
| Project Engine | Auth Module | Middleware call | JWT validation on every request |
| Project Engine | Database Layer | SQL queries | Reads/writes `projects`, `loads`, `clients`, `generators`, `folders`, `project_generators`, `project_activity` tables |
| Project Engine | Calculation Engine | Function call | Passes load arrays for power math, receives totals and sizing recommendations |
| Requirements Pipeline | Auth Module | Middleware call | JWT validation and role checks (client vs. engineer) |
| Requirements Pipeline | Database Layer | SQL queries | Reads/writes `client_requirements`, `requirement_changes`, `notifications` tables |
| Requirements Pipeline | Email SMTP (external) | SMTP | Sends notification emails on requirement status changes |
| Report Generator | Auth Module | Middleware call | JWT validation on report requests |
| Report Generator | Database Layer | SQL queries | Reads project, load, generator, client data for report content |
| Report Generator | PDF Server | HTTP (localhost:5020) | Sends project data payload, receives generated PDF bytes |
| Layout Builder | Project Engine | REST API (via Nginx) | Fetches project details, generator data; saves layout data |
| Calculation Engine | (none) | -- | Stateless pure function module; no outbound dependencies |
| PDF Server | (none) | -- | Stateless; receives data, returns PDF; no outbound dependencies |

---

## [x] Component Description Table

| Component | Responsibility | Owned Data (Tables) | Exposed Interface | Dependencies |
|-----------|---------------|---------------------|------------------|-------------|
| **Nginx** | TLS termination, reverse proxy routing, static file serving, rate limiting, gzip compression | None | Ports 80/443 (external), forwards to internal services | None (entry point) |
| **Auth Module** | User registration, login, logout, JWT issuance and validation, session management, role-based access control (admin/engineer/client) | `users`, `sessions` | `POST /api/auth/login`, `POST /api/auth/register`, `POST /api/auth/logout`, `GET /api/auth/me`, `PUT /api/auth/profile` | Database Layer |
| **Project Engine** | Full lifecycle management of power distribution projects: create, read, update, delete projects and their associated loads, clients, generators, and folder organization; project activity logging | `projects`, `loads`, `clients`, `generators`, `folders`, `project_generators`, `project_activity` | `GET/POST/PUT/DELETE /api/projects/*`, `GET/POST/PUT/DELETE /api/loads/*`, `GET/POST/PUT/DELETE /api/clients/*`, `GET/POST/PUT/DELETE /api/generators/*`, `GET/POST/PUT/DELETE /api/folders/*` | Auth Module, Calculation Engine, Database Layer |
| **Calculation Engine** | Perform power calculations: total connected load, demand load with diversity factors, unit conversions (kW/kVA/amps), generator sizing recommendations based on load profiles | None (stateless, pure functions) | Internal Python module; called by Project Engine via function import | None |
| **Requirements Pipeline** | Manage client-submitted power requirement forms: submission, engineer review queue, approval/rejection workflow, status tracking, email and in-app notifications on status changes | `client_requirements`, `requirement_changes`, `notifications` | `POST /api/requirements`, `GET /api/requirements`, `PUT /api/requirements/:id`, `PUT /api/requirements/:id/approve`, `PUT /api/requirements/:id/reject`, `GET /api/notifications` | Auth Module, Database Layer, Email SMTP (external) |
| **Layout Builder** | Interactive canvas-based site layout designer: drag-and-drop equipment placement, equipment library sidebar, grid snapping, pan/zoom, layer management, export to PNG/SVG | None (client-side Zustand state; persists via Project Engine REST API) | Standalone SPA served at `/layout-builder/`; communicates with backend via Project Engine REST endpoints | Project Engine (via REST API) |
| **Report Generator** | Orchestrate PDF report generation: fetch project data from database, format into report structure, send to PDF Server for rendering, return PDF to user | None (stateless orchestrator) | `POST /api/reports/generate` (returns PDF binary) | Auth Module, Database Layer, PDF Server |
| **PDF Server** | Render PDF documents from structured data using ReportLab templates: cover pages, load schedule tables, single-line diagrams, equipment lists, summary pages | None (stateless) | `POST /generate-pdf` on port 5020 (internal only, not exposed via Nginx) | None |
| **Database Layer** | Provide SQLite connection management, query execution, schema migrations, WAL mode configuration, backup utilities | All 12 tables: `users`, `projects`, `loads`, `clients`, `generators`, `folders`, `project_generators`, `client_requirements`, `sessions`, `notifications`, `requirement_changes`, `project_activity` | Internal Python module; no direct API exposure | None |
| **Frontend (Main App)** | Serve the user interface for all non-layout-builder pages: login, registration, dashboard, project views, requirement forms, admin panels, client portal, profile, settings | None (client-side; fetches data via REST API) | 9 HTML pages served as static files by Nginx | Auth Module, Project Engine, Requirements Pipeline (all via REST API) |

---

## [x] Database Schema Overview

| Table | Owner Component | Key Columns | Purpose |
|-------|----------------|-------------|---------|
| `users` | Auth Module | id, email, password_hash, role, name, language | User accounts and credentials |
| `sessions` | Auth Module | id, user_id, token, expires_at, created_at | Active session tracking |
| `projects` | Project Engine | id, name, user_id, client_id, status, location, created_at | Power distribution projects |
| `loads` | Project Engine | id, project_id, name, wattage, quantity, diversity_factor, type | Electrical loads within projects |
| `clients` | Project Engine | id, name, email, phone, company, created_at | Client records linked to projects |
| `generators` | Project Engine | id, name, rated_kva, rated_kw, fuel_type, model | Generator fleet catalog |
| `folders` | Project Engine | id, name, user_id, parent_id, created_at | Project folder organization |
| `project_generators` | Project Engine | id, project_id, generator_id, quantity | Generator assignment to projects |
| `project_activity` | Project Engine | id, project_id, user_id, action, details, created_at | Project audit trail |
| `client_requirements` | Requirements Pipeline | id, client_id, project_name, description, status, submitted_at | Client power requirement submissions |
| `requirement_changes` | Requirements Pipeline | id, requirement_id, user_id, old_status, new_status, notes, changed_at | Requirement status change history |
| `notifications` | Requirements Pipeline | id, user_id, type, message, read, created_at | In-app notifications |

---

## [x] Validation Checklist

- [x] Every component has a single, clear responsibility.
- [x] Every component lists its owned data (tables or "none" for stateless).
- [x] No two components own the same data (clear table ownership).
- [x] All interactions are labeled with type (HTTP proxy, SQL, function call, REST, SMTP).
- [x] Every functional requirement traces to at least one component.
- [x] No circular dependencies exist (Auth <-- Project Engine --> Calc Engine; all write to DB Layer).
- [x] API Gateway/entry point (Nginx) is shown.

---

## COMPLETION CHECKLIST

- [x] Diagram drawn with all 10 components identified
- [x] Each component box shows responsibility and owned data
- [x] All interactions labeled with type and description
- [x] Component Description Table filled in for every component
- [x] API Gateway (Nginx) included as entry point
- [x] Database schema overview with table ownership
- [x] Inter-component relationship table completed
- [x] Validation Checklist items all pass
- [x] Diagram reviewed by System Architect

---

## CROSS-REFERENCES

| Artifact | Location | Relationship |
|----------|----------|--------------|
| Architecture Description Document | [architecture-description.md](architecture-description.md) | Component diagram feeds into ADD Section 5 |
| System Context Diagram | [system-context-diagram.md](system-context-diagram.md) | Context diagram defines external boundaries; component diagram shows internals |
| Architecture Decision Records | [architecture-decision-records.md](architecture-decision-records.md) | ADR-001 through ADR-005 drive component boundaries and technology choices |
| Software Requirements Specification | Phase 2 SRS | Functional requirements trace to components |
| Runbook | [Create Architecture Description](../../phase-3-system-architecture/runbooks/create-architecture-description.md) | Step-by-step procedure |
