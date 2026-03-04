# Common Development Pitfalls -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P5-003 |
| **Use When** | Before pushing code or during self-review |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] Read the DDD, ticket description, API spec, and data model before writing code
- [ ] Tests written before implementation (TDD: Red-Green-Refactor)
- [ ] PR is under 400 lines of diff (one ticket = one PR)
- [ ] Full test suite passes (`npm test`), not just changed files
- [ ] Linter passes with no warnings (`npm run lint`)
- [ ] No hardcoded configuration -- URLs, keys, constants use config/env vars
- [ ] No empty catch blocks -- errors logged with context, handled or rethrown
- [ ] No N+1 queries -- loops with DB calls use JOINs or batch loading
- [ ] No force-push during active review -- push new commits, squash on merge
- [ ] CI pipeline verified on `develop` after merge

---

## SELECTION CRITERIA / DECISION TABLE

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| Design doc is missing or unclear | Stop, ask Tech Lead or design author | Coding based on ticket title alone |
| Cannot write a test first | Requirement is unclear -- clarify before coding | Writing code then retrofitting tests |
| PR exceeds 400 lines | Split by layer: data model, service, API, integration | Submitting as single large PR |
| Full test suite is slow (> 30s) | Log as tech debt item; still run before push | Skipping full suite |
| Lint rule seems wrong for a case | Discuss with Tech Lead before disabling | Silently disabling or ignoring |
| Value differs between environments | Move to environment variable or config | Hardcoding in source |
| Error caught in try-catch | Log with context (what, with what data), handle or rethrow | Empty catch block |
| Loop contains a database call | Use JOINs or batch loading | Individual queries per iteration |
| Reviewer is mid-review | Push new commits to address feedback | Rebase + force-push |
| PR just merged to `develop` | Verify CI passes; fix immediately if broken | Moving on without checking |

---

## QUICK-REFERENCE TABLE

| Pitfall | One-Line Fix |
|---------|-------------|
| Coding without design | Read the DDD before writing any code |
| Tests after code | Write the failing test first (TDD) |
| Large PRs | One ticket, one PR, under 400 lines |
| Skipping full test suite | Run `npm test` before every push |
| Ignoring linter | Run `npm run lint` and fix all warnings |
| Hardcoded config | Use environment variables and config |
| Swallowing errors | Log with context, then handle or rethrow |
| N+1 queries | Use JOINs or batch loading |
| Force-push in review | Push new commits, squash on merge |
| Not verifying after merge | Check CI on `develop` after every merge |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| For background | Training | [training/development-phase-overview.md](training/development-phase-overview.md) |
| Coding Standards | Standard | [../standards/coding-standards.md](../standards/coding-standards.md) |
