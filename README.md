# hmz-openclaw-skills-official

> **Official OpenClaw Skill Set** — curated skills optimized specifically for the OpenClaw AI gateway, enabling intelligent multi-provider model routing within Claude Code.

Part of [claude-ai-system](https://github.com/hmzainjamil/claude-ai-system).

---

## Overview

Standard Claude Code skills tell Claude what to do. OpenClaw skills go further — they also tell OpenClaw *how to route the task* to the cheapest capable model, ensuring cost optimization is embedded into the skill itself.

Every skill here ships with:
- Task detection logic
- Provider routing preference
- Cost guard rules
- Fallback model chain

---

## Skill Categories

### Model Routing Skills

These skills control which model handles each task type:

| Skill | Routes To | Fallback | Use When |
|---|---|---|---|
| `code-gen-router` | DeepSeek-V3 | GPT-4o-mini | Any code generation task |
| `research-router` | Groq llama3-70b | Gemini 2.0 Flash | Research, analysis, fact-finding |
| `content-router` | GPT-4o-mini | Gemini Flash | Content drafting, copywriting |
| `reasoning-router` | DeepSeek-V3 | Groq llama3 | Logic, math, complex analysis |
| `local-first-router` | Ollama llama3 | GPT4All Phi-3 | Any task, force local/free |
| `free-only-router` | Groq (free tier) | Gemini (free tier) | Zero-cost requirement |
| `fast-router` | Groq (fastest) | Gemini Flash | Latency-sensitive tasks |
| `long-context-router` | Gemini 1.5 Pro | DeepSeek-V3 | >50k token documents |

### Provider-Specific Skills

| Skill | Provider | Token Cost | Best For |
|---|---|---|---|
| `groq-burst` | Groq | Free | Ultra-fast inference, real-time tasks |
| `gemini-research` | Gemini 2.0 Flash | Free | Research, summarization, long docs |
| `deepseek-code` | DeepSeek-V3 | ~$0.001/1k | Complex code, debugging, architecture |
| `openrouter-smart` | OpenRouter (dynamic) | ~$0.001/1k | Any task, auto-selects cheapest |
| `ollama-local` | Ollama | Free forever | Offline tasks, zero API cost |
| `gpt4all-metal` | GPT4All (Metal GPU) | Free forever | Mac-accelerated local inference |
| `glm-fast` | GLM 4.5-air | Low cost | Multilingual, fast response |

### Quality & Cost Control Skills

| Skill | Function |
|---|---|
| `output-validator` | Score response quality before returning to Claude (reject if below threshold) |
| `cost-guard` | Block expensive model calls when cheaper alternative exists |
| `fallback-handler` | Auto-retry with backup model on provider failure or timeout |
| `token-counter` | Track token usage per provider per session → report savings |
| `parallel-batcher` | Combine multiple small calls into one batch (fewer round-trips) |
| `cache-hit-checker` | Detect repeated research queries → return cached result (zero cost) |

---

## Skill Format

Each skill ships as a `SKILL.md` with OpenClaw routing metadata:

```markdown
---
name: code-gen-router
type: openclaw-routing
preferred_model: deepseek-v3
fallback_chain: [gpt-4o-mini, groq/llama3-70b, ollama/llama3]
max_cost_per_call: 0.005
triggers: [code, generate, build, write function, implement, debug]
---

## Routing Behavior
When this skill is active, all code generation tasks route to DeepSeek-V3.
Claude handles: final review, integration, user-facing explanation.
DeepSeek-V3 handles: actual code writing, debugging, refactoring.
```

---

## Activation

```bash
# Auto-activates via OpenClaw gateway keyword detection
# No manual setup required for gateway-managed skills

# Manual session override
~/.claude/bin/skill-on code-gen-router
# → All code tasks this session route to DeepSeek-V3

# Check active routing skills
~/.claude/bin/skill-on --list | grep router

# Deactivate after task
~/.claude/bin/skill-off code-gen-router
```

---

## Cost Enforcement Rules (Hard-Coded)

These rules apply to every task regardless of skill:

1. **Never use Claude for sub-tasks** — Claude is final output synthesis only
2. **Local first for short tasks** — Ollama/GPT4All for tasks under 500 tokens
3. **OpenRouter for long tasks** — 2k+ tokens → dynamic cheapest model
4. **Batch parallel calls** — 1 round-trip beats 5 sequential calls
5. **Cache research within session** — same research query in same session = cache hit
6. **Block Opus for everything** — Opus only on explicit user request

---

## Token Savings Report

```bash
# End of session summary
cat ~/.claude/logs/openclaw.log | grep "session_summary" | tail -1

# Example output:
# Claude tokens: 2,847 (final synthesis only)
# Tier 0 tokens: 48,391 (sub-tasks, research, code gen)
# Cost: $0.051 total vs $3.62 if all-Claude
# Savings: 98.6%
```

---

## Full System

[claude-ai-system](https://github.com/hmzainjamil/claude-ai-system) | [hmz-openclaw](https://github.com/hmzainjamil/hmz-openclaw) | [claude-ai-skills](https://github.com/hmzainjamil/claude-ai-skills)

---

*HMZ AI Agency — auto-synced daily at 6:30 AM*
