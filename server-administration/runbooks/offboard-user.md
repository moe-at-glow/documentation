# Runbook: Offboard a User

Step-by-step procedure to remove a team member's access from a server.

---

## Steps

### 1. Disable the account immediately

```bash
# Lock the account and set expiry to prevent login
sudo usermod --lock --expiredate 1 <username>
```

### 2. Remove SSH access

```bash
sudo rm /home/<username>/.ssh/authorized_keys
```

### 3. Review group membership

```bash
groups <username>
# Remove from all groups if needed
sudo gpasswd -d <username> developers
sudo gpasswd -d <username> <app>-admin
sudo gpasswd -d <username> docker
# ... repeat for each group
```

### 4. Check for running processes

```bash
ps -u <username>
# Kill any running processes
sudo pkill -u <username>
```

### 5. Review cron jobs

```bash
sudo crontab -u <username> -l
# Remove if any
sudo crontab -u <username> -r
```

### 6. Transfer ownership of important files

```bash
# Find files owned by the user outside their home
sudo find / -user <username> -not -path "/home/<username>/*" -ls 2>/dev/null

# Change ownership to appropriate user/group
sudo chown -R root:<appropriate-group> /path/to/files
```

### 7. Delete the account (after 30-day grace period)

```bash
# Remove user and their home directory
sudo userdel --remove <username>
```

---

## Checklist

```
[ ] Account locked and expired
[ ] SSH authorized_keys removed
[ ] Removed from all groups
[ ] Running processes killed
[ ] Cron jobs reviewed and removed
[ ] File ownership transferred
[ ] Account deleted (after grace period)
[ ] Team documentation updated
[ ] Any shared passwords/secrets rotated
```
