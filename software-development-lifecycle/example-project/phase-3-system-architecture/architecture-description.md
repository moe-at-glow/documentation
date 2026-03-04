> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Architecture Description Document -- Power Atlas

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P3-002 |
| **When to Use** | Documenting the full system architecture for a project (one per project) |
| **Owner** | Tech Lead |
| **Reviewer** | System Architect, Product Owner, QA Lead |
| **SLA** | 5 business days for initial draft |
| **Runbook** | [Create Architecture Description](../../phase-3-system-architecture/runbooks/create-architecture-description.md) |
| **Last Verified** | 2026-03-05 |

---

## SCALING GATE

> **Applied:** Small project (1-2 devs) -- Sections 6 (Process View), 8 (Development View), and 14 (Appendices) are included but abbreviated. Quality attributes in Section 9 focus on Performance, Security, and Usability.

---

## [x] Document Control

| Field | Value |
|-------|-------|
| Document Title | Power Atlas -- Architecture Description Document |
| Version | 1.0 |
| Status | Approved |
| Author | Hamzah Hazime |
| Date Created | 2025-12-15 |
| Last Updated | 2026-01-20 |
| Related SRS | Power Atlas SRS v1.0 |

### [x] Revision History

| Version | Date | Author | Description |
|---------|------|--------|-------------|
| 0.1 | 2025-12-15 | Hamzah Hazime | Initial draft with core architecture |
| 0.2 | 2025-12-28 | Hamzah Hazime | Added deployment view and ADR references |
| 1.0 | 2026-01-20 | Hamzah Hazime | Approved after architecture review |

### [x] Approvers

| Name | Role | Signature | Date |
|------|------|-----------|------|
| Hamzah Hazime | Tech Lead | Approved | 2026-01-20 |
| Abdulaziz Al-Otaibi | Product Owner | Approved | 2026-01-22 |
| Sara Al-Rashid | QA Lead | Approved | 2026-01-22 |

---

## [x] 1. Executive Summary

Power Atlas is an internal web application built for GlowPowerRental to manage temporary power distribution projects. The system enables power engineers to create projects, define electrical loads, assign generators, calculate power requirements, and generate professional PDF reports. A separate client-facing requirements pipeline allows customers to submit power needs that engineers review and incorporate into projects.

The architecture follows a **modular monolithic** approach deployed on a single DigitalOcean droplet. The backend is a Python Flask application serving a REST API, with SQLite as the database. The frontend is a multi-page application built with Vite, Tailwind CSS, and vanilla JavaScript. A specialized Layout Builder sub-application uses React 18, TypeScript, and Konva.js for interactive canvas-based site layout design. PDF generation is handled by a dedicated Python ReportLab service. Nginx acts as the reverse proxy handling TLS termination and routing.

This architecture prioritizes simplicity, fast development velocity, and low operational overhead, consistent with a small team (1-2 developers) and a single-server deployment model.

---

## [x] 2. Architecture Goals and Constraints

### [x] Goals

| ID | Goal | Priority |
|----|------|----------|
| AG-001 | Deliver sub-200ms response times for power calculation operations | High |
| AG-002 | Support bilingual (English/Arabic) interface with RTL layout | High |
| AG-003 | Enable offline-friendly PDF generation without external service dependencies | High |
| AG-004 | Maintain simple deployment and operations for a 1-2 person team | High |
| AG-005 | Provide a responsive, drag-and-drop layout builder for site plans | Medium |
| AG-006 | Support future IoT telemetry integration without major refactoring | Low |

### [x] Constraints

