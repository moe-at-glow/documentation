# Logging and Monitoring

Where logs go, how to read them, and what to monitor.

---

## Log Destinations

| Log Type | Destination | How to Read |
|----------|-------------|-------------|
| System | `/var/log/syslog` | `sudo journalctl` |
| Services | journald | `sudo journalctl -u <app-name>` |
| Nginx access | `/var/log/nginx/access.log` | `sudo tail -f /var/log/nginx/access.log` |
| Nginx errors | `/var/log/nginx/error.log` | `sudo tail -f /var/log/nginx/error.log` |
| App-specific | `/opt/<app>/logs/` or journald | Depends on app config |
| Auth/SSH | `/var/log/auth.log` | `sudo tail -f /var/log/auth.log` |

---

## Common Log Commands

```bash
# System logs from the last hour
sudo journalctl --since "1 hour ago"

# Follow a service's logs live
sudo journalctl -u <app-name> -f

# Today's logs for a service
sudo journalctl -u <app-name> --since today

# Errors only, last week
sudo journalctl --priority=err --since "1 week ago"

# Disk usage of logs
sudo journalctl --disk-usage
```

---

## Log Rotation

All app logs must be rotated. Create `/etc/logrotate.d/<app-name>`:

```
/opt/<app-name>/logs/*.log {
    daily
    missingok
    rotate 14
    compress
    delaycompress
    notifempty
    create 640 <app-name> <app-name>-admin
    postrotate
        systemctl reload <app-name> > /dev/null 2>&1 || true
    endscript
}
```

---

## What to Monitor

| Metric | Alert Threshold | Check Command |
|--------|----------------|---------------|
| Disk usage | Warn 80%, Critical 90% | `df -h` |
| CPU usage | Sustained > 90% | `top` / monitoring agent |
| Memory usage | Sustained > 90% | `free -h` |
| Service status | Any service down | `systemctl is-active <app>` |
| SSL cert expiry | 30 days before | `sudo certbot certificates` |
| Failed SSH logins | > 10 in 5 minutes | fail2ban / `/var/log/auth.log` |
| Open ports | Unexpected ports open | `sudo ss -tlnp` |
