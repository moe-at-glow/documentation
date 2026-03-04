# Git Workflow Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P5-002 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead |
| **Verification Method** | CI Pipeline / Branch Protection Rules |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Single approval on PRs; squash merge only; release tagging optional
> **IF** medium project (3-5 devs) **THEN** Standard requirements; 1 approval on develop, 2 on main
> **IF** large project (6+ devs) **THEN** Full compliance required; all branch protections enforced

---

## COMPLIANCE REQUIREMENTS

### CR-1: Branching Strategy

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | `main` branch: production-ready, always deployable | All repos | [ ] Branch protection rules | Revert unauthorized merge |
| 2 | `develop` branch: integration branch for latest development code | All repos | [ ] Branch protection rules | Revert unauthorized merge |
| 3 | `feature/*` branches: created from develop, merge into develop | New features | [ ] PR target branch check | Reject PR |
| 4 | `bugfix/*` branches: created from develop, merge into develop | Non-urgent fixes | [ ] PR target branch check | Reject PR |
| 5 | `hotfix/*` branches: created from main, merge into main + develop | Urgent production fixes | [ ] PR target branch check | Reject PR |
| 6 | `release/*` branches: created from develop, merge into main + develop | Release prep | [ ] PR target branch check | Reject PR |

### CR-2: Branch Naming

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Always include ticket number: `feature/TICKET-123-short-description` | All branches | [ ] CI branch name check | Reject PR |
| 2 | Use lowercase and hyphens only | All branches | [ ] CI branch name check | Reject PR |
| 3 | Description: 3-5 words (`feature/ticket-123-late-fee-calc`) | All branches | [ ] Code review check | Request change |
| 4 | No personal names or dates in branch names | All branches | [ ] Code review check | Request change |

### CR-3: Commit Message Format

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Format: `<type>(<scope>): <description>` | All commits | [ ] Commit lint hook | Reject commit |
| 2 | Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `perf` | All commits | [ ] Commit lint hook | Reject commit |
| 3 | Description: imperative present tense ("add feature" not "added feature") | All commits | [ ] Code review check | Request change |
| 4 | No period at end of description | All commits | [ ] Commit lint hook | Reject commit |
| 5 | First line under 72 characters | All commits | [ ] Commit lint hook | Reject commit |
| 6 | Body explains WHY, not WHAT | All commits with body | [ ] Code review check | Request change |
| 7 | Reference ticket in footer: `Refs: TICKET-123` | All commits | [ ] Code review check | Request change |

### CR-4: Pull Request Requirements

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Title: conventional commit format (`feat(billing): add late fee calculation`) | All PRs | [ ] PR lint check | Reject PR |
| 2 | Description: what changed, why, how; link to ticket | All PRs | [ ] Code review check | Reject PR |
| 3 | Type of change specified (Feature / Bug fix / Refactor / Docs) | All PRs | [ ] PR template check | Reject PR |
| 4 | Related ticket linked | All PRs | [ ] PR template check | Reject PR |
| 5 | Screenshots required for UI changes | UI PRs | [ ] Code review check | Reject PR |
| 6 | Test evidence included | All PRs | [ ] Code review check | Reject PR |
| 7 | PR checklist completed | All PRs | [ ] PR template check | Reject PR |
| 8 | Use Pull Request Template | All PRs | [ ] PR template enforcement | Reject PR |

### CR-5: Merge Strategy

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Squash merge: `feature/*` -> `develop` | Feature merges | [ ] GitHub merge settings | Reject non-squash merge |
| 2 | Merge commit: `release/*` -> `main` | Release merges | [ ] Code review check | Request change |
| 3 | Merge commit: `hotfix/*` -> `main` + `develop` | Hotfix merges | [ ] Code review check | Request change |

### CR-6: Release Tagging (SemVer)

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | MAJOR: breaking API changes, incompatible data migrations | Major releases | [ ] Release review | Block release |
| 2 | MINOR: new features, backward-compatible | Minor releases | [ ] Release review | Block release |
| 3 | PATCH: bug fixes, backward-compatible | Patch releases | [ ] Release review | Block release |
| 4 | Tag format: `vX.Y.Z` (`v1.2.3`) | All tags | [ ] CI tag format check | Reject tag |

### CR-7: Protected Branches

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | `main`: require PR, 2 approvals, CI pass, no force push, no direct commits | main branch | [ ] GitHub branch protection | Enforce via platform |
| 2 | `develop`: require PR, 1 approval, CI pass, no force push | develop branch | [ ] GitHub branch protection | Enforce via platform |

### CR-8: Conflict Resolution

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Pull latest develop into feature branch before merge | All feature PRs | [ ] PR up-to-date check | Block merge |
| 2 | Resolve conflicts locally; run tests after resolution | All conflicts | [ ] CI pass after resolution | Block merge |
| 3 | Consult original author if conflict resolution is unclear | Ambiguous conflicts | [ ] Code review check | Request change |

---

## COMPLIANCE CHECKLIST

- [ ] Branch created from correct source (feature/bugfix from develop; hotfix from main)
- [ ] Branch name includes ticket number, uses lowercase-hyphens, 3-5 word description
- [ ] No personal names or dates in branch name
- [ ] All commits follow conventional commit format: `type(scope): description`
- [ ] Commit types restricted to: feat, fix, docs, refactor, test, chore, perf
- [ ] Commit descriptions: imperative tense, no trailing period, under 72 chars
- [ ] Ticket referenced in commit footer
- [ ] PR uses Pull Request Template
- [ ] PR title in conventional commit format
- [ ] PR description includes: what, why, how, ticket link, type of change
- [ ] Screenshots included for UI changes
- [ ] Test evidence included in PR
- [ ] Correct merge strategy used (squash for features; merge commit for releases/hotfixes)
- [ ] Release tagged with SemVer format `vX.Y.Z`
- [ ] Branch protection rules active on main (2 approvals) and develop (1 approval)
- [ ] Conflicts resolved locally with tests passing post-resolution

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