| ID | Constraint | Type | Impact |
|----|-----------|------|--------|
| AC-001 | Single DigitalOcean droplet (4 vCPU, 8 GB RAM) | Infrastructure | Eliminates distributed architectures; must run all services on one server |
| AC-002 | Team of 1-2 developers | Team | Favors simple stack, monolithic deployment, minimal ops overhead |
| AC-003 | Must support Arabic RTL and bilingual content | Regulatory/UX | Requires i18n-aware frontend; Tailwind RTL utilities needed |
| AC-004 | Single DigitalOcean droplet (company standard for internal tools) | Infrastructure | Single droplet only; no managed database or CDN services |
| AC-005 | Saudi Arabian data residency preferred | Regulatory | DigitalOcean region selection; no cross-border data transfer for client data |
| AC-006 | Python team expertise | Technical | Backend must be Python-based; rules out Node.js, Go, Java backends |

---

## [x] 3. Architecture-Significant Requirements

| Requirement ID | Description | Category | Architecture Impact |
|---------------|-------------|----------|-------------------|
| SWR-F-001 | Engineers create and manage power distribution projects | Functional | Drives Project Engine component with full CRUD API |
| SWR-F-010 | System calculates total power, diversity factors, and generator sizing | Functional | Requires Calculation Engine with unit conversion and power math |
| SWR-F-015 | Interactive drag-and-drop layout builder for site plans | Functional | Requires separate React/Konva.js sub-application |
| SWR-F-020 | Generate PDF reports with project details, load schedules, layouts | Functional | Drives dedicated PDF Server with ReportLab |
| SWR-F-025 | Clients submit power requirements via portal | Functional | Requires Requirements Pipeline with separate client-facing views |
| SWR-NFR-P001 | Power calculations complete within 200ms | Performance | In-process calculation; SQLite for low-latency reads |
| SWR-NFR-P002 | Page load time under 2 seconds on 4G connection | Performance | Vanilla JS (small bundle), Vite build optimization |
| SWR-NFR-S001 | Passwords hashed with bcrypt, sessions managed via JWT | Security | Auth Module with bcrypt + JWT + CSRF tokens |
| SWR-NFR-S002 | Role-based access: Admin, Engineer, Client | Security | Auth middleware with role checks on every API route |
| SWR-NFR-A001 | 99.5% uptime during business hours (Sun-Thu 8am-6pm AST) | Availability | Single droplet with systemd auto-restart; Nginx health checks |
| SWR-NFR-U001 | Bilingual English/Arabic interface | Usability | i18n layer in frontend; RTL Tailwind utilities |

---

## [x] 4. System Context View

### [x] System Context Diagram

```
                                +------------------+
                                |  Email SMTP      |
                                |  Service         |
                                +--------+---------+
                                         ^
                                    SMTP (port 587)
                                    (notifications,
                                     password resets)
                                         |
+----------------+              +--------+---------+              +----------------+
| Power          | HTTPS        |                  | SMTP         | Future:        |
| Engineers      +------------->+                  +- - - - - - ->+ Moyasar        |
| (Web Browser)  | (projects,   |   POWER ATLAS    |              | Payment GW     |
+----------------+  loads,      |                  |              +----------------+
                 |  calcs,      |   GlowPower      |
                 |  layouts)    |   Rental          |
+----------------+              |                  |              +----------------+
| Admin Users    | HTTPS        |                  | - - - - - -> | Future:        |
| (Web Browser)  +------------->+                  |   HTTPS      | ZATCA          |
|                | (user mgmt,  |                  |              | E-Invoicing    |
+----------------+  settings,   +--------+---------+              +----------------+
                 |  reports)             |
                                    HTTPS |
+----------------+                       |
| Client Users   | HTTPS        +--------+---------+
| (Web Browser)  +------------->+  (requirement    |
|                | (requirement |   submissions,   |
+----------------+  forms,      |   status views)  |
                 |  status)     +------------------+
                                         |
                                    MQTT (future)
                                         |
                                +--------v---------+
                                | Future:          |
                                | IoT Sensors      |
                                | (generator       |
                                |  telemetry)      |
                                +------------------+
```

### [x] External Entities

