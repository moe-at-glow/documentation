# Getting Started with the SDLC Framework

This guide helps you navigate and use the GlowPowerRental SDLC documentation. Read this first before diving into any phase.

---

## What Is This Framework?

The **SDLC (Software Development Lifecycle) Framework** is GlowPowerRental's official process for building software. It defines how every project moves from an initial idea to a running system in production. Instead of each team inventing their own process, everyone follows the same phases, produces the same artifacts, and passes through the same approval gates.

The framework is based on international standards (ISO/IEC/IEEE 12207, 29148, and 42010) but adapted for GlowPowerRental's size and way of working. It is not academic -- it is operational. Every document tells you exactly what to do, what to produce, and who must approve it.

### Why Does It Exist?

Without a shared process:
- Requirements get lost between what the business asked for and what developers build
- Architecture decisions are made in hallway conversations and never recorded
- Testing is inconsistent -- some projects have thorough testing, others ship untested
- New team members take months to figure out "how we do things here"

This framework solves those problems by making the process explicit, repeatable, and auditable.

### What Does "QRH Format" Mean?

**QRH** stands for **Quick Reference Handbook** -- a format borrowed from aviation. Pilots use QRH checklists during flight to ensure no critical step is missed, even under pressure. Our documents follow the same principle: short, actionable, checkbox-driven. No long paragraphs of explanation. Just steps to follow and boxes to check.

If you need background understanding (the "why"), read the **training materials** in each phase's `guides/training/` directory. The operational documents assume you already understand the concepts and just need to execute.

---

## Key Terms and Keywords

Before you read any document, understand these terms. They appear everywhere in the framework.

### Document Types

| Term | What It Means |
|---|---|
| **Runbook** | A step-by-step procedure you follow to complete a task. Like a recipe -- do step 1, then step 2, then step 3. Each runbook has entry criteria (what must be true before you start), procedure steps, and exit criteria (what must be true when you are done). |
| **Standard** | A set of rules that must be followed. Standards are compliance checklists -- each rule has a checkbox and a consequence if violated. You do not "follow" a standard step-by-step; you check your work against it. |
| **Template** | A blank form you copy and fill in. Templates give you the structure of an artifact so you do not have to figure out what sections to include. |
| **Reference** | A lookup table or decision tree. When you need to make a choice (which architecture pattern? what defect severity?), the reference gives you a structured way to decide. |
| **Guide** | A quick-reference card that summarizes key decisions and common pitfalls. Guides assume you already understand the concept and just need a reminder. |
| **Training** | Background and educational material. Read this when learning a phase for the first time. Training explains the "why" behind the process. |

### Framework Keywords

| Term | What It Means |
|---|---|
| **Phase** | One stage of the software lifecycle. There are 8 phases (Business Analysis, Requirements, Architecture, Design, Development, Testing, Deployment, Operations). Each phase has its own directory. |
| **Phase Gate** | An approval checkpoint at the end of each phase. A group of reviewers evaluates whether all required artifacts are complete and meet quality standards before the project can move to the next phase. |
| **Artifact** | Any document or deliverable produced during a phase. Examples: Business Case, SRS, Architecture Description Document, Test Plan. |
| **Entry Criteria** | Conditions that must be true before you can start a phase or runbook. If entry criteria are not met, do not begin. |
| **Exit Criteria** | Conditions that must be true before a phase or runbook is considered complete. Every exit criterion has a checkbox. |
| **Abort Condition** | A situation where you must stop immediately and escalate. Do not continue the procedure -- follow the escalation path. |
| **Scaling Gate** | A rule at the top of every document that tells you how much of the document applies based on your project size (small, medium, or large). |
| **RACI Matrix** | A table showing who is Responsible (does the work), Accountable (owns the outcome), Consulted (provides input), and Informed (kept up to date) for each activity. |
| **RTM** | Requirements Traceability Matrix. A table that tracks each requirement from business need through design, code, and test case. Ensures nothing is lost. |
| **ADR** | Architecture Decision Record. A document that records a significant technical decision with context, alternatives considered, and rationale for the choice made. |
| **BRD** | Business Requirements Document. Describes what the business needs in business language. |
| **SRS** | Software Requirements Specification. Describes what the software must do in technical language, derived from the BRD. |
| **ADD** | Architecture Description Document. Describes the system structure, components, interfaces, and deployment topology. |
| **DDD** | Detailed Design Document. Describes how a specific component works internally -- classes, data model, API contracts, error handling. |
| **MoSCoW** | A prioritization method: **M**ust Have (non-negotiable), **S**hould Have (important but not critical), **C**ould Have (nice to have), **W**on't Have (out of scope for this release). |
| **PlantUML** | The mandatory diagramming tool. You write text markup in `.puml` files and it generates diagrams (sequence, component, ERD, etc.). |

