<p align="center">
  <img src="https://img.shields.io/badge/HMZ-OPENCLAW%20SKILLS-E74C3C?style=for-the-badge&logoColor=white" alt="HMZ OpenClaw Skills" height="60">
</p>

<h1 align="center">HMZ OpenClaw Skills Official</h1>

<p align="center">
  <strong>Official OpenClaw skill collection — production skills for Claude Code, Cursor, Windsurf, and any MCP-compatible AI coding agent</strong>
</p>

<p align="center">
  <a href="https://github.com/hmzainjamil"><img src="https://img.shields.io/badge/By-HMZ-6C3EE8?style=for-the-badge" alt="By HMZ"></a>
  <a href="#skills"><img src="https://img.shields.io/badge/Skills-Official-E74C3C?style=for-the-badge" alt="Official Skills"></a>
  <a href="#"><img src="https://img.shields.io/badge/Claude%20Code-Native-15C1E6?style=for-the-badge" alt="Claude Code Native"></a>
  <a href="#"><img src="https://img.shields.io/badge/Cursor-Compatible-20A34E?style=for-the-badge" alt="Cursor Compatible"></a>
</p>

<p align="center">
  <a href="#overview">Overview</a> &bull;
  <a href="#quick-start">Quick Start</a> &bull;
  <a href="#skills">Skills</a> &bull;
  <a href="#use-cases">Use Cases</a> &bull;
  <a href="#installation">Installation</a>
</p>

---

## Overview

**HMZ OpenClaw Skills Official** is the official OpenClaw skill collection, maintained as part of the HMZ AI system. These skills extend Claude Code and other AI coding agents with deep domain expertise — paid media, SEO, lead generation, web scraping, and automation — delivered through the OpenClaw skill format.

OpenClaw skills differ from standard Claude Code skills in that they:
- Support **persistent state** across sessions (via OpenClaw gateway)
- Work across **multiple IDEs** (Claude Code, Cursor, Windsurf, Codex, Gemini CLI)
- Include **tool bindings** — each skill declares which MCP tools it requires
- Are **auto-versioned** — updates deploy without manual reinstall

---

## Quick Start

```bash
# Install via OpenClaw CLI
openclaw skill install hmz-openclaw-skills-official

# Or install individual skills
openclaw skill install ads-strategy
openclaw skill install apify-ultimate-scraper
openclaw skill install lead-gen-ai

# Or reference skills directly in Claude Code
/plugin install ads-strategy@hmz-openclaw-skills-official
```

---

## Skills

| Skill | Domain | Key capability |
|---|---|---|
| `ads-strategy` | Paid Media | Full campaign architecture, budget allocation, bidding |
| `ads-creative` | Creative | UGC scripts, AI video briefs, image ad generation |
| `ads-copy` | Copywriting | RSA optimization, headline banks, ad copy testing |
| `geo-technical` | SEO | Technical audit: crawlability, Core Web Vitals, schema |
| `geo-citability` | AEO/GEO | AI search visibility — ChatGPT, Perplexity, Gemini citations |
| `market-launch` | Marketing | Full GTM strategy — ICP, messaging, channels, launch calendar |
| `market-emails` | Email | Cold, nurture, re-engagement, transactional sequences |
| `apify-ultimate-scraper` | Data | Universal scraper — 130+ Actors for any platform |
| `lead-gen-ai` | Lead Gen | Vibe Prospecting + Apollo → Excel export with 11 fields |
| `llm-burst` | Optimization | 15-model parallel burst — Groq, Gemini, DeepSeek, GPT4All |
| `website-builder` | Web | $10K website from one prompt — Next.js + Vercel |
| `ugc-agency` | Creative | 20 UGC ads from one prompt via Arcads API |

---

## Use Cases

| Goal | Skill | Prompt |
|---|---|---|
| **Google Ads audit** | `ads-strategy` | "Audit my campaign structure — quality scores, wasted spend, impression share" |
| **Meta competitor spy** | `ads-creative` | "Pull last 90 days ads for [brand] from Meta Ad Library → Airtable swipe file" |
| **Technical SEO** | `geo-technical` | "Full technical audit of [domain] — Core Web Vitals, crawl, schema" |
| **AI search optimization** | `geo-citability` | "Why does [competitor] get cited in ChatGPT? What content fixes it?" |
| **Lead extraction** | `lead-gen-ai` | "50 dentists in NYC — phone, email, Instagram, Google rating. Excel." |
| **Cold outreach** | `market-emails` | "7-email B2B sequence targeting e-com brands doing $1M+ revenue" |
| **Web scraping** | `apify-ultimate-scraper` | "Scrape all reviews for [product] on Amazon + Trustpilot" |
| **UGC video batch** | `ugc-agency` | "20 UGC ads for skincare — 4 hook types, Arcads actors" |

---

## Installation

### Claude Code

```bash
# Full collection
git clone https://github.com/hmzainjamil/hmz-openclaw-skills-official.git
cp -r hmz-openclaw-skills-official/skills/* ~/.claude/skills/

# Individual skill
/plugin install ads-strategy@hmz-openclaw-skills-official
```

### Cursor / Windsurf

```bash
# Add to your workspace rules
# Reference: hmz-openclaw-skills-official/skills/<skill-name>/SKILL.md
```

### Codex CLI / Gemini CLI

```bash
git clone https://github.com/hmzainjamil/hmz-openclaw-skills-official.git
# Skills auto-discovered from AGENTS.md index
```

---

## Resources

- **[hmz-openclaw](https://github.com/hmzainjamil/hmz-openclaw)** — OpenClaw gateway configuration
- **[claude-ai-skills](https://github.com/hmzainjamil/claude-ai-skills)** — Full HMZ skills library
- **[hmz-antigravity-awesome-skills](https://github.com/hmzainjamil/hmz-antigravity-awesome-skills)** — Antigravity skill collection (55K chars)
- **[claude-ai-system](https://github.com/hmzainjamil/claude-ai-system)** — Full HMZ system

## License

MIT

---

<p align="center">Built by <a href="https://github.com/hmzainjamil">Hafiz Muhammad Zulqarnain</a> &mdash; HMZ AI Agency</p>