# ClickUp Workflow

> How to set up, run, and maintain ClickUp for projects following this SDLC framework.

---

## 1. Project Space Setup

1. Create a new ClickUp **Space** named after the project
2. Create **four Folders**, one per phase:
   - `1 - Define`
   - `2 - Design`
   - `3 - Build & Verify`
   - `4 - Ship & Run`
3. Within each Folder, create a **List** for each sprint/iteration
4. Set up **Custom Fields**:

| Field | Type | Values |
|-------|------|--------|
| Priority | Dropdown | Critical, High, Medium, Low |
| Phase | Dropdown | Define, Design, Build & Verify, Ship & Run |
| Deliverable # | Number | Matches deliverable numbers in phase cheat sheets |
| Status | Status | Open, In Progress, Review, Closed |
| Assignee | People | Team members |

5. Create **Views**:
   - **Board View** (default) — Kanban by status
   - **List View** — for backlog grooming
   - **Gantt View** (optional) — for timeline visibility

---

## 2. Task Structure & Naming

### Naming Convention

Format: `[PHASE-#] Deliverable name`

Examples:
- `[DEFINE-1] Business Case`
- `[DEFINE-4] Business Requirements Document`
- `[DESIGN-1] Architecture Description Document`
- `[DESIGN-D1] System Context Diagram`
- `[BUILD-2] Pull Request: User Authentication`
- `[SHIP-1] Deployment Checklist`

### Task Structure

- Each **numbered deliverable** from the phase cheat sheets becomes a ClickUp task
- Large deliverables get **subtasks** (e.g., SRS sections, individual test cases)
- Use **labels/tags** for document type: `template`, `standard`, `runbook`, `diagram`

### Linking to SDLC Docs

Add a custom text field or comment linking to the relevant:
- Phase cheat sheet section
- Template file
- Runbook

---

## 3. Status Workflow

```
Open → In Progress → Review → Closed
```

| Status | When to Enter | Who Moves |
|--------|--------------|-----------|
| Open | Task created, requirements clear | BA or Tech Lead |
| In Progress | Work has started | Assignee |
| Review | Draft complete, ready for review | Assignee |
| Closed | Approved by reviewer/stakeholder | Reviewer |

### Mapping to Phase Gates

- All tasks in a phase must reach **Closed** before the phase gate review
- Create a dedicated task: `[PHASE] Gate Review` using [runbooks/conduct-reviews.md](runbooks/conduct-reviews.md)

---

## 4. Sprint/Iteration Cadence

| Phase | Suggested Sprint Length | Notes |
|-------|------------------------|-------|
| Define | 1-2 weeks | Short sprints, mostly meetings and writing |
| Design | 1-2 weeks | Architecture + design can overlap |
| Build & Verify | 2 weeks | Standard dev sprints |
| Ship & Run | 1 week | Deployment + monitoring |

### Sprint Planning

1. Pull deliverables from the current phase folder
2. Estimate effort: documentation tasks = hours, development tasks = story points
3. Assign based on RACI in [framework.md](framework.md)
4. Don't mix phases in a sprint unless the team is small and phases overlap

---

## 5. Board Hygiene Checklist

Run this check every 2 weeks (during backlog grooming):

- [ ] No task older than 2 sprints without an update
- [ ] All tasks have an assignee
- [ ] Completed tasks moved to Closed (not left in Review)
- [ ] Backlog groomed — irrelevant tasks removed or deprioritized
- [ ] Blocked tasks have a comment explaining the blocker
- [ ] Archive completed sprints/lists monthly
- [ ] Custom fields populated on all active tasks

---

## 6. Linking PRs to Tasks

### Branch Naming

Use ClickUp task ID in branch names:
```
feature/CU-xxxx-short-description
bugfix/CU-xxxx-short-description
hotfix/CU-xxxx-short-description
```

### Commit Messages

Include ClickUp task ID in commit messages (conventional commit format):
```
feat(auth): add login endpoint [CU-1234]
fix(api): handle null response from payment service [CU-5678]
docs(define): add BRD for Power Atlas [CU-9012]
```

See [standards/coding-and-git.md](standards/coding-and-git.md) for full conventional commit reference.

### GitHub Integration

1. Install the ClickUp GitHub integration
2. Connect your repository
3. Automatic linking: commits and PRs with `CU-xxxx` will appear in the ClickUp task
4. Optional: auto-move tasks to "Review" when PR is opened
