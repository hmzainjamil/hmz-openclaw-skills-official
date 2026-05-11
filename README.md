# hmz-openclaw-skills-official

> **Official OpenClaw skill definitions — production-grade Claude Code skills for OpenClaw gateway**

[![skills](https://img.shields.io/badge/skills-official-blue?style=flat)](.) [![gateway](https://img.shields.io/badge/gateway-OpenClaw-purple?style=flat)](.) [![status](https://img.shields.io/badge/status-production-brightgreen?style=flat)](.)

[Overview](#overview) · [Skills](#skills) · [Format](#format) · [Usage](#usage) · [Tips](#tips)

---

## 🧠 OVERVIEW

Official repository of Claude Code skill definitions for the OpenClaw gateway. These skills extend Claude Code's capabilities with domain-specific knowledge, tool orchestration, and automated workflows. All skills follow the blockchain manifest pattern — load only what's needed, unload after.

| Component | Value |
|---|---|
| Gateway | OpenClaw (ai.openclaw.gateway LaunchAgent) |
| Skill format | SKILL.md with frontmatter metadata |
| Activation | `skill-on <name>` / auto via `skill-auto-activate` |
| Location | `~/.claude/skills/` (active) or `~/.claude/skills-archive/` (dormant) |
| Lock file | `~/.claude/skills-lock.json` (manifest) |

---

## ⚙️ SKILL ARCHITECTURE

```
~/.claude/skills/              ← always-active core skills
~/.claude/skills-archive/      ← dormant, loaded on demand
~/.claude/bin/skill-on         ← activate: moves archive→active
~/.claude/bin/skill-off        ← deactivate: moves active→archive
~/.claude/bin/skill-search     ← find skills by keyword
~/.claude/bin/skill-auto-activate  ← UserPromptSubmit hook
```

| Component | Purpose |
|---|---|
| `SKILL.md` | Skill definition file with instructions |
| `skills-lock.json` | Blockchain manifest tracking active state |
| `skill-router` | Routes prompts to relevant skills |
| `find-skills` | Discovery tool for skill matching |

---

## 📦 SKILL CATEGORIES

| Category | Skills | Auto-activated by |
|---|---|---|
| Core (always on) | caveman, compress, context-compression, compact-guard, summarize, skill-router | Always |
| Ads | ads-strategy, ads-copy, ads-creative, ads-keywords | "ads, ppc, meta, google ads, campaign" |
| SEO/GEO | geo, geo-technical, geo-content, geo-schema | "seo, geo, ranking, schema" |
| Legal | legal, legal-review | "legal, contract, nda, compliance" |
| Agency | agency, agency-client, agency-pipeline | "agency, client, proposal" |
| AI/Agents | all-agents | "agent, multi-agent, orchestrate" |

---

## 📄 SKILL FORMAT

```markdown
---
name: skill-name
description: One-line description for auto-activation matching
triggers: [keyword1, keyword2, keyword3]
tier: core|domain|specialized
---

# Skill: <Name>

## Purpose
What this skill does and when to use it.

## Instructions
Step-by-step behavior for Claude to follow.

## Examples
Concrete examples of the skill in action.
```

---

## 💡 TIPS

■ **Skill Management (5)**
| Tip | Source |
|---|---|
| `skill-search <keyword>` finds the right skill before activating | CLI ref |
| Never leave domain skills active after task — always run `skill-off` | Gating protocol |
| `skill-auto-activate` runs on every prompt via UserPromptSubmit hook | Hook config |
| Core skills cost near-zero tokens — domain skills cost more | Token economics |
| `~/.claude/skills-lock.json` shows currently active skill manifest | Manifest |

■ **Development (4)**
| Tip | Source |
|---|---|
| New skills go in `skills-archive/` first — activate to test | Dev workflow |
| Skill triggers must be specific — avoid broad words that fire on everything | Design rule |
| Test skill with `skill-on <name>` then test prompt, then `skill-off` | QA workflow |
| SKILL.md frontmatter `description` is used for auto-match — make it specific | Format spec |

---

## ☠️ TOOLS REPLACED

| OpenClaw Skills | Replaced |
|---|---|
| Domain-specific Claude behavior | Generic prompts every time |
| Auto-activation | Manually pasting instructions |
| Skill gating | Loading everything = slow, expensive |
| Manifest tracking | Not knowing what's active |

---

## ⚠️ GOTCHAS

| Issue | Fix |
|---|---|
| Skill fires on wrong prompt | Tighten trigger keywords in frontmatter |
| Skill stays active after task | Always `skill-off <name>` after completion |
| `skill-auto-activate` not running | Check UserPromptSubmit hook in settings.json |
| Skills in wrong folder | `active → ~/.claude/skills/`, `dormant → skills-archive/` |

---

*Part of [DigiMinds AI Agency Stack](https://github.com/hmzainjamil) — OpenClaw skill ecosystem*
