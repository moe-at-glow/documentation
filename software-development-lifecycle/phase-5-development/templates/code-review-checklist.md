# Code Review Checklist

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P5-002 |
| **When to Use** | Reviewing any pull request |
| **Owner** | Developer |
| **Reviewer** | Tech Lead |
| **SLA** | Complete review within 4 hours of assignment |
| **Runbook** | [Conduct Code Review Runbook](../runbooks/conduct-code-review.md) |
| **Last Verified** | 2026-03-04 |

---

## Scaling Decision Gate

| PR Size | Review Approach |
|---------|-----------------|
| **< 100 lines** | Single pass, focus on correctness and tests |
| **100-400 lines** | Full checklist, one reviewer minimum |
| **400-800 lines** | Full checklist, two reviewers, split by area |
| **> 800 lines** | Request PR be split before reviewing |

---

## [ ] PR Information

| Field | Value |
|-------|-------|
| PR Title | <!-- --> |
| Author | <!-- --> |
| Reviewer | <!-- --> |
| Ticket | <!-- TICKET-NNN --> |
| Related DDD | <!-- link or path --> |
| Date Reviewed | <!-- YYYY-MM-DD --> |

---

## [ ] 1. PR Quality

- [ ] PR description explains what, why, and how
- [ ] PR is under 400 lines of diff
- [ ] Commit messages follow conventional commit format
- [ ] PR addresses a single ticket or concern
- [ ] Test plan is documented in the PR description

---

## [ ] 2. Correctness

- [ ] Code does what the DDD specifies
- [ ] All acceptance criteria from the ticket are addressed
- [ ] Edge cases from the design are handled
- [ ] Error scenarios produce appropriate responses
- [ ] No logic errors in calculations or conditions
- [ ] Data types are correct (no implicit conversions that could cause bugs)

---

## [ ] 3. Security

- [ ] Input is validated at system boundaries
- [ ] Database queries use parameterized statements (no SQL concatenation)
- [ ] Authentication is checked on protected endpoints
- [ ] Authorization is checked (user can only access their own data)
- [ ] No secrets, API keys, or passwords in code
- [ ] No sensitive data logged (passwords, tokens, PII)
- [ ] File uploads validated (type, size) if applicable
- [ ] CORS configuration is appropriate if changed

---

## [ ] 4. Performance

- [ ] No N+1 database queries (check loops with DB calls)
- [ ] List endpoints have pagination
- [ ] Database indexes exist for filtered/sorted columns
- [ ] No unnecessary data fetched (SELECT * when only a few fields needed)
- [ ] Expensive operations are not repeated unnecessarily
- [ ] Async operations are properly awaited (no fire-and-forget unless intentional)

---

## [ ] 5. Testing

- [ ] Unit tests are present for new business logic
- [ ] Tests cover the happy path
- [ ] Tests cover error/edge cases
- [ ] Tests are meaningful (not just `expect(true).toBe(true)`)
- [ ] Tests follow AAA pattern (Arrange-Act-Assert)
- [ ] Test names describe the scenario and expected result
- [ ] Coverage meets thresholds (80% business logic, 90% critical paths)
- [ ] No skipped tests (`.skip` or `xit`)
- [ ] Mocks are appropriate (external dependencies, not the unit under test)

---

## [ ] 6. Code Quality

- [ ] Naming is clear and follows conventions (camelCase variables, PascalCase classes)
- [ ] Functions are focused (single responsibility)
- [ ] No dead code (unused variables, unreachable branches, commented-out code)
- [ ] No debug code (console.log, TODO, FIXME without ticket reference)
- [ ] Error handling is present and appropriate (no empty catch blocks)
- [ ] Logging follows the logging standard (structured, with context)
- [ ] Configuration values are externalized (not hardcoded)
- [ ] TypeScript strict mode violations are justified

---

## [ ] 7. Standards Compliance

- [ ] File and folder structure follows project conventions
- [ ] Import ordering follows the standard (node modules, external, internal)
- [ ] Error responses follow the standard error format
- [ ] API endpoints follow REST conventions and API design standard
- [ ] Database changes include a migration file
- [ ] Migration is reversible (has both up and down)

---

## [ ] Review Decision

| Decision | Criteria |
|----------|----------|
| **Approve** | No blocking issues. Code is ready to merge. |
| **Request Changes** | One or more blocking issues that must be fixed. |
| **Comment** | Questions or observations only. Not blocking. |

**Decision:** <!-- Approve / Request Changes / Comment -->

---

## [ ] Feedback Summary

### [ ] Blocking Issues

<!-- List any [blocking] issues here -->

1. <!-- [blocking] description -->

### [ ] Suggestions

<!-- List any [suggestion] or [nit] items here -->

1. <!-- [suggestion] description -->

### [ ] Questions

<!-- List any questions here -->

1. <!-- [question] description -->

### [ ] Positive Observations

<!-- Call out anything well-done -->

1. <!-- description -->

---

## Completion Checklist

- [ ] PR Information table filled in
- [ ] All applicable checklist sections reviewed
- [ ] Non-applicable sections marked N/A with reason
- [ ] Review decision recorded (Approve / Request Changes / Comment)
- [ ] Blocking issues documented with clear descriptions
- [ ] Suggestions and questions captured
- [ ] Feedback submitted in PR tool

---

## Cross-References

| Document | Path | Relationship |
|----------|------|--------------|
| Conduct Code Review Runbook | [../runbooks/conduct-code-review.md](../runbooks/conduct-code-review.md) | Parent runbook |
| Pull Request Template | [pull-request-template.md](pull-request-template.md) | PR being reviewed follows this template |
| Technical Debt Register | [technical-debt-register.md](technical-debt-register.md) | Log debt identified during review |
