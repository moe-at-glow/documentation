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

### Step 1: Clone Repository

| Action | Owner | SLA |
|--------|-------|-----|
| Clone project repository via SSH | Developer | 10 min |

```bash
git clone git@github.com:glowpowerrental/[project-name].git
cd [project-name]
```

- [ ] Repository cloned successfully
- [ ] Working directory set to project root

> **IF** clone fails with permission error **THEN** verify SSH key is added to GitHub account
> **ELSE IF** clone fails with network error **THEN** verify VPN/network connectivity
> **ELSE** proceed to Step 2

### Step 2: Install Dependencies

| Action | Owner | SLA |
|--------|-------|-----|
| Install npm packages | Developer | 10 min |

```bash
npm install
```

- [ ] All dependencies installed without errors

> **IF** npm install fails **THEN** delete `node_modules` and `package-lock.json`, retry `npm install`
> **ELSE** proceed to Step 3

### Step 3: Configure Environment Variables

| Action | Owner | SLA |
|--------|-------|-----|
| Copy example env file | Developer | 5 min |
| Set local values in .env | Developer | 15 min |

```bash
cp .env.example .env
```

- [ ] `.env` file created from `.env.example`
- [ ] All required variables populated with local values
- [ ] `.env` file is in `.gitignore` (never committed)

> **IF** a required variable value is unknown **THEN** consult Tech Lead or check project wiki
> **ELSE** proceed to Step 4

### Step 4: Start Infrastructure Services

| Action | Owner | SLA |
|--------|-------|-----|
| Start Docker Compose services | Developer | 5 min |
| Verify all containers are running | Developer | 5 min |

```bash
docker compose up -d
docker compose ps
```

- [ ] PostgreSQL container running and healthy
- [ ] Redis container running and healthy
- [ ] Mosquitto container running and healthy

> **IF** containers fail to start **THEN** check Docker daemon is running; check port conflicts with `docker compose logs`
> **ELSE** proceed to Step 5

### Step 5: Run Database Migrations

| Action | Owner | SLA |
|--------|-------|-----|
| Execute database migrations | Developer | 5 min |

```bash
npm run db:migrate
```

- [ ] All migrations applied successfully

> **IF** migration fails **THEN** verify PostgreSQL container is healthy; check `DATABASE_URL` in `.env`
> **ELSE** proceed to Step 6

### Step 6: Seed Development Data

| Action | Owner | SLA |
|--------|-------|-----|
| Load seed data into database | Developer | 5 min |

```bash
npm run db:seed
```

- [ ] Seed data loaded without errors

### Step 7: Start Development Server

| Action | Owner | SLA |
|--------|-------|-----|
| Start the application in development mode | Developer | 5 min |

```bash
npm run dev
```

- [ ] Application starts without errors
- [ ] Application available at `http://localhost:3000`

### Step 8: Verify Setup

| Action | Owner | SLA |
|--------|-------|-----|
| Run health check endpoint | Developer | 5 min |
| Run full test suite | Developer | 15 min |

```bash
curl http://localhost:3000/api/v1/health
npm test
```

- [ ] Health check returns 200 OK
- [ ] All tests pass

> **IF** health check fails **THEN** check application logs for startup errors
> **ELSE IF** tests fail **THEN** verify seed data loaded; verify `.env` matches `.env.example` structure
> **ELSE** proceed to Step 9

### Step 9: Configure IDE Extensions

| Action | Owner | SLA |
|--------|-------|-----|
| Install required VS Code extensions | Developer | 10 min |

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

### Step 10: Set Up Git Hooks

| Action | Owner | SLA |
|--------|-------|-----|
| Initialize Husky pre-commit hooks | Developer | 5 min |

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

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Coding Standards | Standard | [../standards/coding-standards.md](../standards/coding-standards.md) |
| Git Workflow Standard | Standard | [../standards/git-workflow-standard.md](../standards/git-workflow-standard.md) |
| Unit Testing Standard | Standard | [../standards/unit-testing-standard.md](../standards/unit-testing-standard.md) |
| Implement Feature | Runbook | [./implement-feature.md](./implement-feature.md) |
