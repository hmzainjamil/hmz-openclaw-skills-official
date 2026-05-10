# hmz-openclaw-skills-official

> **Official OpenClaw skill set** — skills optimized for the OpenClaw gateway, enabling intelligent multi-provider AI routing within Claude Code.

Part of [claude-ai-system](https://github.com/hmzainjamil/claude-ai-system).

---

## Overview

The official skill library designed specifically for the OpenClaw gateway. Each skill is tested for cost efficiency, routing correctness, and output quality across all supported providers.

---

## Skill Categories

### Model Routing Skills

| Skill | Purpose | Routes To |
|---|---|---|
| `code-gen-router` | Code generation tasks | DeepSeek-V3 |
| `research-router` | Research and analysis | Groq llama3-70b |
| `content-router` | Content drafting | GPT-4o-mini |
| `reasoning-router` | Complex reasoning | DeepSeek-V3 |
| `local-first-router` | Force local model | Ollama / GPT4All |
| `free-only-router` | Only free-tier models | Groq + Gemini |

### Provider Skills

| Skill | Provider | Best For |
|---|---|---|
| `groq-burst` | Groq | Ultra-fast inference |
| `gemini-research` | Gemini 2.0 Flash | Research, summarization |
| `deepseek-code` | DeepSeek-V3 | Code generation, debugging |
| `openrouter-smart` | OpenRouter | Dynamic cheapest routing |
| `ollama-local` | Ollama | Offline, zero-cost tasks |
| `gpt4all-metal` | GPT4All | Mac GPU-accelerated local |

### Quality & Cost Control

| Skill | Purpose |
|---|---|
| `output-validator` | Validate quality before returning to Claude |
| `cost-guard` | Block expensive calls when cheaper alternative exists |
| `fallback-handler` | Retry with backup model on provider failure |
| `token-counter` | Track token usage per provider per session |

---

## How Skills Activate

```bash
# Auto-routes through OpenClaw gateway on every task
# No manual setup required

# Manual override for session
~/.claude/bin/skill-on code-gen-router
# Forces DeepSeek-V3 for all code tasks this session
```

---

## Cost Rules (Hard-Enforced)

1. Never use Claude for tasks where Groq/Gemini achieves same quality
2. Always try local Ollama first for tasks under 500 tokens
3. Use OpenRouter smart routing for tasks over 2k tokens
4. Batch parallel calls — 1 round-trip beats 5 sequential
5. Cache repeated research calls within same session

---

## Integration with OpenClaw

```
Skill loaded → OpenClaw reads routing preference
→ All model calls for this task routed accordingly
→ Cost tracked in ~/.claude/logs/openclaw.log
```

---

## Full System

[claude-ai-system](https://github.com/hmzainjamil/claude-ai-system) | [hmz-openclaw](https://github.com/hmzainjamil/hmz-openclaw) | [claude-ai-skills](https://github.com/hmzainjamil/claude-ai-skills)

*HMZ AI Agency — auto-synced daily*
