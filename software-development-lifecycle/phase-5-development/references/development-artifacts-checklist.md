# Development Artifacts Checklist

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P5-001 |
| **Use When** | Verifying artifact completeness before ticket transition, sprint review, or release |
| **Last Updated** | 2026-03-04 |

---

## REQUIRED ARTIFACTS — PER FEATURE / TICKET

| # | Artifact | Description | Produced By | Reviewed By |
|---|----------|-------------|-------------|-------------|
| 1 | Feature branch | Branch following naming convention `feature/TICKET-NNN-description` | Developer | -- |
| 2 | Unit tests | Tests written before implementation (TDD), covering business logic at 80%+ | Developer | Code Reviewer |
| 3 | Implementation code | Source code matching the approved DDD | Developer | Code Reviewer |
| 4 | Conventional commit(s) | Commit messages following `type(scope): description` format | Developer | Code Reviewer |
| 5 | Pull request | PR with description, test plan, and linked ticket | Developer | Code Reviewer |
| 6 | Code review record | Review comments, feedback, and approval on the PR | Code Reviewer | -- |

## REQUIRED ARTIFACTS — PER SPRINT

| # | Artifact | Description | Produced By | Reviewed By |
|---|----------|-------------|-------------|-------------|
| 7 | Updated Technical Debt Register | New debt items identified, resolved items closed | Developer / Tech Lead | Tech Lead |
| 8 | Sprint demo | Working software demonstrated to stakeholders | Development Team | Product Owner |

## REQUIRED ARTIFACTS — PER RELEASE

| # | Artifact | Description | Produced By | Reviewed By |
|---|----------|-------------|-------------|-------------|
| 9 | Release branch | Branch `release/X.Y.Z` with version bumps and final fixes | Tech Lead | -- |
| 10 | Release tag | Git tag on `main` with semantic version | Tech Lead | -- |
| 11 | Changelog | Summary of changes in the release | Tech Lead | Product Owner |

---

## ARTIFACT QUALITY CRITERIA

| Artifact | Quality Check |
|----------|--------------|
| Unit tests | Coverage meets threshold. Tests are meaningful (not just asserting `true`). AAA structure. |
| Implementation | Matches DDD. Passes linter. No hardcoded config. No secrets. No debug code. |
| Commits | Follow conventional format. Reference ticket numbers. Descriptive messages. |
| Pull request | Description explains what, why, and how. Test plan included. Under 400 lines. |
| Code review | All comments have severity prefix. Blocking issues explained with alternatives. |
| Tech debt register | Impact and effort scored. Priority calculated. Status current. |

---

## VERIFICATION CHECKLIST — TICKET TRANSITION (DEV → TEST)

- [ ] Feature branch merged to `develop`
- [ ] CI pipeline passes on `develop`
- [ ] Unit tests included and passing
- [ ] Coverage meets required thresholds
- [ ] PR approved by at least one reviewer
- [ ] All blocking review comments resolved
- [ ] Conventional commit message references ticket
- [ ] No linter warnings
- [ ] Technical debt items (if any) recorded in register

---

## DECISION TREE

### Which artifacts are missing?

```
START
  │
  ├─ IF moving ticket from Dev → Test
  │    THEN verify all Per Feature artifacts (#1–#6)
  │    AND run Verification Checklist above
  │
  ├─ IF end of sprint
  │    THEN verify Per Sprint artifacts (#7–#8)
  │    IF new tech debt was introduced
  │      THEN verify Technical Debt Register updated
  │    IF no sprint demo prepared
  │      THEN STOP — demo is mandatory
  │
  └─ IF preparing a release
       THEN verify Per Release artifacts (#9–#11)
       AND verify ALL open tickets have Per Feature artifacts complete
       IF changelog not generated
         THEN STOP — changelog required before tagging
```

### Quality gate failed — what to check?

```
START
  │
  ├─ IF unit test coverage < 80%
  │    THEN add missing tests before proceeding
  │
  ├─ IF linter warnings present
  │    THEN run `npm run lint:fix` and review remaining issues
  │
  ├─ IF PR exceeds 400 lines
  │    THEN split into smaller PRs by logical boundary
  │
  ├─ IF commit messages do not follow conventional format
  │    THEN amend commits using interactive rebase
  │    SEE REF-P5-002 (Conventional Commits Reference)
  │
  └─ IF blocking review comments unresolved
       THEN address each comment or discuss with reviewer
       DO NOT merge until all blocking comments resolved
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Implement Feature | Runbook | `../runbooks/implement-feature.md` |
| Conduct Code Review | Runbook | `../runbooks/conduct-code-review.md` |
| Manage Technical Debt | Runbook | `../runbooks/manage-technical-debt.md` |
| Conventional Commits Reference | Reference | `./conventional-commits-reference.md` |
| Pull Request Template | Template | `../templates/pull-request-template.md` |
| Code Review Checklist | Template | `../templates/code-review-checklist.md` |
| Technical Debt Register | Template | `../templates/technical-debt-register.md` |
| Coding Standards | Standard | `../standards/coding-standards.md` |
| Git Workflow Standard | Standard | `../standards/git-workflow-standard.md` |
| Code Review Standard | Standard | `../standards/code-review-standard.md` |
| Unit Testing Standard | Standard | `../standards/unit-testing-standard.md` |
