# OpenClaw 🦾

> **Autonomous multi-agent AI operating system. 9 specialized agents. Local-first. Near-zero API cost. Production-grade pipelines from a single prompt.**

Built by **[Bakhouche Akram](https://bak-dev.com)** — Full-Stack Engineer, AI/ML systems architect, 12+ years exp

---

## The Problem

Running AI agents at scale is expensive, fragile, and unstructured.

- One model handles everything → hallucinations compound, costs explode
- No pipeline enforcement → agents skip steps, skip research, ship broken code
- Cloud-only AI → $0.05+ per task, vendor lock-in, data leakage risk
- No memory → every session starts from zero

**OpenClaw solves this.**

---

## What It Is

OpenClaw is a **self-contained, multi-agent AI runtime** — a structured operating system for autonomous AI work. It routes tasks through a strict sequential pipeline of 9 specialized agents, each running the right model for the job, 90% on local hardware.

Think of it as a **fully autonomous software engineering team**, always on, always structured, near-zero marginal cost.

---

## Architecture

```
ACP Client (TUI / Discord / Slack / Telegram / HTTP / WebSocket)
        │
        ▼
 ┌─────────────┐
 │  main 🔀    │   Qwen 3 8B · local · always-on router
 └──────┬──────┘
        ▼
 ┌─────────────┐
 │ orchestor 👑│   Claude Sonnet 4.6 · API · enforces pipeline order
 └──────┬──────┘
        ▼
 research 🔎 → cto ⚙️ → quant 📊 → risk 🛡️ → coder 💻 → ops 🚀
```

**Strict sequential pipeline. No agent skips the queue. No code before research. No deploy before risk approval.**

---

## Agent Registry

| Agent | Role | Model | Cost |
|-------|------|-------|------|
| 🔀 **main** | Always-on router, entrypoint | Qwen 3 8B · local | $0 |
| 👑 **orchestor** | CEO — pipeline control, task decomposition | Claude Sonnet 4.6 · API | ~$0.01/task |
| 🔎 **research** | Find existing solutions, avoid reinventing | Claude 4.5 / Qwen 3.5 27B | $0–$0.01 |
| ⚙️ **cto** | System architecture, module design, stack selection | Qwen 3.5 27B · local | $0 |
| 📊 **quant** | Trading strategies, backtesting, quantitative logic | DeepSeek R1 14B · local | $0 |
| 🛡️ **risk** | Risk validation, safety checks, blockers | Qwen 3 14B · local | $0 |
| 💻 **coder** | Production-grade code, tested, typed, Dockerized | Qwen 2.5 Coder 32B · local | $0 |
| ⚡ **coder-fast** | Rapid prototyping, fast iteration loops | Qwen 2.5 Coder 7B · local | $0 |
| 🚀 **ops** | Deployment, infra, containers, CI/CD | Mistral Small 7B · local | $0 |

**Average cost per full pipeline run: < $0.02.** 90% of tasks never touch the API.

---

## Cost Model

```
Local Ollama (RTX 3090 / any GPU)  ──── 90% of all work ────  $0.00/task
Anthropic Claude (API)             ──── orchestration only ──  ~$0.01/task
────────────────────────────────────────────────────────────────────────
Estimated monthly cost (50 tasks/day):  < $15/month
Equivalent cloud-only cost:             > $500/month
Savings:                                97%+
```

Cost-aware router (`OPENCLAW_ROUTER_MODE=cost_aware_capability_based`) auto-selects the cheapest model capable of handling the task. Auto-downgrades to local when API budget is exceeded.

---

## Core Capabilities

- **Multi-channel ingestion** — Discord, Slack, Telegram, HTTP REST, WebSocket, TUI
- **Structured memory** — short-term + long-term + shared vector store across agents
- **Agent-to-agent routing** — direct agent calls, allowlisted, auditable
- **Web tooling** — search (DuckDuckGo), fetch, scraping built in
- **Cursor integration** — Cursor IDE as a first-class execution environment
- **Exec sandbox** — blocked tools list, token-gated gateway, no camera/sms/system_admin
- **Full observability** — DAG run storage, execution tracing, metrics, audit logs
- **Self-improvement loop** — agents update their own rules, skills, and workspace context

---

## Stack

| Layer | Technology |
|-------|------------|
| Runtime | OpenClaw daemon + Ollama |
| Local inference | Qwen 3, Qwen 2.5 Coder, DeepSeek R1, Mistral Small |
| Cloud reasoning | Anthropic Claude Sonnet 4.6 / 4.5 |
| Memory | Local vector store (configurable) |
| Channels | Discord bot, Slack socket, Telegram bot, HTTP gateway |
| Integrations | Cursor IDE, DuckDuckGo, custom plugins |
| Infra | Docker-ready, WSL2/Linux native |

---

## Channels & Integrations

```
Discord ──┐
Slack   ──┤──► OpenClaw Gateway (localhost:18789) ──► Agent Pipeline
Telegram──┤
HTTP    ──┤
TUI     ──┘
```

All channels funnel into a single token-authenticated gateway. Slack is allowlisted by channel. Every exec call is sandboxed and logged.

---

## Quickstart

 -- FUTURE --

## Directory Structure

```
.openclaw/
├── openclaw.json           # Central config (gitignored — contains tokens)
├── .env                    # Environment variables (gitignored)
├── .cursor/
│   ├── rules/              # Persistent Cursor AI rules
│   └── skills/             # Reusable agent skills
├── agents/                 # Per-agent runtime state (gitignored)
├── workspace/              # Default agent workspace
├── workspace-orchestor/    # CEO workspace
├── workspace-research/     # Research agent workspace
├── workspace-cto/          # CTO architecture workspace
├── workspace-quant/        # Quant strategy workspace
├── workspace-risk/         # Risk agent workspace
├── workspace-coder/        # Production coder workspace
├── workspace-coder-fast/   # Fast iteration workspace
├── workspace-ops/          # Ops/deployment workspace
├── completions/            # Shell completions (bash/zsh/fish/ps1)
└── logs/                   # Audit logs (gitignored)
```

---

## Roadmap & TODO

### Phase 1 — Foundation (current)
- [x] Multi-agent pipeline (9 agents)
- [x] Local Ollama + Anthropic hybrid routing
- [x] Discord / Slack / Telegram channel integrations
- [x] HTTP gateway with token auth and exec sandbox
- [x] Cursor IDE integration
- [x] Agent workspace system (AGENTS.md / SOUL.md / MEMORY.md)
- [x] Self-improvement infrastructure (rules, skills, backlog)
- [x] Cost-aware model router

### Phase 2 — TypeScript Rewrite & SDK (next)
- [ ] **MCP server** — expose all agents as MCP tools consumable by any MCP client

### Phase 3 — Intelligence Layer


### Phase 4 — Platform
- [ ] Web dashboard — live agent DAG visualization, cost tracking

---

## Use Cases

| Domain | What OpenClaw builds autonomously |
|--------|----------------------------------|
| **Crypto / Quant** | Backtesting engines, strategy bots, risk models, exchange connectors |
| **Full-Stack Dev** | REST APIs, React frontends, Dockerized services, CI/CD pipelines |
| **Data Engineering** | ETL pipelines, scraping systems, ML training pipelines |
| **OSINT / Research** | Intelligence tools, data aggregation, automated research reports |
| **DevOps** | Infra automation, deployment pipelines, monitoring setup |

---

## Why OpenClaw vs. alternatives

| | OpenClaw | LangChain | CrewAI | AutoGen |
|-|----------|-----------|--------|---------|
| Local-first | ✅ | Partial | Partial | Partial |
| Structured pipeline | ✅ strict | ❌ | Partial | ❌ |
| Cost < $0.05/task | ✅ | ❌ | ❌ | ❌ |
| Multi-channel (Discord/Slack/TG) | ✅ | ❌ | ❌ | ❌ |
| Agent self-improvement | ✅ | ❌ | ❌ | ❌ |
| Cursor IDE native | ✅ | ❌ | ❌ | ❌ |
| Production deploy pipeline | ✅ | ❌ | ❌ | ❌ |

---

## Author

**Bakhouche Akram** — [@akrambak](https://github.com/akrambak)

Full-Stack Engineer & AI Systems Architect with 12+ years of production experience.

**Background:**
- Full-stack web & mobile (Flutter, Laravel, Node.js, React, Vue.js)
- AI/ML systems — trading bots, ML time-series forecasting, OSINT tools
- PrestaShop / PHP expert, e-commerce platform architecture
- Multi-agent AI systems, LLM orchestration, local inference optimization
- Open source: [TikTok-OSINT](https://github.com/akrambak/TikTok-OSINT) (126 ⭐), ML_Predict_Trading, aegis-planner

**Stack:** Python · TypeScript · Flutter/Dart · Laravel PHP · Docker · TensorFlow · Ollama · Anthropic · Firebase · Elasticsearch · PostgreSQL · Redis

**Contact:** me@bak-dev.com · **Web:** [bak-dev.com](https://bak-dev.com)

---

## For Recruiters & Clients

**What this project demonstrates:**

- System design at scale — 9-agent pipeline with strict contracts between components
- Cost engineering — 97% cost reduction vs cloud-only AI without sacrificing capability
- Production mindset — sandboxing, audit logs, token auth, secret management, rollback
- Self-improving systems — the system improves its own rules and skills over time
- Multi-modal integration — local GPU inference, cloud APIs, chat platforms, IDE
- TypeScript-first roadmap — strong typing, SDK design, modern tooling

**Available for:** consulting, senior engineering roles, AI systems architecture, technical co-founder positions.

---

## License

MIT — See [LICENSE](LICENSE)

---

<p align="center">
  <strong>OpenClaw — Build once. Route intelligently. Deploy continuously.</strong><br/>
  <a href="https://bak-dev.com">bak-dev.com</a> · <a href="https://github.com/akrambak">github.com/akrambak</a>
</p>
