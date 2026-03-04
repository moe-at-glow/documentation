# Code Review Best Practices -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P5-001 |
| **Use When** | Preparing or reviewing a pull request |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] Self-reviewed with `git diff develop` -- no debug code, no unrelated changes
- [ ] PR is under 400 lines of diff
- [ ] PR description includes What, Why, How, and Testing sections
- [ ] Every reviewer comment has a response
- [ ] Reviewed tests before reviewing implementation
- [ ] All blocking issues are resolved before approving

---

## SELECTION CRITERIA / DECISION TABLE

### PR Size Decision

| PR Size (Lines Changed) | Recommended Action | Avoid |
|--------------------------|-------------------|-------|
| < 100 | Submit as-is | Over-splitting simple changes |
| 100 - 400 | Submit as-is | Batching unrelated changes |
| 400+ | Split into multiple PRs (data model, service, API, integration) | Submitting as a single PR |

### Comment Response Decision

| Comment Type | Recommended Action | Avoid |
|-------------|-------------------|-------|
| Blocking | Fix it, reply with what changed | Ignoring or deferring |
| Suggestion | Implement or explain why not | Silence |
| Question | Answer it | Leaving unanswered |
| Nit | Fix if easy, otherwise acknowledge | Ignoring without response |

### Approval Decision

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| All blocking issues resolved, code matches design, tests present | Approve | Withholding for nits or style preferences |
| Correctness bug or security vulnerability found | Request changes with explanation | Approving with known defects |
| Style preference already covered by linter | Approve | Blocking on linter-enforced style |
| Non-blocking suggestion author declined | Approve | Withholding approval |

---

## QUICK-REFERENCE TABLE

### Review Layers

| Layer | What to Check |
|-------|--------------|
| **Correctness** | Does it do what the design says? Edge cases handled? |
| **Security** | Input validation? SQL injection? Auth checks? Secrets in code? |
| **Performance** | N+1 queries? Missing pagination? Unnecessary computation? |
| **Readability** | Clear names? Reasonable function length? Understandable by new developer? |
| **Standards** | Follows coding standards? Conventional commits? |

### Comment Severity Prefixes

| Prefix | Meaning |
|--------|---------|
| `[blocking]` | Must fix before merge |
| `[suggestion]` | Would improve code, not required |
| `[nit]` | Minor style or preference |
| `[question]` | Seeking clarification |

### Review Etiquette

| Do | Do Not |
|----|--------|
| Be specific and constructive | Be vague ("this is wrong") |
| Focus on the code, not the person | Make it personal ("you always...") |
| Ask questions when unsure | Assume bad intent |
| Suggest alternatives | Just say "fix this" |
| Respond within 1 business day | Let PRs sit for days |
| Approve when satisfied | Withhold approval for nits |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| For background | Training | [training/development-phase-overview.md](training/development-phase-overview.md) |
| Coding Standards | Standard | [../standards/coding-standards.md](../standards/coding-standards.md) |
| PR Template | Template | [../templates/pull-request-template.md](../templates/pull-request-template.md) |
