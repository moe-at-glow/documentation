# Getting Started with the SDLC Framework

This guide helps you navigate and use the SDLC documentation. Read this first before diving into any phase.

---

## What Is This Framework?

The **SDLC (Software Development Lifecycle) Framework** is the official process for building software. It defines how every project moves from an initial idea to a running system in production. Instead of each team inventing their own process, everyone follows the same phases, produces the same artifacts, and passes through the same approval gates.

The framework is operational -- every document tells you exactly what to do, what to produce, and who must approve it.

### Why Does It Exist?

Without a shared process:
- Requirements get lost between what the business asked for and what developers build
- Architecture decisions are made in hallway conversations and never recorded
- Testing is inconsistent -- some projects have thorough testing, others ship untested
- New team members take months to figure out "how we do things here"

This framework solves those problems by making the process explicit, repeatable, and auditable.

---

## Key Terms

Before you read any document, understand these terms. They appear everywhere in the framework.

### Document Types

| Term | What It Means |
|------|---------------|
| **Runbook** | A step-by-step procedure you follow to complete a task. Like a recipe -- do step 1, then step 2, then step 3. Each runbook has entry criteria (what must be true before you start), procedure steps, and exit criteria (what must be true when you are done). |
| **Standard** | A set of rules that must be followed. Standards are compliance checklists -- each rule has a checkbox and a consequence if violated. You do not "follow" a standard step-by-step; you check your work against it. |
| **Template** | A blank form you copy and fill in. Templates give you the structure of an artifact so you do not have to figure out what sections to include. |
| **Reference** | A lookup table or decision tree. When you need to make a choice (which architecture pattern? what defect severity?), the reference gives you a structured way to decide. |

### Framework Keywords

| Term | What It Means |
|------|---------------|
| **Phase** | One stage of the software lifecycle. There are 4 phases (Define, Design, Build & Verify, Ship & Run). Each phase has its own cheat sheet in `phases/`. |
| **Phase Gate** | An approval checkpoint at the end of each phase. A group of reviewers evaluates whether all required artifacts are complete and meet quality standards before the project can move to the next phase. |
| **Artifact** | Any document or deliverable produced during a phase. Examples: Business Case, SRS, Architecture Description Document, Test Plan. |
| **Entry Criteria** | Conditions that must be true before you can start a phase or runbook. If entry criteria are not met, do not begin. |
| **Exit Criteria** | Conditions that must be true before a phase or runbook is considered complete. Every exit criterion has a checkbox. |
| **Scaling Gate** | A rule in every document that tells you how much applies based on your project size (small, medium, or large). |
| **RACI Matrix** | A table showing who is Responsible (does the work), Accountable (owns the outcome), Consulted (provides input), and Informed (kept up to date) for each activity. |

### Acronyms

| Acronym | Full Name | What It Is |
|---------|-----------|------------|
| **RTM** | Requirements Traceability Matrix | Tracks each requirement from business need through design, code, and test case. Ensures nothing is lost. |
| **ADR** | Architecture Decision Record | Records a significant technical decision with context, alternatives considered, and rationale. |
| **BRD** | Business Requirements Document | Describes what the business needs in business language. |
| **SRS** | Software Requirements Specification | Describes what the software must do in technical language, derived from the BRD. |
| **ADD** | Architecture Description Document | Describes the system structure, components, interfaces, and deployment topology. |
| **DDD** | Detailed Design Document | Describes how a specific component works internally -- classes, data model, API contracts, error handling. |
| **MoSCoW** | Must / Should / Could / Won't | A prioritization method: **M**ust Have (non-negotiable), **S**hould Have (important but not critical), **C**ould Have (nice to have), **W**on't Have (out of scope for this release). |
| **PlantUML** | — | The mandatory diagramming tool. You write text markup in `.puml` files and it generates diagrams. |
| **UAT** | User Acceptance Testing | Final testing by business users to confirm the system meets their requirements. |

### Requirement ID Prefixes

All requirements and artifacts use standardized ID prefixes:

| Prefix | Meaning | Example |
|--------|---------|---------|
| `BR-` | Business Requirement | BR-001 |
| `STK-` | Stakeholder Requirement | STK-001 |
| `SWR-` | Software Requirement | SWR-001 |
| `SWR-NFR-` | Non-Functional Requirement | SWR-NFR-P001 |
| `ADR-` | Architecture Decision Record | ADR-001 |
| `UC-` | Use Case | UC-001 |
| `TC-` | Test Case | TC-001 |
| `DEF-` | Defect Report | DEF-001 |

