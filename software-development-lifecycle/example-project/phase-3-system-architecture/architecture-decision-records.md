> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Architecture Decision Records -- Power Atlas

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P3-001 |
| **When to Use** | Recording any architecture-significant decision (technology, pattern, integration) |
| **Owner** | Tech Lead |
| **Reviewer** | System Architect |
| **SLA** | 2 business days per ADR |
| **Runbook** | [Write Architecture Decision Record](../../phase-3-system-architecture/runbooks/write-architecture-decision-record.md) |
| **Last Verified** | 2026-03-05 |

---

## SCALING GATE

> **Applied:** Small project (1-2 devs) -- Evaluation Matrix optional; Alternatives Considered reduced to minimum 1 alternative per ADR.

---

## [x] ADR-001: Monolithic Architecture on Single Droplet

### [x] Status

Accepted

### [x] Date

2025-12-10

### [x] Context

- Power Atlas needs to serve power engineers, admins, and clients with a web application that includes a REST API, static frontend, PDF generation service, and a database.
- The infrastructure budget is capped at $50/month, which affords a single DigitalOcean droplet (4 vCPU, 8 GB RAM).
- The development team consists of 1-2 developers who also handle operations.
- Projected user base is under 100 concurrent users (internal tool for GlowPowerRental staff and their clients).
- Requirements: SWR-NFR-A001 (99.5% uptime), AC-001 (single droplet), AC-002 (small team), AC-004 (budget constraint).

### [x] Decision

We will deploy Power Atlas as a monolithic application on a single DigitalOcean droplet, with Nginx as reverse proxy, Flask as the API server, a separate PDF generation process, and SQLite as the database -- all on the same machine.

### [x] Consequences

#### [x] Positive

- Minimal operational complexity: one server to monitor, update, and back up
- No inter-service network latency; all communication is localhost or in-process
- Single deployment target simplifies CI/CD to a simple SSH + git pull + restart
- Infrastructure cost stays under $20/month for the droplet

#### [x] Negative

- Single point of failure: if the droplet goes down, the entire application is unavailable
- Vertical scaling only: must upgrade the droplet to handle more load (no horizontal scaling)
- All services compete for the same CPU and RAM resources

#### [x] Risks

- Droplet failure causes total outage: mitigated by daily automated backups and documented 30-minute recovery procedure (spin up new droplet, restore from backup)
- Resource contention during PDF generation spikes: mitigated by limiting PDF generation to 2 concurrent requests via semaphore; PDF server is lightweight (ReportLab is CPU-bound but fast)

### [x] Alternatives Considered

#### [x] Microservices on Kubernetes (DigitalOcean Managed K8s)

- **Description:** Separate services for auth, projects, PDF generation, each in its own container, orchestrated by Kubernetes
- **Pros:** Independent scaling, fault isolation, technology diversity per service
- **Cons:** Minimum $60/month for managed K8s + node pools; massive operational overhead for 1-2 developers; overkill for < 100 users
- **Why rejected:** Exceeds budget, team cannot maintain Kubernetes infrastructure, application complexity does not warrant service decomposition

#### [x] Docker Compose on Single Server

- **Description:** Same single server, but each component (Flask, PDF server, Nginx, SQLite) runs in its own Docker container managed by Docker Compose
- **Pros:** Better isolation, reproducible environments, easier to migrate to multi-server later
- **Cons:** Adds Docker layer complexity; debugging requires container log inspection; no real scaling benefit on one server
- **Why rejected:** Added complexity without meaningful benefit for the current scale; direct systemd management is simpler and more transparent for the team

### [x] Related Documents

- Requirements: SWR-NFR-A001, AC-001, AC-002, AC-004
- Architecture: ADD Sections 7 (Deployment View), 11 (Risks)

---

## [x] ADR-002: SQLite over PostgreSQL for Database

### [x] Status

Accepted

### [x] Date

2025-12-10

### [x] Context

- Power Atlas requires a relational database to store users, projects, loads, clients, generators, folders, requirements, sessions, notifications, and activity logs.
- The application runs on a single server (per ADR-001) with all data access from a single Flask process (4 Gunicorn workers).
- Projected data volume: < 10,000 projects, < 100,000 load records, < 500 users over the system lifetime.
- Concurrent write operations are infrequent (mostly read-heavy dashboard and project views).
- Requirements: SWR-NFR-P001 (< 200ms calculations), AC-001 (single server), AC-002 (small team).

### [x] Decision