| Entity | Type | Protocol | Data Exchanged | Direction |
|--------|------|----------|---------------|-----------|
| Power Engineers | Human | HTTPS | Projects, loads, generators, layouts, calculations, PDF reports | Both |
| Admin Users | Human | HTTPS | User accounts, system settings, audit logs, reports | Both |
| Client Users | Human | HTTPS | Requirement submissions, requirement status, notifications | Both |
| Email SMTP Service | System | SMTP (587) | Password reset emails, requirement status notifications, project alerts | Outbound |
| Moyasar Payment Gateway (future) | System | HTTPS REST | Payment transactions, invoices, refunds | Both |
| ZATCA E-Invoicing (future) | System | HTTPS REST | Tax invoices, compliance reports | Outbound |
| IoT Sensors (future) | System | MQTT | Generator telemetry: fuel level, runtime hours, load percentage, GPS | Inbound |

---

## [x] 5. Logical/Functional View

### [x] Component Diagram

See [component-diagram.md](component-diagram.md) for the full diagram.

### [x] Component Descriptions

| Component | Responsibility | Owned Data | Exposed Interface | Dependencies |
|-----------|---------------|------------|------------------|-------------|
| Auth Module | Handle user registration, login, logout, session management, role-based access control | `users`, `sessions` | `POST /api/auth/login`, `POST /api/auth/register`, `POST /api/auth/logout`, `GET /api/auth/me` | Database Layer |
| Project Engine | Manage project lifecycle, loads, clients, generators, and folder organization | `projects`, `loads`, `clients`, `generators`, `folders`, `project_generators`, `project_activity` | `GET/POST/PUT/DELETE /api/projects/*`, `GET/POST/PUT/DELETE /api/loads/*`, `GET/POST/PUT/DELETE /api/clients/*`, `GET/POST/PUT/DELETE /api/generators/*`, `GET/POST/PUT/DELETE /api/folders/*` | Auth Module, Database Layer |
| Calculation Engine | Perform power calculations, diversity factors, unit conversions, generator sizing recommendations | None (stateless) | Internal Python module called by Project Engine | Project Engine |
| Requirements Pipeline | Manage client requirement submissions, engineer review workflow, approval/rejection, notifications | `client_requirements`, `requirement_changes`, `notifications` | `GET/POST/PUT /api/requirements/*`, `GET /api/notifications/*` | Auth Module, Database Layer |
| Layout Builder | Provide interactive canvas for drag-and-drop equipment placement, site layout design, and PNG/SVG export | None (client-side state via Zustand) | Standalone SPA at `/layout-builder/`, communicates with Project Engine via REST | Project Engine |
| Report Generator | Generate PDF documents from project data using templates (load schedules, single-line diagrams, cover pages) | None (stateless) | `POST /api/reports/generate` internally proxied to PDF server on port 5020 | Project Engine, Database Layer |
| Database Layer | Provide data persistence, migrations, connection management for SQLite | All tables (shared responsibility with owning components) | Internal Python module; no direct API exposure | None |

---

## [x] 6. Process/Runtime View

### [x] Key Scenarios

#### [x] Scenario 1: Engineer Creates a Project and Calculates Power

```
Engineer        Nginx (80)      Flask (8000)      SQLite          Calc Engine
   |                |                |                |                |
   |  POST /api/    |                |                |                |
   |  projects      |                |                |                |
   +--------------->+ proxy_pass     |                |                |
   |                +--------------->+ validate JWT   |                |
   |                |                + INSERT project |                |
   |                |                +--------------->+ write          |
   |                |                +<---------------+ OK             |
   |                +<---------------+ 201 Created    |                |
   +<---------------+                |                |                |
   |                |                |                |                |
   |  POST /api/    |                |                |                |
   |  loads         |                |                |                |
   +--------------->+--------------->+ validate JWT   |                |
   |                |                + INSERT loads   |                |
   |                |                +--------------->+ write          |
   |                |                +<---------------+ OK             |
   |                |                |                |                |
   |                |                + calculate()    |                |
   |                |                +------------------------------->+
   |                |                |                |   power math   |
   |                |                +<-------------------------------+
   |                |                |   results      |                |
   |                +<---------------+ 201 + totals   |                |
   +<---------------+                |                |                |
```

