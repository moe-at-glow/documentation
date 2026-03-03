# Runbook: Provision a New Server

Step-by-step procedure to set up a new Linux server from scratch.

---

## Phase 1: Base System

```bash
# Update the system
sudo apt update && sudo apt upgrade -y

# Set hostname
sudo hostnamectl set-hostname <server-name>

# Set timezone
sudo timedatectl set-timezone <timezone>
# Example: sudo timedatectl set-timezone Asia/Dubai

# Verify
hostnamectl
timedatectl
```

## Phase 2: Security Foundation

### 2.1 Create the first admin user

```bash
sudo useradd --create-home --shell /bin/bash --comment "Admin Name" <username>
sudo usermod -aG sudo <username>
sudo passwd <username>
```

### 2.2 Install SSH key for admin

```bash
sudo mkdir -p /home/<username>/.ssh
sudo chmod 700 /home/<username>/.ssh
sudo sh -c 'echo "<public-key>" > /home/<username>/.ssh/authorized_keys'
sudo chmod 600 /home/<username>/.ssh/authorized_keys
sudo chown -R <username>:<username> /home/<username>/.ssh
```

### 2.3 Harden SSH

Edit `/etc/ssh/sshd_config`:

```
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
MaxAuthTries 3
LoginGraceTime 30
ClientAliveInterval 300
ClientAliveCountMax 2
AllowGroups server-admin developers
X11Forwarding no
```

```bash
# Test before restarting (prevent lockout)
sudo sshd -t
sudo systemctl restart ssh
```

### 2.4 Set up firewall

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp comment "SSH"
sudo ufw allow 80/tcp comment "HTTP"
sudo ufw allow 443/tcp comment "HTTPS"
sudo ufw enable
sudo ufw status verbose
```

### 2.5 Install fail2ban

```bash
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

### 2.6 Enable automatic security updates

```bash
sudo apt install unattended-upgrades -y
sudo dpkg-reconfigure -plow unattended-upgrades
```

## Phase 3: Groups and Users

```bash
# Create team groups
sudo groupadd server-admin
sudo groupadd developers
sudo groupadd readonly

# Add admin to server-admin
sudo usermod -aG server-admin <username>
```

Then onboard each team member per [Onboard a New User](onboard-user.md).

## Phase 4: Standard Directories

```bash
# Central documentation
sudo mkdir -p /srv/docs
sudo mkdir -p /srv/backups

# Initialize docs as a git clone (or symlink)
cd /srv/docs
sudo git clone <documentation-repo-url> .
# Or: sudo git init && sudo git remote add origin <url>

# Set permissions
sudo chown -R root:server-admin /srv/docs
sudo chmod -R 775 /srv/docs
sudo chown root:server-admin /srv/backups
sudo chmod 770 /srv/backups
```

## Phase 5: Core Services

### 5.1 Docker (if needed)

```bash
sudo apt install docker.io docker-compose-v2 -y
sudo systemctl enable docker
sudo systemctl start docker
```

### 5.2 Nginx

```bash
sudo apt install nginx -y
sudo systemctl enable nginx

# Remove default site
sudo rm /etc/nginx/sites-enabled/default

sudo systemctl start nginx
```

### 5.3 Certbot (Let's Encrypt)

```bash
sudo apt install certbot python3-certbot-nginx -y
sudo systemctl enable certbot.timer
sudo systemctl start certbot.timer

# Verify
sudo certbot renew --dry-run
```

## Phase 6: Deploy Applications

Deploy each application per [Deploy a New Application](deploy-application.md).

## Verification Checklist

```
[ ] SSH key-only access works
[ ] Root login is disabled
[ ] Firewall is active with correct rules
[ ] fail2ban is running
[ ] Automatic updates are enabled
[ ] Team groups exist
[ ] /srv/docs/ has the documentation repo
[ ] Core services (docker, nginx, certbot) are running
[ ] At least one admin user can sudo
```
