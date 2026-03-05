# Runbook: Deploy and Operate

## 1. Purpose

This runbook provides step-by-step procedures for deploying releases to production and maintaining ongoing operations. It is the companion runbook for [Phase 4: Ship & Run](../phases/4-ship-and-run.md) and should be followed by any team member performing a deployment or responding to a production incident.

---

## 2. Prerequisites

Before starting a deployment, confirm all of the following:

- [ ] UAT signed off by Product Owner
- [ ] All critical and high-severity defects resolved (see [Defect Severity](../references/defect-severity.md))
- [ ] Medium/low defects deferred only with Product Owner acceptance
- [ ] Deployment diagram (D3) matches the target production environment
- [ ] Release branch or tag is ready in version control (see [Coding & Git Standard](../standards/coding-and-git.md))
- [ ] Team member performing deployment has access to the production server

---

## 3. Pre-Deployment Checklist

Complete every item before executing the deployment procedure.

- [ ] **Verify environment variables** -- Compare `.env.example` against production `.env`; confirm all new variables are set with correct values
- [ ] **Run database migration on backup/staging** -- Execute migrations against a copy of the production database to confirm they apply cleanly
- [ ] **Take database backup** -- Run `pg_dump` (or equivalent) and verify the backup file is valid and stored off-server
- [ ] **Verify SSL certificates** -- Run `certbot certificates` or check UptimeRobot; confirm expiry is > 14 days away
- [ ] **Confirm rollback procedure** -- Identify the previous release tag and confirm the rollback steps in Section 5 are current
- [ ] **Check disk space** -- Confirm the server has sufficient disk space for the deployment (`df -h`)
- [ ] **Notify team** -- Post in the team channel that a deployment is being prepared

---

## 4. Deployment Procedure

Execute these steps in order. If any step fails, stop and evaluate whether to proceed or rollback.

### Step 1: Notify Team Deployment Starting

Post in the team Slack/Teams channel:

```
Deployment starting: [app-name] v[version]
Deploying: [your name]
Expected duration: ~15 minutes
```

### Step 2: Tag the Release

Follow [Coding & Git Standard](../standards/coding-and-git.md) for tagging conventions.

```bash
git tag -a v[version] -m "release: v[version] — [brief summary]"
git push origin v[version]
```

Use conventional commit messages in the tag annotation.

### Step 3: Pull Latest on Server

SSH into the server and deploy:

```bash
ssh deploy@your-server
cd /var/www/your-app
git fetch --all --tags
git checkout v[version]
npm install --production   # or equivalent dependency install
```

### Step 4: Run Database Migrations

```bash
npm run migrate            # or equivalent migration command
```

Verify migration output shows no errors. If a migration fails, do NOT proceed -- evaluate rollback.

### Step 5: Restart Application

```bash
pm2 restart your-app       # or: systemctl restart your-app
```

Confirm the process is running:

```bash
pm2 status                 # or: systemctl status your-app
```

### Step 6: Run Smoke Tests

Execute the smoke test suite against production:

- [ ] Application responds on the expected URL (HTTP 200)
- [ ] Login flow works
- [ ] Core business workflow completes end-to-end
- [ ] API health endpoint returns healthy status
- [ ] No 5xx errors in the last 2 minutes of logs

### Step 7: Verify Monitoring

- [ ] Infrastructure monitoring shows the server is healthy (CPU, memory, disk)
- [ ] UptimeRobot confirms the application is UP
- [ ] Application logs show no errors (`journalctl -u your-app --since "2 minutes ago"` or `pm2 logs`)

### Step 8: Notify Team Deployment Complete

Post in the team channel:

```
Deployment complete: [app-name] v[version]
Status: SUCCESS
Release notes: [link to release notes]
Monitoring for the next 30 minutes.
```

---

## 5. Rollback Procedure

### When to Rollback

Initiate a rollback if any of the following occur after deployment:

- **P1 or P2 defect** discovered in production (see [Defect Severity](../references/defect-severity.md))
- **Data corruption** detected or suspected
- **No fix available** within 30 minutes of identifying the issue
- **Core business workflow** is broken

### Rollback Steps

1. **Notify** -- Post in the team channel: "Rollback initiated for v[version]. Reason: [brief description]."
2. **Revert application** -- Check out the previous release tag and restart:
   ```bash
   cd /var/www/your-app
   git checkout v[previous-version]
   npm install --production
   pm2 restart your-app
   ```
3. **Restore database if needed** -- If migrations caused data issues:
   ```bash
   pg_restore --clean --dbname=your_db /path/to/backup.sql
   ```
4. **Verify** -- Run the same smoke tests from Step 6 against the rolled-back version
5. **Communicate** -- Notify the team and stakeholders that the rollback is complete
6. **Document** -- Log the rollback reason and outcome; schedule a post-mortem

---

## 6. Post-Deployment Monitoring

