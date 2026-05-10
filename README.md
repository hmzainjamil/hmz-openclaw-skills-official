# hmz-openclaw-skills-official

> **Official OpenClaw skill set** — curated skills optimized for the OpenClaw gateway, enabling multi-provider AI routing within Claude Code workflows.

Part of [claude-ai-system](https://github.com/hmzainjamil/claude-ai-system).

---

## Overview

These are the official skills designed and tested specifically for the OpenClaw AI gateway. Each skill is optimized for cost efficiency, routing correctness, and output quality.

---

## Skill Categories

### Model Routing Skills
| Skill | Purpose | Preferred Model |
|---|---|---|
| `code-gen-router` | Route code generation tasks | DeepSeek-V3 |
| `research-router` | Route research + analysis | Groq llama3-70b |
| `content-router` | Route content drafting | GPT-4o-mini |
| `reasoning-router` | Route complex reasoning | DeepSeek-V3 |
| `local-first-router` | Force local model (Ollama/GPT4All) | Ollama |

### Provider Skills
| Skill | Provider | Use Case |
|---|---|---|
| `groq-burst` | Groq | Ultra-fast inference tasks |
| `gemini-research` | Gemini 2.0 Flash | Research, summarization |
| `deepseek-code` | DeepSeek-V3 | Code generation, debugging |
| `openrouter-smart` | OpenRouter | Dynamic cheapest model |
| `ollama-local` | Ollama | Offline, zero-cost tasks |

### Quality Control Skills
| Skill | Purpose |
|---|---|
| `output-validator` | Validate model output quality before returning |
| `cost-guard` | Reject expensive model calls when cheaper alternative exists |
| `fallback-handler` | Retry with backup model on provider failure |

---

## Integration

```bash
# Auto-activates via OpenClaw gateway
# No manual setup required — gateway routes based on task type

# Manual override
~/.claude/bin/skill-on code-gen-router
# → Forces DeepSeek-V3 for all code tasks this session
```

---

## Cost Optimization Rules

1. Never use Claude for tasks where Groq/Gemini suffice
2. Always try local Ollama first for small tasks (< 500 tokens)
3. Use OpenRouter smart routing for tasks over 2k tokens
4. Batch parallel calls — 1 round-trip beats 5 sequential

---

## Full System

[claude-ai-system](https://github.com/hmzainjamil/claude-ai-system) | [hmz-openclaw](https://github.com/hmzainjamil/hmz-openclaw) | [claude-ai-skills](https://github.com/hmzainjamil/claude-ai-skills)

---

*HMZ AI Agency — auto-synced daily*
