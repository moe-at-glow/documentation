> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Test Plan -- Power Atlas

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P6-001 |
| **When to Use** | Creating sprint or release test plans |
| **Owner** | QA Lead |
| **Reviewer** | Tech Lead / Product Owner |
| **SLA** | 2 business days |
| **Runbook** | [Execute Test Cycle](../../phase-6-testing/runbooks/execute-test-cycle.md) |
| **Last Verified** | 2026-03-05 |

---

## Test Plan Information

| Field | Value |
|-------|-------|
| Test Plan ID | TP-001 |
| Project | Power Atlas -- GlowPowerRental |
| Sprint / Release | Release 1.0.0 |
| Author | Nadia Al-Rashid (QA Lead) |
| Date Created | 2026-02-08 |
| Approved By | Nadia Al-Rashid (QA Lead), Omar Khalil (Tech Lead) |
| Status | Completed |

---

## 1. Scope

### In Scope

| Module | Feature | Test Level |
|--------|---------|-----------|
| Auth | User registration, login, password reset, JWT management, session timeout, account lockout | Unit / Integration / System |
| Projects | Create, read, update, delete projects; status transitions (draft / active / archived); project sharing | Unit / Integration / System |
| Loads | Add, edit, remove electrical loads within a project; load categorisation (lighting, HVAC, tools, other) | Unit / Integration / System |
| Calculations | Single-phase kW, three-phase kW, kVA conversion; total aggregation per project; diversity factor application | Unit / Integration / System |
| Requirements | Client requirement submission via public form; requirement code generation (PR{DDMMYYYY}-{seq}); admin review, approve/reject workflow; client notification | Unit / Integration / System |
| Layout Builder | Drag-and-drop generator placement; auto-sizing suggestion; cable run calculation; PDF report generation | Unit / Integration / System |

### Out of Scope

| Item | Reason |
|------|--------|
| Payment and billing integration | Deferred to Release 2.0 -- third-party gateway contract not finalised |
| Native mobile application testing | Mobile apps scheduled for Release 1.2; current scope is responsive web only |
| Load balancer and CDN configuration | Infrastructure responsibility handled separately by DevOps team |
| Third-party SMS gateway end-to-end testing | Mocked in test environment; production verification handled in deployment checklist |

---

## 2. Test Approach

### Test Levels

| Level | Scope | Tools | Responsible |
|-------|-------|-------|-------------|
| Unit | Individual functions and methods: calculation formulas, input validators, JWT token generation, requirement code formatter, PDF content builder | Jest (JavaScript), pytest (Python calculation engine) | Developer |
| Integration | API endpoint contracts across all 6 modules; database read/write round-trips; inter-service calls between Node.js API and Python calculation engine | Supertest (Node.js), pytest (Python) | Developer / QA Engineer |
| System | End-to-end user journeys through the browser: project lifecycle, requirement workflow, PDF generation and download, cross-browser rendering | Playwright | QA Engineer |
| Performance | API response time under load; concurrent user simulation; database query performance under volume | k6 | QA Engineer |
| UAT | Business acceptance of key workflows by Product Owner and field engineers | Manual execution in staging | Product Owner / Field Engineers |

### Test Types

- [x] Functional testing
- [x] Regression testing
- [x] Performance testing
- [x] Security testing
- [x] Smoke testing
- [x] Exploratory testing

### Test Data Strategy

| Data Set | Description | Used For |
|----------|-------------|----------|
| Minimal | 2 users, 3 projects, 10 loads, 1 client requirement | Unit and integration tests |
| Standard | 10 users, 20 projects, 150 loads across single/three-phase, 15 client requirements | System and regression tests |
| Performance | 100 users, 500 projects, 5,000 loads, 200 client requirements | k6 load tests |

---

## 3. Test Environment

| Component | Version / Configuration |
|-----------|------------------------|
| Application | `release/1.0.0` branch |
| Node.js | 20.11 LTS |
| Python | 3.12 |
| Database | SQLite 3.45 (test environment) |
| Server | localhost:8000 |
| Browser matrix | Chromium 122, Firefox 123, WebKit (Safari) via Playwright |
| OS | Ubuntu 22.04 (CI), macOS 14 (local QA) |
| Test Data Set | Standard (see above) |

### Environment Setup Steps

