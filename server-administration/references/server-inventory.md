# Server Inventory

All servers, their roles, and key details. Update this file when servers are provisioned or decommissioned.

---

## Servers

| Server Name | IP / Hostname | Provider | OS | Role | Applications | Admin Contact |
|-------------|--------------|----------|-----|------|-------------|---------------|
| oule | 143.198.155.11 | DigitalOcean (SFO3) | Ubuntu 24.04 LTS | Application server | OpenClaw Gateway, Cloudflare Tunnel | hhazime |

---

## Access Information

| Server | SSH Command | Notes |
|--------|-----------|-------|
| oule | `ssh hhazime@143.198.155.11` | Admin access |
| oule | `ssh mkebbi@143.198.155.11` | Developer access |

---

## Domains

| Domain | Target | Server | Notes |
|--------|--------|--------|-------|
| oule.glowpowerrental.com | Cloudflare Tunnel | oule | OpenClaw gateway + Google Chat webhook |
| oule-dashboard.glowpowerrental.com | Cloudflare Tunnel | oule | OpenClaw dashboard |