### QRH Conventions Used in Documents

| You See | It Means |
|---|---|
| `- [ ]` | A checkbox. Tick it when the item is verified or complete. |
| `> **IF** ... **THEN** ...` | A conditional gate. Read the condition. If it matches your situation, follow the THEN path. Otherwise check the next condition or the ELSE path. |
| `> **ABORT IF** ...` | A stop condition. If this is true, do not continue. Escalate immediately using the path described. |
| `**SCALING GATE**` | Check your project size. The rules below tell you which parts of the document are required for small, medium, and large projects. |
| `SLA: X days` | The maximum time allowed for a step. If you cannot complete it within the SLA, escalate. |
| `Escalation: [Name/Role]` | The person to contact if something goes wrong or takes too long. |

---

## How This Framework Is Organized

The SDLC documentation covers 8 phases of software delivery. Each phase has its own directory with five types of documents:

| Document Type | What It Is | When You Use It |
|---|---|---|
| **Standards** | Compliance rules with pass/fail checkboxes | Before starting work -- know what is required |
| **Runbooks** | Step-by-step procedures with entry/exit criteria | While doing the work -- follow the steps |
| **Templates** | Copy-paste starting points for artifacts | When producing a deliverable -- fill in the blanks |
| **References** | Lookup tables and decision trees | When making a decision -- find the answer |
| **Guides** | Quick-reference cards with decision tables | When you need a refresher -- scan the tables |
| **Training** (`guides/training/`) | Background and educational overviews | When learning a phase for the first time |

**Workflow for any task:**
1. Read the **training overview** to understand the phase (first time only)
2. Read the **standard** to know what compliance is required
3. Follow the **runbook** step-by-step to do the work
4. Use the **template** to produce each artifact
5. Check the **reference** when you need a decision aid
6. Scan the **guide** when you need a quick reminder

---

## What to Read Based on Your Role

Not everyone needs to read everything. Start with the phases relevant to your role:

| Role | Primary Phases | Start Here |
|---|---|---|
| **Business Analyst** | Phase 1, Phase 2 | [Phase 1 Training](phase-1-business-analysis/guides/training/business-analysis-overview.md), then [Phase 2 Training](phase-2-requirements-engineering/guides/training/requirements-engineering-overview.md) |
| **Tech Lead / Architect** | Phase 3, Phase 4 | [Phase 3 Training](phase-3-system-architecture/guides/training/architecture-description-overview.md), then [Phase 4 Training](phase-4-design/guides/training/design-phase-overview.md) |
| **Developer** | Phase 4, Phase 5 | [Phase 5 Training](phase-5-development/guides/training/development-phase-overview.md), then [Phase 4 Training](phase-4-design/guides/training/design-phase-overview.md) |
| **QA Lead / Tester** | Phase 2 (requirements), Phase 6 | [Phase 6 Training](phase-6-testing/guides/training/testing-phase-overview.md), then [Phase 2 Training](phase-2-requirements-engineering/guides/training/requirements-engineering-overview.md) |
| **Product Owner** | Phase 1, Phase 2, Phase 6 (UAT) | [Phase 1 Training](phase-1-business-analysis/guides/training/business-analysis-overview.md) |
| **Project Sponsor** | Phase 1 (approval gates) | [SDLC Framework Standard](standards/sdlc-framework.md) -- Gate Review Procedure section |

