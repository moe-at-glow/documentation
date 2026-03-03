# Template: Application README

Copy this file to `/opt/<app-name>/README.md` and fill in the sections.

---

```markdown
# <Application Name>

## Overview

Brief description of what this application does and why it exists.

## Architecture

- **Runtime:** (e.g., Node.js 20, Python 3.12, Docker Compose)
- **Port:** (e.g., 3000)
- **Database:** (e.g., PostgreSQL on port 5432, or "none")
- **Dependencies:** (e.g., requires mosquitto running, depends on Redis)
- **Reverse proxy:** (e.g., proxied via Nginx at https://app.example.com)

## Access

| Item | Value |
|------|-------|
| URL | https://app.example.com |
| Service account | `<app-name>` |
| Admin group | `<app-name>-admin` |
| Operator group | `<app-name>-operator` |
| systemd service | `<app-name>.service` |

## Deployment

<!-- Step-by-step instructions to deploy or update -->

1. SSH into the server.
2. Pull the latest changes: `cd /opt/<app-name> && sudo git pull`
3. Rebuild (if needed): `sudo docker compose build`
4. Restart: `sudo systemctl restart <app-name>`
5. Verify: `sudo systemctl status <app-name>`

## Configuration

<!-- What environment variables and config files are needed -->

Environment variables are in `/opt/<app-name>/.env`:

| Variable | Description | Example |
|----------|------------|---------|
| `PORT` | Application port | `3000` |
| `DB_HOST` | Database hostname | `localhost` |
| `DB_PASS` | Database password | (secret) |

## Troubleshooting

<!-- Common issues and resolutions -->

**Service won't start:**
```bash
sudo journalctl -u <app-name> --since "10 minutes ago"
```

**Port already in use:**
```bash
sudo ss -tlnp | grep <port>
```

## Logs

```bash
# Live logs
sudo journalctl -u <app-name> -f

# Last hour
sudo journalctl -u <app-name> --since "1 hour ago"
```

## Backup and Restore

```bash
# Backup
sudo /opt/<app-name>/bin/backup.sh

# Restore
sudo systemctl stop <app-name>
sudo tar xzf /srv/backups/<app-name>-YYYY-MM-DD.tar.gz -C /
sudo systemctl start <app-name>
```
```
