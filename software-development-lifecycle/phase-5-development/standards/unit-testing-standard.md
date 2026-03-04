# Unit Testing Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P5-004 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead |
| **Verification Method** | CI Pipeline / Coverage Reports |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** 60% overall coverage; critical paths 80%; test naming enforced
> **IF** medium project (3-5 devs) **THEN** Standard thresholds; AAA structure enforced; mocking strategy reviewed
> **IF** large project (6+ devs) **THEN** Full compliance required; coverage gates block CI; test data factories mandatory

---

## COMPLIANCE REQUIREMENTS

### CR-1: Coverage Thresholds

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Business logic (services, calculators): 80% line coverage minimum | Service/calculator files | [ ] CI coverage gate | Build failure |
| 2 | Critical paths (payments, fee calculation): 90% line coverage minimum | Payment/fee modules | [ ] CI coverage gate | Build failure |
| 3 | Utilities and helpers: 60% line coverage minimum | Utility files | [ ] CI coverage gate | Build failure |
| 4 | Controllers (HTTP layer): coverage not required (integration tested) | Controller files | [ ] Excluded in coverage config | N/A |
| 5 | Generated code, configuration: excluded from coverage | Generated/config files | [ ] Excluded in coverage config | N/A |

### CR-2: Test Naming

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | `describe` block: name of unit under test (`LateFeeCalculator`) | All test files | [ ] Code review check | Request change |
| 2 | Nested `describe`: method name (`calculateFee`) | All test files | [ ] Code review check | Request change |
| 3 | `it` block format: `should [expected behavior] when [condition]` | All test cases | [ ] Code review check | Request change |

### CR-3: Test Structure (AAA)

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Each test follows Arrange-Act-Assert pattern | All test cases | [ ] Code review check | Request change |
| 2 | Exactly one Act per test | All test cases | [ ] Code review check | Request change |
| 3 | No multiple behaviors tested in a single test | All test cases | [ ] Code review check | Request change |

### CR-4: What to Test

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Business logic and calculations | All services | [ ] Coverage gate | Build failure |
| 2 | Edge cases (zero values, maximum values) | All services | [ ] Code review check | Request change |
| 3 | Error handling (invalid inputs, missing data, external failures) | All services | [ ] Code review check | Request change |
| 4 | Boundary conditions (e.g., 0 days overdue vs 1 day overdue) | All services | [ ] Code review check | Request change |
| 5 | State transitions (valid and invalid) | Stateful entities | [ ] Code review check | Request change |
| 6 | Validation rules (required fields, format, business rules) | All validators | [ ] Code review check | Request change |

### CR-5: What NOT to Test

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Do not unit test framework code (Express routing, ORM internals) | All test files | [ ] Code review check | Request removal |
| 2 | Do not unit test third-party library internals | All test files | [ ] Code review check | Request removal |
| 3 | Do not test trivial getters/setters with no logic | All test files | [ ] Code review check | Request removal |
| 4 | Do not test private methods directly; test via public interface | All test files | [ ] Code review check | Request refactor |
| 5 | Do not test database queries in unit tests; use integration tests | All unit test files | [ ] Code review check | Move to integration suite |

### CR-6: Mocking Strategy

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Mock: external services (payment gateway, email provider) | All unit tests | [ ] Code review check | Request change |
| 2 | Mock: database repositories | All unit tests | [ ] Code review check | Request change |
| 3 | Mock: message brokers | All unit tests | [ ] Code review check | Request change |
| 4 | Mock: HTTP clients for external APIs | All unit tests | [ ] Code review check | Request change |
| 5 | Mock: system clock for time-dependent tests | Time-dependent tests | [ ] Code review check | Request change |
| 6 | Do NOT mock: the unit under test | All unit tests | [ ] Code review check | Reject PR |
| 7 | Do NOT mock: pure business logic | All unit tests | [ ] Code review check | Request change |
| 8 | Do NOT mock: input data and test fixtures | All unit tests | [ ] Code review check | Request change |
| 9 | Do NOT mock: standard library functions | All unit tests | [ ] Code review check | Request change |

### CR-7: Test Data Management

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Use factory/builder functions for test data creation | All test files | [ ] Code review check | Request change |
| 2 | No production data (real names, emails, financial data) in tests | All test files | [ ] Code review check | Reject PR; data escalation |
| 3 | Minimal test data: only fields relevant to the test | All test files | [ ] Code review check | Request change |
| 4 | Each test creates its own data; no shared state between tests | All test files | [ ] Code review check | Reject PR |

### CR-8: Test Isolation

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Tests must not depend on other tests' state or execution order | All test files | [ ] CI randomized test order | Reject PR |
| 2 | Reset mocks between tests (`jest.clearAllMocks` in `beforeEach`) | All test files | [ ] Code review check | Request change |
| 3 | No external dependencies (database, network, file system) in unit tests | All unit test files | [ ] Code review check | Move to integration suite |
| 4 | Individual test under 100ms execution time | All test cases | [ ] CI test timing report | Request optimization |
| 5 | Full unit suite under 30 seconds | All unit tests | [ ] CI pipeline timing | Request optimization |

---

## COMPLIANCE CHECKLIST

- [ ] Business logic coverage >= 80%
- [ ] Critical path coverage >= 90%
- [ ] Utility coverage >= 60%
- [ ] Controllers excluded from coverage requirements
- [ ] Test names follow `should [behavior] when [condition]` format
- [ ] All tests use Arrange-Act-Assert structure
- [ ] One Act per test; one behavior per test
- [ ] Business logic, edge cases, error handling, boundaries, state transitions, and validation tested
- [ ] No tests for framework internals, third-party libs, trivial getters, private methods, or DB queries
- [ ] External services, repositories, brokers, HTTP clients, and clock mocked
- [ ] Unit under test never mocked
- [ ] Test data created via factory functions; no production data
- [ ] Each test creates its own data; no shared state
- [ ] Mocks reset in `beforeEach`
- [ ] No external dependencies in unit tests (DB, network, filesystem)
- [ ] Individual test < 100ms; full suite < 30 seconds

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Implement Feature | Runbook | ../runbooks/implement-feature.md |
| Setup Development Environment | Runbook | ../runbooks/setup-development-environment.md |
| Conduct Code Review | Runbook | ../runbooks/conduct-code-review.md |
| Manage Technical Debt | Runbook | ../runbooks/manage-technical-debt.md |
| Pull Request Template | Template | ../templates/pull-request-template.md |
| Code Review Checklist | Template | ../templates/code-review-checklist.md |
| Technical Debt Register | Template | ../templates/technical-debt-register.md |
