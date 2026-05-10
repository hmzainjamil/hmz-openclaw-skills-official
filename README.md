<div align="center">

# 🦞 OpenClaw Skills — Official Skill Registry

**Integrated by [Hafiz Muhammad Zulqarnain](https://github.com/hmzainjamil)**  
*Claude AI Power User | AI Systems Engineer*

[![System](https://img.shields.io/badge/Part_of-claude--ai--system-blue?style=flat-square)](https://github.com/hmzainjamil/claude-ai-system)
[![Skills](https://img.shields.io/badge/Skills-Official_Registry-blue?style=flat-square)](#)

</div>

---

## Overview

Official skill registry for OpenClaw — the Claude Code skill management framework. This repo contains the canonical skill definitions used across the HMZ AI system.

## What Are Skills?

Skills are structured prompts stored as markdown files that extend Claude's capabilities with domain-specific knowledge, workflows, and automation pipelines. Each skill activates via keyword detection and deactivates after the task completes.

## Skill Structure

```
skill-name/
├── SKILL.md          ← Main skill definition
│   ├── frontmatter   ← name, description, allowed-tools
│   ├── triggers      ← keywords that auto-activate this skill
│   ├── workflow      ← step-by-step pipeline
│   └── examples      ← usage examples
└── assets/           ← optional supporting files
```

## HMZ Active Skills (45 total)

| Category | Skills |
|---|---|
| Lead Generation | lead-gen-ai, vibe-prospecting, client-hunting |
| Website Building | website-builder, website-lead-agency, framer-motion-builder |
| Ads Management | ads-strategy, ads-copy, ads-creative, ads-keywords, ads-competitors |
| SEO & GEO | geo, geo-technical, geo-content, geo-schema, geo-ai-visibility |
| Reporting | report-creator, ads-report-pdf, audit-360 |
| UI/UX | ui-ux-promax, premium-web-design, framer-motion-builder |
| Agency Ops | ugc-agency, market-social, agency-pipeline |
| Optimization | optimize-commands, launch-optimized, caveman |
| Data | airtable-sdk, openpyxl-export |

## Skill Management Commands

```bash
# Activate a skill
~/.claude/bin/skill-on <skill-name>

# Deactivate a skill  
~/.claude/bin/skill-off <skill-name>

# Search skills
~/.claude/bin/skill-search <keyword>

# List all active skills
~/.claude/bin/skill-list

# Auto-activate based on prompt
~/.claude/bin/skill-auto-activate "your prompt here"
```

## Skill Archive

9,528 archived skills live at:
- **Local**: `~/.claude/skills-archive/`
- **GitHub**: [hmz-skills-archive](https://github.com/hmzainjamil/hmz-skills-archive)

---

**Part of [claude-ai-system](https://github.com/hmzainjamil/claude-ai-system)**