#### [x] Scenario 2: Client Submits Requirements, Engineer Reviews

```
Client          Nginx           Flask             SQLite           Email SMTP
   |                |                |                |                |
   |  POST /api/    |                |                |                |
   |  requirements  |                |                |                |
   +--------------->+--------------->+ validate JWT   |                |
   |                |                | (client role)  |                |
   |                |                + INSERT req     |                |
   |                |                +--------------->+                |
   |                |                + INSERT notif   |                |
   |                |                +--------------->+                |
   |                |                + send email     |                |
   |                |                +------------------------------->+
   |                |                +<-------------------------------+
   |                +<---------------+ 201 Created    |                |
   +<---------------+                |                |                |
   |                |                |                |                |
Engineer        Nginx           Flask             SQLite           Email SMTP
   |                |                |                |                |
   |  PUT /api/     |                |                |                |
   |  requirements/ |                |                |                |
   |  {id}/approve  |                |                |                |
   +--------------->+--------------->+ validate JWT   |                |
   |                |                | (engineer role)|                |
   |                |                + UPDATE req     |                |
   |                |                +--------------->+                |
   |                |                + INSERT change  |                |
   |                |                +--------------->+                |
   |                |                + notify client  |                |
   |                |                +------------------------------->+
   |                +<---------------+ 200 OK         |                |
   +<---------------+                |                |                |
```

#### [x] Scenario 3: PDF Report Generation

```
Engineer        Nginx (80)      Flask (8000)      PDF Server (5020)   SQLite
   |                |                |                |                   |
   |  POST /api/    |                |                |                   |
   |  reports/gen   |                |                |                   |
   +--------------->+--------------->+ validate JWT   |                   |
   |                |                + fetch project  |                   |
   |                |                +---------------------------------->+
   |                |                +<----------------------------------+
   |                |                + POST to :5020  |                   |
   |                |                +--------------->+ ReportLab         |
   |                |                |                | build PDF         |
   |                |                +<---------------+ PDF bytes         |
   |                +<---------------+ 200 + PDF file |                   |
   +<---------------+                |                |                   |
```

### [x] Scheduled Jobs

| Job Name | Schedule | Components Involved | Data Processed | Duration Target |
|----------|---------|--------------------|--------------------|----------------|
| Session Cleanup | Daily 02:00 AST | Auth Module, Database Layer | Expired session records | < 5 seconds |
| Notification Digest | Daily 07:00 AST | Requirements Pipeline | Pending unread notifications | < 10 seconds |

---

## [x] 7. Deployment View

### [x] Deployment Diagram

