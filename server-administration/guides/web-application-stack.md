# Web Application Stack

How web applications are deployed, proxied, and secured.

---

## Stack Overview

```
Client → DNS → Server IP → ufw → Nginx (TLS) → localhost:<port> → Application
```

| Layer | Technology | Configuration Location |
|-------|-----------|----------------------|
| DNS | Your DNS provider | External |
| Firewall | ufw | `sudo ufw status` |
| Web server | Nginx | `/etc/nginx/sites-available/` |
| TLS | Let's Encrypt / certbot | `/etc/letsencrypt/` |
| Application | Varies (Node.js, Python, Docker) | `/opt/<app-name>/` |

---

## Nginx as Reverse Proxy

Nginx handles:
- **TLS termination** — decrypts HTTPS, forwards plain HTTP to the app.
- **Static file serving** — serves files from `/var/www/<domain>/` without hitting the app.
- **Security headers** — adds HSTS, X-Frame-Options, etc.
- **HTTP → HTTPS redirect** — port 80 always redirects to 443.

Applications handle:
- **Business logic only** — bind to `127.0.0.1:<port>`, serve HTTP (not HTTPS).

---

## Adding a New Web Application

1. Deploy the application per [Deploy Application](../runbooks/deploy-application.md).
2. Create an Nginx vhost per [Nginx Vhost Template](../templates/nginx-vhost.md).
3. Provision a TLS certificate:
   ```bash
   sudo certbot --nginx -d <domain>
   ```
4. Verify: `curl -I https://<domain>`
5. Update the [Port Registry](../references/port-registry.md).

---

## Security Headers

Every Nginx vhost must include:

```nginx
add_header X-Frame-Options "SAMEORIGIN" always;
add_header X-Content-Type-Options "nosniff" always;
add_header X-XSS-Protection "1; mode=block" always;
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
```

---

## Static Files vs Application Files

| Type | Location | Served By |
|------|----------|-----------|
| Static assets (HTML, CSS, JS, images) | `/var/www/<domain>/` | Nginx directly |
| Application code | `/opt/<app-name>/` | The application process |
| Uploaded files | `/opt/<app-name>/data/uploads/` | Application (or Nginx alias) |
