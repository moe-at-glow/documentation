# Contributing to Documentation

How to add, edit, and maintain documentation in this repository.

---

## Workflow

1. **Create a branch:** `git checkout -b docs/<topic>/<what>`
2. **Make your changes** in the appropriate directory.
3. **Commit:** `git commit -m "docs: <what you changed>"`
4. **Push:** `git push -u origin docs/<topic>`
5. **Open a pull request** for review.
6. **Merge** after at least one approval.

## Where Does It Go?

### Pick the topic directory first

Each major subject has its own top-level directory (e.g., `server-administration/`, `docker/`, `apis/`). If none exists for your subject, create one — see the root README for how.

### Then pick the subdirectory

| I want to... | Put it in `<topic>/` |
|--------------|-----------|
| Explain how something works | `guides/` |
| Define a rule or convention | `standards/` |
| Write step-by-step operational instructions | `runbooks/` |
| Record a factual value (port, IP, account) | `references/` |
| Provide a copy-paste starting point | `templates/` |
| Document a design decision | `architecture/decisions/` |

**Example:** A runbook for deploying apps goes in `server-administration/runbooks/deploy-application.md`.

## File Naming

- **Lowercase, hyphenated:** `deploy-application.md`, not `Deploy Application.md`
- **One topic per file:** Don't combine SSH and firewall in one document.
- **ADRs are numbered:** `001-use-docker-compose.md`, `002-choose-nginx.md`

## Writing Style

- **Runbooks are imperative.** "Run this command." Not "You might want to."
- **Standards are specific.** "Use Ed25519 SSH keys." Not "Use strong keys."
- **Be concise.** Tables over paragraphs. Commands over descriptions.
- **Keep it current.** Update docs when you change systems.

## Commit Message Format

```
docs: <short description>

Examples:
docs(server): add runbook for SSL certificate renewal
docs(server): update port registry with new grafana port
docs(docker): add guide for multi-stage builds
docs: fix broken link in server architecture guide
```
