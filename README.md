# dvoGPT: Build, Deploy, and Run Autonomous Support Agents  
[![Repo](https://img.shields.io/badge/repo-lockard--LLC/dvoGPT-blue)](https://github.com/lockard-LLC/dvoGPT.git)  
[![Discord Follow](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fdiscord.com%2Fapi%2Finvites%2Fautogpt%3Fwith_counts%3Dtrue&query=%24.approximate_member_count&label=total%20members&logo=discord&logoColor=white&color=7289da)](https://discord.gg/autogpt) &ensp;
[![Twitter Follow](https://img.shields.io/twitter/follow/Auto_GPT?style=social)](https://twitter.com/Auto_GPT) &ensp;

<!-- Keep these links. Translations will automatically update with the README. -->
[Deutsch](https://zdoc.app/de/Significant-Gravitas/AutoGPT) | 
[Español](https://zdoc.app/es/Significant-Gravitas/AutoGPT) | 
[français](https://zdoc.app/fr/Significant-Gravitas/AutoGPT) | 
[日本語](https://zdoc.app/ja/Significant-Gravitas/AutoGPT) | 
[한국어](https://zdoc.app/ko/Significant-Gravitas/AutoGPT) | 
[Português](https://zdoc.app/pt/Significant-Gravitas/AutoGPT) | 
[Русский](https://zdoc.app/ru/Significant-Gravitas/AutoGPT) | 
[中文](https://zdoc.app/zh/Significant-Gravitas/AutoGPT)

---

## What is dvoGPT?

**dvoGPT** is an AutoGPT fork and a trauma-informed, privacy-first autonomous agent platform built to help survivors of domestic violence (DVO/EPO holders) with the practical, safety-critical tasks involved in leaving and rebuilding life. dvoGPT combines multi-agent automation with a survivor-centered UX and strict privacy rules so people can safely search for housing, track court dates, monitor offender custody (VINELink), arrange veterinary care through **SafePaws**, apply for benefits, plan moves, and coordinate transportation — all while minimizing the risk of discovery.

> **Short:** Autonomous, discreet, trauma-aware assistance — helping survivors plan safer next steps, one secure task at a time.

---

## Hosting Options
- **Self-host (Free)** — run locally or in your own cloud with Docker Compose.  
- **Managed / Cloud** — future plan: a hosted version with enhanced operational support (waitlist / beta when available).

> **NOTE:** Running the platform for real-world users requires legal review, security audits, and partnerships with advocacy organizations. See *Security, privacy & safety* below.

---

## Why an AutoGPT fork?

AutoGPT provides an agent-based architecture and tooling well-suited for multi-step, autonomous workflows. dvoGPT adapts that architecture and hardens it for safety, privacy, and trauma-informed interaction — while adding domain-specific modules (housing, legal docket tracking, SafePaws vet coordination, VINELink monitoring, walkability and transit calculations, etc.).

---

## System Requirements

### Hardware
- CPU: 4+ cores recommended  
- RAM: Minimum 8GB (16GB recommended)  
- Storage: ≥10GB free

### Software
- Linux (Ubuntu 20.04+), macOS (10.15+), or Windows 10/11 with WSL2  
- Docker Engine (20.10+)  
- Docker Compose (2.0+)  
- Git (2.30+)  
- Node.js (16+) and npm/yarn  
- Python 3.11+  
- VS Code or any modern editor

### Network
- Stable internet for dev & optional integrations  
- Outbound HTTPS access to configured APIs (Walk Score, Google Maps, VINELink, OpenAI, etc.)

---

## Quickstart — Local Dev (Recommended)

> This repo is containerized for a reproducible dev environment. The minimal scaffold includes a React frontend, FastAPI backend, an agent worker, Postgres and Redis.

**Clone & run**
```bash
git clone https://github.com/lockard-LLC/dvoGPT.git
cd dvoGPT
cp .env.example .env    # edit .env with local placeholders (DO NOT commit real keys)
docker compose up --build -d
# Frontend: http://localhost:3000
# Backend health: http://localhost:8000/health
````

**Quick health checks**

```bash
curl -fsS http://localhost:8000/health
curl -fsS http://localhost:3000/ | head -n 20
```

**.env variables (high level)**
The repo contains `.env.example`. Typical variables:

* `OPENAI_API_KEY` — LLM provider (dev/stub or restricted key)
* `VINELINK_API_KEY` — placeholder (register and legal review required)
* `WALK_SCORE_KEY` — Walk Score API key
* `GOOGLE_MAPS_KEY` — Maps & Directions API key
* `DATABASE_URL` — Postgres URL
* `REDIS_URL` — Redis URL

**Security reminder:** Never commit real API keys or survivor data to the repository.

---

## Core features (domain-focused)

* **Stealth & Emergency Controls** — rapid-exit button, configurable decoy screens, optional duress code, ephemeral session storage and redaction of local traces.
* **Autonomous Tasking** — multi-agent orchestration for housing search, landlord communication, lease termination letters (DVO-aware), VINELink monitoring, job search and benefits assistance, and SafePaws veterinary coordination.
* **Housing Optimization** — walkability, grocery proximity, transit time, total cost-of-occupancy, pet-friendly filtering and DVO-related lease-break assistance.
* **Legal Case Management** — court docket tracking, calendar reminders, evidence organization, and VINELink custody alerts.
* **Employment & Benefits Automation** — job matching, resume/CV builder, automated SNAP/DCBS application assistance (local flows).
* **SafePaws Integration** — appointment scheduling, encrypted pet records, discount-tier management, emergency stabilization routing.
* **Move Coordination & Logistics** — checklists, timelines, budget planning, transport planning and volunteer/agency coordination.
* **Trauma-Informed UX** — plain language, progressive disclosure, and built-in links to human advocates & hotlines.

---

## AutoGPT ancestry — what we keep from the original

dvoGPT is a purpose-driven fork of the AutoGPT ecosystem. We preserve several proven pieces from the original project model:

* **Agent-based architecture** for continuous, multi-step automation.
* **Frontend / Backend split** (React frontend, API-backed orchestration).
* **Forge / Bench tooling concepts** for building and validating agents.
* **CLI conveniences** for running and managing agents locally.

We adapt these elements with strict privacy, auditability, and safety constraints appropriate for survivor-facing software.

---

## Example agents (domain examples)

1. **Housing Search & Relocation Agent**

   * Aggregates listings, scores them by walkability/transit, calculates cost-of-occupancy, flags pet-friendly units, drafts landlord outreach and move timelines.

2. **VINELink Monitor / Court Tracker Agent**

   * Tracks abuser custody status (VINELink placeholder until org registration), watches court docket updates, sends discreet alerts to the survivor or advocate, and triggers a safety plan on release.

3. **SafePaws Vet Coordinator Agent**

   * Schedules initial wellness checks at partner clinics, tracks vaccinations and medication schedules, and escalates emergency stabilization requests to partner hospitals.

---

## Frontend & Server (overview)

### Frontend

* React (Vite or CRA) — trauma-informed UI, rapid-exit, decoy templates.
* Agent Builder & Interaction: low-code blocks to configure flows.
* Monitoring & Analytics: local dev telemetry for debugging (not enabled for production without consent).

### Backend

* FastAPI (Python) — authentication, encrypted storage, agent orchestration endpoints.
* Agent Worker(s) — multi-agent orchestration (LangChain or custom); workers are sandboxed and constrained for safe web access.
* Data stores: Postgres (encrypted at rest) and Redis for queues.

---

## Security, Privacy & Safety (MUST READ)

dvoGPT is intended for highly vulnerable people. Security and ethics are non-negotiable.

* **Do not run for live survivors without legal review & partners.** Before any pilot, obtain legal counsel, sign partnership MOUs, and perform security & privacy audits.
* **No real keys in commits.** Use `.env` and secrets managers (Vault, AWS Secrets Manager) — never commit credentials.
* **Ephemeral sessions & minimal logging.** By default, sessions should be memory-only and server logs must redact secrets (e.g., `sk-` or `VINELINK-`).
* **Stealth mode & rapid-exit.** The UI includes a rapid-exit control that immediately replaces the page with configurable decoy content and clears session state. Document and test this in user flows.
* **Explicit consent for external contact.** Any communication with landlords, vets or legal agents must be explicit and auditable. Provide an option to route calls/messages through a vetted advocate.
* **VINELink & court integrations require registration.** Do not integrate or automate against court/VINELink APIs without the required org agreements and legal review.
* **Human-in-the-loop for high-risk actions.** For any action that could materially alter a survivor's risk (moving, alerting law enforcement), require human confirmation and advocate involvement.

---

## License & legal notes

This project includes derived ideas and structural elements from the AutoGPT ecosystem. See `LICENSE` in this repository for our licensing terms. Parts of the original AutoGPT platform are distributed under mixed licenses (Polyform Shield for `autogpt_platform` in the upstream project and MIT for other parts). When integrating third-party components or API SDKs, respect their license and terms of service.

---

## Contribute & Code of Conduct

We welcome contributors who understand the sensitivity of this domain.

**How to contribute**

1. Fork this repo and create a feature branch.
2. Run tests and linters locally.
3. Open a Pull Request describing the change, security/privacy impact, and migration steps. For features touching integrations (VINELink, payments, clinic scheduling), include a risk assessment and manual test plan.
4. All PRs must include a short safety impact statement for real-world use.

**Code of Conduct**
This project works with people in crisis. Maintain trauma-informed language, respect privacy, and consider the human impact of changes.

See `CONTRIBUTING.md` for details.

---

## Classic AutoGPT tooling & notes

dvoGPT preserves compatibility with certain AutoGPT concepts:

* **Forge** — tooling patterns to scaffold new agents and reduce boilerplate.
* **Benchmark / agbenchmark** — for automated, objective testing of agent behavior.
* **Frontend / CLI** — local UI and management CLI to run and monitor agents.

If you rely on these upstream tools, consult their docs and adapt for safety constraints.

---

## Support & community

* Repo: `https://github.com/lockard-LLC/dvoGPT.git`
* Founder / contact: Jerry — `jerry@lockard.llc`
* For general AutoGPT community help: Discord (AutoGPT): [https://discord.gg/autogpt](https://discord.gg/autogpt)

**Security issues:** If you discover a security or privacy vulnerability, please open a private security issue or email the maintainer directly rather than posting publicly.

---

## Pilot checklist (before real use)

1. Legal review of agreements & privacy policy.
2. Formal partnerships with advocacy organizations and SafePaws clinics.
3. Penetration test & privacy audit.
4. Staff training (trauma-informed procedures).
5. Emergency escalation workflows (hotline, local authorities, advocates).
6. Proof of insurance / indemnification where required.

---

## Acknowledgements

dvoGPT is inspired by the AutoGPT multi-agent ecosystem and built with a survivor-first mission. Thanks to the open-agent community and the many advocates and practitioners who advise on safety and trauma-informed design.

---

### Final note

This project is about people — do not rush features to production without careful safety planning, legal review, and advocate involvement.