**Everyone** should read:
- This guide (you are here)
- [SDLC Framework Standard](standards/sdlc-framework.md) -- the authoritative reference for all phases, roles, and gates

---

## Understanding Project Scale

Every document has a **SCALING GATE** at the top. This tells you how much of the document applies to your project:

| Scale | Team Size | What It Means |
|---|---|---|
| **Small** | 1-2 developers | Reduced artifacts. User stories can replace formal BRD. Design can live in tickets. Manual testing is acceptable. |
| **Medium** | 3-5 developers | All artifacts required. Some formats can be streamlined. Validation can be a single review session. |
| **Large** | 6+ developers | Full compliance. No reductions without written sponsor and tech lead approval. |

**How to apply:** When you open any document, check the Scaling Gate first. If your project is small, you may skip sections marked as medium/large only.

---

## Understanding the Document Format (QRH)

All operational documents use **QRH (Quick Reference Handbook)** format. Here is how to read them:

| Section | What It Tells You |
|---|---|
| **Metadata table** (top) | Who owns it, how to verify compliance, when it was last reviewed |
| **SCALING GATE** | Which sections apply to your project size |
| **ENTRY CRITERIA** | What must be true before you start (do not skip these) |
| **ABORT CONDITIONS** | When to stop and escalate -- if any condition is met, do not continue |
| **Procedure steps** | Numbered actions with IF/THEN/ELSE decision gates |
| **EXIT CRITERIA** | Checkboxes that must all be checked before you are done |
| **OUTPUT ARTIFACTS** | What you should have produced, with links to templates |
| **CROSS-REFERENCES** | Related documents (standards, runbooks, guides) |

**Key conventions:**
- `- [ ]` = checkbox -- tick it when the item is verified
- `> **IF** ... **THEN** ...` = conditional gate -- follow the path that matches your situation
- `> **ABORT IF** ...` = stop condition -- do not proceed, escalate instead

---

## Tools

### PlantUML (Mandatory for Diagrams)

All architecture and design diagrams must be created as PlantUML `.puml` files. PlantUML is a text-based diagramming tool where you write markup and it generates diagrams.

**Templates are provided** -- you do not need to start from scratch:
- Phase 3 templates: `phase-3-system-architecture/diagrams/*.puml` (system context, component, sequence, deployment, ERD, state)
- Phase 4 templates: `phase-4-design/diagrams/*.puml` (class, API flow, data flow)

**How to use:**
1. Copy the relevant `.puml` template to your project's `diagrams/` directory
2. Edit the file with your project-specific components, actors, and flows
3. Render locally using PlantUML CLI (`java -jar plantuml.jar diagram.puml`) or a VS Code extension
4. Commit the `.puml` source file to your repository (the source file is the deliverable, not the image)

### Git Conventions