### First 30 Minutes

The deployer remains online and actively monitors:

- [ ] Watch application logs for errors (`pm2 logs --lines 100` or `journalctl -f`)
- [ ] Check error rates -- zero 5xx responses expected
- [ ] Verify response times are within normal range
- [ ] Confirm no anomalies in CPU/memory graphs

### First 24 Hours

- [ ] Review error logs at end of business day
- [ ] Check performance metrics (response time, throughput)
- [ ] Confirm database connection pool is stable
- [ ] Verify no user-reported issues in the team channel

### First Week

- [ ] Collect user feedback on new features (informal -- Slack or standup)
- [ ] Monitor for edge-case defects that only appear with real usage patterns
- [ ] Confirm no resource usage trends (memory leaks, disk growth)
- [ ] Close the release in the project tracker

---

## 7. Release Notes

Use this template for every production release. Post in the team channel and attach to the project tracker.

```markdown
## Release v[X.Y.Z] -- [YYYY-MM-DD]

### Deployed By
[Name]

### New Features
- [Feature description] ([ticket-id])

### Bug Fixes
- [Fix description] ([ticket-id])

### Breaking Changes
- [Description and migration steps, if any]

### Database Migrations
- [Migration description, if any]

### Known Issues
- [Description and workaround, if any]

### Configuration Changes
- [New or changed environment variables, if any]
```

---

## 8. Operational Procedures

### Daily

- [ ] Check monitoring dashboard
- [ ] Review application error logs
- [ ] Respond to any alerts within SLA (see Section 9)

### Weekly

- [ ] Review open defects and triage new ones
- [ ] Verify backup integrity -- confirm latest backup exists and is valid
- [ ] Check disk usage trends

### Monthly

- [ ] Apply OS and runtime security patches (`apt update && apt upgrade`)
- [ ] Review resource utilization -- assess whether the server needs resizing
- [ ] Rotate application logs if not automated
- [ ] Renew or verify SSL certificates

### Quarterly

- [ ] Update application dependencies (npm audit / npm update)
- [ ] Capacity planning -- review growth trends and plan infrastructure changes
- [ ] Review and update this runbook if procedures have changed
- [ ] Conduct an operations review with the Tech Lead and Product Owner

---

## 9. Incident Response

### Severity Levels and Response Times

| Severity | Description | Response Time | Resolution Target |
|----------|-------------|---------------|-------------------|
| P1 -- Critical | Application down or data corruption | 15 minutes | 1 hour |
| P2 -- High | Core feature broken, no workaround | 30 minutes | 4 hours |
| P3 -- Medium | Feature degraded, workaround exists | 4 hours | Next business day |
| P4 -- Low | Minor issue, cosmetic, or enhancement | Next business day | Next sprint |

For detailed severity definitions, see [Defect Severity](../references/defect-severity.md).

### Incident Communication Template

Post in the team channel when an incident is identified:

```
INCIDENT: [P1/P2/P3/P4] — [brief description]
Detected: [time]
Impact: [what is affected]
Assigned to: [name]
Status: INVESTIGATING / MITIGATED / RESOLVED
Next update: [time]
```

Update the thread every 30 minutes for P1/P2 until resolved.

### Post-Mortem Process

Conduct a post-mortem for every P1 and P2 incident within 3 business days:

1. **Timeline** -- What happened, when, and in what order
2. **Root cause** -- Why did it happen (use 5-whys if needed)
3. **Impact** -- Who was affected and for how long
4. **Resolution** -- What was done to fix it
5. **Action items** -- What will we change to prevent recurrence (assign owners and due dates)

Document the post-mortem in the project tracker and review action items in the next sprint planning.

---

## 10. Outputs Checklist

Confirm all outputs are complete after a deployment:

- [ ] Application deployed and accessible in production
- [ ] Smoke tests passing
- [ ] Monitoring alerts configured and active
- [ ] Release notes published and shared with the team
- [ ] Rollback procedure confirmed and documented
- [ ] Team notified of deployment outcome
- [ ] Post-deployment monitoring period completed (30 min minimum)
- [ ] Any incidents logged and post-mortems scheduled

---

## Cross-References

| Document | Link |
|----------|------|
| Phase 4: Ship & Run | [phases/4-ship-and-run.md](../phases/4-ship-and-run.md) |
| Coding & Git Standard | [standards/coding-and-git.md](../standards/coding-and-git.md) |
| Defect Severity Reference | [references/defect-severity.md](../references/defect-severity.md) |
| SDLC Framework | [framework.md](../framework.md) |
| Defect Report Template | [templates/defect-report.md](../templates/defect-report.md) |
| Test Summary Report Template | [templates/test-summary-report.md](../templates/test-summary-report.md) |
| UAT Sign-Off Template | [templates/uat-sign-off.md](../templates/uat-sign-off.md) |
