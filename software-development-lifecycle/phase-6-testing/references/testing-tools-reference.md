# Testing Tools Reference

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P6-004 |
| **Use When** | Selecting tools for a test level, running tests, or configuring CI pipelines |
| **Last Updated** | 2026-03-04 |

---

## Test Frameworks

| Tool | Purpose | Test Level | Documentation |
|------|---------|-----------|---------------|
| Jest | Test runner and assertion library | Unit, Integration | https://jestjs.io/docs/ |
| Supertest | HTTP assertion library for Express apps | Integration | https://github.com/ladjs/supertest |
| ts-jest | TypeScript preprocessor for Jest | Unit, Integration | https://kulshekhar.github.io/ts-jest/ |

---

## Unit Testing Tools

| Tool | Purpose | Usage |
|------|---------|-------|
| Jest | Test runner, assertions, mocking | `npm test` |
| jest.fn() | Mock functions | `const mock = jest.fn().mockReturnValue(42)` |
| jest.spyOn() | Spy on existing methods | `jest.spyOn(service, 'calculate')` |
| jest.useFakeTimers() | Mock system clock | Time-dependent tests |

### Commands

```bash
npm test                          # Run all unit tests
npm run test:watch                # Watch mode
npm run test:coverage             # With coverage report
npx jest <file-path>              # Specific test file
npx jest --testPathPattern="<p>"  # Tests matching path pattern
npx jest -t "<name>"              # Tests matching name pattern
```

---

## Integration Testing Tools

| Tool | Purpose | Usage |
|------|---------|-------|
| Supertest | HTTP requests to Express app | `request(app).get('/api/v1/rentals')` |
| Docker Compose | Spin up test database | `docker compose -f docker-compose.test.yml up` |
| pg (node-postgres) | Direct database access for seeds/assertions | `db.query('SELECT * FROM ...')` |

### Commands

```bash
docker compose -f docker-compose.test.yml up -d                                    # Start test DB
DATABASE_URL=postgresql://test:test@localhost:5433/glowpower_test npm run db:migrate # Migrate
npm run test:integration                                                            # Run tests
docker compose -f docker-compose.test.yml down                                      # Stop test DB
```

---

## System / E2E Testing Tools

| Tool | Purpose | Usage |
|------|---------|-------|
| Node fetch / axios | HTTP client for API calls | System test scripts |
| Custom test runner | Orchestrates multi-step scenarios | `npm run test:system` |

### Commands

```bash
STAGING_URL=https://staging.glowpower.sa npm run test:system  # Against staging
STAGING_URL=http://localhost:3000 npm run test:system          # Against local
```

---

## Performance Testing Tools

| Tool | Purpose | Documentation |
|------|---------|---------------|
| k6 | Load testing (scriptable, CLI-based) | https://k6.io/docs/ |
| Artillery | Load testing (YAML config, easy setup) | https://artillery.io/docs/ |

### k6 Example

```javascript
// tests/performance/rental-load.js
import http from 'k6/http';
import { check, sleep } from 'k6';

export const options = {
  stages: [
    { duration: '2m', target: 50 },
    { duration: '5m', target: 100 },
    { duration: '2m', target: 0 },
  ],
  thresholds: {
    http_req_duration: ['p(95)<200'],
    http_req_failed: ['rate<0.01'],
  },
};

export default function () {
  const res = http.get('https://staging.glowpower.sa/api/v1/rentals', {
    headers: { Authorization: `Bearer ${__ENV.TOKEN}` },
  });
  check(res, {
    'status is 200': (r) => r.status === 200,
    'response time < 500ms': (r) => r.timings.duration < 500,
  });
  sleep(1);
}
```

```bash
k6 run tests/performance/rental-load.js
```

---

## Security Testing Tools

| Tool | Purpose | Usage |
|------|---------|-------|
| npm audit | Dependency vulnerability scan | `npm audit --production` |
| ESLint security plugin | Static analysis for security patterns | Integrated in `npm run lint` |
| OWASP ZAP (optional) | Dynamic application security testing | Manual or CI integration |

### Commands

```bash
npm audit --production                    # Check for vulnerabilities
npm audit --production --audit-level=high # Critical and high only
npm audit fix                             # Auto-fix where possible
```

---

## Code Coverage Tools

| Tool | Purpose | Usage |
|------|---------|-------|
| Jest --coverage | Line, branch, function coverage | `npm run test:coverage` |
| Istanbul / nyc | Coverage reporting (used by Jest internally) | Configured in jest.config.ts |

### Commands

```bash
npm run test:coverage
# Output locations:
#   Terminal: coverage/lcov-report/index.html
#   LCOV:    coverage/lcov.info (for CI tools)
```

---

## Test Data Tools

| Tool | Purpose | Usage |
|------|---------|-------|
| Factory functions | Generate test objects | `createTestRental({ daysOverdue: 3 })` |
| Seed scripts | Load database test data | `npm run db:seed` |
| Faker.js (optional) | Generate realistic fake data | Names, emails, addresses |

---

## CI Integration

### GitHub Actions Test Workflow

```yaml
# .github/workflows/test.yml
name: Tests
on: [pull_request]

jobs:
  unit-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version: 20 }
      - run: npm ci
      - run: npm test -- --coverage

  integration-tests:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres:15
        env:
          POSTGRES_DB: glowpower_test
          POSTGRES_USER: test
          POSTGRES_PASSWORD: test
        ports: ['5432:5432']
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version: 20 }
      - run: npm ci
      - run: npm run db:migrate
        env:
          DATABASE_URL: postgresql://test:test@localhost:5432/glowpower_test
      - run: npm run test:integration
        env:
          DATABASE_URL: postgresql://test:test@localhost:5432/glowpower_test

  security-audit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version: 20 }
      - run: npm ci
      - run: npm audit --production --audit-level=high
```

---

## DECISION TREE

```
What test level are you working on?
  UNIT -->
    Use Jest + ts-jest
    IF mocking needed --> jest.fn() or jest.spyOn()
    IF time-dependent --> jest.useFakeTimers()

  INTEGRATION -->
    Use Jest + Supertest + Docker Compose (postgres)
    IF testing HTTP endpoints --> Supertest
    IF testing database directly --> pg (node-postgres)

  SYSTEM / E2E -->
    Use custom test runner with fetch/axios
    IF testing against staging --> Set STAGING_URL env var
    IF testing locally --> Run full stack first

  PERFORMANCE -->
    IF scriptable load test needed --> k6
    IF simple YAML config preferred --> Artillery

  SECURITY -->
    IF dependency scan --> npm audit
    IF static analysis --> ESLint security plugin
    IF dynamic scan --> OWASP ZAP
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Execute Test Cycle | Runbook | ../runbooks/execute-test-cycle.md |
| Write Integration Tests | Runbook | ../runbooks/write-integration-tests.md |
| Write System Tests | Runbook | ../runbooks/write-system-tests.md |
| Report and Track Defects | Runbook | ../runbooks/report-and-track-defects.md |
| Perform Regression Testing | Runbook | ../runbooks/perform-regression-testing.md |
