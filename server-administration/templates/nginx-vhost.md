# Template: Nginx Virtual Host

Copy and adapt for each web-facing application. Save to `/etc/nginx/sites-available/<domain>`.

---

## Reverse Proxy (most common)

```nginx
server {
    listen 443 ssl http2;
    server_name <domain>;

    ssl_certificate     /etc/letsencrypt/live/<domain>/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/<domain>/privkey.pem;

    # Security headers
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;

    # Proxy to application
    location / {
        proxy_pass http://127.0.0.1:<APP_PORT>;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Static files (optional — uncomment if needed)
    # location /static/ {
    #     alias /var/www/<domain>/static/;
    #     expires 30d;
    # }
}

# HTTP → HTTPS redirect
server {
    listen 80;
    server_name <domain>;
    return 301 https://$host$request_uri;
}
```

## WebSocket Support (add inside location block)

```nginx
    location /ws {
        proxy_pass http://127.0.0.1:<APP_PORT>;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
```

## Static Site Only (no application backend)

```nginx
server {
    listen 443 ssl http2;
    server_name <domain>;

    ssl_certificate     /etc/letsencrypt/live/<domain>/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/<domain>/privkey.pem;

    root /var/www/<domain>;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

## Enabling the Site

```bash
sudo ln -s /etc/nginx/sites-available/<domain> /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

## Provisioning TLS (first time)

```bash
# Before certbot — use a temporary HTTP-only config, then run:
sudo certbot --nginx -d <domain>
```
