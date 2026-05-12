# hmz-openclaw-skills-official
> 37 official OpenClaw skills — curated for Claude Code from the OpenClaw marketplace.

[![openclaw](https://img.shields.io/badge/openclaw-active-blue?style=flat&labelColor=555)](.)
[![mae](https://img.shields.io/badge/MAE-powered-green?style=flat&labelColor=555)](.)
[![tier0](https://img.shields.io/badge/tier0-11models-orange?style=flat&labelColor=555)](.)
[![license](https://img.shields.io/badge/license-MIT-lightgrey?style=flat&labelColor=555)](LICENSE)

[concepts](#concepts) · [architecture](#architecture) · [tips](#tips) · [startups](#startups) · [star](#star)

---

## 🧠 CONCEPTS <a id="concepts"></a>

| Feature | Location | Description |
|---|---|---|
| [**MAE Integration**](~/.claude/bin/mae) | `~/.claude/bin/mae` | All tasks routed through MAE swarm — 12 agents, wave-batched, RAM-safe |
| [**Tier 0 Routing**](~/.claude/tier0.env) | `~/.claude/tier0.env` | Groq · Gemini · DeepSeek · Kimi · Bytez — $0 for 95% of tasks |
| [**TCC Queue**](~/.claude/bin/tcc) | `~/.claude/bin/tcc` | `tcc blast "t1" "t2"` — parallel task execution |
| [**llm-burst**](~/.claude/bin/llm-burst) | `~/.claude/bin/llm-burst` | 11 models race simultaneously — Bytez + Groq + Gemini + Kimi + ... |
| [**Paperclip**](http://127.0.0.1:3100) | `http://127.0.0.1:3100` | CEO layer — goals, budgets, agent org chart, cost tracking |
| [**OpenCLI**](~/installed-repos/opencli/) | `~/installed-repos/opencli/` | 90+ site adapters — zero LLM cost per call |
| [**Deer Flow**](~/installed-repos/deer-flow/) | `~/installed-repos/deer-flow/` | ByteDance deep research pipeline |
| [**auto-github-push**](~/.claude/bin/auto-github-push) | `~/.claude/bin/auto-github-push` | PostToolUse hook — auto-uploads any new script to GitHub |

### 🔥 Hot

| Feature | Location | Description |
|---|---|---|
| [**Bytez 100+ models**](~/.claude/bin/llm-burst) | `~/.claude/bin/llm-burst` | `call_bytez()` — free OpenAI-compatible API, integrated in burst |
| [**Codex delegation**](.) | `~/.claude/bin/mae` | MAE delegates complex coding to OpenAI Codex agent automatically |
| [**Kimi K2.6**](~/.claude/tier0.env) | `~/.claude/tier0.env` | 262K context, vision, video — replaces Claude Opus at 5% cost |

---

## ⚙️ ARCHITECTURE <a id="architecture"></a>

```
User prompt → mae run "goal"
        │
  TCC decompose (Groq fast)
        │
  ┌─────┴────────────────────────────┐
  │    Tier 0 Swarm (11 models)      │
  │  Kimi-K2.6 · Groq · Gemini      │
  │  DeepSeek · Bytez · Ollama       │
  │  GLM · GPT4o · OpenRouter       │
  └─────────────────────────────────┘
        │
  Groq-70B synthesis
        │
  ~/.claude/tcc-logs/ + Paperclip
```

---

## 💡 TIPS AND TRICKS (8) <a id="tips"></a>

[mae-ops](#tips-mae) · [models](#tips-models)

<a id="tips-mae"></a>
■ **MAE Operations (4)**

| Tip | Source |
|---|---|
| `mae run "goal"` — always the default. 12 agents, ~8s, max quality. | [hmzainjamil](https://github.com/hmzainjamil) |
| `tcc blast "t1" "t2" "t3"` — parallel fire multiple tasks simultaneously | [hmzainjamil](https://github.com/hmzainjamil) |
| `tcc fire all` — execute entire pending queue at once | [hmzainjamil](https://github.com/hmzainjamil) |
| `mae daily` — full DigiMinds ops: email, leads, content, KPI report | [hmzainjamil](https://github.com/hmzainjamil) |

<a id="tips-models"></a>
■ **Tier 0 Models (4)**

| Tip | Source |
|---|---|
| Bytez free tier: `BYTEZ_API_KEY=cb4a7065a586ec6ca26394724ce5ec49` — 100+ models | [Bytez](https://bytez.com) |
| Groq `llama-3.3-70b-versatile` — synthesis. `llama-3.1-8b-instant` — decomposition | [Groq](https://groq.com) |
| `llm-burst --models bytez,groq,gemini "prompt"` — 3 free models race in ~2s | [hmzainjamil](https://github.com/hmzainjamil) |
| Kimi K2.6: 262K context, vision, video. `--models kimi-k2.6` in llm-burst | [Moonshot AI](https://moonshot.cn) |

---

## ☠️ STARTUPS / BUSINESSES <a id="startups"></a>

| Feature | Replaced |
|---|---|
| **MAE 12-agent swarm** | [AutoGPT](https://autogpt.net), [CrewAI](https://crewai.com), [SuperAGI](https://superagi.com) |
| **Bytez 100+ free models** | [OpenRouter paid](https://openrouter.ai), [Together AI](https://together.ai) |
| **TCC parallel task queue** | [Linear](https://linear.app), [ClickUp AI](https://clickup.com), [Asana](https://asana.com) |
| **Paperclip company OS** | [Notion AI](https://notion.so), [Monday.com](https://monday.com) |

---

## Star History <a id="star"></a>
[![Star History Chart](https://api.star-history.com/svg?repos=hmzainjamil/hmz-openclaw-skills-official&type=Date)](https://star-history.com/#hmzainjamil/hmz-openclaw-skills-official&Date)
