# Setup Development Environment

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P5-002 |
| **Owner** | Developer |
| **Accountable** | Developer |
| **SLA** | 4 hours |
| **Escalation** | Tech Lead (technical blockers), DevOps (infrastructure issues) |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Machine meets minimum hardware requirements
- [ ] Admin/sudo access available on workstation
- [ ] Repository access granted (GitHub SSH key configured)
- [ ] Required software installed:

| Requirement | Version | Purpose |
|------------|---------|---------|
| Git | 2.40+ | Version control |
| Node.js | 20 LTS | Application runtime |
| npm | 10+ | Package management |
| Docker | 24+ | Local services (PostgreSQL, Redis, Mosquitto) |
| Docker Compose | 2.20+ | Service orchestration |
| VS Code (recommended) | Latest | Code editor |

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Repository access denied | STOP. Request access from repository admin. | Tech Lead |
| Docker fails to install or start | STOP. Verify system compatibility and resources. | DevOps |
| Required software version unavailable for OS | STOP. Request alternative setup instructions. | Tech Lead |
| Port conflicts with existing services | STOP. Identify conflicting process and resolve or reassign ports. | Tech Lead |

---

## PROCEDURE

### Step 1: Clone Repository (SLA: 10 min)

```bash
git clone git@github.com:<org>/[project-name].git
cd [project-name]
```

- [ ] Repository cloned successfully
- [ ] Working directory set to project root

> **IF** clone fails with permission error **THEN** verify SSH key is added to GitHub account
> **ELSE IF** clone fails with network error **THEN** verify VPN/network connectivity

### Step 2: Install Dependencies (SLA: 10 min)

```bash
npm install
```

- [ ] All dependencies installed without errors

> **IF** npm install fails **THEN** delete `node_modules` and `package-lock.json`, retry `npm install`

### Step 3: Configure Environment Variables (SLA: 20 min)

```bash
cp .env.example .env
```

- [ ] `.env` file created from `.env.example`
- [ ] All required variables populated with local values
- [ ] `.env` file is in `.gitignore` (never committed)

> **IF** a required variable value is unknown **THEN** consult Tech Lead or check project wiki

### Step 4: Start Infrastructure Services (SLA: 10 min)

```bash
docker compose up -d
docker compose ps
```

- [ ] PostgreSQL container running and healthy
- [ ] Redis container running and healthy
- [ ] Mosquitto container running and healthy

> **IF** containers fail to start **THEN** check Docker daemon is running; check port conflicts with `docker compose logs`

### Step 5: Run Database Migrations and Seed Data (SLA: 10 min)

```bash
npm run db:migrate
npm run db:seed
```

- [ ] All migrations applied successfully
- [ ] Seed data loaded without errors

> **IF** migration fails **THEN** verify PostgreSQL container is healthy; check `DATABASE_URL` in `.env`

### Step 6: Start Development Server and Verify (SLA: 20 min)

```bash
npm run dev
```

Then in a separate terminal:

```bash
curl http://localhost:3000/api/v1/health
npm test
```

- [ ] Application starts without errors
- [ ] Application available at `http://localhost:3000`
- [ ] Health check returns 200 OK
- [ ] All tests pass

> **IF** health check fails **THEN** check application logs for startup errors
> **ELSE IF** tests fail **THEN** verify seed data loaded; verify `.env` matches `.env.example` structure

### Step 7: Configure IDE Extensions (SLA: 10 min)

| Extension | Purpose |
|-----------|---------|
| ESLint | Linting |
| Prettier | Code formatting |
| TypeScript Importer | Auto-imports |
| GitLens | Git history and blame |
| REST Client | API testing |

- [ ] All extensions installed and active
- [ ] ESLint showing inline warnings/errors
- [ ] Prettier formatting on save enabled

### Step 8: Set Up Git Hooks (SLA: 5 min)

```bash
npm run prepare
```

- [ ] Pre-commit hook active (runs linter on staged files)
- [ ] Pre-push hook active (runs unit tests)

---

## EXIT CRITERIA

- [ ] Repository cloned and dependencies installed
- [ ] Environment variables configured
- [ ] Docker infrastructure services running
- [ ] Database migrated and seeded
- [ ] Development server starts and health check passes
- [ ] Full test suite passes
- [ ] IDE configured with required extensions
- [ ] Git hooks installed

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Local `.env` file | `.env.example` in repository | Local workstation (never committed) |
| Running Docker services | `docker-compose.yml` in repository | Local workstation |

---

## Development Tools Reference

Condensed from REF-P5-003. Use this table to identify each tool in the stack, its purpose, and whether it is required or optional.

### Core Stack and Development Tools

| Tool | Purpose | Required / Optional |
|------|---------|---------------------|
| Node.js 20 LTS | Application runtime | Required |
| TypeScript 5.x | Type-safe JavaScript | Required |
| Express 4.x | HTTP framework | Required |
| PostgreSQL 15+ | Primary database | Required |
| Redis 7+ | Caching, session store | Required |
| Mosquitto 2.x | MQTT broker (IoT telemetry) | Required |
| npm 10+ | Package management | Required |
| ESLint | Code linting (`.eslintrc.js`) | Required |
| Prettier | Code formatting (`.prettierrc`) | Required |
| Jest | Unit testing (`jest.config.ts`) | Required |
| Husky | Git hooks (`.husky/`) | Required |
| lint-staged | Lint staged files on commit | Required |
| ts-node | TypeScript execution | Required |
| nodemon | Auto-restart on file changes | Required |
| Docker | Containerization (`Dockerfile`) | Required |
| Docker Compose | Local service orchestration (`docker-compose.yml`) | Required |
| GitHub Actions | CI/CD pipeline (`.github/workflows/`) | Required |

### Optional / Supplementary Tools

| Tool | Purpose | Required / Optional |
|------|---------|---------------------|
| pgAdmin | Visual database exploration | Optional |
| Postman | GUI-based API testing with collections | Optional |
| Docker VS Code extension | Docker file support in editor | Optional |
| PostgreSQL VS Code extension | In-editor database explorer | Optional |
| Error Lens VS Code extension | Inline error display | Optional |

### Key npm Scripts

| Script | Purpose |
|--------|---------|
| `npm run dev` | Start dev server with hot reload |
| `npm test` | Run unit test suite |
| `npm run test:watch` | TDD workflow (watch mode) |
| `npm run test:coverage` | Tests with coverage report |
| `npm run lint` / `lint:fix` | Check / auto-fix lint errors |
| `npm run format` | Format all files with Prettier |
| `npm run db:migrate` | Apply database schema changes |
| `npm run db:seed` | Populate development test data |
| `npm run build` | Compile TypeScript for deployment |
| `npm run prepare` | Set up Husky git hooks |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Coding and Git Standards | Standard | [../standards/coding-and-git.md](../standards/coding-and-git.md) |
| Code Review Standard | Standard | [../standards/code-review.md](../standards/code-review.md) |
| Build and Verify Phase | Phase | [../phases/3-build-and-verify.md](../phases/3-build-and-verify.md) |
| Pull Request Template | Template | [../templates/pull-request.md](../templates/pull-request.md) |
| Code Review Checklist | Template | [../templates/code-review-checklist.md](../templates/code-review-checklist.md) |
| Implement Feature | Runbook | [../runbooks/implement-feature.md](../runbooks/implement-feature.md) |