```
+------------------------------------------------------------------------+
|                    DigitalOcean Droplet (Ubuntu 24.04)                  |
|                    4 vCPU / 8 GB RAM / 160 GB SSD                      |
|                    Region: Jeddah or nearest (FRA1 fallback)           |
|                                                                        |
|  +------------------------------------------------------------------+  |
|  |                     Nginx (port 80/443)                          |  |
|  |  - TLS termination (Let's Encrypt)                               |  |
|  |  - Reverse proxy to Flask (:8000)                                |  |
|  |  - Static file serving (/public/*)                               |  |
|  |  - Rate limiting (60 req/min per IP)                             |  |
|  |  - Gzip compression                                              |  |
|  +--------+----------------------+------------------+---------------+  |
|           |                      |                  |                  |
|           v                      v                  v                  |
|  +----------------+    +-----------------+   +----------------+        |
|  | Flask App      |    | PDF Server      |   | Static Files   |        |
|  | (Gunicorn)     |    | (Python)        |   | (Vite build)   |        |
|  | Port: 8000     |    | Port: 5020      |   |                |        |
|  |                |    |                 |   | index.html     |        |
|  | Modules:       |    | ReportLab       |   | login.html     |        |
|  |  - auth        |    | PDF templates   |   | register.html  |        |
|  |  - projects    |    |                 |   | req-form.html  |        |
|  |  - loads       |    +-----------------+   | req-admin.html |        |
|  |  - clients     |                          | client-portal  |        |
|  |  - generators  |                          | profile.html   |        |
|  |  - folders     |                          | settings.html  |        |
|  |  - requirements|    +-----------------+   | user-mgmt.html |        |
|  |                |--->| SQLite DB       |   |                |        |
|  +----------------+    | /database/      |   | /layout-builder|        |
|                        | power_atlas.db  |   | (React SPA)    |        |
|                        +-----------------+   +----------------+        |
|                                                                        |
|  +------------------------------------------------------------------+  |
|  |  Future Services (pre-installed, inactive)                       |  |
|  |  - Mosquitto MQTT Broker (port 1883)                             |  |
|  |  - InfluxDB (port 8086) -- telemetry time-series                 |  |
|  |  - Grafana (port 3000) -- telemetry dashboards                   |  |
|  +------------------------------------------------------------------+  |
+------------------------------------------------------------------------+
```

### [x] Infrastructure Components

| Component | Specification | Purpose | Location |
|-----------|--------------|---------|----------|
| DigitalOcean Droplet | 4 vCPU, 8 GB RAM, 160 GB SSD, Ubuntu 24.04 | All application services | FRA1 (Frankfurt) or nearest to Saudi Arabia |
| Nginx 1.24+ | Reverse proxy, web server | TLS termination, static files, rate limiting, routing | Droplet |
| Gunicorn + Flask | 4 workers, Python 3.12 | Backend API server | Droplet, port 8000 |
| PDF Server | Python 3.12, ReportLab | PDF document generation | Droplet, port 5020 |
| SQLite 3.45+ | Single file database | Persistent data storage | Droplet, /database/ directory |
| Let's Encrypt | TLS certificates | HTTPS encryption | Droplet, auto-renewed via certbot |
| Mosquitto (future) | MQTT broker | IoT sensor data ingestion | Droplet, port 1883 |
| InfluxDB (future) | Time-series database | Generator telemetry storage | Droplet, port 8086 |
| Grafana (future) | Dashboard server | Telemetry visualization | Droplet, port 3000 |

### [x] Network Topology

| From | To | Protocol | Port | Encrypted |
|------|-----|----------|------|-----------|
| Users (Internet) | Nginx | HTTPS | 443 | Yes (TLS 1.2+) |
| Nginx | Flask App | HTTP | 8000 | No (localhost only) |
| Flask App | PDF Server | HTTP | 5020 | No (localhost only) |
| Flask App | SQLite | File I/O | N/A | No (local filesystem) |
| Flask App | Email SMTP | SMTP | 587 | Yes (STARTTLS) |
| IoT Sensors (future) | Mosquitto | MQTT | 1883 | Yes (TLS planned) |

---

## [x] 8. Development View

### [x] Repository Structure

