> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Technical Debt Register -- Power Atlas

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P5-003 |
| **Project** | Power Atlas -- GlowPowerRental |
| **Repository** | github.com/glowpowerrental/power-atlas |
| **Owner** | Layla Haddad (Developer) |
| **Reviewer** | Mohammad Al-Farsi (Tech Lead) |
| **Last Updated** | 2026-03-05 |
| **Last Verified** | 2026-03-05 |

---

## Scaling Decision Gate

| Total Open Items | Action |
|------------------|--------|
| **< 10** | Review in retrospective, address opportunistically |
| **10-25** | Dedicate 10% of sprint capacity to debt reduction |
| **25-50** | Dedicate 20% of sprint capacity; escalate to Tech Lead |
| **> 50** | STOP. Schedule dedicated debt sprint before new features |

**Current: 3 open items -- Review in retrospective, address opportunistically.**

---

## Scoring Guide

### Impact (1-5)

| Score | Meaning |
|-------|---------|
| 1 | Cosmetic. No functional impact. |
| 2 | Minor inconvenience. Slightly slows development. |
| 3 | Moderate. Affects developer productivity or minor performance issue. |
| 4 | Significant. Causes bugs, security concerns, or major performance issues. |
| 5 | Critical. Blocks features, data loss risk, or active security vulnerability. |

### Effort (1-5)

| Score | Meaning |
|-------|---------|
| 1 | Less than 2 hours |
| 2 | Half day to 1 day |
| 3 | 2-3 days |
| 4 | 1 sprint (1-2 weeks) |
| 5 | Multiple sprints or architectural change |

### Priority

**Priority = Impact / Effort**

| Priority | Action |
|----------|--------|
| >= 3.0 | Schedule in current or next sprint |
| 1.5 - 2.9 | Backlog, schedule within 2-3 sprints |
| 1.0 - 1.4 | Backlog, address opportunistically |
| < 1.0 | Accept. Document. Review quarterly. |

---

## Status Values

| Status | Meaning |
|--------|---------|
| Open | Identified but not yet scheduled |
| Scheduled | Ticket created, assigned to a sprint |
| In Progress | Actively being resolved |
| Resolved | Fixed and verified |
| Accepted | Deliberately accepted. Will not fix. Reviewed quarterly. |

---

## Register

| ID | Title | Category | Impact | Effort | Priority | Status | Date Identified |
|----|-------|----------|--------|--------|----------|--------|-----------------|
| TD-001 | SQLite scalability limit at ~200 concurrent users | Infrastructure | 4 | 5 | 0.8 | Open | 2026-02-10 |
| TD-002 | BYPASS_AUTH=true flag in development config | Code | 5 | 1 | 5.0 | Scheduled | 2026-02-14 |
| TD-003 | Mixed vanilla JS and React in frontend | Design | 3 | 5 | 0.6 | Accepted | 2026-02-20 |

---

## Entry Details

### TD-001: SQLite Scalability Limit at ~200 Concurrent Users

| Field | Value |
|-------|-------|
| **ID** | TD-001 |
| **Title** | SQLite scalability limit at ~200 concurrent users |
| **Category** | Infrastructure |
| **Impact** | 4 (Significant -- database locks under concurrent write load cause request failures and potential data corruption) |
| **Effort** | 5 (Multiple sprints -- requires schema migration, ORM changes, connection pooling, deployment infrastructure for PostgreSQL) |
| **Priority** | 0.8 (Accept. Document. Review quarterly.) |
| **Status** | Open |
| **Affected Components** | `database/power_calculator.db`, all server modules (`auth.py`, `projects.py`, `loads.py`, `clients.py`, `generators.py`, `requirements.py`) |
| **Date Identified** | 2026-02-10 |
| **Identified By** | Mohammad Al-Farsi (Tech Lead), during architecture review |
| **Ticket** | -- |
| **Resolved Date** | -- |

**Description:**

Power Atlas uses a single SQLite3 database file (`database/power_calculator.db`) as its primary data store. SQLite uses file-level locking for writes, which means only one write transaction can execute at a time. Under testing, performance degrades noticeably at approximately 50 concurrent users and becomes unreliable above approximately 200 concurrent users, with `SQLITE_BUSY` errors and write timeouts.

