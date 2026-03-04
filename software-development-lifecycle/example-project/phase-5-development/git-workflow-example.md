> **EXAMPLE PROJECT -- Power Atlas** | This is a completed reference artifact. Use as a model when creating your own project artifacts.

# Git Workflow Example -- Power Atlas

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P5-002 |
| **Project** | Power Atlas -- GlowPowerRental |
| **Repository** | github.com/glowpowerrental/power-atlas |
| **Branching Model** | Gitflow (main, develop, feature/*, release/*, hotfix/*) |
| **Merge Strategy** | Squash merge to develop; merge commit to main |
| **Tag Format** | SemVer `vX.Y.Z` |
| **Last Verified** | 2026-03-05 |

---

## Branch Flow Overview

This example traces the complete lifecycle of the power calculation engine feature, from branch creation through production release.

```
main ─────────────────────────────────────────────────────────●── v1.0.0
                                                              ↑
                                                     merge commit
                                                              ↑
release/v1.0 ────────────────────────────────────●───●───────●
                                                 ↑           |
                                            branch from    merge to
                                             develop     main + develop
                                                 ↑
develop ──●──────────────────────●───────────────●────────────────────
          ↑                      ↑
     initial setup         squash merge
          ↑                      ↑
          ↑    feature/power-    ↑
          ↑    calculation-      ↑
          ↑    engine            ↑
          ↑         ↑            ↑
          ↑         ●──●──●──●──●
          ↑         ↑  ↑  ↑  ↑  ↑
          ↑      commits 1-5  PR #42
          ↑      (see below)  approved
          ↑
     project start
```

---

## Step-by-Step Workflow

### Step 1: Create Feature Branch from Develop

```bash
# Ensure develop is up to date
git checkout develop
git pull origin develop

# Create the feature branch
git checkout -b feature/power-calculation-engine

# Push the branch to remote to establish tracking
git push -u origin feature/power-calculation-engine
```

**Branch naming convention:** `feature/<ticket-or-description>` using lowercase and hyphens only. In this case, the branch covers requirements SWR-CALC-001 through SWR-CALC-006, so a descriptive name is used rather than a single ticket number.

---

### Step 2: Develop with Conventional Commits

The following five commits were made on the `feature/power-calculation-engine` branch during development. Each follows the conventional commit format: `<type>(<scope>): <description>`.

#### Commit 1: Test scaffolding (TDD -- tests first)

```
commit 8b1a4f2d3e5c6a7b9d0f1e2c3a4b5d6e7f8a9b0c
Author: Layla Haddad <layla.haddad@glowpowerrental.com>
Date:   Mon Feb 17 09:15:22 2026 +0300

test(calc): add unit tests for power calculation functions

Write failing tests for singlePhase, threePhase, kWToKVA, kVAToKW,
and totalLoad. Tests define expected behavior before implementation.

Includes edge case tests for zero values, negative inputs, NaN,
and very large loads (10MW).

Refs: SWR-CALC-001, SWR-CALC-002, SWR-CALC-003, SWR-CALC-004
```

#### Commit 2: Core implementation

```
commit 2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d
Author: Layla Haddad <layla.haddad@glowpowerrental.com>
Date:   Mon Feb 17 11:42:08 2026 +0300

feat(calc): implement PowerCalculator class with unit conversions

Add PowerCalculator with static methods for single-phase power,
three-phase power, kW-to-kVA, kVA-to-kW, and total load summation.

Uses IEEE-standard formulas with sqrt(3) for three-phase calculations.
Default power factor is 0.8 (configurable per call). All inputs
validated with descriptive PowerCalculationError on failure.

Refs: SWR-CALC-001, SWR-CALC-002, SWR-CALC-003, SWR-CALC-004
```

#### Commit 3: Backend API endpoints

```
commit 4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f
Author: Layla Haddad <layla.haddad@glowpowerrental.com>
Date:   Tue Feb 18 08:30:45 2026 +0300

feat(api): add server-side calculation endpoints with JWT auth

Add POST endpoints for /api/calculations/single-phase,
/api/calculations/three-phase, and /api/calculations/convert.

Server-side calculation mirrors frontend logic to enable
independent validation of client-submitted values before
persisting to database. All endpoints require JWT authentication.

Refs: SWR-CALC-005, SWR-CALC-006
```

#### Commit 4: Backend tests

```
commit 6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b
Author: Layla Haddad <layla.haddad@glowpowerrental.com>
Date:   Tue Feb 18 10:15:33 2026 +0300

test(api): add parameterized tests for calculation endpoints

Add tests mirroring frontend test cases for server-side parity.
Include tests for unauthenticated access (401) and malformed
JSON payloads (400).

Refs: SWR-CALC-005, SWR-CALC-006
```

#### Commit 5: Address code review feedback

```
commit a3f7c2e9b1d4f6a8c0e2d4f6a8b0c2d4e6f8a0b2
Author: Layla Haddad <layla.haddad@glowpowerrental.com>
Date:   Wed Feb 19 14:20:17 2026 +0300

fix(calc): add negative value validation for kW/kVA conversions

Add input validation to reject negative values in kWToKVA and
kVAToKW functions. Previously, negative inputs produced negative
results silently, which is physically meaningless for generator
sizing. Also rename `calc` variable to `calculation_input` in
calculations.py for clarity.

Addresses blocking review feedback from PR #42.

Refs: SWR-CALC-005
```

---

### Step 3: Open Pull Request

```bash
# Ensure feature branch is up to date with develop
git checkout feature/power-calculation-engine
git pull origin develop
# No conflicts in this case

# Push final commits
git push origin feature/power-calculation-engine
```

PR #42 opened: `feat(calc): implement power calculation engine with unit conversions`
- Base branch: `develop`
- Compare branch: `feature/power-calculation-engine`
- Reviewer assigned: Mohammad Al-Farsi
- See [pull-request-example.md](pull-request-example.md) for full PR content
- See [code-review-record.md](code-review-record.md) for review details

---

### Step 4: Squash Merge to Develop

After PR #42 is approved and all blocking feedback is resolved:

```bash
# On GitHub: Merge PR #42 using "Squash and merge"
# Squash commit message:
```

```
feat(calc): implement power calculation engine with unit conversions (#42)

Add PowerCalculator class with single-phase, three-phase, kW/kVA
conversions and server-side validation endpoints. 100% test coverage
on frontend; parameterized backend tests with auth and error cases.

Refs: SWR-CALC-001, SWR-CALC-002, SWR-CALC-003, SWR-CALC-004, SWR-CALC-005, SWR-CALC-006
```

**Why squash merge to develop:** The five individual commits on the feature branch represent the development journey (TDD setup, implementation, review fixes). On the `develop` branch, we want a single clean commit representing the completed feature. This keeps the develop history readable and makes it easy to revert a complete feature if needed.

```bash
# After merge, delete the feature branch
git push origin --delete feature/power-calculation-engine
git branch -d feature/power-calculation-engine
```

---

### Step 5: Create Release Branch

When the team is ready to prepare v1.0.0 for production (after the calculation engine and other features are merged to develop):

```bash
# Create release branch from develop
git checkout develop
git pull origin develop
git checkout -b release/v1.0
git push -u origin release/v1.0
```

**What happens on the release branch:**
- Final QA testing and bug fixes only
- Version number updated in `package.json` and `pyproject.toml`
- Changelog updated
- No new features -- only fixes for bugs found during release testing

```bash
# Example: version bump commit on release branch
git commit -m "chore(release): bump version to 1.0.0

Update package.json and pyproject.toml version fields.
Update CHANGELOG.md with v1.0.0 release notes."
```

```bash
# Example: last-minute bug fix on release branch
git commit -m "fix(calc): handle power factor rounding edge case at PF=0.999

Floor power factor to 4 decimal places to prevent floating-point
comparison issues when PF is very close to 1.0.

Refs: SWR-CALC-003"
```

---

### Step 6: Merge Release to Main (Merge Commit)

```bash
# Merge release branch into main using a merge commit
git checkout main
git pull origin main
git merge --no-ff release/v1.0 -m "Merge release/v1.0 into main

Release v1.0.0 of Power Atlas.

Features included:
- Power calculation engine (single-phase, three-phase, kW/kVA)
- Project management with autosave
- Client and generator management
- JWT authentication with bcrypt password hashing
- Interactive layout builder (React + Konva)

Refs: SWR-CALC-001 through SWR-CALC-006, SWR-AUTH-001 through SWR-AUTH-004"
```

**Why merge commit to main:** A merge commit on `main` preserves the full history of what was included in each release. The merge commit itself serves as a record: "at this point, all of release/v1.0 became production code." This makes it easy to compare releases and identify exactly what shipped.

---

### Step 7: Tag the Release

```bash
# Create an annotated tag on main
git tag -a v1.0.0 -m "v1.0.0 - Power Atlas initial release

Power Atlas v1.0.0 -- event power planning and generator sizing tool.

Key features:
- Power calculation engine with single-phase, three-phase, kW/kVA conversions
- Project management with autosave
- Client database and generator fleet management
- JWT authentication with bcrypt
- Interactive site layout builder
- PDF report generation
- SQLite3 database with full schema migrations

Deployed via systemd service behind Nginx reverse proxy.
Python 3.12 / Flask backend, Vite.js / Tailwind CSS frontend."

# Push tag to remote
git push origin v1.0.0
```

**Tag format:** `v1.0.0` follows SemVer (Semantic Versioning):
- **MAJOR (1):** First production release
- **MINOR (0):** Initial feature set
- **PATCH (0):** No patches yet

---

### Step 8: Back-Merge Release to Develop

```bash
# Merge release fixes back into develop so they are not lost
git checkout develop
git pull origin develop
git merge --no-ff release/v1.0 -m "Merge release/v1.0 back into develop

Incorporate release bug fixes (PF rounding edge case) and version
bump into develop branch."

git push origin develop

# Delete the release branch
git push origin --delete release/v1.0
git branch -d release/v1.0
```

---

## Branch Protection Rules

These rules are configured in the GitHub repository settings:

### `main` Branch

| Rule | Setting |
|------|---------|
| Require pull request before merging | Enabled |
| Required approvals | 2 |
| Require status checks to pass | Enabled (CI pipeline) |
| Require branches to be up to date | Enabled |
| Allow force pushes | Disabled |
| Allow deletions | Disabled |
| Restrict direct commits | Enabled |

### `develop` Branch

| Rule | Setting |
|------|---------|
| Require pull request before merging | Enabled |
| Required approvals | 1 |
| Require status checks to pass | Enabled (CI pipeline) |
| Require branches to be up to date | Enabled |
| Allow force pushes | Disabled |
| Allow deletions | Disabled |

---

## Merge Strategy Summary

| Merge Type | Strategy | Reason |
|------------|----------|--------|
| `feature/*` -> `develop` | Squash merge | Clean single-commit history on develop; feature branch detail preserved in PR |
| `bugfix/*` -> `develop` | Squash merge | Same rationale as feature branches |
| `release/*` -> `main` | Merge commit (`--no-ff`) | Preserves release boundary; shows exactly what shipped |
| `release/*` -> `develop` | Merge commit (`--no-ff`) | Ensures release fixes propagate to develop |
| `hotfix/*` -> `main` | Merge commit (`--no-ff`) | Preserves hotfix record on main |
| `hotfix/*` -> `develop` | Merge commit (`--no-ff`) | Ensures hotfix propagates to develop |

---

## Commit Message Quick Reference

```
<type>(<scope>): <description>    ← first line, under 72 chars, imperative tense

<optional body>                   ← explains WHY, not WHAT

Refs: <ticket-ids>                ← footer, references requirements
```

| Type | Use When |
|------|----------|
| `feat` | Adding a new feature |
| `fix` | Fixing a bug |
| `test` | Adding or modifying tests only |
| `docs` | Documentation changes only |
| `refactor` | Code restructuring with no behavior change |
| `chore` | Build, CI, dependency updates |
| `perf` | Performance improvements |

---

## Completion Checklist

- [x] Branch created from correct source (feature from develop)
- [x] Branch name uses lowercase-hyphens, descriptive name
- [x] All commits follow conventional commit format
- [x] Ticket referenced in commit footers
- [x] PR submitted using Pull Request Template
- [x] Code review completed and blocking issues resolved
- [x] Squash merge used for feature -> develop
- [x] Release branch created from develop for v1.0
- [x] Merge commit used for release -> main
- [x] Release tagged with SemVer format v1.0.0
- [x] Release branch merged back into develop
- [x] Feature and release branches deleted after merge

---

## Cross-References

| Document | Path | Relationship |
|----------|------|--------------|
| Pull Request #42 | [pull-request-example.md](pull-request-example.md) | PR created during this workflow |
| Code Review Record | [code-review-record.md](code-review-record.md) | Review conducted during this workflow |
| Git Workflow Standard | [../../phase-5-development/standards/git-workflow-standard.md](../../phase-5-development/standards/git-workflow-standard.md) | Standard this example follows |
| Git Branching Strategy Guide | [../../phase-5-development/guides/git-branching-strategy.md](../../phase-5-development/guides/git-branching-strategy.md) | Reference guide for branching model |
| Conventional Commits Reference | [../../phase-5-development/references/conventional-commits-reference.md](../../phase-5-development/references/conventional-commits-reference.md) | Commit format reference |