1. Clone repository and checkout `release/1.0.0` branch.
2. Run `npm install` in the `/api` directory to install Node.js dependencies.
3. Run `pip install -r requirements.txt` in the `/calc-engine` directory for the Python calculation engine.
4. Copy `.env.test.example` to `.env.test` and verify `DATABASE_URL=sqlite:///test.db`, `JWT_SECRET=test-secret-key`, `PORT=8000`.
5. Run `npm run db:migrate:test` to create the test SQLite database and apply all migrations.
6. Run `npm run db:seed:test` to load the standard test data set.
7. Run `npm run test:smoke` to verify the environment is healthy (hits `/api/health` and checks database connectivity).

---

## 4. Test Cases

### Critical Priority

| ID | Title | Requirement | Type | Status |
|----|-------|------------|------|--------|
| TC-001 | Single-phase power calculation accuracy | SWR-CALC-001 | Functional | Pass |
| TC-002 | Three-phase power calculation accuracy | SWR-CALC-002 | Functional | Pass |
| TC-003 | kW to kVA conversion accuracy | SWR-CALC-003 | Functional | Pass |
| TC-005 | User login with valid credentials | SWR-AUTH-001 | Functional | Pass |
| TC-006 | Account lockout after 5 failed attempts | SWR-AUTH-004 | Security | Pass |
| TC-015 | End-to-end: Create project, add loads, calculate, generate PDF | SWR-PROJ-001, SWR-LOAD-001, SWR-CALC-001, SWR-PDF-001 | System | Pass |

### High Priority

| ID | Title | Requirement | Type | Status |
|----|-------|------------|------|--------|
| TC-004 | Zero and negative input validation for calculations | SWR-CALC-004 | Functional | Pass |
| TC-007 | Create project with all fields | SWR-PROJ-001 | Functional | Pass |
| TC-008 | Add load to project and verify total recalculation | SWR-LOAD-001, SWR-CALC-005 | Functional | Pass |
| TC-009 | Submit client requirement via public form | SWR-REQ-001 | Functional | Pass |
| TC-010 | Admin approve requirement and verify notification | SWR-REQ-003 | Functional | Pass |
| TC-011 | Generate PDF report for project with 10 loads | SWR-PDF-001 | Functional | Fail |
| TC-013 | Session timeout after 1 hour inactivity | SWR-AUTH-005 | Security | Pass |

### Medium Priority

| ID | Title | Requirement | Type | Status |
|----|-------|------------|------|--------|
| TC-012 | Project sharing between users | SWR-PROJ-004 | Functional | Pass |
| TC-014 | Concurrent project edits (optimistic locking) | SWR-PROJ-005 | Functional | Blocked |

### Low Priority

| ID | Title | Requirement | Type | Status |
|----|-------|------------|------|--------|
| TC-016 | Tooltip rendering on mobile viewport | SWR-UI-012 | Functional | Fail |
| TC-017 | Load list pagination with 100+ items | SWR-LOAD-006 | Functional | Pass |

---

## 5. Entry Criteria

- [x] Code merged to `release/1.0.0` branch
- [x] CI pipeline passes (unit + integration tests green)
- [x] Test environment deployed at localhost:8000 and health check passes
- [x] Standard test data set loaded and verified
- [x] Test plan approved by QA Lead and Tech Lead

---

## 6. Exit Criteria

- [x] All critical and high priority test cases executed
- [x] All critical and high severity defects resolved and verified
- [x] Regression test suite passes with zero critical/high failures
- [x] Unit test code coverage meets thresholds: >= 80% overall, >= 90% calculation engine
- [x] Test summary report written and approved
- [ ] UAT sign-off obtained from Product Owner (conditional approval received)

---

## 7. Risks and Mitigations

| Risk | Impact | Likelihood | Mitigation |
|------|--------|-----------|-----------|
| Python calculation engine integration instability | High -- incorrect power values propagate to PDF reports | Medium | Run calculation engine integration tests on every PR; pin Python dependency versions |
| SQLite limitations mask concurrency defects that appear in production PostgreSQL | High -- optimistic locking may behave differently | Medium | Run a parallel concurrency test suite against a PostgreSQL staging instance before release |
| Arabic and RTL text rendering issues in PDF output | Medium -- affects Saudi-market clients | High | Dedicated PDF rendering tests with Arabic load names; engage Arabic-speaking field engineer in UAT |
| Limited QA staffing (2 people) may cause schedule slip | Medium -- delays release by up to 1 week | Medium | Prioritise critical path tests first; developer assists with automated test creation |
| Test data does not represent production scale | Medium -- performance issues missed | Low | Use the performance data set (5,000 loads) for k6 tests; compare against production query patterns |