- **Branching:** See [Git Workflow Standard](phase-5-development/standards/git-workflow-standard.md)
- **Commit messages:** Use conventional commit format: `type(scope): description`
  - Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`
  - Example: `feat(calculation-engine): add power factor correction formula`
- **Pull requests:** Use the [PR Template](phase-5-development/templates/pull-request-template.md)

### Requirement ID Prefixes

All requirements and artifacts use standardized ID prefixes:

| Prefix | Meaning | Example |
|---|---|---|
| `BR-` | Business Requirement | BR-001 |
| `STK-` | Stakeholder Requirement | STK-001 |
| `SYS-` | System Requirement | SYS-001 |
| `SWR-` | Software Requirement | SWR-001 |
| `SWR-NFR-` | Non-Functional Requirement | SWR-NFR-P001 |
| `ADR-` | Architecture Decision Record | ADR-001 |
| `UC-` | Use Case | UC-001 |
| `TC-` | Test Case | TC-001 |
| `DEF-` | Defect Report | DEF-001 |

Numbers are assigned sequentially and never reused.

---

## Your Project Journey: From Idea to Production

This is the step-by-step path every project follows. Each step links to the runbook you will execute.

```
 PROJECT IDEA
      │
      ▼
 ┌─────────────────────────────────────────────────────────┐
 │  KICKOFF                                                │
 │  Complete the Project Kickoff Checklist                  │
 │  → Sponsor identified, team assigned, repo created       │
 └──────────────────────┬──────────────────────────────────┘
                        │
                        ▼
 ┌─────────────────────────────────────────────────────────┐
 │  PHASE 1: BUSINESS ANALYSIS                 ~23 days    │
 │                                                          │
 │  Step 1 ─ Conduct Business Needs Analysis     (5 days)  │
 │           → Problem Statement approved by Sponsor        │
 │                        │                                 │
 │  Step 2 ─ Develop Business Case              (10 days)  │
 │           → Business Case approved by Sponsor            │
 │                        │                                 │
 │  Step 3 ─ Identify Stakeholders               (3 days)  │
 │           → Stakeholder Register validated                │
 │                        │                                 │
 │  Step 4 ─ Create Project Charter              (5 days)  │
 │           → Charter signed by Sponsor                    │
 │                                                          │
 │  ── GATE REVIEW ──                                       │
 │  Reviewers: Project Sponsor, Product Owner               │
 │  Decision: Proceed / Conditional / Rework / Stop         │
 └──────────────────────┬──────────────────────────────────┘
                        │
                        ▼
 ┌─────────────────────────────────────────────────────────┐
 │  PHASE 2: REQUIREMENTS ENGINEERING          ~25 days    │
 │                                                          │
 │  Step 5 ─ Conduct Stakeholder Analysis        (5 days)  │
 │           → Refined Stakeholder Register + Comms Plan    │
 │                        │                                 │
 │  Step 6 ─ Extract Business Requirements      (15 days)  │
 │           → BRD baselined and approved                   │
 │                        │                                 │
 │  Step 7 ─ Derive Software Requirements        (5 days)  │
 │           → SRS with SWR-XXX requirements                │
 │                        │                                 │
 │  Step 8 ─ Validate & Baseline Requirements              │
 │           → RTM populated, Validation Report, sign-off   │
 │                                                          │
 │  ── GATE REVIEW ──                                       │
 │  Reviewers: Product Owner, BA, Tech Lead, Domain Expert  │
 │  Decision: Proceed / Conditional / Rework / Stop         │
 └──────────────────────┬──────────────────────────────────┘
                        │
                        ▼
 ┌─────────────────────────────────────────────────────────┐
 │  PHASE 3: SYSTEM ARCHITECTURE               ~15 days    │
 │                                                          │
 │  Step 9 ─ Create Architecture Description               │
 │           → ADD with all viewpoints (ISO 42010)          │
 │           → PlantUML diagrams: system-context, component,│
 │             sequence, deployment, ERD, state              │
 │           → ADRs for all significant decisions            │
 │                                                          │
 │  ── GATE REVIEW ──                                       │
 │  Reviewers: Tech Lead, Product Owner, QA Lead            │
 └──────────────────────┬──────────────────────────────────┘
                        │
                        ▼
 ┌─────────────────────────────────────────────────────────┐
 │  PHASE 4: DESIGN                            ~10 days    │
 │                                                          │
 │  Step 10 ─ Create Detailed Design per component         │
 │            → DDD, API Specs, Data Model, UI Wireframes   │
 │            → PlantUML diagrams: class, API flow,         │
 │              data flow                                   │
 │                                                          │
 │  ── GATE REVIEW ──                                       │
 │  Reviewers: Tech Lead, Developer(s)                      │
 └──────────────────────┬──────────────────────────────────┘
                        │
                        ▼
 ┌─────────────────────────────────────────────────────────┐
 │  PHASE 5: DEVELOPMENT                       Variable    │
 │                                                          │
 │  Per feature:                                            │
 │  Step 11 ─ Implement Feature (TDD)                      │
 │            → Source code, unit tests, code review         │
 │            → PR submitted using PR template               │
 │                                                          │
 │  ── GATE REVIEW ──                                       │
 │  Reviewers: Tech Lead, QA Lead                           │
 └──────────────────────┬──────────────────────────────────┘
                        │
                        ▼
 ┌─────────────────────────────────────────────────────────┐
 │  PHASE 6: TESTING                           Variable    │
 │                                                          │
 │  Step 12 ─ Execute Test Cycle                           │
 │            → Test Plan, Test Cases, Defect Reports       │
 │            → Test Summary Report                         │
 │            → UAT Sign-Off                                │
 │                                                          │
 │  ── GATE REVIEW ──                                       │
 │  Reviewers: Product Owner, Tech Lead, QA Lead            │
 └──────────────────────┬──────────────────────────────────┘
                        │
                        ▼
                   DEPLOYMENT