We will use SQLite (WAL mode) as the primary relational database for Power Atlas.

### [x] Consequences

#### [x] Positive

- Zero configuration: no database server process to install, configure, or manage
- Sub-millisecond read latency: data is on local SSD with no network round-trip
- Backup is a single file copy (`cp power_atlas.db power_atlas.db.bak`)
- Excellent for read-heavy workloads with modest write concurrency
- No additional memory footprint (SQLite runs in-process)

#### [x] Negative

- Write concurrency is limited: SQLite locks the entire database during writes (WAL mode mitigates but does not eliminate)
- No built-in replication or clustering for high availability
- Cannot easily migrate to a separate database server if the application scales beyond one machine
- Limited to SQL features supported by SQLite (no stored procedures, limited ALTER TABLE)

#### [x] Risks

- Write contention under concurrent API requests: mitigated by WAL mode (allows concurrent reads during writes) and serializing write operations; projected max 50 concurrent users generates minimal write contention
- Database corruption from unexpected shutdown: mitigated by WAL mode (crash-safe) and daily backups; SQLite is well-tested for crash recovery

### [x] Alternatives Considered

#### [x] PostgreSQL

- **Description:** Full-featured relational database running as a separate server process on the same droplet
- **Pros:** Better write concurrency, full SQL support, built-in replication, industry standard for web applications
- **Cons:** Requires 200-500 MB additional RAM for the PostgreSQL server process; requires configuration, monitoring, and maintenance (pg_hba.conf, vacuum, connection pooling); adds operational complexity for a small team
- **Why rejected:** Operational overhead is not justified for < 100 concurrent users and < 500 write operations per hour; SQLite's simplicity aligns with the small-team constraint

#### [x] MySQL/MariaDB

- **Description:** Alternative relational database with similar capabilities to PostgreSQL
- **Pros:** Good performance, wide ecosystem, managed options available
- **Cons:** Same operational overhead as PostgreSQL; slightly less developer tooling in Python ecosystem compared to PostgreSQL; no meaningful advantage over PostgreSQL for this use case
- **Why rejected:** If we needed a server-based database, PostgreSQL would be preferred; MySQL offers no advantage that would change the SQLite vs. server-database decision

### [x] Related Documents

- Requirements: SWR-NFR-P001, AC-001, AC-002
- Architecture: ADD Sections 5 (Logical View), 7 (Deployment View)

---

## [x] ADR-003: Flask over Django/FastAPI for Backend Framework

### [x] Status

Accepted

### [x] Date

2025-12-12

### [x] Context

- Power Atlas backend needs to serve a REST API for project management, authentication, calculations, and PDF generation orchestration.
- The development team has strong Python expertise and experience with Flask.
- The application is a traditional request-response web API (not real-time, not async-heavy).
- The modular API structure requires clean separation into auth, projects, loads, clients, generators, folders, and requirements modules.
- Requirements: AC-006 (Python team expertise), AC-002 (small team), SWR-F-001 through SWR-F-025.

### [x] Decision

We will use Flask as the backend web framework for Power Atlas, organized into modular Blueprints for each domain (auth, projects, loads, clients, generators, folders, requirements).

### [x] Consequences

#### [x] Positive

- Team already proficient in Flask: zero ramp-up time
- Flask Blueprints provide clean module separation without framework-imposed patterns
- Lightweight: only pulls in what is needed (no ORM, admin panel, or template engine required)
- Large ecosystem of extensions (Flask-JWT-Extended, Flask-Limiter, Flask-CORS) for cross-cutting concerns
- Simple to understand and debug: explicit routing, no magic

#### [x] Negative

- No built-in ORM: must write SQL queries directly or add SQLAlchemy (we chose direct SQL for simplicity with SQLite)
- No built-in admin panel: admin features must be built manually
- Synchronous by default: long-running operations block a Gunicorn worker (mitigated by having 4 workers and keeping operations fast)

#### [x] Risks

- Flask's synchronous nature limits throughput for I/O-bound operations: mitigated by the fact that SQLite I/O is local (sub-millisecond) and PDF generation is offloaded to a separate process on port 5020
- Framework may feel limiting if application grows significantly: mitigated by modular Blueprint structure that could be extracted into separate services if needed

### [x] Alternatives Considered

#### [x] Django