---

## 8. Schedule

| Activity | Start Date | End Date | Responsible |
|----------|-----------|---------|-------------|
| **Week 1: Unit + Integration** | | | |
| Test plan review and approval | 2026-02-08 | 2026-02-09 | Nadia Al-Rashid (QA Lead) |
| Test environment setup | 2026-02-08 | 2026-02-09 | Tariq Mansour (DevOps) |
| Unit test execution and gap coverage | 2026-02-10 | 2026-02-12 | Ahmad Nasser (QA Engineer) + Omar Khalil (Dev) |
| Integration test execution | 2026-02-11 | 2026-02-14 | Ahmad Nasser (QA Engineer) |
| **Week 2: System + Performance** | | | |
| System test execution (Playwright) | 2026-02-15 | 2026-02-19 | Ahmad Nasser (QA Engineer) |
| Performance test execution (k6) | 2026-02-17 | 2026-02-19 | Nadia Al-Rashid (QA Lead) |
| Security test execution | 2026-02-18 | 2026-02-19 | Ahmad Nasser (QA Engineer) |
| Defect triage and fixing | 2026-02-15 | 2026-02-21 | Omar Khalil (Dev) |
| **Week 3: Regression + UAT** | | | |
| Regression test execution | 2026-02-22 | 2026-02-23 | Ahmad Nasser (QA Engineer) |
| Re-test fixed defects | 2026-02-22 | 2026-02-24 | Ahmad Nasser (QA Engineer) |
| UAT execution | 2026-02-24 | 2026-02-26 | Fatima Hassan (PO) + Field Engineers |
| Test summary report | 2026-02-26 | 2026-02-27 | Nadia Al-Rashid (QA Lead) |
| UAT sign-off | 2026-02-27 | 2026-02-28 | Fatima Hassan (PO) |

### Resources

| Role | Name | Allocation |
|------|------|-----------|
| QA Lead | Nadia Al-Rashid | 100% for 3 weeks |
| QA Engineer | Ahmad Nasser | 100% for 3 weeks |
| Developer (test support) | Omar Khalil | 50% for 3 weeks (defect fixing, test data, environment support) |
| Product Owner (UAT) | Fatima Hassan | 50% for Week 3 |
| Field Engineers (UAT) | Khalid Barakat, Yusuf Darwish, Layla Omari | 2 days in Week 3 |

---

## 9. Approvals

| Role | Name | Date | Signature |
|------|------|------|-----------|
| QA Lead | Nadia Al-Rashid | 2026-02-09 | N. Al-Rashid |
| Tech Lead | Omar Khalil | 2026-02-09 | O. Khalil |

---

## Completion Checklist

- [x] Test Plan Information filled in completely
- [x] Scope defined (in-scope and out-of-scope)
- [x] Test approach and test types selected
- [x] Test environment documented
- [x] Test cases listed with priorities assigned
- [x] Entry criteria defined and verifiable
- [x] Exit criteria defined and measurable
- [x] Risks identified with mitigations
- [x] Schedule populated with dates and owners
- [x] Approvals obtained from all required roles

---

## Cross-References

| Type | Document | Link |
|------|----------|------|
| Runbook | Execute Test Cycle | [../../phase-6-testing/runbooks/execute-test-cycle.md](../../phase-6-testing/runbooks/execute-test-cycle.md) |
| Template | Test Plan Template | [../../phase-6-testing/templates/test-plan-template.md](../../phase-6-testing/templates/test-plan-template.md) |
| Artifact | Test Cases | [test-cases.md](test-cases.md) |
| Artifact | Defect Reports | [defect-reports.md](defect-reports.md) |
| Artifact | Test Summary Report | [test-summary-report.md](test-summary-report.md) |
| Artifact | UAT Sign-Off | [uat-sign-off.md](uat-sign-off.md) |