```

### Step-by-Step with Runbook Links

| Step | Phase | Runbook | Duration | You Produce | Who Approves |
|:---:|---|---|:---:|---|---|
| -- | Kickoff | [Project Kickoff Checklist](standards/sdlc-framework.md) | -- | Team, repo, channel | -- |
| 1 | Phase 1 | [Conduct Business Needs Analysis](phase-1-business-analysis/runbooks/conduct-business-needs-analysis.md) | 5 days | Problem Statement | Sponsor |
| 2 | Phase 1 | [Develop Business Case](phase-1-business-analysis/runbooks/develop-business-case.md) | 10 days | Business Case, Risk Register, KPIs | Sponsor |
| 3 | Phase 1 | [Identify Stakeholders](phase-1-business-analysis/runbooks/conduct-initial-stakeholder-identification.md) | 3 days | Stakeholder Register | Sponsor |
| 4 | Phase 1 | [Create Project Charter](phase-1-business-analysis/runbooks/create-project-charter.md) | 5 days | Project Charter, RACI, Milestones | Sponsor |
| -- | Gate 1 | [Gate Review Procedure](standards/sdlc-framework.md) | 1 day | Gate Decision Record | Sponsor + PO |
| 5 | Phase 2 | [Conduct Stakeholder Analysis](phase-2-requirements-engineering/runbooks/conduct-stakeholder-analysis.md) | 5 days | Refined Register, Comms Plan | Sponsor |
| 6 | Phase 2 | [Extract Business Requirements](phase-2-requirements-engineering/runbooks/extract-business-requirements.md) | 15 days | BRD (baselined) | Sponsor |
| 7 | Phase 2 | [Derive Software Requirements](phase-2-requirements-engineering/runbooks/derive-software-requirements.md) | 5 days | SRS | Tech Lead |
| 8 | Phase 2 | [Validate Requirements](phase-2-requirements-engineering/runbooks/validate-requirements.md) | -- | RTM, Validation Report | PO + Stakeholders |
| -- | Gate 2 | [Gate Review Procedure](standards/sdlc-framework.md) | 1 day | Gate Decision Record | PO + Tech Lead |
| 9 | Phase 3 | [Create Architecture Description](phase-3-system-architecture/runbooks/create-architecture-description.md) | 15 days | ADD, ADRs, PlantUML diagrams | Tech Lead + PO |
| -- | Gate 3 | [Gate Review Procedure](standards/sdlc-framework.md) | 1 day | Gate Decision Record | Tech Lead + PO |
| 10 | Phase 4 | [Create Detailed Design](phase-4-design/runbooks/create-detailed-design.md) | 10 days | DDD, API Specs, Data Model, PlantUML | Tech Lead |
| -- | Gate 4 | [Gate Review Procedure](standards/sdlc-framework.md) | 1 day | Gate Decision Record | Tech Lead |
| 11 | Phase 5 | [Implement Feature](phase-5-development/runbooks/implement-feature.md) | Variable | Source Code, Unit Tests, PRs | Tech Lead |
| -- | Gate 5 | [Gate Review Procedure](standards/sdlc-framework.md) | 1 day | Gate Decision Record | Tech Lead + QA |
| 12 | Phase 6 | [Execute Test Cycle](phase-6-testing/runbooks/execute-test-cycle.md) | Variable | Test Plan, Cases, Defects, UAT Sign-Off | PO + QA Lead |
| -- | Gate 6 | [Gate Review Procedure](standards/sdlc-framework.md) | 1 day | Gate Decision Record | PO + Tech Lead + QA |

### How Artifacts Flow Between Phases

Each phase produces artifacts that feed into the next:

```
Phase 1                Phase 2              Phase 3              Phase 4              Phase 5         Phase 6
───────                ───────              ───────              ───────              ───────         ───────
Business Case ───────► BRD ────────────────► ADD ────────────────► DDD ──────────────► Source Code ──► Test Cases
Project Charter ─────► SRS ────────────────► ADRs ───────────────► API Specs ─────────►               ► Defects
Stakeholder Register ► RTM (updated at every phase) ─────────────► Data Model ────────►               ► UAT Sign-Off
                       Validation Report     PlantUML diagrams    PlantUML diagrams
