<p align="center">
  <img src="https://glowpowerrental-uploads.blr1.cdn.digitaloceanspaces.com/assets/logos/logonobg.png" alt="Glow Power Rental" width="280">
</p>

<h1 align="center">Documentation</h1>

<p align="center">
  Central knowledge base for standards, procedures, and technical references.<br>
  Version-controlled. Reviewable. Searchable.
</p>

---

## Topics

| | Topic | Description |
|---|-------|-------------|
| :server: | [**Server Administration**](server-administration/) | Directory layout, users & groups, security, deployment standards, runbooks |

<!--
Upcoming topics — uncomment and link when created:

| :whale: | [**Docker & Containers**](docker/) | Image standards, Compose patterns, registry management |
| :electric_plug: | [**IoT & Telemetry**](iot-telemetry/) | MQTT, sensor protocols, data pipelines |
| :globe_with_meridians: | [**Networking**](networking/) | DNS, VPN, firewall rules, domain management |
| :gear: | [**CI/CD**](ci-cd/) | Pipelines, deployment workflows, GitHub Actions |
| :floppy_disk: | [**Databases**](databases/) | Setup, backup, replication, query standards |
| :link: | [**APIs**](apis/) | Design standards, authentication, versioning |
| :computer: | [**Development**](development/) | Coding standards, Git workflow, code review |
| :lock: | [**Security**](security/) | Vulnerability management, incident response, compliance |
-->

---

## How to Find What You Need

Each topic is organized into the same categories:

| Looking for... | Go to | Example |
|----------------|-------|---------|
| A rule or convention | `<topic>/standards/` | "What groups should a web app belong to?" |
| Step-by-step instructions | `<topic>/runbooks/` | "How do I deploy a new application?" |
| An explanation of how something works | `<topic>/guides/` | "How does the reverse proxy architecture work?" |
| A specific value or fact | `<topic>/references/` | "What port is Grafana running on?" |
| A copy-paste starting point | `<topic>/templates/` | "Give me a systemd unit file to start from" |
| A design decision and its rationale | `<topic>/architecture/` | "Why did we choose Nginx over Caddy?" |

---

## Repo Structure

```
documentation/
├── README.md                              ← You are here
├── CONTRIBUTING.md                        ← How to add and edit docs
│
├── server-administration/                 ← Topic
│   ├── README.md                          ← Topic index
│   ├── standards/                         ← Rules we follow
│   ├── runbooks/                          ← How to do things
│   ├── guides/                            ← How things work
│   ├── references/                        ← Quick-lookup data
│   ├── templates/                         ← Starter files
│   └── architecture/decisions/            ← Decision records
│
├── <next-topic>/                          ← Same structure
│   └── ...
└── ...
```

---

## Adding a New Topic

1. Create the directory:
   ```bash
   mkdir -p <topic-name>/{standards,runbooks,guides,references,templates,architecture/decisions}
   ```
2. Add a `README.md` inside it with an overview and links.
3. Add a row to the **Topics** table in this file.
4. Commit and push.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full guide.

**Quick version:**

1. Branch: `git checkout -b docs/<topic>/<what>`
2. Write your doc in the right directory.
3. File names: `lowercase-hyphenated.md`
4. One subject per file.
5. Pull request → review → merge.

---

<p align="center">
  <sub>Maintained by the Glow Power Rental team. Review cycle: quarterly.</sub>
</p>
