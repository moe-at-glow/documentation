# Runbook: Decommission an Application

Step-by-step procedure to safely remove an application from a server.

---

## Prerequisites

- Team and stakeholders have been notified.
- A decision has been made and documented.
- Final backup has been planned.

---

## Steps

### 1. Create a final backup

```bash
sudo /opt/<app-name>/bin/backup.sh
# Or manually:
sudo tar czf /srv/backups/<app-name>-final-$(date +%Y-%m-%d).tar.gz /opt/<app-name>/
```

### 2. Stop and disable the service

```bash
sudo systemctl stop <app-name>.service
sudo systemctl disable <app-name>.service
```

### 3. Remove the Nginx virtual host

```bash
sudo rm /etc/nginx/sites-enabled/<domain>
sudo rm /etc/nginx/sites-available/<domain>
sudo nginx -t && sudo systemctl reload nginx
```

### 4. Remove firewall rules

```bash
sudo ufw status numbered
# Delete the relevant rule by number
sudo ufw delete <rule-number>
```

### 5. Remove the application directory

```bash
sudo rm -rf /opt/<app-name>/
```

### 6. Remove the systemd unit file

```bash
sudo rm /etc/systemd/system/<app-name>.service
sudo systemctl daemon-reload
```

### 7. Remove the service account and groups

```bash
sudo userdel <app-name>
sudo groupdel <app-name>-admin
sudo groupdel <app-name>-operator
sudo groupdel <app-name>-readonly
```

### 8. Remove log rotation config

```bash
sudo rm /etc/logrotate.d/<app-name>
```

### 9. Clean up TLS certificate (if dedicated)

```bash
sudo certbot delete --cert-name <domain>
```

### 10. Update documentation

- Update [Port Registry](../references/port-registry.md) — remove the port entry.
- Update [Server Inventory](../references/server-inventory.md) — remove or mark as decommissioned.
- Remove or archive the entry in `/srv/docs/applications/`.

---

## Checklist

```
[ ] Team and stakeholders notified
[ ] Final backup created and verified
[ ] Service stopped and disabled
[ ] Nginx virtual host removed
[ ] Firewall rules removed
[ ] Application directory removed
[ ] systemd unit file removed
[ ] Service account and groups removed
[ ] Log rotation config removed
[ ] TLS certificate removed (if dedicated)
[ ] Port registry updated
[ ] Server inventory updated
[ ] Documentation updated
```