Numbers are assigned sequentially and never reused.

---

## How This Framework Is Organized

| Directory | What It Contains | When You Use It |
|-----------|------------------|-----------------|
| `phases/` | Phase cheat sheets with deliverables, activities, and gate criteria | Starting and managing each phase |
| `standards/` | Compliance rules with pass/fail checkboxes | Before starting work -- know what is required |
| `runbooks/` | Step-by-step procedures with entry/exit criteria | While doing the work -- follow the steps |
| `templates/` | Copy-paste starting points for artifacts | When producing a deliverable -- fill in the blanks |
| `references/` | Lookup tables and decision trees | When making a decision -- find the answer |
| `diagrams/` | PlantUML `.puml` templates | When creating architecture and design diagrams |

**Workflow for any task:**
1. Open the **phase cheat sheet** to see what you need to produce
2. Read the **standard** to know what compliance is required
3. Follow the **runbook** step-by-step to do the work
4. Use the **template** to produce each artifact
5. Check the **reference** when you need a decision aid

---

## What to Read Based on Your Role

Not everyone needs to read everything. Start with the phases relevant to your role:

| Role | Primary Phases | Start Here |
|------|---------------|------------|
| **Business Analyst** | Phase 1 (Define) | [phases/1-define.md](phases/1-define.md) + [runbooks/gather-requirements.md](runbooks/gather-requirements.md) |
| **Tech Lead / Architect** | Phase 2 (Design) | [phases/2-design.md](phases/2-design.md) + [runbooks/architect-and-design.md](runbooks/architect-and-design.md) |
| **Developer** | Phase 2 + 3 | [phases/3-build-and-verify.md](phases/3-build-and-verify.md) + [runbooks/implement-feature.md](runbooks/implement-feature.md) |
| **QA Lead / Tester** | Phase 1 (requirements) + 3 | [phases/3-build-and-verify.md](phases/3-build-and-verify.md) + [runbooks/run-test-cycle.md](runbooks/run-test-cycle.md) |
| **Product Owner** | Phase 1 + 3 (UAT) | [phases/1-define.md](phases/1-define.md) + [runbooks/start-a-project.md](runbooks/start-a-project.md) |
| **Project Sponsor** | Phase 1 (approval gates) | [framework.md](framework.md) -- Gate Review Procedure section |

**Everyone** should read:
- This guide (you are here)
- [framework.md](framework.md) -- the authoritative reference for all phases, roles, and gates

---

## Understanding Project Scale

Every document has a **Scaling Gate**. This tells you how much of the document applies to your project:

| Scale | Duration | Team | What It Means |
|-------|----------|------|---------------|
| **Small** | < 2 weeks | 1-2 developers | Reduced artifacts. User stories can replace formal BRD. Design can live in tickets. Manual testing is acceptable. |
| **Medium** | 2-8 weeks | 3-5 developers | All artifacts required. Some formats can be streamlined. Validation can be a single review session. |
| **Large** | 8+ weeks | 6+ developers | Full compliance. No reductions without written sponsor and tech lead approval. |

**How to apply:** When you open any document, check the Scaling Gate first. If your project is small, you may skip sections marked as medium/large only.

---

## Understanding the Document Format

All operational documents follow a consistent format:

| Section | What It Tells You |
|---------|-------------------|
| **Metadata table** (top) | Who owns it, how to verify compliance, when it was last reviewed |
| **Scaling Gate** | Which sections apply to your project size |
| **Entry Criteria** | What must be true before you start (do not skip these) |
| **Procedure steps** | Numbered actions with decision gates |
| **Exit Criteria** | Checkboxes that must all be checked before you are done |
| **Deliverables** | What you should have produced, with links to templates |
| **Cross-References** | Related documents (standards, runbooks, templates) |

**Key conventions:**
- `- [ ]` = checkbox -- tick it when the item is verified
- `> **IF** ... **THEN** ...` = conditional gate -- follow the path that matches your situation
- `SLA: X days` = the maximum time allowed for a step

---

## Tools

### PlantUML (Mandatory for Diagrams)

All architecture and design diagrams must be created as PlantUML `.puml` files.

**Templates are provided** in [diagrams/](diagrams/) -- you do not need to start from scratch. Copy the relevant `.puml` template to your project's `diagrams/` directory, edit with your project-specific components, and commit the `.puml` source file (the source file is the deliverable, not the image).

### Git Conventions

