# Secrets Management Standard

How to handle passwords, API keys, tokens, certificates, and other sensitive data.

---

## Rules

1. **Never commit secrets to git.** Use `.gitignore` to exclude `.env` files.
2. **Never put secrets in systemd unit files.** Use `EnvironmentFile=` to reference `.env`.
3. **Never store secrets in home directories.** They belong in `/opt/<app>/.env`.
4. **Never share secrets over chat, email, or tickets.** Use a password manager or encrypted transfer.
5. **Never log secrets.** Ensure application code does not print secrets to stdout/stderr.
6. **Restrict file permissions on all secret files.**

---

## .env File Standard

```bash
# /opt/<app-name>/.env
# Ownership: root:<app>-admin
# Permissions: 640

# Database
DB_HOST=localhost
DB_PORT=5432
DB_NAME=appdb
DB_USER=app_user
DB_PASS=<generated-strong-password>

# API Keys
API_KEY=<key>
API_SECRET=<secret>

# Application
NODE_ENV=production
PORT=3000
LOG_LEVEL=info
```

## File Permissions

```bash
# .env file: root owns, app-admin group can read
sudo chown root:<app>-admin /opt/<app-name>/.env
sudo chmod 640 /opt/<app-name>/.env

# Credentials directory: certificates, tokens, key files
sudo mkdir -p /opt/<app-name>/credentials/
sudo chown root:<app>-admin /opt/<app-name>/credentials/
sudo chmod 750 /opt/<app-name>/credentials/
```

## .gitignore (for app repos)

```
.env
.env.*
credentials/
*.pem
*.key
*.p12
```

## Rotating Secrets

1. Generate a new secret.
2. Update the `.env` file.
3. Restart the service: `sudo systemctl restart <app-name>`.
4. Verify the application is healthy.
5. Revoke the old secret at the source (API provider, database, etc.).
6. Log the rotation date and who performed it.
