# Group Permission Matrix

Quick reference for what each group can do. See [Users and Groups Standard](../standards/users-and-groups.md) for full details.

---

## Team Groups

| Group | Sudo | Deploy Apps | Restart Services | View Logs | Edit Config | Access Secrets |
|-------|------|------------|-----------------|-----------|-------------|----------------|
| `sudo` | Full | Yes | Yes | Yes | Yes | Yes |
| `server-admin` | No | Yes | Yes | Yes | Yes | Yes |
| `developers` | Limited | Yes | Yes | Yes | No | No |
| `readonly` | No | No | No | Yes | No | No |

## Developers — Limited Sudo

Members of the `developers` group receive passwordless sudo for the following commands only (via `/etc/sudoers.d/developers`):

| Category | Commands |
|----------|----------|
| **Service management** | `systemctl start/stop/restart/enable/disable/status *`, `systemctl daemon-reload` |
| **Logs** | `journalctl *` |
| **Package installation** | `apt install *`, `apt update`, `apt-get install *`, `apt-get update` |
| **App directories** | `mkdir -p /opt/*`, `chown * /opt/*`, `chmod * /opt/*` |
| **Service accounts** | `useradd --system *`, `groupadd *` |
| **Nginx** | `nginx -t`, `systemctl reload nginx` |
| **TLS certificates** | `certbot *` |

Developers **cannot**: manage system users, edit SSH config, modify firewall rules, or access `/etc/sudoers`.

## Application Groups

| Group | Deploy | Restart | View Logs | Edit Config | Access Secrets |
|-------|--------|---------|-----------|-------------|----------------|
| `<app>-admin` | Yes | Yes | Yes | Yes | Yes |
| `<app>-operator` | Yes | Yes | Yes | No | No |
| `<app>-readonly` | No | No | Yes | No | No |

## System Groups

| Group | Purpose | Grant To |
|-------|---------|----------|
| `www-data` | Nginx/Apache process | Web server only |
| `docker` | Docker socket access | Developers who need containers |
| `ssl-cert` | TLS certificate access | Services needing certs |