- **Branching:** See [standards/coding-and-git.md](standards/coding-and-git.md)
- **Commit messages:** Use conventional commit format: `type(scope): description [CU-xxxx]`
  - Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`
  - Example: `feat(billing): add late fee calculation [CU-1234]`
- **Pull requests:** Use [templates/pull-request.md](templates/pull-request.md)

---

## Your First Project — Step by Step

### 1. Understand the Framework

Read [framework.md](framework.md) to understand:
- The 4 phases (Define → Design → Build & Verify → Ship & Run)
- Your role in the RACI matrix
- How project size affects what you skip

### 2. Set Up ClickUp

Follow [clickup-workflow.md](clickup-workflow.md) to:
- Create a Space for your project
- Set up folders for each phase
- Configure custom fields and views

### 3. Phase 1: Define

Open [phases/1-define.md](phases/1-define.md) and work through the deliverables:

1. **Business Case** — Use [templates/business-case.md](templates/business-case.md), follow [runbooks/start-a-project.md](runbooks/start-a-project.md)
2. **Project Charter** — Use [templates/project-charter.md](templates/project-charter.md)
3. **Stakeholder Register** — Use [templates/stakeholder-register.md](templates/stakeholder-register.md)
4. **BRD** — Use [templates/business-requirements-document.md](templates/business-requirements-document.md), follow [runbooks/gather-requirements.md](runbooks/gather-requirements.md)
5. **SRS** (medium+ projects) — Use [templates/software-requirements-specification.md](templates/software-requirements-specification.md)
6. **Use Cases** (medium+ projects) — Use [templates/use-case.md](templates/use-case.md)
7. **RTM** (medium+ projects) — Use [templates/requirements-traceability-matrix.md](templates/requirements-traceability-matrix.md)

**Gate:** All deliverables reviewed → [runbooks/conduct-reviews.md](runbooks/conduct-reviews.md)

### 4. Phase 2: Design

Open [phases/2-design.md](phases/2-design.md) and produce:

1. **Architecture Description Document** — Use [templates/architecture-description-document.md](templates/architecture-description-document.md)
2. **ADRs** — Use [templates/architecture-decision-record.md](templates/architecture-decision-record.md)
3. **Detailed Design Document** (medium+) — Use [templates/detailed-design-document.md](templates/detailed-design-document.md)
4. **API Specification** (if API) — Use [templates/api-specification.md](templates/api-specification.md)
5. **Data Model Document** (if DB) — Use [templates/data-model-document.md](templates/data-model-document.md)
6. **PlantUML Diagrams** — Templates in [diagrams/](diagrams/)

Follow [runbooks/architect-and-design.md](runbooks/architect-and-design.md) for step-by-step guidance.

**Gate:** Architecture + Design reviews → [runbooks/conduct-reviews.md](runbooks/conduct-reviews.md)

### 5. Phase 3: Build & Verify

Open [phases/3-build-and-verify.md](phases/3-build-and-verify.md).

**Development:**
1. Set up environment → [runbooks/setup-dev-environment.md](runbooks/setup-dev-environment.md)
2. Implement features → [runbooks/implement-feature.md](runbooks/implement-feature.md)
3. Follow coding standards → [standards/coding-and-git.md](standards/coding-and-git.md)
4. Submit PRs using [templates/pull-request.md](templates/pull-request.md)
5. Review code → [standards/code-review.md](standards/code-review.md)

**Testing:**
1. Write test plan → [templates/test-plan.md](templates/test-plan.md)
2. Execute tests → [runbooks/run-test-cycle.md](runbooks/run-test-cycle.md)
3. Follow testing standards → [standards/testing.md](standards/testing.md)
4. Get UAT sign-off → [templates/uat-sign-off.md](templates/uat-sign-off.md)

**Gate:** All tests pass, UAT signed off

### 6. Phase 4: Ship & Run

Open [phases/4-ship-and-run.md](phases/4-ship-and-run.md).

1. Deploy → [runbooks/deploy-and-operate.md](runbooks/deploy-and-operate.md)
2. Monitor
3. Operate

---

## Need Help?

- **"What document do I need?"** → [references/artifacts-checklist.md](references/artifacts-checklist.md)
- **"What does this term mean?"** → [references/glossary.md](references/glossary.md)
- **"How do I classify a defect?"** → [references/defect-severity.md](references/defect-severity.md)
- **"What does a finished project look like?"** → [example-project/](example-project/)
- **"How do I update these docs?"** → [maintaining-docs.md](maintaining-docs.md)