- **Description:** Full-featured Python web framework with ORM, admin panel, authentication, and batteries-included philosophy
- **Pros:** Built-in ORM, admin panel, authentication system, migrations, form validation; large community
- **Cons:** Heavy framework overhead for what is essentially a REST API; Django ORM adds abstraction layer that is unnecessary with SQLite direct queries; opinionated project structure does not match our modular layout; team would need to learn Django conventions
- **Why rejected:** Too heavy for our use case; built-in features (admin panel, ORM, template engine) are not needed since we have a separate frontend and direct SQL; team Flask expertise means faster delivery

#### [x] FastAPI

- **Description:** Modern Python web framework built on Starlette, with automatic OpenAPI docs, async support, and Pydantic validation
- **Pros:** Automatic API documentation, native async support, Pydantic request validation, excellent type hints
- **Cons:** Async paradigm requires different mental model and different libraries (async SQLite drivers, async SMTP); team has no async Python experience; benefits of async are negligible when database is local SQLite
- **Why rejected:** Async benefits are not realized with local SQLite (no network I/O to database); team would need to learn async patterns; Flask delivers equivalent functionality with team's existing expertise

### [x] Related Documents

- Requirements: AC-006, AC-002, SWR-F-001 through SWR-F-025
- Architecture: ADD Sections 5 (Logical View), 8 (Development View)

---

## [x] ADR-004: Konva.js with React for Layout Builder

### [x] Status

Accepted

### [x] Date

2025-12-15

### [x] Context

- Power Atlas requires an interactive layout builder where engineers can drag and drop equipment (generators, distribution boards, cable runs) onto a site plan canvas.
- The layout builder must support: panning, zooming, snapping to grid, equipment library sidebar, layer management, and export to PNG/SVG for PDF reports.
- This is a rich interactive application with complex state (equipment positions, connections, canvas transforms).
- The main application frontend uses vanilla JavaScript (per ADR-005), but the layout builder's complexity warrants a more structured approach.
- Requirements: SWR-F-015 (interactive layout builder).

### [x] Decision

We will build the Layout Builder as a separate React 18 + TypeScript sub-application using Konva.js (via react-konva) for canvas rendering and Zustand for state management.

### [x] Consequences

#### [x] Positive

- Konva.js provides high-performance 2D canvas rendering with built-in support for drag-and-drop, transforms, and event handling on canvas objects
- React component model is ideal for the complex UI (toolbar, sidebar, properties panel, canvas) with many interacting state pieces
- TypeScript catches equipment type mismatches and layout data structure errors at compile time
- Zustand provides simple, performant state management without Redux boilerplate
- react-konva integrates Konva.js declaratively into React component tree

#### [x] Negative

- Adds React, TypeScript, and Konva.js as dependencies (increases overall project complexity)
- Layout Builder has a separate build pipeline from the main application
- Developers must context-switch between vanilla JS (main app) and React/TS (layout builder)

#### [x] Risks

- Konva.js performance degrades with very large numbers of canvas objects (> 1000): mitigated by typical site layouts having 50-200 equipment items; can implement viewport culling if needed
- React/Konva version incompatibilities: mitigated by pinning versions and using react-konva as the integration layer

### [x] Alternatives Considered

#### [x] Fabric.js (Canvas Library without React)

- **Description:** Feature-rich HTML5 Canvas library with built-in object model, serialization, and manipulation
- **Pros:** Self-contained (no React needed), good serialization support, active community
- **Cons:** No native React integration (would need vanilla JS or wrapper); less performant than Konva.js for large numbers of objects; API is more complex for custom object types
- **Why rejected:** Lack of React integration means managing complex UI state manually; Konva.js + React provides better developer experience for the toolbar/sidebar/properties panel UI surrounding the canvas

#### [x] SVG-based approach (D3.js or plain SVG manipulation)

- **Description:** Render equipment as SVG elements in the DOM, manipulated via D3.js or direct DOM APIs
- **Pros:** SEO-friendly (not relevant here), native DOM events, no canvas abstraction
- **Cons:** SVG performance degrades significantly with many elements (DOM nodes are expensive); drag-and-drop requires manual implementation; zoom/pan on SVG is complex
- **Why rejected:** Canvas-based rendering (Konva.js) significantly outperforms SVG for interactive applications with frequent redraws and many draggable objects

### [x] Related Documents

- Requirements: SWR-F-015
- Architecture: ADD Sections 5 (Logical View), 8 (Development View)

---

## [x] ADR-005: Vanilla JavaScript for Main Application Frontend

### [x] Status

Accepted

### [x] Date

2025-12-12

### [x] Context

