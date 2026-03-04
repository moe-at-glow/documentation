# Git Branching Strategy -- Quick Reference

| Field | Value |
|-------|-------|
| **Reference ID** | QR-P5-002 |
| **Use When** | Creating, naming, or merging a Git branch |
| **Last Updated** | 2026-03-04 |

---

## PRE-FLIGHT CHECK

- [ ] Pulled latest from parent branch before creating new branch
- [ ] Branch name follows convention: `type/TICKET-NNN-short-description`
- [ ] Not committing directly to `main` or `develop`
- [ ] Not rebasing a shared branch
- [ ] Feature branch lifetime is days, not weeks
- [ ] Merged branches are deleted immediately after merge

---

## SELECTION CRITERIA / DECISION TABLE

### Branch Type Selection

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| New functionality | Branch from `develop` as `feature/TICKET-NNN-desc` | Branching from `main` |
| Bug found in development/testing | Branch from `develop` as `bugfix/TICKET-NNN-desc` | Fixing directly on `develop` |
| Critical production bug | Branch from `main` as `hotfix/TICKET-NNN-desc`, merge to both `main` and `develop` | Branching from `develop` for production fixes |
| Preparing a release | Branch from `develop` as `release/X.Y.Z`, merge to both `main` and `develop` | Adding new features on release branch |
| Technical debt | Branch from `develop` as `refactor/TD-NNN-desc` | Long-lived refactor branches |

### Merge Strategy Selection

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| Feature/bugfix to `develop` | Squash merge | Merge commit (clutters history) |
| Release to `main` | Merge commit | Squash merge (loses release boundary) |
| `main` back to `develop` after release/hotfix | Merge commit | Squash merge (loses history) |
| Hotfix to `main` | Merge commit | Squash merge |

### Branch Sync Decision

| Situation | Recommended Action | Avoid |
|-----------|-------------------|-------|
| `develop` ahead of your unshared feature branch | `git rebase origin/develop` | Merging (creates noise) |
| `develop` ahead of a shared branch | `git merge origin/develop` | Rebasing (rewrites shared history) |

---

## QUICK-REFERENCE TABLE

### Branch Naming

| Branch Type | Pattern | Example |
|-------------|---------|---------|
| Feature | `feature/TICKET-NNN-short-description` | `feature/TICKET-123-late-fee-calc` |
| Bugfix | `bugfix/TICKET-NNN-short-description` | `bugfix/TICKET-456-fix-rounding` |
| Hotfix | `hotfix/TICKET-NNN-short-description` | `hotfix/TICKET-789-critical-payment-fix` |
| Release | `release/X.Y.Z` | `release/1.2.0` |
| Refactor | `refactor/TD-NNN-short-description` | `refactor/TD-001-optimize-rental-query` |

### Branch Naming Rules

| Rule | Example |
|------|---------|
| Lowercase only | `feature/ticket-123-add-login` |
| Hyphens to separate words | `bugfix/ticket-456-fix-rounding` |
| Include ticket number | `feature/TICKET-123-description` |
| Short but descriptive | `feature/TICKET-123-late-fee-calc` not `feature/TICKET-123` |
| No special characters | No spaces, underscores, or dots |

### Long-Lived Branches

| Branch | Purpose | Protection |
|--------|---------|------------|
| `main` | Production-ready code; every commit is a tagged release | PR approval + passing CI; no direct commits |
| `develop` | Integration branch for all feature work | PR approval + passing CI; no direct commits |

### Hotfix Process

| Step | Action |
|------|--------|
| 1 | Branch from `main` |
| 2 | Fix with minimal changes |
| 3 | PR to `main`, expedited review |
| 4 | After merge, PR `main` into `develop` |
| 5 | Tag release on `main` (patch version bump) |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| For background | Training | [training/development-phase-overview.md](training/development-phase-overview.md) |
| Git Workflow Standard | Standard | [../standards/git-workflow-standard.md](../standards/git-workflow-standard.md) |
