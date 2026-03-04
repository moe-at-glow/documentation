# Development Phase Overview

How the Development phase fits into the GlowPowerRental SDLC and what it produces.

---

## Purpose

The Development phase transforms approved designs into working, tested code. It is Phase 5 of 8 in the SDLC framework.

**Input:** Approved Detailed Design Documents (DDDs), API specifications, and data models from Phase 4.

**Output:** Working code on the `develop` branch, with passing tests, ready for Phase 6 (Testing).

---

## Where Development Fits

```
Phase 2          Phase 3            Phase 4         Phase 5           Phase 6
Requirements --> Architecture --> Design --> [DEVELOPMENT] --> Testing
     SRS            ADD            DDD         Working Code        Test Results
     RTM            ADRs           API Spec    Unit Tests          Test Reports
                                   Data Model  PR History          Defect Log
```

Development does not define WHAT to build (that is Requirements) or HOW to structure it (that is Architecture and Design). Development implements the approved design with discipline.

---

## Key Principles

### 1. Design First, Code Second

Never start coding without an approved DDD. If the design is missing or unclear:

1. Stop.
2. Ask the Tech Lead or the author of the design.
3. If the design needs changes, update the DDD first through the design change process.

Coding without a design leads to rework, inconsistency, and integration failures.

### 2. Test-Driven Development (TDD)

GlowPowerRental follows TDD for business logic:

```
Write Failing Test --> Write Minimum Code --> Tests Pass --> Refactor --> Repeat
     (Red)                (Green)             (Green)       (Green)
```

Why TDD:
- Forces you to understand the expected behavior before writing code.
- Produces tests as a side effect of development, not an afterthought.
- Results in simpler, more focused implementations.
- Provides a safety net for refactoring.

### 3. Small, Focused Changes

Each pull request should:
- Implement one ticket or one logical change.
- Stay under 400 lines of diff.
- Be reviewable in under 30 minutes.

Large PRs are split into multiple smaller PRs that build on each other.

### 4. Continuous Integration

Every push triggers the CI pipeline:
- Lint check
- Unit tests
- Build verification

All checks must pass before a PR can be reviewed or merged.

---

## Development Workflow

```
1. Pick ticket from sprint backlog
        |
2. Read ticket + DDD + API spec
        |
3. Create feature branch from develop
        |
4. Write failing tests (Red)
        |
5. Write implementation (Green)
        |
6. Add edge case tests
        |
7. Run full test suite + linter
        |
8. Self-review (git diff)
        |
9. Commit with conventional message
        |
10. Push + create PR
        |
11. Address review feedback
        |
12. Squash merge to develop
```

Each step is detailed in the [Implement Feature Runbook](../runbooks/implement-feature.md).

---

## Roles and Responsibilities

| Role | Responsibility |
|------|---------------|
| Developer | Implements features following TDD, writes tests, creates PRs, addresses feedback |
| Code Reviewer | Reviews PRs within 1 business day, provides constructive feedback |
| Tech Lead | Reviews architecture-impacting changes, resolves technical disputes, approves exceptions |
| QA Engineer | Verifies implementation against acceptance criteria (Phase 6), reports defects |

---

## Development Standards

| Standard | Purpose | Document |
|----------|---------|----------|
| Coding Standards | Code style, naming, formatting, TypeScript rules | [coding-standards.md](../standards/coding-standards.md) |
| Git Workflow | Branching, commits, merging, versioning | [git-workflow-standard.md](../standards/git-workflow-standard.md) |
| Code Review | Review process, feedback format, SLA | [code-review-standard.md](../standards/code-review-standard.md) |
| Unit Testing | Coverage targets, test structure, mocking | [unit-testing-standard.md](../standards/unit-testing-standard.md) |

---

## Artifacts Produced

| Artifact | Description |
|----------|-------------|
| Source code | Implementation of approved designs on feature branches |
| Unit tests | Tests covering business logic (80%+), critical paths (90%+) |
| Pull requests | Documented changes with description, test plan, and review history |
| Commit history | Conventional commit messages linking to tickets |
| Technical debt register | Newly identified debt items recorded for future resolution |

---

## Common Mistakes

| Mistake | Why It Happens | How to Avoid |
|---------|---------------|--------------|
| Coding before reading the design | Eagerness to start | Make "read DDD" the first step in every ticket |
| Skipping tests | Time pressure | TDD means tests come first, not last |
| Large PRs | Batching too much work | One ticket = one PR. Split if over 400 lines. |
| Not running the full test suite | "My change is small" | Always run `npm test` before pushing |
| Force-pushing during review | Wanting a clean history | Push new commits during review. Squash on merge. |
| Ignoring linter warnings | "It still works" | Linter errors are bugs. Fix them. |

---

## Phase Exit Criteria

Development is complete for a ticket when:

- [ ] All acceptance criteria from the ticket are implemented
- [ ] Implementation matches the DDD specification
- [ ] Unit tests pass with required coverage
- [ ] Linter passes with no warnings
- [ ] PR is approved by at least one reviewer
- [ ] Code is merged to `develop`
- [ ] CI pipeline passes on `develop`

The ticket then moves to Phase 6 (Testing) for integration testing, system testing, and QA verification.