```
power-atlas/
+-- server/                    # Flask backend
|   +-- app.py                 # Application entry point
|   +-- config.py              # Configuration management
|   +-- auth/                  # Auth module (login, register, sessions)
|   +-- projects/              # Project engine routes and models
|   +-- loads/                 # Load management module
|   +-- clients/               # Client management module
|   +-- generators/            # Generator catalog and assignment
|   +-- folders/               # Folder organization module
|   +-- requirements/          # Requirements pipeline module
|   +-- middleware/             # JWT validation, CSRF, rate limiting
|   +-- utils/                 # Calculation engine, helpers
|   +-- pdf_server.py          # PDF generation service (port 5020)
|   +-- templates/             # PDF report templates (ReportLab)
+-- public/                    # Frontend (Vite + Tailwind + vanilla JS)
|   +-- index.html             # Dashboard / project list
|   +-- login.html             # Login page
|   +-- register.html          # Registration page
|   +-- requirement-form.html  # Client requirement submission
|   +-- requirements-admin.html # Engineer requirement review
|   +-- client-portal.html     # Client status portal
|   +-- profile.html           # User profile management
|   +-- settings.html          # System settings (admin)
|   +-- user-management.html   # User administration (admin)
|   +-- src/                   # JavaScript source files
|   +-- styles/                # Tailwind CSS source
|   +-- vite.config.js         # Vite build configuration
+-- layout-builder-source/     # React Layout Builder sub-app
|   +-- src/
|   |   +-- App.tsx            # Root component
|   |   +-- store/             # Zustand state management
|   |   +-- components/        # Canvas, toolbar, equipment library
|   |   +-- hooks/             # Custom React hooks
|   |   +-- types/             # TypeScript type definitions
|   +-- tsconfig.json
|   +-- package.json
+-- database/
|   +-- power_atlas.db         # SQLite database file
|   +-- migrations/            # Schema migration scripts
|   +-- seed.py                # Test data seeding
+-- nginx/
|   +-- power-atlas.conf       # Nginx site configuration
+-- deploy/
    +-- setup.sh               # Server provisioning script
    +-- deploy.sh              # Deployment script
```

### [x] Build Pipeline

```
Developer Push --> SSH to Droplet --> git pull --> pip install --> vite build --> restart services
                                                                                     |
                                                            +------------------------+
                                                            |
                                              systemctl restart power-atlas
                                              systemctl restart power-atlas-pdf
```

### [x] Module Mapping

| Logical Component | Code Module/Package | Repository |
|------------------|--------------------|-----------|
| Auth Module | `server/auth/` | power-atlas (monorepo) |
| Project Engine | `server/projects/`, `server/loads/`, `server/clients/`, `server/generators/`, `server/folders/` | power-atlas (monorepo) |
| Calculation Engine | `server/utils/calculations.py` | power-atlas (monorepo) |
| Requirements Pipeline | `server/requirements/` | power-atlas (monorepo) |
| Layout Builder | `layout-builder-source/` | power-atlas (monorepo) |
| Report Generator | `server/pdf_server.py`, `server/templates/` | power-atlas (monorepo) |
| Database Layer | `database/`, `server/config.py` | power-atlas (monorepo) |
| Frontend (Main App) | `public/` | power-atlas (monorepo) |

---

## [x] 9. Quality Attribute Approaches

### [x] Performance

| NFR | Approach | Implementation |
|-----|----------|---------------|
| SWR-NFR-P001 | In-process calculation with no external service calls | Python calculation module invoked directly by Flask; SQLite local file reads with sub-millisecond latency |
| SWR-NFR-P002 | Minimal JavaScript bundle, no SPA framework for main app | Vanilla JS with Vite tree-shaking; average page JS < 50 KB gzipped |
| SWR-NFR-P003 | Static asset caching | Nginx serves static files with cache-control headers (1 year for hashed assets) |

### [x] Security

| NFR | Approach | Implementation |
|-----|----------|---------------|
| SWR-NFR-S001 | Password hashing with adaptive cost | bcrypt with work factor 12; salted per-user |
| SWR-NFR-S002 | Token-based authentication | JWT tokens with 24-hour expiry; refresh via session table |
| SWR-NFR-S003 | Cross-site request forgery prevention | CSRF tokens generated per session; validated on all state-changing requests |
| SWR-NFR-S004 | Rate limiting | Nginx rate limiting at 60 requests/minute per IP; Flask-Limiter for API-specific limits |
| SWR-NFR-S005 | Role-based access control | Middleware checks user role (admin/engineer/client) before route handler execution |

