# Runbook: Deploy a New Application

Step-by-step procedure to deploy a new application on a server.

---

## Prerequisites

- The application is ready to run (code, Docker image, or binary).
- You have sudo access.
- You know which port the application needs.
- The port is not already in use (check [Port Registry](../references/port-registry.md)).

---

## Steps

### 1. Create the directory structure

```bash
sudo mkdir -p /opt/<app-name>/{bin,config,data,logs,credentials}
```

### 2. Create the service account

```bash
sudo useradd --system \
    --no-create-home \
    --shell /usr/sbin/nologin \
    --comment "<App Name> service account" \
    <app-name>
```

### 3. Create application groups

```bash
sudo groupadd <app-name>-admin
sudo groupadd <app-name>-operator
sudo groupadd <app-name>-readonly

# Add service account to its admin group
sudo usermod -aG <app-name>-admin <app-name>
```

### 4. Set permissions

```bash
# Root owns the directory, app-admin group has access
sudo chown -R root:<app-name>-admin /opt/<app-name>/
sudo chmod 750 /opt/<app-name>/

# Data directory: service account needs write access
sudo chown -R <app-name>:<app-name>-admin /opt/<app-name>/data/

# Logs: readable by operators
sudo setfacl -m g:<app-name>-operator:rx /opt/<app-name>/logs/
sudo setfacl -m g:<app-name>-readonly:rx /opt/<app-name>/logs/
```

### 5. Create the .env file

```bash
sudo touch /opt/<app-name>/.env
sudo chown root:<app-name>-admin /opt/<app-name>/.env
sudo chmod 640 /opt/<app-name>/.env

# Edit with your secrets
sudo nano /opt/<app-name>/.env
```

### 6. Deploy application code

For **native applications**:
```bash
# Copy or clone your application into /opt/<app-name>/
```

For **Docker Compose**:
```bash
# Place docker-compose.yml in /opt/<app-name>/
sudo cp docker-compose.yml /opt/<app-name>/
```

### 7. Create the systemd service

Create `/etc/systemd/system/<app-name>.service`:

For native apps, use the [systemd service template](../templates/systemd-service.md).

For Docker Compose apps:
```ini
[Unit]
Description=<App Name>
After=docker.service
Requires=docker.service

[Service]
Type=oneshot
RemainAfterExit=yes
WorkingDirectory=/opt/<app-name>
ExecStart=/usr/bin/docker compose up -d --remove-orphans
ExecStop=/usr/bin/docker compose down
ExecReload=/usr/bin/docker compose up -d --remove-orphans

[Install]
WantedBy=multi-user.target
```

### 8. Enable and start

```bash
sudo systemctl daemon-reload
sudo systemctl enable <app-name>.service
sudo systemctl start <app-name>.service
sudo systemctl status <app-name>.service
```

### 9. Configure Nginx reverse proxy (if web-facing)

Use the [Nginx vhost template](../templates/nginx-vhost.md), then:

```bash
sudo ln -s /etc/nginx/sites-available/<domain> /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl reload nginx
```

### 10. Provision TLS certificate (if HTTPS)

```bash
sudo certbot --nginx -d <domain>
```

### 11. Update firewall (if directly exposed)

```bash
# Only if NOT proxied through Nginx
sudo ufw allow <port>/tcp comment "<app-name>"
```

### 12. Write documentation

- Create `/opt/<app-name>/README.md` using the [Application README template](../templates/application-readme.md).
- Update the [Port Registry](../references/port-registry.md).
- Update the [Server Inventory](../references/server-inventory.md).

### 13. Assign team access

```bash
sudo usermod -aG <app-name>-operator <developer-username>
```

---

## Checklist

```
[ ] Directory created at /opt/<app-name>/
[ ] Service account created (no login shell, no home)
[ ] Groups created (<app>-admin, <app>-operator, <app>-readonly)
[ ] Permissions set on all directories and files
[ ] .env file created with restricted permissions (640)
[ ] Application code deployed
[ ] systemd unit file created and enabled
[ ] Service is running and healthy
[ ] Logs are flowing (journald or /opt/<app>/logs/)
[ ] Nginx reverse proxy configured (if web-facing)
[ ] TLS certificate provisioned (if HTTPS)
[ ] Firewall rules updated (if directly exposed)
[ ] README.md written for the application
[ ] Port registry updated
[ ] Server inventory updated
[ ] Team members added to application groups
[ ] Team notified of new application
```
