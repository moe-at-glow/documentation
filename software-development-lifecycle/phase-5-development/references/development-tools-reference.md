# Development Tools Reference

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P5-003 |
| **Use When** | Setting up development environment, selecting tools for a task, troubleshooting tooling |
| **Last Updated** | 2026-03-04 |

---

## CORE STACK

| Tool | Version | Purpose | Documentation |
|------|---------|---------|---------------|
| Node.js | 20 LTS | Application runtime | https://nodejs.org/docs/latest-v20.x/api/ |
| TypeScript | 5.x | Type-safe JavaScript | https://www.typescriptlang.org/docs/ |
| Express | 4.x | HTTP framework | https://expressjs.com/ |
| PostgreSQL | 15+ | Primary database | https://www.postgresql.org/docs/15/ |
| Redis | 7+ | Caching, session store | https://redis.io/docs/ |
| Mosquitto | 2.x | MQTT broker (IoT telemetry) | https://mosquitto.org/documentation/ |

---

## DEVELOPMENT TOOLS

| Tool | Purpose | Config File |
|------|---------|-------------|
| npm | Package management | `package.json`, `package-lock.json` |
| ESLint | Code linting | `.eslintrc.js` |
| Prettier | Code formatting | `.prettierrc` |
| Jest | Unit testing | `jest.config.ts` |
| Husky | Git hooks | `.husky/` |
| lint-staged | Run linter on staged files | `package.json` (lint-staged section) |
| ts-node | TypeScript execution | `tsconfig.json` |
| nodemon | Auto-restart on changes | `nodemon.json` |

---

## INFRASTRUCTURE TOOLS

| Tool | Purpose | Config File |
|------|---------|-------------|
| Docker | Containerization | `Dockerfile` |
| Docker Compose | Local service orchestration | `docker-compose.yml` |
| GitHub Actions | CI/CD pipeline | `.github/workflows/` |

---

## NPM SCRIPTS

| Script | Command | Purpose |
|--------|---------|---------|
| `npm run dev` | Start development server with hot reload | Day-to-day development |
| `npm run build` | Compile TypeScript to JavaScript | Build for deployment |
| `npm start` | Start compiled application | Production startup |
| `npm test` | Run unit test suite | Verify all tests pass |
| `npm run test:watch` | Run tests in watch mode | TDD workflow |
| `npm run test:coverage` | Run tests with coverage report | Check coverage thresholds |
| `npm run lint` | Run ESLint | Check for code issues |
| `npm run lint:fix` | Run ESLint with auto-fix | Auto-fix lint issues |
| `npm run format` | Run Prettier | Format all files |
| `npm run db:migrate` | Run database migrations | Apply schema changes |
| `npm run db:migrate:undo` | Revert last migration | Roll back schema change |
| `npm run db:seed` | Seed development data | Populate test data |
| `npm run prepare` | Set up Husky git hooks | One-time setup |

---

## VS CODE EXTENSIONS

| Extension | ID | Purpose |
|-----------|----|---------|
| ESLint | `dbaeumer.vscode-eslint` | In-editor linting |
| Prettier | `esbenp.prettier-vscode` | In-editor formatting |
| TypeScript Importer | `pmneo.tsimporter` | Auto-import suggestions |
| GitLens | `eamodio.gitlens` | Git blame, history |
| REST Client | `humao.rest-client` | Test API endpoints from VS Code |
| Docker | `ms-azuretools.vscode-docker` | Docker file support |
| PostgreSQL | `ckolkman.vscode-postgres` | Database explorer |
| Error Lens | `usernamehw.errorlens` | Inline error display |

---

## DATABASE TOOLS

| Tool | Purpose | When to Use |
|------|---------|-------------|
| `psql` | PostgreSQL CLI | Quick queries, debugging |
| pgAdmin | PostgreSQL GUI | Visual database exploration |
| VS Code PostgreSQL extension | In-editor queries | Development workflow |
| `npm run db:migrate` | Schema migrations | Applying schema changes |

---

## API TESTING TOOLS

| Tool | Purpose |
|------|---------|
| VS Code REST Client | Quick API testing from editor |
| curl | Command-line API testing |
| Postman (optional) | GUI-based API testing with collections |

---

## DECISION TREE

### Which tool do I need for this task?

```
START — What are you trying to do?
  │
  ├─ IF writing or modifying application code
  │    THEN use TypeScript + ts-node
  │    AND run `npm run dev` for hot reload
  │    IF you need to debug
  │      THEN run `npm run dev -- --inspect`
  │      AND attach VS Code debugger (port 9229)
  │
  ├─ IF running or writing tests
  │    THEN use Jest
  │    IF doing TDD (write test → watch → implement)
  │      THEN run `npm run test:watch`
  │    IF checking coverage
  │      THEN run `npm run test:coverage`
  │    IF debugging a failing test
  │      THEN use VS Code "Debug Tests" launch config
  │
  ├─ IF fixing code style or formatting issues
  │    IF linter errors
  │      THEN run `npm run lint:fix`
  │    IF formatting issues
  │      THEN run `npm run format`
  │
  ├─ IF working with the database
  │    IF applying schema changes
  │      THEN run `npm run db:migrate`
  │    IF rolling back a migration
  │      THEN run `npm run db:migrate:undo`
  │    IF populating test data
  │      THEN run `npm run db:seed`
  │    IF running ad-hoc queries
  │      THEN use `psql` or VS Code PostgreSQL extension
  │
  ├─ IF testing API endpoints
  │    IF quick one-off test
  │      THEN use curl or VS Code REST Client (.http file)
  │    IF building a test collection
  │      THEN use Postman
  │
  ├─ IF managing containers / local services
  │    THEN use Docker Compose
  │    Run `docker compose up` for all services
  │    Run `docker compose up <service>` for specific service
  │
  └─ IF setting up a new development environment
       THEN follow Setup Development Environment runbook
       AND run `npm run prepare` for git hooks
```

### Which npm script should I run?

```
START — What outcome do you need?
  │
  ├─ IF start coding           → `npm run dev`
  ├─ IF run all tests           → `npm test`
  ├─ IF TDD workflow            → `npm run test:watch`
  ├─ IF check coverage          → `npm run test:coverage`
  ├─ IF check for lint errors   → `npm run lint`
  ├─ IF auto-fix lint errors    → `npm run lint:fix`
  ├─ IF format code             → `npm run format`
  ├─ IF apply DB migrations     → `npm run db:migrate`
  ├─ IF rollback DB migration   → `npm run db:migrate:undo`
  ├─ IF seed test data          → `npm run db:seed`
  ├─ IF build for deployment    → `npm run build`
  ├─ IF start production app    → `npm start`
  └─ IF set up git hooks        → `npm run prepare`
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Setup Development Environment | Runbook | `../runbooks/setup-development-environment.md` |
| Implement Feature | Runbook | `../runbooks/implement-feature.md` |
| Coding Standards | Standard | `../standards/coding-standards.md` |
| Unit Testing Standard | Standard | `../standards/unit-testing-standard.md` |
| Git Workflow Standard | Standard | `../standards/git-workflow-standard.md` |
| Development Artifacts Checklist | Reference | `./development-artifacts-checklist.md` |
| Conventional Commits Reference | Reference | `./conventional-commits-reference.md` |