### [x] Usability

| NFR | Approach | Implementation |
|-----|----------|---------------|
| SWR-NFR-U001 | Bilingual interface | i18n JSON files for English and Arabic; Tailwind RTL plugin for layout mirroring |
| SWR-NFR-U002 | Responsive design | Tailwind breakpoints (sm/md/lg/xl); mobile-first approach |

### [x] Reliability

| NFR | Approach | Implementation |
|-----|----------|---------------|
| SWR-NFR-A001 | Auto-restart on failure | systemd service units with `Restart=always` and `RestartSec=5` |
| SWR-NFR-A002 | Database backup | Daily SQLite backup via cron to local backup directory; weekly off-site copy |
| SWR-NFR-A003 | Graceful error handling | Flask error handlers return structured JSON; frontend displays user-friendly messages |

---

## [x] 10. Technology Stack

| Technology | Version | Purpose | License | ADR Reference |
|-----------|---------|---------|---------|---------------|
| Python | 3.12 | Backend runtime | PSF License | ADR-003 |
| Flask | 3.0 | Web framework / REST API | BSD-3-Clause | ADR-003 |
| Gunicorn | 21.2 | WSGI HTTP server (4 workers) | MIT | ADR-001 |
| SQLite | 3.45 | Relational database | Public Domain | ADR-002 |
| Nginx | 1.24 | Reverse proxy, TLS, static files | BSD-2-Clause | ADR-001 |
| Vite | 5.x | Frontend build tool | MIT | ADR-005 |
| Tailwind CSS | 3.4 | Utility-first CSS framework | MIT | ADR-005 |
| Vanilla JavaScript | ES2022 | Main app frontend logic | N/A | ADR-005 |
| React | 18.2 | Layout Builder UI framework | MIT | ADR-004 |
| TypeScript | 5.3 | Layout Builder type safety | Apache-2.0 | ADR-004 |
| Konva.js | 9.x | HTML5 Canvas library for layout builder | MIT | ADR-004 |
| Zustand | 4.x | Layout Builder state management | MIT | ADR-004 |
| ReportLab | 4.1 | PDF document generation | BSD | ADR-001 |
| bcrypt | 4.1 | Password hashing | Apache-2.0 | -- |
| PyJWT | 2.8 | JWT token generation/validation | MIT | -- |
| Let's Encrypt | -- | TLS certificates | N/A | -- |
| Mosquitto (future) | 2.0 | MQTT broker for IoT | EPL/EDL | -- |
| InfluxDB (future) | 2.7 | Time-series telemetry database | MIT | -- |
| Grafana (future) | 10.x | Telemetry dashboards | AGPL-3.0 | -- |

---

## [x] 11. Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| SQLite write contention under concurrent load | Low | Medium | WAL mode enabled; write operations serialized via Flask request queue; projected max 50 concurrent users well within limits |
| Single point of failure (one droplet) | Medium | High | Daily automated backups; documented recovery procedure; 99.5% SLA acceptable for internal tool |
| Layout Builder bundle size bloats page load | Low | Low | Layout Builder is a separate route; lazy-loaded only when engineer navigates to it; main app unaffected |
| Team knowledge concentration (1-2 developers) | High | Medium | Architecture documented; code modular; standard Python/JS stack easy to hire for |
| SQLite database file corruption | Low | High | WAL mode for crash resistance; daily backups; migration scripts for rebuild |
| Future IoT volume exceeds single-server capacity | Low | Medium | InfluxDB handles time-series separately; can offload MQTT broker to second droplet when needed |

---

## [x] 12. Architecture Decision Records

| ADR | Title | Status |
|-----|-------|--------|
| ADR-001 | Monolithic architecture on single droplet | Accepted |
| ADR-002 | SQLite over PostgreSQL for database | Accepted |
| ADR-003 | Flask over Django/FastAPI for backend framework | Accepted |
| ADR-004 | Konva.js with React for layout builder | Accepted |
| ADR-005 | Vanilla JS for main application frontend | Accepted |

