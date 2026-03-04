# Runbook: Onboard a New User

Step-by-step procedure to add a new team member to a server.

---

## Prerequisites

- You have sudo access on the target server.
- The new user has generated an SSH key pair and given you their **public** key.
  - Key must be in **OpenSSH format** (single line starting with `ssh-ed25519` or `ssh-rsa`).
  - PuTTY/SSH2 format (`---- BEGIN SSH2 PUBLIC KEY ----`) will **not work** — convert with `ssh-keygen -i -f key.pub`.
  - Preferred key type: **Ed25519** (`ssh-keygen -t ed25519 -C "<username>"`).
- You know which team group and application groups they need.

---

## Steps

### 1. Create the user account

```bash
sudo useradd --create-home \
    --shell /bin/bash \
    --comment "<Full Name> - <Role>" \
    <username>

# Set temporary password (forces change on first login)
sudo passwd <username>
sudo chage --lastday 0 <username>
```

### 2. Assign to groups

```bash
# Team group (pick one)
sudo usermod -aG developers <username>    # Most developers
sudo usermod -aG server-admin <username>  # System administrators
sudo usermod -aG readonly <username>      # Read-only access

# Application groups (as needed)
sudo usermod -aG <app>-admin <username>
sudo usermod -aG <app>-operator <username>

# Docker access (only if needed)
sudo usermod -aG docker <username>

# Sudo access (only if absolutely needed)
sudo usermod -aG sudo <username>
```

> **Note:** Members of `developers` automatically get limited sudo (service management, package installation, app directory management) via `/etc/sudoers.d/developers`. No additional setup needed. See [Users and Groups Standard](../standards/users-and-groups.md#limited-sudo-for-developers).

### 3. Install SSH public key

```bash
sudo mkdir -p /home/<username>/.ssh
sudo chmod 700 /home/<username>/.ssh

sudo sh -c 'echo "<their-public-key>" > /home/<username>/.ssh/authorized_keys'

sudo chmod 600 /home/<username>/.ssh/authorized_keys
sudo chown -R <username>:<username> /home/<username>/.ssh
```

### 4. Verify

```bash
# Check group membership
groups <username>

# Check home directory
ls -la /home/<username>/

# Ask the user to test SSH access from their machine
# ssh <username>@<server-ip>
```

### 5. Share documentation

Tell the new user to read:

1. `/srv/docs/README.md` — Server standards overview
2. `/srv/docs/standards/` — All standards they must follow
3. `/opt/<app>/README.md` — Documentation for the apps they'll work on

---

## Checklist

```
[ ] User account created with personal username
[ ] Temporary password set with forced change
[ ] SSH public key installed
[ ] Added to correct team group
[ ] Added to correct application groups
[ ] Docker access (if needed)
[ ] Sudo access (if needed and approved)
[ ] User can SSH in with their key
[ ] User has read the documentation
[ ] User knows who to contact for access issues
[ ] User added to team communication channels
```
