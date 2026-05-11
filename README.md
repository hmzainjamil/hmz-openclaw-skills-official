# hmz-openclaw-skills-official

![OpenClaw](https://img.shields.io/badge/OpenClaw-Official_Skills-E74C3C?style=flat&labelColor=000) ![Skills](https://img.shields.io/badge/skills-production_certified-blue?style=flat&labelColor=555) ![Gateway](https://img.shields.io/badge/gateway-port_51827-orange?style=flat&labelColor=555) ![Status](https://img.shields.io/badge/status-always--on-green?style=flat&labelColor=555)

OpenClaw official skill library — production-certified MCP skills that extend Claude's capabilities through the OpenClaw gateway. These are not experimental prompts. Every skill here has been validated, versioned, and deployed to the permanent LaunchAgent at `ai.openclaw.gateway`.

## 🧠 WHAT THIS IS

OpenClaw runs at `http://127.0.0.1:51827` as a permanent LaunchAgent. It exposes skills to Claude Code as MCP tools — each skill is a purpose-built capability with its own input schema, routing config, and output contract.

This repo holds the _official_ skill set: vetted, tested, and locked. Experimental skills live in `hmz-skills-archive` until they graduate here.

| Skill | Tool Name | Description |
|---|---|---|
| Model Router | `oclaw_route` | Routes any task to cheapest capable model (Tier 0 mandate) |
| Cost Estimator | `oclaw_estimate_cost` | Estimates token cost before running expensive tasks |
| Prompt Compressor | `oclaw_compress` | Caveman-compresses any prompt to cut token overhead |
| Skill Searcher | `oclaw_skill_search` | Finds matching skills by keyword from the manifest |
| Context Guard | `oclaw_context_check` | Warns when context window approaching limit |
| Memory Writer | `oclaw_save_memory` | Writes structured memory files with correct frontmatter |
| LaunchAgent Monitor | `oclaw_launchagent_status` | Lists all LaunchAgents with status, exit codes, PID |

## ⚙️ GATEWAY ARCHITECTURE

```
Claude Code Tool Call
    ↓
OpenClaw MCP Server (port 51827)
    ↓ skill lookup
Skill Registry (this repo)
    ↓ route decision
Tier 0 Model (Ollama / Groq / Gemini / DeepSeek)
    ↓ result
Claude Code (final output only if needed)
```

**LaunchAgent config** (`~/Library/LaunchAgents/ai.openclaw.gateway.plist`):
```xml
<key>Label</key><string>ai.openclaw.gateway</string>
<key>KeepAlive</key><true/>
<key>RunAtLoad</key><true/>
<!-- port 51827, working dir: ~/installed-repos/openclaw -->
```

## 💡 SKILL SCHEMA

Every official skill file:

```yaml
---
skill: oclaw_route
version: 2.1.0
status: production
mcp_tool_name: oclaw_route
tier: 0
models: [ollama:llama3, groq:llama3-70b, gemini:flash, deepseek-v3]
fallback: claude-haiku
---
Route any task to the cheapest capable model. Accepts a task description
and complexity score (1-10), returns selected model + rationale.

Input: { task: string, complexity: 1-10, context_size: number }
Output: { model: string, reason: string, estimated_cost: number }
```

## 🔧 SKILL LIFECYCLE

```bash
# Promote a skill from archive to official
cp ~/.claude/skills-archive/my-skill.md ~/installed-repos/openclaw-skills-official/skills/
# → triggers gateway reload via file watcher

# Check skill status
curl http://127.0.0.1:51827/skills | jq '.[] | .name, .status'

# Invoke a skill directly
curl -X POST http://127.0.0.1:51827/invoke   -d '{"skill": "oclaw_compress", "input": {"text": "long prompt here"}}'

# Reload skills without restarting gateway
curl -X POST http://127.0.0.1:51827/reload
```

## ☠️ OFFICIAL VS ARCHIVE

| Criterion | Official (this repo) | Archive (`hmz-skills-archive`) |
|---|---|---|
| Tested in production | Yes | No |
| Has output schema | Required | Optional |
| Versioned | Semver | none |
| Auto-loads at startup | Yes | No — manual activation only |
| Failure behavior | Logged + fallback | May crash silently |

Skills graduate from archive → official after: 5+ successful uses, defined schema, fallback behavior documented.

## 📁 REPO STRUCTURE

```
hmz-openclaw-skills-official/
├── skills/
│   ├── oclaw_route.md
│   ├── oclaw_estimate_cost.md
│   ├── oclaw_compress.md
│   ├── oclaw_skill_search.md
│   ├── oclaw_context_check.md
│   ├── oclaw_save_memory.md
│   └── oclaw_launchagent_status.md
├── registry.json            ← machine-readable skill manifest
├── CHANGELOG.md             ← version history per skill
└── tests/
    └── skill-smoke-tests.sh ← validates all skills on gateway startup
```