Full ADRs are located in [architecture-decision-records.md](architecture-decision-records.md).

---

## [x] 13. Traceability

| SWR ID | Architecture Component | Viewpoint | ADR Reference |
|--------|----------------------|-----------|---------------|
| SWR-F-001 | Project Engine | Logical | -- |
| SWR-F-010 | Calculation Engine | Logical | -- |
| SWR-F-015 | Layout Builder | Logical | ADR-004 |
| SWR-F-020 | Report Generator | Logical | ADR-001 |
| SWR-F-025 | Requirements Pipeline | Logical | -- |
| SWR-NFR-P001 | Calculation Engine, Database Layer | Quality Attributes | ADR-002 |
| SWR-NFR-P002 | Frontend (Main App) | Quality Attributes | ADR-005 |
| SWR-NFR-S001 | Auth Module | Quality Attributes | -- |
| SWR-NFR-S002 | Auth Module | Quality Attributes | -- |
| SWR-NFR-A001 | Deployment (systemd, Nginx) | Deployment | ADR-001 |
| SWR-NFR-U001 | Frontend (Main App) | Quality Attributes | ADR-005 |

---

## [x] 14. Appendices

### [x] Appendix A: Glossary

| Term | Definition |
|------|-----------|
| Load | An electrical load item within a project (e.g., lighting tower, AC unit) with wattage, quantity, and diversity factor |
| Generator | A power generator unit from GlowPowerRental's fleet, with rated capacity in kVA/kW |
| Diversity Factor | A multiplier (0.0-1.0) applied to loads to account for non-simultaneous usage |
| Layout Builder | The React/Konva.js sub-application for designing site power distribution layouts |
| Requirements Pipeline | The workflow for client power requirement submission, engineer review, and approval |
| Project Activity | An audit log entry recording changes to a project (created, modified, status changed) |

### [x] Appendix B: References

| Document | Version | Date |
|----------|---------|------|
| Power Atlas -- Software Requirements Specification | 1.0 | 2025-12-01 |
| Power Atlas -- Business Requirements Document | 1.0 | 2025-11-15 |
| GlowPowerRental IT Infrastructure Policy | 2.0 | 2025-10-01 |

---

## COMPLETION CHECKLIST

- [x] Document Control filled in with version, author, and SRS reference
- [x] Approvers identified
- [x] Executive Summary written
- [x] Architecture Goals and Constraints documented
- [x] Architecture-Significant Requirements listed with traceability
- [x] System Context View diagram and external entities table completed
- [x] Component Diagram and descriptions completed
- [x] Process/Runtime View covers top scenarios
- [x] Deployment View with infrastructure and network topology
- [x] Development View with repo structure and module mapping
- [x] Quality Attribute Approaches for Performance, Security, Usability, Reliability
- [x] Technology Stack table completed with ADR references
- [x] Risks and Mitigations identified
- [x] ADR index populated
- [x] Traceability matrix linked
- [x] Reviewed by System Architect, Product Owner, and QA Lead

---

## CROSS-REFERENCES

| Artifact | Location | Relationship |
|----------|----------|--------------|
| Architecture Decision Records | [architecture-decision-records.md](architecture-decision-records.md) | ADRs support decisions in this document |
| Component Diagram | [component-diagram.md](component-diagram.md) | Detailed component view for Section 5 |
| System Context Diagram | [system-context-diagram.md](system-context-diagram.md) | Detailed context view for Section 4 |
| Software Requirements Specification | Phase 2 SRS | Source requirements driving the architecture |
| Requirements Traceability Matrix | Phase 2 RTM | Full traceability from requirements to components |
| Runbook | [Create Architecture Description](../../phase-3-system-architecture/runbooks/create-architecture-description.md) | Step-by-step procedure |
