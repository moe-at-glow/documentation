# Naming Conventions

Consistent naming across users, groups, services, files, and directories.

---

## Summary Table

| Entity | Convention | Examples |
|--------|-----------|---------|
| Human users | First initial + last name, lowercase | `jsmith`, `mhazime` |
| Service accounts | App name, lowercase | `telemetry`, `n8n`, `grafana` |
| Team groups | Descriptive, lowercase, hyphenated | `server-admin`, `developers` |
| App groups | `<app>-<role>` | `telemetry-admin`, `n8n-operator` |
| App directories | `/opt/<app-name>/`, lowercase, hyphenated | `/opt/pdf-server/`, `/opt/n8n/` |
| Service files | `<app-name>.service`, matches `/opt/` dir name | `pdf-server.service`, `n8n.service` |
| Nginx vhosts | Domain name | `app.example.com` |
| Web roots | `/var/www/<domain>/` | `/var/www/app.example.com/` |
| Documentation files | Lowercase, hyphenated `.md` | `deploy-application.md` |
| Environment files | `.env` inside app directory | `/opt/<app>/.env` |
| Backup files | `<app>-YYYY-MM-DD.tar.gz` | `telemetry-2026-03-01.tar.gz` |
| Log files | `<app>.log` or via journald | `journalctl -u telemetry` |
| ADR files | `NNN-short-title.md` | `001-use-docker-compose.md` |

## Rules

- **Always lowercase.** No `MyApp`, no `PDF_Server`.
- **Hyphens, not underscores.** `pdf-server`, not `pdf_server`.
- **Match names across the stack.** If the app is `pdf-server`, then the directory is `/opt/pdf-server/`, the service is `pdf-server.service`, the user is `pdf-server`, the groups are `pdf-server-admin` / `pdf-server-operator`.
- **Be specific.** `telemetry-ingester` is better than `app1`.
- **No spaces or special characters.** Ever.