- Power Atlas main application consists of multiple pages: dashboard, login, register, requirement forms, admin panels, client portal, profile, settings, and user management.
- These pages are primarily form-based CRUD interfaces with data tables, filters, and simple interactivity.
- Page load performance is important (SWR-NFR-P002: under 2 seconds on 4G).
- The Layout Builder already uses React (ADR-004), so React is available in the project but adds significant bundle size.
- The team is proficient in both vanilla JavaScript and React.
- Requirements: SWR-NFR-P002 (page load < 2s), AC-002 (small team), SWR-NFR-U001 (bilingual).

### [x] Decision

We will build the main application frontend as a multi-page application using vanilla JavaScript, Vite as the build tool, and Tailwind CSS for styling. React is used only for the Layout Builder sub-application.

### [x] Consequences

#### [x] Positive

- Minimal JavaScript bundle size: each page loads only the JS it needs (typically < 50 KB gzipped)
- No framework abstraction overhead: direct DOM manipulation is transparent and debuggable
- Faster initial page load compared to SPA frameworks (no framework runtime to download and parse)
- Vite provides hot module replacement during development and optimized builds for production
- Tailwind CSS utility classes with RTL plugin handle bilingual layout efficiently
- Each HTML page is independently deployable and cacheable

#### [x] Negative

- No component reuse system: shared UI elements (navigation, footers, modals) must be managed via template partials or JS includes
- State management across pages requires localStorage or URL parameters (no in-memory router state)
- Form validation and data binding must be implemented manually (no framework helpers)

#### [x] Risks

- Code duplication across pages (navigation bars, API call patterns): mitigated by shared utility modules (`public/src/api.js`, `public/src/components/`) imported by each page
- Difficulty maintaining consistency across 9 HTML pages: mitigated by Tailwind design system and shared component JS modules

### [x] Alternatives Considered

#### [x] React Single-Page Application for Entire Frontend

- **Description:** Build the entire frontend (including all pages) as a React SPA with React Router
- **Pros:** Component reuse, consistent state management, established patterns for forms and data fetching
- **Cons:** 150-200 KB framework bundle added to every page load; SPA requires client-side routing (adds complexity for SEO-irrelevant internal tool); entire frontend must be loaded before any page is interactive; overkill for form-based CRUD pages
- **Why rejected:** Page load time would increase significantly (SWR-NFR-P002 violation risk); the majority of pages are simple forms that do not benefit from React's virtual DOM; React is justified only for the Layout Builder's complex interactive canvas

#### [x] Vue.js or Svelte Lightweight SPA

- **Description:** Use a lighter-weight framework (Vue 3 or Svelte) for the main app to get component reuse without React's bundle size
- **Pros:** Smaller bundle than React; good component model; Svelte compiles away the framework
- **Cons:** Adds another framework to the project (alongside React for Layout Builder); team would need to learn a new framework; still adds framework overhead for pages that do not need it
- **Why rejected:** Introducing a second framework alongside React increases cognitive load; vanilla JS is simpler and the team is already proficient; the CRUD pages do not justify any framework overhead

### [x] Related Documents

- Requirements: SWR-NFR-P002, AC-002, SWR-NFR-U001
- Architecture: ADD Sections 5 (Logical View), 8 (Development View), 9 (Quality Attributes)

---

## COMPLETION CHECKLIST

- [x] All ADRs have unique IDs and descriptive titles
- [x] All ADR statuses set (Accepted)
- [x] Context describes the problem with requirement references
- [x] Each decision is specific and implementable
- [x] Positive and negative consequences listed for each ADR
- [x] Risks identified with mitigations for each ADR
- [x] At least 1 alternative considered per ADR (small project scaling gate)
- [x] Related documents linked for each ADR
- [x] Reviewed by System Architect

---

## CROSS-REFERENCES

| Artifact | Location | Relationship |
|----------|----------|--------------|
| Architecture Description Document | [architecture-description.md](architecture-description.md) | ADRs are listed in ADD Section 12 |
| Component Diagram | [component-diagram.md](component-diagram.md) | Decisions drive component boundaries |
| System Context Diagram | [system-context-diagram.md](system-context-diagram.md) | Decisions affect external integrations |
| Software Requirements Specification | Phase 2 SRS | Requirements referenced in Context sections |
| Runbook | [Write Architecture Decision Record](../../phase-3-system-architecture/runbooks/write-architecture-decision-record.md) | Step-by-step procedure |
