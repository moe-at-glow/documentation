# Group Permission Matrix

Quick reference for what each group can do. See [Users and Groups Standard](../standards/users-and-groups.md) for full details.

---

## Team Groups

| Group | Sudo | Deploy Apps | Restart Services | View Logs | Edit Config | Access Secrets |
|-------|------|------------|-----------------|-----------|-------------|----------------|
| `sudo` | Yes | Yes | Yes | Yes | Yes | Yes |
| `server-admin` | No | Yes | Yes | Yes | Yes | Yes |
| `developers` | No | Yes | Yes | Yes | No | No |
| `readonly` | No | No | No | Yes | No | No |

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
