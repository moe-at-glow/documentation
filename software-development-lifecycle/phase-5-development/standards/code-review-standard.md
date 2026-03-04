# Code Review Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P5-003 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead |
| **Verification Method** | PR Approval Gates / Process Audit |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** 1 approval required; Tech Lead reviews architecture/security changes only
> **IF** medium project (3-5 devs) **THEN** Standard requirements; 1 approval for develop, 2 for main
> **IF** large project (6+ devs) **THEN** Full compliance required; domain-specific reviewers assigned

---

## COMPLIANCE REQUIREMENTS

### CR-1: Review Process Rules

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | No code merges to develop or main without at least one approval | All PRs | [ ] Branch protection enforced | Revert unauthorized merge |
| 2 | Reviews completed within 1 business day of request | All PRs | [ ] SLA monitoring | Escalate to Tech Lead |
| 3 | PRs kept under 400 lines of change; split larger changes | All PRs | [ ] PR size check in CI | Reject PR; require split |
| 4 | Author must self-review own diff before requesting review | All PRs | [ ] PR checklist completion | Reject review request |

### CR-2: Reviewer Selection

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Architecture-impacting changes (new component, new dependency, schema change): Tech Lead (required) + Senior Developer | Architecture PRs | [ ] Reviewer assignment check | Block merge |
| 2 | Standard feature or bug fix: any peer developer | Standard PRs | [ ] At least 1 reviewer assigned | Block merge |
| 3 | Documentation only: any team member | Docs PRs | [ ] At least 1 reviewer assigned | Block merge |
| 4 | Security-related (auth, input validation, crypto): Tech Lead required | Security PRs | [ ] Reviewer assignment check | Block merge; security escalation |

### CR-3: Review Scope

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Correctness: code does what design specifies; edge cases handled | All PRs | [ ] Reviewer confirms in approval | Request change |
| 2 | Design adherence: matches approved DDD and API spec | All PRs | [ ] Reviewer confirms in approval | Reject PR |
| 3 | Security: OWASP Top 10, SQL injection, XSS, hardcoded secrets, auth checks | All PRs | [ ] Security items in checklist | Reject PR; security escalation |
| 4 | Performance: no N+1 queries, pagination present, no unnecessary computation, indexes exist | All PRs | [ ] Reviewer confirms in approval | Request change |
| 5 | Testability: unit tests present, test behavior not implementation, adequate coverage | All PRs | [ ] Coverage gate in CI | Reject PR |
| 6 | Readability: clear naming, reasonable function length, comments where needed | All PRs | [ ] Reviewer confirms in approval | Request change |
| 7 | Maintainability: DRY, SOLID, comprehensible to new developers | All PRs | [ ] Reviewer confirms in approval | Request change |
| 8 | Standards compliance: coding standards, conventional commits, proper error handling | All PRs | [ ] Reviewer confirms in approval | Reject PR |

### CR-4: Feedback Format

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Blocking feedback prefixed with `[blocking]` | Must-fix items | [ ] Reviewer uses prefix | Request correction |
| 2 | Suggestions prefixed with `[suggestion]` | Optional improvements | [ ] Reviewer uses prefix | Request correction |
| 3 | Nitpicks prefixed with `[nit]` | Trivial items | [ ] Reviewer uses prefix | Request correction |

### CR-5: Author Response to Feedback

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | `[blocking]`: must fix before merge; explain fix in reply | All blocking feedback | [ ] Blocking comments resolved | Block merge |
| 2 | `[suggestion]`: implement or explain why not; both acceptable | All suggestions | [ ] Author responded | Request response |
| 3 | `[nit]`: fix if easy; ignore if trivial and time-constrained | All nits | [ ] No action required | N/A |
| 4 | Questions: reply with explanation | All questions | [ ] Author responded | Request response |

### CR-6: Re-Review Triggers

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Re-review required when blocking feedback addressed | PRs with blocking feedback | [ ] Re-review requested | Block merge |
| 2 | Re-review required when significant code changes made after initial review | PRs with post-review changes | [ ] Re-review requested | Block merge |
| 3 | Re-review required when new files added after review | PRs with new files | [ ] Re-review requested | Block merge |
| 4 | Re-review NOT required for: typo fixes, formatting, non-blocking suggestions, minor renames | Minor changes | [ ] N/A | N/A |

---

## COMPLIANCE CHECKLIST

- [ ] PR has at least one approval before merge
- [ ] Review completed within 1 business day SLA
- [ ] PR is under 400 lines of change (or split into multiple PRs)
- [ ] Author self-reviewed diff before requesting review
- [ ] Correct reviewer assigned based on change type (Tech Lead for architecture/security)
- [ ] Reviewer checked: correctness, design adherence, security, performance, testability, readability, maintainability, standards compliance
- [ ] Feedback uses correct prefixes: `[blocking]`, `[suggestion]`, `[nit]`
- [ ] All `[blocking]` feedback resolved before merge
- [ ] All `[suggestion]` feedback responded to
- [ ] Re-review requested after addressing blocking feedback or significant changes
- [ ] Code Review Checklist template completed

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
