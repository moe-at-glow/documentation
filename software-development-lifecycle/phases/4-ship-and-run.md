# Phase 4: Ship & Run (Deployment + Operations)

> **Purpose:** Get the verified build into production safely and keep it running reliably. This phase covers deployment procedures, release management, monitoring, and ongoing operational support.

---

## Entry Criteria

- [ ] Phase 3 (Build & Verify) gate passed
- [ ] All critical/high defects resolved
- [ ] UAT signed off
- [ ] Deployment diagram (D3) matches target environment
- [ ] Rollback procedure documented and tested

---

## Deliverables

| # | Document | Template | Required | Runbook |
|---|----------|----------|----------|---------|
| 1 | Deployment Checklist | See [Deployment Checklist](#deployment-checklist) below | All projects | [runbooks/deploy-and-operate.md](../runbooks/deploy-and-operate.md) |
| 2 | Release Notes | See [Release Notes Template](#release-notes-template) below | All projects | [runbooks/deploy-and-operate.md](../runbooks/deploy-and-operate.md) |
| 3 | Monitoring Setup | See [Monitoring Setup](#monitoring-setup) below | All projects | [runbooks/deploy-and-operate.md](../runbooks/deploy-and-operate.md) |
| 4 | Rollback Procedure | See [Rollback Procedure](#rollback-procedure) below | All projects | [runbooks/deploy-and-operate.md](../runbooks/deploy-and-operate.md) |

> **Note:** Phase 4 deliverables use inline templates (below) rather than separate template files because deployment artifacts are environment-specific and maintained directly in the deploy runbook.

**PlantUML diagrams:** Deployment diagram (D3) should already exist from Phase 2. Verify it matches actual deployment.

---

## Deployment Checklist

- [ ] Database migrations tested on staging/backup
- [ ] Environment variables configured
- [ ] SSL certificates valid
- [ ] Backup taken before deployment
- [ ] Deploy to staging first (if available)
- [ ] Smoke tests pass on staging
- [ ] Deploy to production
- [ ] Smoke tests pass on production
- [ ] Monitor logs for 30 minutes post-deploy
- [ ] Notify team of successful deployment

---

## Release Notes Template

```
## Release [version] — [date]

### New Features
- [Feature description] ([CU-xxxx])

### Bug Fixes
- [Fix description] ([CU-xxxx])

### Breaking Changes
- [Description and migration steps]

### Known Issues
- [Description and workaround]
```

---

## Monitoring Setup

| What | Tool | Alert Threshold |
|------|------|----------------|
| Server uptime | Infrastructure monitoring / UptimeRobot | Down > 1 min |
| CPU usage | Infrastructure monitoring | > 80% for 5 min |
| Memory usage | Infrastructure monitoring | > 85% for 5 min |
| Disk usage | Infrastructure monitoring | > 80% |
| Application errors | Application logs (journalctl / PM2) | Any 5xx errors |
| SSL expiry | UptimeRobot / certbot --dry-run | < 14 days |
| Database connections | Application health endpoint | Pool exhaustion |

---

## Rollback Procedure

1. **Identify** — Confirm the issue is caused by the new deployment
2. **Decide** — Rollback if: P1/P2 defect, data corruption risk, or no quick fix within 30 min
3. **Execute** — `git checkout [previous-tag] && [deploy command]` or restore from backup
4. **Verify** — Run smoke tests on rolled-back version
5. **Communicate** — Notify team and stakeholders
6. **Post-mortem** — Document what went wrong in the next sprint retrospective

---

## Key Activities

1. **Pre-deployment** — Final build, environment config, backup
2. **Deployment** — Execute deployment, run smoke tests
3. **Post-deployment** — Monitor, verify, communicate
4. **Operations** — Monitor uptime, respond to incidents, apply security patches
5. **Maintenance** — Regular backups, log rotation, dependency updates

---

## Standards

- [Coding & Git Standard](../standards/coding-and-git.md) — for release tagging and conventional commits

---

## Roles

| Role | Deployment Responsibility | Operations Responsibility |
|------|--------------------------|--------------------------|
| Tech Lead | Owns deployment plan, makes go/no-go call | Reviews monitoring alerts, leads incident response |
| Developer | Executes deployment steps, runs smoke tests | Investigates production issues, applies hotfixes |
| QA Lead | Verifies deployment checklist, runs regression | Validates post-deployment behavior |
| Product Owner | Approves release notes, gives final go/no-go | Reviews user-reported issues |

---

## Top 5 Pitfalls

| # | Pitfall | Warning Sign | Fix |
|---|---------|-------------|-----|
| 1 | **No rollback plan** | "We'll figure it out if something breaks" | Always have a tested rollback procedure before deploying |
| 2 | **Skipping staging** | Direct deploy to production | Test on a staging copy first (separate Docker container or staging server) |
| 3 | **Missing environment variables** | App crashes on startup with undefined config | Use .env.example and verify all vars are set before deploy |
| 4 | **No post-deploy monitoring** | Issues discovered by users, not team | Watch logs for at least 30 minutes after deployment |
| 5 | **Database migrations without backup** | Data loss when migration fails | Always backup the database before running migrations |

---

## Exit Criteria / Phase Gate

- [ ] Application deployed and accessible
- [ ] Monitoring alerts configured
- [ ] Smoke tests passing in production
- [ ] Release notes published
- [ ] Rollback procedure documented
- [ ] Team notified of deployment

---

## Scaling Notes

| Project Size | Skip/Simplify |
|-------------|---------------|
| Small (< 2 weeks) | Manual deploy OK. Monitoring = basic uptime check. |
| Medium (2-8 weeks) | Scripted deploy. Infrastructure monitoring + application health check. |
| Large (8+ weeks) | CI/CD pipeline. Full monitoring stack. Automated rollback. |

---

## Operational Cadence

| Frequency | Activity |
|-----------|----------|
| Daily | Check monitoring dashboard, review error logs |
| Weekly | Review open defects, check backup integrity |
| Monthly | Apply security patches, review resource usage |
| Quarterly | Dependency updates, capacity planning |

---

## Previous Phase

← [Phase 3: Build & Verify](3-build-and-verify.md)
