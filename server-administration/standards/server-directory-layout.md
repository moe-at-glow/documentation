# Server Directory Layout Standard

Where everything lives on a server. Follow the Filesystem Hierarchy Standard (FHS) with these conventions.

---

## Directory Map

```
/
├── opt/                          # All custom/third-party applications
│   └── <app-name>/               # One directory per application
│       ├── README.md             # App documentation
│       ├── .env                  # Environment variables (restricted)
│       ├── bin/                  # Executables and scripts
│       ├── config/               # Configuration files
│       ├── data/                 # Persistent data
│       ├── logs/                 # App logs (if not using journald)
│       ├── credentials/          # Certs, API keys, tokens
│       └── docker-compose.yml    # If containerized
│
├── srv/                          # Site-specific data
│   ├── docs/                     # Server-local documentation symlink or clone
│   └── backups/                  # Local backup staging
│
├── var/
│   ├── www/                      # Web server document roots ONLY
│   │   ├── <domain.com>/         # One directory per virtual host
│   │   └── html/                 # Default web root
│   ├── log/                      # System and service logs
│   └── lib/                      # State data (databases, etc.)
│
├── etc/
│   ├── nginx/                    # Web server configuration
│   │   ├── sites-available/      # All virtual host configs
│   │   └── sites-enabled/        # Symlinks to active configs
│   ├── systemd/system/           # Custom systemd unit files
│   └── logrotate.d/              # Log rotation configs
│
├── home/
│   └── <username>/               # Personal files ONLY
│       ├── .ssh/                 # SSH keys
│       ├── .bashrc               # Shell config
│       └── .profile              # Environment
│
└── tmp/                          # Temporary files (cleared on reboot)
```

## Rules

| Rule | Rationale |
|------|-----------|
| **Never put project files in `/home/`** | Home dirs are personal. Projects there are invisible to the team and create bus-factor risk. |
| **Applications live in `/opt/<app-name>/`** | FHS standard for third-party software. Predictable, discoverable, isolated. |
| **Static web assets go in `/var/www/<domain>/`** | Document roots only. Application logic stays in `/opt/`. |
| **Secrets never live in `/home/` or git** | Secrets belong in `/opt/<app>/.env` with strict permissions (640). |
| **Logs go to journald or `/var/log/`** | Centralized logging. App logs in `/opt/<app>/logs/` only when journald is not feasible. |
| **Custom systemd units go in `/etc/systemd/system/`** | Never modify files in `/lib/systemd/`. |
| **Backup staging goes in `/srv/backups/`** | Centralized, predictable, easy to monitor disk usage. |

## What Does NOT Belong Where

| Location | Does NOT belong |
|----------|----------------|
| `/home/<user>/` | Application code, docker-compose files, project docs, `.env` files |
| `/var/www/` | Application logic, backend code, databases, docker stacks |
| `/opt/<app>/` | Other apps' data, shared libraries, system binaries |
| `/tmp/` | Anything you want to keep after a reboot |
| `/root/` | Anything. Never work as root. |
