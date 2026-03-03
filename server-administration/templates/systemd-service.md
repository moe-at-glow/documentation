# Template: systemd Service Unit

Copy and adapt for each application. Save to `/etc/systemd/system/<app-name>.service`.

---

## Native Application

```ini
[Unit]
Description=<Application Name> - <brief description>
Documentation=file:///opt/<app-name>/README.md
After=network.target
# Uncomment if this app depends on another service:
# After=postgresql.service
# Requires=postgresql.service

[Service]
Type=simple
User=<app-name>
Group=<app-name>-admin
WorkingDirectory=/opt/<app-name>
EnvironmentFile=/opt/<app-name>/.env
ExecStart=/opt/<app-name>/bin/start.sh
ExecStop=/opt/<app-name>/bin/stop.sh
Restart=on-failure
RestartSec=10
StandardOutput=journal
StandardError=journal
SyslogIdentifier=<app-name>

# Security hardening
NoNewPrivileges=yes
ProtectSystem=strict
ProtectHome=yes
ReadWritePaths=/opt/<app-name>/data /opt/<app-name>/logs
PrivateTmp=yes

[Install]
WantedBy=multi-user.target
```

## Docker Compose Application

```ini
[Unit]
Description=<Application Name> (Docker Compose)
Documentation=file:///opt/<app-name>/README.md
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

## After Creating the Unit File

```bash
sudo systemctl daemon-reload
sudo systemctl enable <app-name>.service
sudo systemctl start <app-name>.service
sudo systemctl status <app-name>.service
```
