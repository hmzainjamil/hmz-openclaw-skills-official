# hmz-openclaw-skills-official

> **Official OpenClaw skill definitions — production Claude Code skills for domain-specific capabilities, auto-activated by keyword matching via UserPromptSubmit hook**

[![skills](https://img.shields.io/badge/skills-official_production-blue?style=flat)](.) [![gateway](https://img.shields.io/badge/gateway-OpenClaw-purple?style=flat)](.) [![activation](https://img.shields.io/badge/activation-auto_on_demand-green?style=flat)](.) [![manifest](https://img.shields.io/badge/manifest-blockchain_gated-orange?style=flat)](.)

[Overview](#overview) · [Architecture](#architecture) · [Skill Inventory](#skill-inventory) · [Format](#format) · [Activation](#activation) · [Tips](#tips) · [Gotchas](#gotchas)

---

## 🧠 OVERVIEW

Official repository of Claude Code skill definitions for the OpenClaw gateway. Skills are SKILL.md files containing domain-specific instructions, tool references, and behavioral rules — loaded into Claude's context on demand. The blockchain manifest (`skills-lock.json`) tracks exactly which skills are active at any moment. Zero token overhead when dormant.

| Component | Value |
|---|---|
| Gateway | OpenClaw (`ai.openclaw.gateway` LaunchAgent) |
| Active skills location | `~/.claude/skills/` |
| Dormant skills location | `~/.claude/skills-archive/` |
| Skill format | SKILL.md with YAML frontmatter |
| Manifest | `~/.claude/skills-lock.json` |
| Auto-activate | `~/.claude/bin/skill-auto-activate` (UserPromptSubmit hook) |
| Manual activate | `~/.claude/bin/skill-on <name>` |
| Deactivate | `~/.claude/bin/skill-off <name>` |
| Search | `~/.claude/bin/skill-search <keyword>` |
| Status | `~/.claude/bin/skill-status` |

---

## ⚙️ ARCHITECTURE

```
User prompt
    │
    ▼
UserPromptSubmit hook → skill-auto-activate
    │
    ├─► keyword match → skill-on <matched-skill>
    │       └─► move archive → active
    │       └─► update skills-lock.json manifest
    │
    ▼
Claude session loads ~/.claude/skills/ (active only)
    │
    ▼
Task completes → skill-off <name>
    │
    └─► move active → archive
    └─► update manifest
```

| Component | Role |
|---|---|
| `skill-auto-activate` | Keyword matcher — fires on every prompt |
| `skill-on` | Activates: moves skill dir from archive → skills/ |
| `skill-off` | Deactivates: moves skill dir from skills/ → archive/ |
| `skill-search` | Finds skills by keyword in SKILL.md content |
| `skill-status` | Shows current manifest — what's active + timestamps |
| `skill-router` | Always-on core skill for routing decisions |
| `skills-lock.json` | Blockchain manifest tracking active state |

---

## 📦 SKILL INVENTORY

### Always-Active Core (never unloaded)
| Skill | Purpose | Token Cost |
|---|---|---|
| `caveman` | Context compression — saves 40% tokens | Near-zero |
| `compress` | Output compression for long responses | Near-zero |
| `context-compression` | Window management | Near-zero |
| `context-window-management` | Prevents context overflow | Near-zero |
| `compact-guard` | Blocks context dumps | Near-zero |
| `summarize` | Structured summarization | Near-zero |
| `skill-router` | Routes to correct domain skill | Near-zero |
| `find-skills` | Discovery tool | Near-zero |
| `launch-optimized` | Session startup optimization | One-time |

### Domain Skills (load on demand)
| Category | Skills | Trigger Keywords |
|---|---|---|
| Ads | `ads-strategy`, `ads-copy`, `ads-creative`, `ads-keywords`, `ads-audience`, `ads-funnel`, `ads-landing`, `ads-video` | ads, ppc, meta, google ads, campaign, roas |
| SEO/GEO | `geo`, `geo-technical`, `geo-content`, `geo-schema`, `geo-citability` | seo, geo, ranking, schema, crawl, ai visibility |
| Legal | `legal`, `legal-review` | legal, contract, nda, compliance, terms |
| Agency | `agency`, `agency-client`, `agency-pipeline` | agency, client, proposal, pipeline, retainer |
| AI/Agents | `all-agents` | agent, multi-agent, orchestrate, paperclip |
| Apify | `apify-actor-development`, `apify-ultimate-scraper` | apify, scrape, extract, actor, crawl |
| Startup | `startup-optimized`, `market-launch` | startup, mvp, founder, investor, launch |
| Market | `market-ads`, `market-social`, `market-brand` | marketing, brand, social, content |

---

## 📄 SKILL FILE FORMAT

```markdown
---
name: ads-strategy
description: PPC campaign strategy — Google Ads, Meta Ads, ROAS optimization, audience targeting
triggers: [ads, ppc, google ads, meta ads, campaign, roas, cpc, ctr, audience]
tier: domain
dependencies: []
---

# Skill: Ads Strategy

## Purpose
When to use this skill and what it enables.

## Instructions
Step-by-step behavioral rules for Claude to follow.
Written as direct commands: "Always check...", "Never assume..."

## Tool References
Which MCP tools or external systems to use.

## Examples
Concrete examples showing correct skill application.

## Gotchas
Common mistakes and how to avoid them.
```

---

## ⚡ ACTIVATION WORKFLOW

```bash
# 1. Search for the right skill
~/.claude/bin/skill-search "google ads"
# → matches: ads-strategy, ads-keywords, ads-copy, ads-creative

# 2. Activate what you need
~/.claude/bin/skill-on ads-strategy
# → moves ~/.claude/skills-archive/ads-strategy/ → ~/.claude/skills/
# → updates skills-lock.json

# 3. Skill is now in context for the session

# 4. After task — always deactivate
~/.claude/bin/skill-off ads-strategy
# → moves back to archive
# → updates manifest

# 5. Check what's active
~/.claude/bin/skill-status
# → shows manifest: active skills + timestamp each was loaded
```

---

## 💡 TIPS

■ **Skill Management (6)**
| Tip | Source |
|---|---|
| `skill-auto-activate` handles 80% of cases — manual only for edge cases | Design |
| Never leave domain skills active after task — `skill-off` is mandatory | Gating rule |
| `skill-status` shows exact manifest — use before starting complex tasks | Debug |
| Archive skills cost zero tokens — loading costs context space | Token economics |
| New skills go to archive first — activate to test, then promote if stable | Dev workflow |
| Core skills can NEVER be unloaded — they're always-on by design | Architecture |

■ **Skill Development (5)**
| Tip | Source |
|---|---|
| SKILL.md frontmatter `description` drives auto-match — make it specific | Format spec |
| `triggers` list = keywords that fire auto-activate | Activation system |
| Keep skill instructions imperative: "Always X", "Never Y" — not descriptive | Writing style |
| Test activation: `skill-on <name>` → trigger prompt → verify behavior | QA workflow |
| Skills that depend on MCP tools must list them in frontmatter | Dependency tracking |

■ **Performance (4)**
| Tip | Source |
|---|---|
| Active skill count should stay under 5 — more = context bloat | Performance rule |
| Long SKILL.md files slow down context loading — keep under 500 lines | Size limit |
| Domain skills with heavy references (example code etc.) = expensive | Token cost |
| Core skills are optimized — zero overhead on every session | Core design |

■ **Debugging (3)**
| Tip | Source |
|---|---|
| Skill not activating → check frontmatter `triggers` list | Debug |
| Wrong skill activating → tighten trigger keywords | Debug |
| Skill active but Claude not using it → check SKILL.md instructions clarity | Debug |

---

## ☠️ TOOLS REPLACED

| OpenClaw Skills | Replaced |
|---|---|
| On-demand domain knowledge | Pasting instructions manually into every prompt |
| Auto-activation by keyword | Manually tracking which skill applies |
| Blockchain manifest | Not knowing what's loaded — context confusion |
| Core always-on compression | Wasting tokens on verbosity |
| Skill deactivation | Leaving context polluted after tasks |
| Archive dormancy | Loading 100+ skills always = slow + expensive |
| Skill search | Scrolling through lists to find the right skill |
| Dependency tracking | Breaking sessions with missing tool dependencies |

---

## ⚠️ GOTCHAS

| Issue | Fix |
|---|---|
| Skill fires on wrong prompt | Tighten `triggers` list in frontmatter — remove broad keywords |
| Domain skill stays active | Always run `skill-off <name>` — don't skip cleanup |
| `skill-auto-activate` not running | Check UserPromptSubmit hook in `~/.claude/settings.json` |
| Skills in wrong folder | Active → `~/.claude/skills/`, dormant → `skills-archive/` |
| Symlink conflicts in skills/ | Delete symlink, re-create as real directory |
| Manifest out of sync | `~/.claude/bin/skill-reset` rebuilds manifest from filesystem |
| Core skill shows as inactive | These are hardcoded — ignore manifest for core skills |
| skill-on fails | Check permissions: `chmod +x ~/.claude/bin/skill-on` |

---

## 🚀 QUICK REFERENCE

```bash
# Find a skill
~/.claude/bin/skill-search "competitor intel"

# Activate
~/.claude/bin/skill-on ads-competitors

# Deactivate
~/.claude/bin/skill-off ads-competitors

# See full manifest
~/.claude/bin/skill-status

# Reset all to default (core only)
~/.claude/bin/skill-reset

# List all available skills
ls ~/.claude/skills-archive/
```

---

*Part of [DigiMinds AI Agency Stack](https://github.com/hmzainjamil) — OpenClaw skill ecosystem | Official production definitions*
