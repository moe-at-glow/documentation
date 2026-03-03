# Server Architecture Overview

How our servers are structured and why.

---

## Design Principles

1. **One application, one directory.** Every app lives in `/opt/<app-name>/` with its own config, data, and logs.
2. **One application, one service account.** Apps never run as root or as a human user.
3. **Group-based access control.** Permissions are granted through groups, never to individual users.
4. **Reverse proxy everything.** All web traffic enters through Nginx on ports 80/443. Applications bind to localhost only.
5. **systemd for all services.** No screen sessions, no nohup, no background processes.
6. **Secrets in .env files.** Not in code, not in systemd units, not in home directories.

---

## Traffic Flow

```
Internet
    │
    ▼
┌─────────┐
│ Firewall │  (ufw: deny all, allow 22/80/443)
│  (ufw)   │
└────┬─────┘
     │
     ▼
┌─────────┐
│  Nginx   │  Port 80 → 301 redirect to 443
│  (443)   │  Port 443 → TLS termination + reverse proxy
└────┬─────┘
     │
     ├──► localhost:3000  (App A)
     ├──► localhost:3001  (App B)
     ├──► localhost:8080  (App C)
     └──► /var/www/<domain>/  (static files)
```

## Directory Layout

See [Server Directory Layout Standard](../standards/server-directory-layout.md) for the full directory tree.

```
/opt/<app>/          Application code, config, data
/var/www/<domain>/   Static web assets (served by Nginx)
/etc/nginx/          Nginx configuration
/etc/systemd/system/ Service unit files
/srv/docs/           Central documentation
/srv/backups/        Backup staging
/home/<user>/        Personal files only
```

## Permissions Model

See [Users and Groups Standard](../standards/users-and-groups.md) and [Group Permission Matrix](../references/group-permission-matrix.md).

```
Human Users ──► Team Groups ──► Access via group permissions
                                    │
Applications ──► Service Accounts ──► App Groups ──► File/directory ACLs
```
