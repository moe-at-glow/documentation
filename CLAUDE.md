# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

This is a **documentation-as-code** repository for Glow Power Rental. It contains no application code, no build system, and no dependencies. All content is Markdown (`.md`) files and PlantUML (`.puml`) diagram source files, managed via Git.

The repository houses two topics today:
- **Server Administration** — infrastructure standards, deployment runbooks, architecture guides
- **Software Development Lifecycle (SDLC)** — a 4-phase framework (Define → Design → Build & Verify → Ship & Run) aligned with ISO 12207/29148/42010

## Repository Architecture

Every topic follows the **same 6-category directory structure**:

```
<topic>/
├── standards/              # Rules and conventions (mandatory)
├── runbooks/               # Step-by-step operational procedures
├── guides/                 # Explanations of how things work
├── references/             # Quick-lookup data (ports, inventories, glossaries)
├── templates/              # Copy-paste starting points for artifacts
└── architecture/decisions/ # Architecture Decision Records (ADRs)
```

This pattern is the core organizational principle. When adding a new topic, replicate this structure exactly.

### SDLC Framework Structure

The SDLC topic has additional files beyond the 6 categories:
- `framework.md` — The authoritative 4-phase model, RACI matrix, phase gates, and scaling rules
- `getting-started.md` — Glossary of terms, acronyms, requirement-type prefixes (BR/STK/SYS/SWR)
- `clickup-workflow.md` — ClickUp integration: task naming, statuses (Open → In Progress → Review → Closed), custom fields
- `maintaining-docs.md` — Ownership table, update rules, quarterly/annual review process
- `phases/` — One cheat sheet per phase linking to all relevant deliverables
- `example-project/` — Complete worked example (Power Atlas) showing all artifacts across phases
- `archive/` — Retired docs from the previous 6-phase model; do not reference

### Requirements Hierarchy

Requirements follow a strict 4-level hierarchy with traceability:
**BR** (Business) → **STK** (Stakeholder) → **SYS** (System) → **SWR** (Software)

Each level is tracked via a Requirements Traceability Matrix (RTM).

## Git Workflow

- **Branch naming:** `docs/<topic>/<what>` (e.g., `docs/sdlc/requirements-engineering-framework`)
- **Commit format:** `docs(scope): short description` (e.g., `docs(server): add runbook for SSL renewal`)
- **File naming:** `lowercase-hyphenated.md` — one subject per file
- **ADR naming:** Sequential numbering — `001-use-docker-compose.md`
- **PR process:** One approval required before merge
- **Main branch:** `main`

## Writing Conventions

- **Runbooks** use imperative voice: "Run this command." not "You might want to."
- **Standards** are specific: "Use Ed25519 SSH keys." not "Use strong keys."
- Prefer tables and commands over prose paragraphs.
- All technical diagrams must be PlantUML (`.puml` files in `diagrams/` directories).
- Process or documentation changes must update docs in the same PR — documentation is not a separate task.
- Before creating a new file, check if an existing file can absorb the content.

## Key Files

| File | What it defines |
|------|----------------|
| `software-development-lifecycle/framework.md` | Authoritative 4-phase model, RACI, gates |
| `software-development-lifecycle/getting-started.md` | Glossary, acronyms, requirement prefixes |
| `software-development-lifecycle/clickup-workflow.md` | ClickUp statuses, task naming, board setup |
| `software-development-lifecycle/maintaining-docs.md` | Doc ownership, update triggers, review cycles |
| `CONTRIBUTING.md` | Branch/commit/file-naming rules |

## Common Tasks

```bash
# Create a new topic with the standard directory structure
mkdir -p <topic-name>/{standards,runbooks,guides,references,templates,architecture/decisions}

# Find all references to a file (useful when renaming/moving)
grep -rn "old-filename.md" --include="*.md" .

# Check for broken internal links
grep -roh '\]\([^)]*\.md\)' --include="*.md" . | sort -u | while read link; do
  target=$(echo "$link" | sed 's/.*(\(.*\))/\1/')
  [ ! -f "$target" ] && echo "BROKEN: $target"
done
```
