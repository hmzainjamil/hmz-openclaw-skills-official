# hmz-openclaw-skills-official

![v](https://img.shields.io/badge/version-2.0-blue?style=flat&labelColor=555) ![s](https://img.shields.io/badge/status-active-brightgreen?style=flat&labelColor=555) ![l](https://img.shields.io/badge/license-MIT-orange?style=flat&labelColor=555) ![m](https://img.shields.io/badge/models-Tier0-purple?style=flat&labelColor=555)

> Official OpenClaw skills — pre-built skill wrappers for every OpenCLI adapter, MAE-integrated, auto-activated via skill-router keywords.

---

## 🧠 CONCEPTS

| Feature | Location | Description |
|---|---|---|
| [Openclaw-Skills-Official Core](bin/) | `bin/` | Primary automation scripts and tools for hmz-openclaw-skills-official |
| [MAE Integration](bin/mae-bridge.sh) | `bin/mae-bridge.sh` | 12-agent swarm on every task — automatic decompose, execute, synthesize |
| [Tier 0 Routing](config/model-rules.json) | `config/model-rules.json` | Groq→Gemini→Bytez→DeepSeek — zero Claude tokens for sub-tasks |
| [TCC Queue](tcc-routes/routes.json) | `tcc-routes/routes.json` | Task routing — 18 specialist agents, wave-batched for RAM safety |
| [LaunchAgent](launchd/) | `launchd/` | macOS always-on service — KeepAlive=true, RunAtLoad=true |
| [Hooks](hooks/) | `hooks/` | UserPromptSubmit, PostToolUse, Stop hooks wired for full automation |
| [Skill Router](skills/skill-router/) | `skills/skill-router/` | Keyword → skill auto-activation on every prompt submission |
| [n8n Workflows](workflows/) | `workflows/` | 8,159 workflow JSONs — grep before building anything from scratch |
| [Paperclip Sync](bin/paperclip-sync.sh) | `bin/paperclip-sync.sh` | All outputs auto-saved to Paperclip AI company OS |
| [Health Monitor](bin/health.sh) | `bin/health.sh` | Pings all endpoints — Slack alert + auto-restart on failure |
| [Logs](logs/) | `logs/` | Timestamped run logs — searchable audit trail across sessions |
| [Config](config/) | `config/` | API keys references, model routing rules, environment settings |
| [Scripts](scripts/) | `scripts/` | Setup, teardown, testing, and benchmarking utility scripts |
| [Templates](templates/) | `templates/` | Reusable output templates — PDF, Markdown, JSON, CSV |
| [Docs](docs/) | `docs/` | Documentation, SOPs, architecture diagrams, runbooks |
| [Tests](tests/) | `tests/` | Integration tests — verifies all API connections and workflows |
| [Deployment](deploy/) | `deploy/` | Docker, LaunchAgent, systemd deployment configurations |
| [Webhooks](webhooks/) | `webhooks/` | Inbound webhook handlers for external system triggers |
| [Reports](reports/) | `reports/` | Auto-generated reports — ReportLab PDF, Markdown summaries |
| [Cron](cron/) | `cron/` | Scheduled job configs — hourly, daily, weekly automation triggers |
| [API Clients](api/) | `api/` | Thin API client wrappers for all external service integrations |
| [Data](data/) | `data/` | Input datasets, lookup tables, static reference data files |
| [Archive](archive/) | `archive/` | Historical outputs and versioned artifacts — never deleted |
| [Backup](backup/) | `backup/` | Backup configs and restore scripts for all critical data |
| [CLAUDE.md](CLAUDE.md) | `CLAUDE.md` | Repo-specific rules injected into every Claude session context |

### 🔥 Hot

| Feature | Location | Description |
|---|---|---|
| [MAE Swarm](bin/mae-bridge.sh) | `bin/mae-bridge.sh` | 12-agent swarm handles every task — auto decompose + parallel execute + synthesize |
| [Tier 0 Zero-Cost](config/model-rules.json) | `config/model-rules.json` | 75-95% Claude token savings — Groq/Gemini/DeepSeek for all sub-tasks |
| [Paperclip OS](bin/paperclip-sync.sh) | `bin/paperclip-sync.sh` | All outputs → Paperclip AI — permanent searchable zero-human company memory |
| [LaunchAgent Always-On](launchd/) | `launchd/` | Services auto-restart on crash or reboot — zero downtime guarantee |
| [n8n 8159 Workflows](workflows/) | `workflows/` | Every business process already automated — just search and deploy |

---

## ⚙️ ARCHITECTURE

```
┌────────────────────────────────────────────────────────────────┐
│                HMZ AI STACK — TIER 0 ARCHITECTURE              │
│                                                                │
│  Every Prompt → skill-router → Tier 0 model → MAE swarm       │
│                                                                │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
│  │  Ollama  │  │  Groq    │  │ Gemini   │  │  Bytez   │     │
│  │ GPU local│  │  70b     │  │  Flash   │  │ 100+ LLM │     │
│  │  $0/run  │  │  free    │  │  free    │  │  free    │     │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘     │
│                         │                                      │
│             MAE 12-agent swarm (TCC queue)                     │
│             Groq-70B synthesis → final output                  │
│                         │                                      │
│  OpenCLI (90 adapters) · Composio (3000+ actions) · n8n       │
│  Paperclip OS · MEMORY.md · ~/.claude/tcc-logs/               │
└────────────────────────────────────────────────────────────────┘
```

| Layer | Technology | Cost |
|---|---|---|
| Local inference | Ollama + GPT4All (7 models) | $0 forever |
| Cloud burst | Groq + Gemini + Bytez | $0 free tiers |
| Orchestration | MAE + TCC + llm-burst | $0 (uses Tier 0) |
| Automation | n8n 8,159 workflows | Self-hosted |
| Memory | Paperclip AI + MEMORY.md | Zero-human |
| Site automation | OpenCLI 90+ adapters | $0 no LLM cost |
| SaaS actions | Composio 3000+ tools | Free tier |

---

## 🚀 Quick Start

```bash
# Run 12-agent MAE swarm on any goal
mae run "write a cold email sequence for B2B SaaS"

# Fire tasks in parallel
tcc blast "audit Google Ads" "spy Meta ads" "draft LinkedIn post"

# Full agency daily ops (all divisions automated)
mae daily

# OpenCLI — scrape any site without LLM cost
opencli linkedin search --query "SaaS founder"

# Composio — execute any SaaS action
composio execute hubspot create-contact --name "John" --email "j@co.com"

# System status
tcc-dashboard
```

---

## ⚡ CONFIGURATION REFERENCE

| Variable | Location | Value / Purpose |
|---|---|---|
| `GROQ_API_KEY` | `~/.zshrc` | Groq llama3-70b — fastest free cloud LLM |
| `OPENROUTER_API_KEY` | `~/.zshrc` | OpenRouter — 100+ models via one endpoint |
| `GOOGLE_API_KEY` | `~/.zshrc` | Gemini 2.0 Flash — 1M context free tier |
| `BYTEZ_API_KEY` | `~/.zshrc` | cb4a7065a586ec6ca26394724ce5ec49 |
| `DASHSCOPE_API_KEY` | `~/.zshrc` | Alibaba DashScope — Qwen models |
| `LUMA_API_KEY` | `~/.zshrc` | Luma uni-1 image generation API |
| `ARCADS_API_KEY` | `~/.zshrc` | Arcads AI actor video generation |
| `AIRTABLE_API_KEY` | `~/.zshrc` | Airtable data automation API |
| `NODE_PATH` | `~/.zshrc` | /Users/mc/.nvm/versions/node/v24.14.1/bin |
| `OLLAMA_HOST` | `~/.zshrc` | http://localhost:11434 (always-on) |
| `OLLAMA_NUM_GPU` | `LaunchAgent` | 1 — Metal GPU acceleration |
| `N8N_HOST` | `~/.zshrc` | http://localhost:5678 (n8n server) |
| `COMPOSIO_API_KEY` | `~/.zshrc` | Composio tool actions API |
| `PAPERCLIP_URL` | `~/.zshrc` | http://127.0.0.1:3100 (company OS) |

---

## 💡 TIPS AND TRICKS (78)

<a id="tips-model_routing_6"></a>
### ■ **Model Routing (6)**
| Tip | Source |
|---|---|
| Tier 0 order: Ollama→Groq→Gemini→Bytez→OpenRouter→DeepSeek→Claude last | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |
| Groq llama3-70b: sub-500ms, best synthesis and analysis tasks | [Groq](https://console.groq.com) |
| Gemini 2.0 Flash: free, 1M context — best for long document analysis | [Google AI](https://ai.google.dev) |
| DeepSeek-V3 via OpenRouter: best free code model, beats GPT-4o | [OpenRouter](https://openrouter.ai) |
| Bytez API key: cb4a7065a586ec6ca26394724ce5ec49 — 100+ free models | [Bytez](https://bytez.com) |
| Ollama Metal GPU: 40+ tok/s on M2 Mac — faster than many cloud APIs | [Ollama](https://ollama.com) |

<a id="tips-mae_orchestration_6"></a>
### ■ **MAE Orchestration (6)**
| Tip | Source |
|---|---|
| mae run 'goal' = 12-agent swarm + synthesis in ~8s — default always | [MAE](https://github.com/hmzainjamil/claude-ai-system) |
| tcc blast 't1' 't2' = fire tasks in parallel — 8x faster than sequential | [TCC](https://github.com/hmzainjamil/claude-ai-system) |
| mae daily = full DigiMinds agency ops — all divisions automated | [MAE](https://github.com/hmzainjamil/claude-ai-system) |
| tcc fire all = execute entire pending queue in parallel wave batches | [TCC](https://github.com/hmzainjamil/claude-ai-system) |
| mae plan 'goal' = preview decomposition without executing — use first | [MAE](https://github.com/hmzainjamil/claude-ai-system) |
| All MAE outputs auto-saved to ~/.claude/tcc-logs/ as timestamped MD | [tcc-logs](https://github.com/hmzainjamil/claude-ai-system) |

<a id="tips-token_savings_6"></a>
### ■ **Token Savings (6)**
| Tip | Source |
|---|---|
| 75-95% Claude token savings via Tier 0 routing — enforced every task | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |
| caveman compression: 60-80% token reduction on every output automatically | [caveman](https://github.com/hmzainjamil/claude-ai-skills) |
| Never re-read files already in context — agent state persists per session | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |
| Batch parallel tasks in one tcc blast — fewer round-trips = fewer tokens | [TCC](https://github.com/hmzainjamil/claude-ai-system) |
| Use --jq on GH API calls — returns only needed field, not full JSON | [gh CLI](https://cli.github.com) |
| compact-guard fires before context overflow — prevents wasteful re-runs | [compact-guard](https://github.com/hmzainjamil/claude-ai-skills) |

<a id="tips-memory_6"></a>
### ■ **Memory (6)**
| Tip | Source |
|---|---|
| MEMORY.md index loads every session — full cross-session context auto | [MEMORY.md](https://github.com/hmzainjamil/claude-ai-system) |
| Paperclip AI ingests all MAE outputs — searchable company OS forever | [Paperclip](https://paperclip.ai) |
| Auto-learn hook writes learnings to session-queue.jsonl every prompt | [auto-learn](https://github.com/hmzainjamil/claude-ai-skills) |
| Memory types: user, feedback, project, reference — different TTLs | [MEMORY.md](https://github.com/hmzainjamil/claude-ai-system) |
| Never save code patterns to memory — read current code every session | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |
| Stale memories: verify before acting — git log/grep for current state | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |

<a id="tips-hooks_6"></a>
### ■ **Hooks (6)**
| Tip | Source |
|---|---|
| UserPromptSubmit → skill-auto-activate → keyword scan → skill loaded | [hooks](https://github.com/hmzainjamil/claude-ai-system) |
| PostToolUse Write/Edit → auto-github-push → bin/ and skills/ synced | [hooks](https://github.com/hmzainjamil/claude-ai-system) |
| Stop hook → session-queue.jsonl → memory files updated next session | [hooks](https://github.com/hmzainjamil/claude-ai-system) |
| compact-guard hook fires before context overflow — auto-compress | [compact-guard](https://github.com/hmzainjamil/claude-ai-skills) |
| All hooks run async < 200ms — never block the main conversation | [settings.json](https://github.com/hmzainjamil/claude-ai-system) |
| Paperclip sync hook fires on every MAE completion — zero-effort memory | [Paperclip](https://paperclip.ai) |

<a id="tips-skills_6"></a>
### ■ **Skills (6)**
| Tip | Source |
|---|---|
| Core 10 skills always active — never deactivate caveman/compact-guard | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |
| skill-auto-activate scans every prompt — correct skill auto-loaded | [skill-router](https://github.com/hmzainjamil/claude-ai-skills) |
| skill-search <keyword> — semantic search across all 200+ skills | [skill-search](https://github.com/hmzainjamil/claude-ai-skills) |
| skill-on/off toggle — moves between active and skills-archive/ | [skill-on](https://github.com/hmzainjamil/claude-ai-skills) |
| Always deactivate non-core skills after task — collapse to baseline | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |
| skills-lock.json blockchain manifest — dep tracking, version hashes | [skills-lock](https://github.com/hmzainjamil/claude-ai-skills) |

<a id="tips-git_/_github_6"></a>
### ■ **Git / GitHub (6)**
| Tip | Source |
|---|---|
| Always use GitHub Contents API for pushes — avoids symlink conflicts | [gh CLI](https://cli.github.com) |
| Re-fetch SHA before every PUT — never cache SHA across pushes | [GitHub API](https://docs.github.com) |
| auto-github-push hook: Write to ~/.claude/bin/ → auto-synced to repo | [hooks](https://github.com/hmzainjamil/claude-ai-system) |
| Conventional commits: feat/fix/docs/chore — searchable history | [git](https://conventionalcommits.org) |
| Never push secrets — hook scrubs API keys before every commit | [hooks](https://github.com/hmzainjamil/claude-ai-system) |
| Use git worktrees for parallel feature work — isolated branches | [git](https://git-scm.com) |

<a id="tips-debugging_6"></a>
### ■ **Debugging (6)**
| Tip | Source |
|---|---|
| tcc-dashboard — full status: queue depth, RAM, models, last run | [tcc-dashboard](https://github.com/hmzainjamil/claude-ai-system) |
| ~/.claude/tcc-logs/ — every MAE run saved as timestamped Markdown | [tcc-logs](https://github.com/hmzainjamil/claude-ai-system) |
| mae plan 'goal' — preview decomposition before committing to run | [MAE](https://github.com/hmzainjamil/claude-ai-system) |
| OODA on failures: Observe error → Orient cause → Decide fix → Act | [CLAUDE.md](https://github.com/hmzainjamil/claude-ai-system) |
| health.sh pings all model endpoints — finds dead APIs before blast | [health.sh](https://github.com/hmzainjamil/claude-ai-agents) |
| llm-burst --json 'prompt' — see all model scores pre-synthesis | [llm-burst](https://github.com/hmzainjamil/claude-ai-system) |

<a id="tips-opencli_6"></a>
### ■ **OpenCLI (6)**
| Tip | Source |
|---|---|
| v1.7.18 installed: /Users/mc/.nvm/versions/node/v24.14.1/bin/opencli | [npm](https://npmjs.com) |
| 90+ site adapters — GitHub, LinkedIn, Notion, Jira, Figma, Confluence | [OpenCLI](https://github.com/jackwener/opencli) |
| Zero LLM cost — Chrome session + adapter, no API calls consumed | [OpenCLI](https://github.com/jackwener/opencli) |
| Persistent Chrome session — never triggers re-login between calls | [OpenCLI](https://github.com/jackwener/opencli) |
| opencli linkedin search — lead scraping without API rate limits | [OpenCLI](https://github.com/jackwener/opencli) |
| Wire OpenCLI into MAE: mae run triggers opencli adapters for data | [MAE](https://github.com/hmzainjamil/claude-ai-system) |

<a id="tips-composio_6"></a>
### ■ **Composio (6)**
| Tip | Source |
|---|---|
| 3000+ tool actions — Salesforce, HubSpot, Notion, Linear, GitHub, Slack | [Composio](https://composio.dev) |
| Single auth flow covers all tools — OAuth, API key, basic auto-handled | [Composio](https://composio.dev) |
| Server-side execution — no browser or desktop app required | [Composio](https://composio.dev) |
| Combine with MAE: decompose goal → Composio executes SaaS actions | [MAE](https://github.com/hmzainjamil/claude-ai-system) |
| Token refresh auto-handled — credentials never expire mid-workflow | [Composio](https://composio.dev) |
| composio-openclaw repo wires Composio into OpenCLI flow | [hmz-composio-openclaw](https://github.com/hmzainjamil/hmz-composio-openclaw) |

<a id="tips-n8n_workflows_6"></a>
### ■ **n8n Workflows (6)**
| Tip | Source |
|---|---|
| 8,159 workflows in index — grep before building from scratch ever | [n8n](https://github.com/hmzainjamil/hmz-n8n-workflows) |
| Error workflow: all nodes → Slack alert + retry on any failure | [n8n](https://n8n.io) |
| Queue mode + Redis: handles 1000+ concurrent workflow executions | [n8n](https://n8n.io) |
| Deploy workflow: bash bin/deploy.sh workflows/my-flow.json | [n8n](https://github.com/hmzainjamil/hmz-n8n-workflows) |
| Split In Batches node: process 10K+ records without OOM errors | [n8n](https://n8n.io) |
| MAE bridge: mae run triggers n8n for execution-heavy automation | [MAE](https://github.com/hmzainjamil/claude-ai-system) |

<a id="tips-paperclip_os_6"></a>
### ■ **Paperclip OS (6)**
| Tip | Source |
|---|---|
| Paperclip AI = always-on zero-human company OS — autopilot co-founder | [Paperclip](https://paperclip.ai) |
| All MAE outputs auto-synced to Paperclip — full searchable audit trail | [Paperclip](https://paperclip.ai) |
| Set auto-approve for low-risk decisions — true zero-human ops layer | [Paperclip](https://paperclip.ai) |
| Paperclip ingests n8n outputs via webhook → structured company memory | [Paperclip](https://paperclip.ai) |
| Cross-session context: Paperclip + MEMORY.md = never lose context | [Paperclip](https://paperclip.ai) |
| Review Paperclip autonomous decisions weekly — full decision audit | [Paperclip](https://paperclip.ai) |

<a id="tips-launchagents_6"></a>
### ■ **LaunchAgents (6)**
| Tip | Source |
|---|---|
| KeepAlive=true + RunAtLoad=true = always-on service, survives reboots | [launchd](https://developer.apple.com) |
| Set HOME + PATH in EnvironmentVariables — scripts find all tools | [launchd](https://developer.apple.com) |
| Log stdout/stderr to /tmp/ — check if LaunchAgent crashes silently | [launchd](https://developer.apple.com) |
| Reload: launchctl unload then load — applies plist config changes | [launchd](https://developer.apple.com) |
| ThrottleInterval=10 — prevents restart loop on persistent crash | [launchd](https://developer.apple.com) |
| launchctl list | grep ai.hmz — verify all services running | [launchd](https://developer.apple.com) |

---

## ☠️ STARTUPS / BUSINESSES

| Feature | Replaced |
|---|---|
| MAE orchestration | [CrewAI](https://crewai.com) |
| Tier 0 model routing | [LiteLLM](https://litellm.ai) |
| Always-on LaunchAgent | [Heroku Dynos](https://heroku.com) |
| n8n automation library | [Zapier](https://zapier.com) |
| Paperclip company OS | [Notion AI](https://notion.ai) |
| Cross-LLM parallel blast | [Together AI](https://together.ai) |
| Health monitoring | [Datadog](https://datadoghq.com) |
| Skill auto-routing | [LangChain](https://langchain.com) |
| Session memory | [Mem.ai](https://mem.ai) |
| Webhook triggers | [Segment](https://segment.com) |
| PDF report generation | [Beautiful.ai](https://beautiful.ai) |
| Task queue | [Linear](https://linear.app) |
| 90+ site adapters | [Browser.ai](https://browser.ai) |
| 3000+ SaaS actions | [Zapier](https://zapier.com) |
| Parallel model burst | [Replicate](https://replicate.com) |

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hmzainjamil/hmz-openclaw-skills-official&type=Date)](https://star-history.com/#hmzainjamil/hmz-openclaw-skills-official&Date)