```

### For Small Projects (1-2 Developers)

The journey is the same but lighter:
- Phase 1: Problem statement in a Jira epic + verbal sponsor approval (no formal business case)
- Phase 2: User stories with acceptance criteria replace formal BRD; SRS equivalent still required
- Phase 3: Only an ADR if modifying existing architecture; skip if working within existing architecture
- Phase 4: Design in the ticket or code comments; no formal DDD for single-component changes
- Phase 5: Code review + unit tests required (no reduction)
- Phase 6: Manual testing with documented results acceptable; no formal test plan

---

## Learn by Example: Power Atlas

The best way to understand what "done" looks like is to study the **Power Atlas example project** -- a complete set of filled-in artifacts for every phase.

**[View Example Project](example-project/)**

Use it to:
- See the expected quality level for each artifact
- Understand how scaling gates are applied (Power Atlas is a Medium project)
- Trace a requirement from business need (Phase 1) through to test case (Phase 6)
- Study how PlantUML diagrams are structured (see `example-project/diagrams/`)

---

## Phase Gate Reviews

At the end of each phase, a **gate review** determines whether the project can proceed. Understanding this process is critical:

1. **Preparation:** The phase lead assembles all required artifacts and distributes them to reviewers at least 2 business days before the review
2. **Review:** Reviewers evaluate each exit criterion as Met, Partially Met, or Not Met
3. **Decision:** One of four outcomes:
   - **Proceed** -- all exit criteria met
   - **Conditional proceed** -- minor items remain, punch list created
   - **Rework** -- exit criteria not met, stay in current phase
   - **Stop** -- fundamental issues, sponsor makes go/no-go decision

The full gate review procedure and reviewer assignments per phase are in the [SDLC Framework Standard](standards/sdlc-framework.md).

---

## Quick Links

| I need to... | Go to |
|---|---|
| Start a new project | [SDLC Framework Standard](standards/sdlc-framework.md) -- Project Kickoff Checklist |
| Write a business case | [Develop Business Case Runbook](phase-1-business-analysis/runbooks/develop-business-case.md) |
| Write requirements (BRD/SRS) | [Phase 2 Runbooks](phase-2-requirements-engineering/runbooks/) |
| Design system architecture | [Create Architecture Description Runbook](phase-3-system-architecture/runbooks/create-architecture-description.md) |
| Design a component | [Create Detailed Design Runbook](phase-4-design/runbooks/create-detailed-design.md) |
| Implement a feature | [Implement Feature Runbook](phase-5-development/runbooks/implement-feature.md) |
| Run a test cycle | [Execute Test Cycle Runbook](phase-6-testing/runbooks/execute-test-cycle.md) |
| See a complete example | [Power Atlas Example Project](example-project/) |
| Understand roles and responsibilities | [SDLC Framework Standard](standards/sdlc-framework.md) -- RACI Matrix |

---

## Navigation

| Direction | Link |
|-----------|------|
| Parent | [SDLC Framework](README.md) |
| Framework Standard | [standards/sdlc-framework.md](standards/sdlc-framework.md) |
| Example Project | [example-project/](example-project/) |
