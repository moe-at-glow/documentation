# Backup and Recovery

What to back up, how often, and how to restore.

---

## What to Back Up

| Data | Location | Frequency | Retention |
|------|----------|-----------|-----------|
| Application data | `/opt/<app>/data/` | Daily | 30 days |
| Application config + .env | `/opt/<app>/config/`, `.env` | On change | 90 days |
| Databases | Dump via `pg_dump`, `mysqldump` | Daily | 30 days |
| TLS certificates | `/etc/letsencrypt/` | Weekly | 90 days |
| Nginx configs | `/etc/nginx/` | On change | 90 days |
| systemd unit files | `/etc/systemd/system/*.service` | On change | 90 days |
| Central documentation | `/srv/docs/` | Git push | Forever |

## What NOT to Back Up

| Data | Why |
|------|-----|
| `/tmp/`, `/var/cache/` | Regenerated automatically |
| `/home/<user>/` | Personal config, users manage their own |
| Docker images | Pulled from registries |
| Logs | Useful but replaceable; back up only for compliance |

---

## Backup Locations

```
/opt/<app>/bin/backup.sh            # Per-app backup script
/srv/backups/                       # Local staging
/srv/backups/<app>-YYYY-MM-DD.tar.gz
```

Offsite: sync `/srv/backups/` to external storage (S3, remote server, etc.).

---

## Example Backup Script

```bash
#!/bin/bash
# /opt/<app-name>/bin/backup.sh
set -euo pipefail

APP="<app-name>"
DATE=$(date +%Y-%m-%d)
BACKUP_DIR="/srv/backups"
BACKUP_FILE="${BACKUP_DIR}/${APP}-${DATE}.tar.gz"

# Create backup
tar czf "$BACKUP_FILE" \
    /opt/${APP}/data/ \
    /opt/${APP}/config/ \
    /opt/${APP}/.env

# Remove backups older than 30 days
find "$BACKUP_DIR" -name "${APP}-*.tar.gz" -mtime +30 -delete

echo "Backup complete: $BACKUP_FILE"
```

---

## Restoring from Backup

```bash
# Stop the service
sudo systemctl stop <app-name>

# Extract backup
sudo tar xzf /srv/backups/<app-name>-YYYY-MM-DD.tar.gz -C /

# Restart the service
sudo systemctl start <app-name>

# Verify
sudo systemctl status <app-name>
```

---

## Testing Restores

**Test restores monthly.** A backup that cannot be restored is not a backup.

```
[ ] Pick a random backup from the last 30 days
[ ] Restore to a test environment (never production)
[ ] Verify the application starts and data is intact
[ ] Document any issues found
```
