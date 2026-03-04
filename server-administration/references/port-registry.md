# Port Registry

All port assignments across servers. Update this file whenever a port is assigned or released.

---

## Rules

- Every application gets a **unique** port.
- Use ports **above 1024** for applications (no root required).
- Never expose application ports directly — proxy through Nginx on 80/443.
- Document every assignment here.

---

## Port Assignments

| Port | Application | Protocol | Server | Notes |
|------|------------|----------|--------|-------|
| 22 | sshd | TCP | all | SSH access |
| 80 | nginx | HTTP | all | Redirects to 443 |
| 443 | nginx | HTTPS | all | Reverse proxy / TLS termination |
| 18789 | openclaw-gateway | TCP | oule | WebSocket gateway, localhost only, proxied via Cloudflare Tunnel |
| 18792 | openclaw-gateway | TCP | oule | Secondary gateway port, localhost only |
| 20241 | cloudflared | TCP | oule | Tunnel metrics endpoint, localhost only |
| — | — | — | — | — |

> **Add new entries above the divider line. Keep sorted by port number.**
