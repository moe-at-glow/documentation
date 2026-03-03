# Users and Groups Standard

How to structure user accounts, service accounts, and group-based permissions on a server.

---

## Principles

- Every **person** gets a personal user account — never share accounts.
- Every **application** gets a dedicated service account — never run apps as root.
- **Groups** control access — never grant permissions to individual users.
- **Least privilege** — give the minimum access needed for the role.

---

## Group Hierarchy

### Team Groups (human users)

| Group | Purpose | Who Gets Added |
|-------|---------|---------------|
| `sudo` | Full administrative access | Minimize. Only senior admins. |
| `server-admin` | Server-wide admin tasks | System administrators |
| `developers` | Deploy and manage applications | Developers, DevOps |
| `readonly` | View logs and documentation | Support, monitoring, auditors |

### Application Groups (per application)

| Group | Purpose | Members |
|-------|---------|---------|
| `<app>-admin` | Full control of the application | App owner, senior devs |
| `<app>-operator` | Run, restart, deploy the application | Developers, CI/CD |
| `<app>-readonly` | Read logs and config | Support, monitoring |

### System Groups

| Group | Purpose |
|-------|---------|
| `www-data` | Web server (nginx/apache) process group |
| `docker` | Docker socket access |
| `ssl-cert` | Access to TLS certificates |

---

## Permission Matrix

| Group | Deploy | Restart | View Logs | Edit Config | Access Secrets |
|-------|--------|---------|-----------|-------------|----------------|
| `<app>-admin` | Yes | Yes | Yes | Yes | Yes |
| `<app>-operator` | Yes | Yes | Yes | No | No |
| `<app>-readonly` | No | No | Yes | No | No |
| `server-admin` | Yes | Yes | Yes | Yes | Yes |
| `developers` | Yes | Yes | Yes | No | No |
| `readonly` | No | No | Yes | No | No |

---

## Creating Groups

```bash
# Team groups (one-time server setup)
sudo groupadd server-admin
sudo groupadd developers
sudo groupadd readonly

# Application groups (repeat for each application)
sudo groupadd <app>-admin
sudo groupadd <app>-operator
sudo groupadd <app>-readonly
```

## Creating Human Users

```bash
sudo useradd --create-home \
    --shell /bin/bash \
    --comment "Jane Smith - Backend Developer" \
    jsmith
```

## Creating Service Accounts

```bash
# System user: no login, no home directory
sudo useradd --system \
    --no-create-home \
    --shell /usr/sbin/nologin \
    --comment "<App Name> service account" \
    <app-name>

# Add to its own admin group
sudo usermod -aG <app>-admin <app-name>
```

## Assigning Users to Groups

```bash
# Add to team group
sudo usermod -aG developers jsmith

# Add to application groups
sudo usermod -aG telemetry-operator jsmith
sudo usermod -aG n8n-admin jsmith

# Docker access (only if needed)
sudo usermod -aG docker jsmith
```

## Verifying

```bash
# Check a user's groups
groups jsmith

# Check who is in a group
getent group developers

# List all human users (UID >= 1000)
awk -F: '$3 >= 1000 {print $1}' /etc/passwd

# List all service accounts (UID 100-999)
awk -F: '$3 >= 100 && $3 < 1000 {print $1}' /etc/passwd
```