The current user base is approximately 15-20 internal GlowPowerRental staff. SQLite is appropriate for this scale and provides the benefit of zero-configuration deployment (the database is a single file, no database server to manage). However, if Power Atlas is opened to external clients or the internal team grows significantly, the single-file database will become the bottleneck.

Additionally, SQLite lacks built-in support for concurrent schema migrations, role-based access control at the database level, and point-in-time recovery -- features that a production system may eventually require.

**Proposed Resolution:**

Plan a migration to PostgreSQL when the active user base exceeds 100 users. The migration would involve:

1. Install and configure PostgreSQL on the deployment server (or provision a managed instance)
2. Create a migration script to transfer the SQLite schema and data to PostgreSQL
3. Update all server modules to use `psycopg2` (or SQLAlchemy with a PostgreSQL dialect) instead of `sqlite3`
4. Implement connection pooling (e.g., `pgbouncer` or SQLAlchemy pool)
5. Update the systemd service configuration and Nginx reverse proxy if connection parameters change
6. Run parallel operation (both databases) for one sprint to validate data consistency

**Trigger for action:** Monthly review of active user count. If count exceeds 100, schedule migration in the next sprint planning session.

---

### TD-002: BYPASS_AUTH=true Flag in Development Configuration

| Field | Value |
|-------|-------|
| **ID** | TD-002 |
| **Title** | BYPASS_AUTH=true flag in development configuration |
| **Category** | Code |
| **Impact** | 5 (Critical -- if this flag is accidentally enabled in production, all API endpoints become accessible without authentication, exposing all client data, project data, and administrative functions) |
| **Effort** | 1 (Less than 2 hours -- remove the flag, remove the conditional check in `auth.py`, add a CI check to reject the flag in non-development configs) |
| **Priority** | 5.0 (Schedule in current or next sprint) |
| **Status** | Scheduled |
| **Affected Components** | `server/api/auth.py`, `config/development.env`, `config/production.env` |
| **Date Identified** | 2026-02-14 |
| **Identified By** | Layla Haddad (Developer), during code review of auth module |
| **Ticket** | SWR-SEC-012 |
| **Resolved Date** | -- |

**Description:**

The authentication handler (`server/api/auth.py`) contains a development convenience flag:

```python
if app.config.get('BYPASS_AUTH') == 'true':
    return func(*args, **kwargs)  # Skip JWT validation entirely
```

This flag is set to `true` in `config/development.env` to allow developers to test API endpoints without generating JWT tokens during local development. However, the flag mechanism has several risks:

- **Accidental production deployment:** If `BYPASS_AUTH=true` is set in the production environment (through a misconfigured `.env` file, environment variable leak, or copy-paste error), the entire authentication layer is silently disabled. Every endpoint that uses the `@jwt_required` decorator becomes publicly accessible.
- **No audit trail:** When auth is bypassed, no user identity is attached to requests, so audit logs show anonymous actions.
- **False confidence:** Developers testing with auth bypassed may not catch authorization bugs (e.g., User A accessing User B's projects) because the auth middleware that enforces ownership checks is entirely skipped.

The production configuration (`config/production.env`) currently does not set this flag, but there is no automated check to prevent it from being added.

**Proposed Resolution:**

1. Remove the `BYPASS_AUTH` conditional from `server/api/auth.py` entirely
2. Delete the `BYPASS_AUTH=true` line from `config/development.env`
3. For local development convenience, provide a CLI script (`scripts/generate-dev-token.py`) that generates a valid JWT for a test user, which developers can use in their HTTP client (Postman, curl, etc.)
4. Add a CI pipeline check that scans all config files and rejects any containing `BYPASS_AUTH`
5. Add a startup warning in the Flask app that logs a CRITICAL-level message if `BYPASS_AUTH` is detected in the environment, even if set to `false`

**Note:** This is the highest-priority debt item. It must be resolved before any production hardening or external user access.

---

### TD-003: Mixed Vanilla JS and React in Frontend

| Field | Value |
|-------|-------|
| **ID** | TD-003 |
| **Title** | Mixed vanilla JS and React in frontend |
| **Category** | Design |
| **Impact** | 3 (Moderate -- two mental models for developers, two build pipelines, potential bundle size overhead from React runtime loaded only for one feature) |
| **Effort** | 5 (Multiple sprints -- rewriting the entire application in React, or rewriting the layout builder in vanilla JS, is a significant effort either way) |
| **Priority** | 0.6 (Accept. Document. Review quarterly.) |
| **Status** | Accepted |
| **Affected Components** | `src/modules/` (vanilla JS modules: `power-calculations.js`, `ProjectManager.js`, `auth-handler.js`, `autosave-manager.js`), `src/layout-builder/` (React + Konva components) |
| **Date Identified** | 2026-02-20 |
| **Identified By** | Mohammad Al-Farsi (Tech Lead), during sprint retrospective |
| **Ticket** | -- |
| **Resolved Date** | -- |

**Description:**

The Power Atlas frontend uses two different rendering approaches:

- **Main application:** Built with Vite.js, Tailwind CSS, and vanilla JavaScript organized into ES modules (`power-calculations.js`, `ProjectManager.js`, `auth-handler.js`, `autosave-manager.js`). Pages are rendered with standard DOM manipulation and Tailwind utility classes.
- **Layout builder:** Built with React and Konva (via `react-konva`) for the interactive drag-and-drop site layout canvas where users place generators, distribution panels, and cable runs.

This split exists for a valid reason: the layout builder requires a 2D canvas with complex state management (undo/redo, snap-to-grid, zoom/pan, object grouping) that React + Konva handles well, while the rest of the application (forms, lists, dashboards) is straightforward enough that vanilla JS with Tailwind is simpler and lighter.

However, the mixed approach creates the following friction:

- **Developer onboarding:** New developers must understand both vanilla JS module patterns and React component patterns, including different state management approaches
- **Two build configurations:** Vite handles both, but the React components require the React plugin and JSX transform, adding complexity to `vite.config.js`
- **Bundle size:** The React runtime (~40 KB gzipped) and react-konva (~15 KB gzipped) are loaded even when the user is not on the layout builder page. Lazy loading mitigates this but adds code-splitting complexity.
- **Shared state:** Passing data between vanilla JS modules and React components requires a bridge pattern (currently using custom events and a shared global store), which is fragile and hard to debug

**Proposed Resolution:**

Accept this debt for v1.0. The layout builder's requirements genuinely benefit from React + Konva, and rewriting it in vanilla JS would be a regression in capability. Rewriting the entire app in React would be a large effort with no immediate user-facing benefit.

For v2.0, evaluate a full React migration when:
- The team has grown and standardizing on one framework reduces onboarding time
- Additional interactive features (e.g., real-time collaboration, complex dashboards) justify the React runtime overhead across the entire app
- The vanilla JS modules have grown complex enough that component-based architecture provides clear maintainability benefits

In the interim, maintain clear boundaries: all new features outside the layout builder use vanilla JS; all layout builder changes use React. Document the bridge pattern in `docs/architecture/frontend-bridge.md`.

---

## Summary Metrics

| Metric | Value | Trend |
|--------|-------|-------|
| Total open items | 3 | Stable |
| Critical items (impact 4-5) | 2 (TD-001, TD-002) | Stable |
| Items resolved this sprint | 0 | -- |
| Items added this sprint | 3 | New project |
| Oldest open item | TD-001 (23 days old) | -- |

---

## Completion Checklist

- [x] New debt entry added to Register table
- [x] Entry Detail block created with all fields populated
- [x] Impact scored (1-5)
- [x] Effort scored (1-5)
- [x] Priority calculated (Impact / Effort)
- [x] Status set correctly
- [x] Affected components identified
- [x] Proposed resolution documented
- [x] Summary metrics updated
- [x] Reviewed in sprint retrospective

---

## Cross-References

| Document | Path | Relationship |
|----------|------|--------------|
| Pull Request #42 | [pull-request-example.md](pull-request-example.md) | TD-002 identified during PR review process |
| Code Review Record | [code-review-record.md](code-review-record.md) | Reviewer flagged floating-point precision as potential future debt |
| Technical Debt Register Template | [../../phase-5-development/templates/technical-debt-register.md](../../phase-5-development/templates/technical-debt-register.md) | Template this artifact is based on |
| Manage Technical Debt Runbook | [../../phase-5-development/runbooks/manage-technical-debt.md](../../phase-5-development/runbooks/manage-technical-debt.md) | Procedure followed |
