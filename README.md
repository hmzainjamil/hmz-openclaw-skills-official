# hmz-openclaw-skills-official — Official Skill Routing Layer for OpenClaw

> **Every skill has routing metadata, fallback chains, cost guards, and quality thresholds. Zero-configuration intelligent routing.**

---

## Overview

`hmz-openclaw-skills-official` defines the official skill set for the OpenClaw AI gateway. Each skill is a routing unit — a named capability with metadata that tells OpenClaw exactly which model to use, what to fall back to, how much it can cost, and what quality threshold to accept.

Skills are the bridge between "I want to write ad copy" and "use GPT-4o-mini with DeepSeek-V3 fallback, max $0.002 per call, reject responses under 200 tokens."

---

## Skill Architecture

### Skill Definition Format

Every skill is defined as a JSON file with routing metadata:

```json
{
  "skill_id": "code-gen-router",
  "version": "1.2.0",
  "description": "Route code generation tasks to optimal models",
  "trigger_keywords": ["code", "function", "script", "debug", "python", "javascript"],
  
  "routing": {
    "primary": "deepseek/deepseek-chat",
    "fallback_chain": [
      "openrouter/codellama-34b",
      "groq/llama3-70b-8192",
      "gpt4all/deepseek-coder",
      "ollama/codellama:13b"
    ],
    "never_use": ["anthropic/claude-sonnet", "anthropic/claude-opus"]
  },
  
  "quality": {
    "min_tokens": 100,
    "max_tokens": 4096,
    "reject_if": ["I cannot", "I'm sorry", "As an AI"],
    "retry_on_rejection": true,
    "max_retries": 3
  },
  
  "cost": {
    "max_per_call_usd": 0.005,
    "max_per_day_usd": 0.50,
    "alert_above_usd": 0.002
  },
  
  "performance": {
    "timeout_seconds": 30,
    "preferred_latency_ms": 2000,
    "parallel_candidates": 3
  }
}
```

---

## Official Skill Catalog

### Core Routing Skills

#### 1. code-gen-router

Routes all code generation, debugging, and scripting tasks.

```
Primary:  DeepSeek-V3
Fallback: CodeLlama-34B > Groq Llama 70B > GPT4All DeepSeek-Coder > Ollama CodeLlama
Cost cap: $0.005/call
Quality:  Min 100 tokens, reject apologies and refusals
Speed:    30s timeout
```

**Best for:**
- Python, JavaScript, TypeScript, bash scripts
- Debugging and error fixing
- Code review and refactoring
- API integration code

#### 2. research-router

Routes research, analysis, and information gathering tasks.

```
Primary:  Groq Llama 3 70B
Fallback: Gemini 2.0 Flash > DeepSeek-V3 > GPT-4o-mini > Ollama Llama3
Cost cap: $0.002/call
Quality:  Min 200 tokens, structured output preferred
Speed:    15s timeout
```

**Best for:**
- Market research
- Competitor analysis
- Topic summarization
- Fact-finding and citations

#### 3. content-router

Routes content creation, copywriting, and drafting tasks.

```
Primary:  GPT-4o-mini
Fallback: Gemini 2.0 Flash > Groq Mixtral > Groq Llama 70B > GPT-3.5-turbo
Cost cap: $0.003/call
Quality:  Min 150 tokens, reject generic outputs
Speed:    20s timeout
```

**Best for:**
- Email copy
- Ad headlines and descriptions
- Blog drafts
- Social media posts
- Proposal sections

#### 4. reasoning-router

Routes complex reasoning, logic, and analytical tasks.

```
Primary:  DeepSeek-V3 (strong reasoner)
Fallback: Kimi-K2.5 > Gemini 1.5 Pro > OpenRouter Nemotron > Groq Llama 70B
Cost cap: $0.008/call
Quality:  Min 300 tokens, chain-of-thought required
Speed:    45s timeout
```

**Best for:**
- Strategic analysis
- Problem decomposition
- Decision frameworks
- Mathematical reasoning
- Complex planning

#### 5. local-first-router

Routes to local models only. Never touches external APIs.

```
Primary:  Ollama Llama3 70B
Fallback: GPT4All Llama3 > Ollama Mistral > GPT4All Phi-3 > Ollama CodeLlama
Cost cap: $0.00 (local only, enforced)
Quality:  Best-effort local quality
Speed:    120s timeout (local can be slow)
```

**Best for:**
- Sensitive/private data processing
- Offline operation
- Cost-zero requirement
- High-volume batch processing

#### 6. free-only-router

Routes to free-tier cloud models only. Never uses paid providers.

```
Primary:  Groq Llama 3 70B
Fallback: Gemini 2.0 Flash > Groq Mixtral > Gemini 1.5 Flash > GPT4All > Ollama
Cost cap: $0.00 (enforced — rejects if any cost)
Quality:  Standard free-tier quality
Speed:    10s timeout
```

**Best for:**
- High-volume tasks
- Non-critical drafts
- Testing and iteration
- Budget-zero workflows

#### 7. fast-router

Routes to fastest models only. Prioritizes latency over quality.

```
Primary:  Groq Llama 3 70B (<500ms)
Fallback: Groq Mixtral > Gemini 2.0 Flash > GPT-4o-mini
Cost cap: $0.001/call
Quality:  Accepts shorter responses
Speed:    2s hard timeout (no stragglers)
```

**Best for:**
- Real-time chat responses
- Quick lookups
- Intermediate pipeline steps
- Time-sensitive automation

#### 8. long-context-router

Routes tasks requiring large context windows.

```
Primary:  Gemini 1.5 Pro (1M token context)
Fallback: Kimi moonshot-v1-128k > Kimi-K2.5 (262K) > Claude Haiku (200K)
Cost cap: $0.02/call (long context is always more expensive)
Quality:  Full document comprehension required
Speed:    120s timeout
```

**Best for:**
- Entire codebase analysis
- Long document summarization
- Multi-file audit reviews
- Book/report processing

---

### Quality Control Skills

These are meta-skills that wrap other skills with additional validation.

#### 9. output-validator

Validates any model output before returning it.

```
Checks:
- Minimum token count met
- No refusal phrases detected
- Requested format (JSON/markdown/code) is valid
- Factual consistency (if reference provided)

Action on failure: retry with next model in fallback chain
```

#### 10. cost-guard

Enforces cost limits on any skill.

```
Guards:
- Per-call limit (configurable)
- Per-hour limit (configurable)
- Per-day limit (configurable)
- Provider-level limits

Action on exceed: block call, alert via Slack/Telegram, log to Airtable
```

#### 11. fallback-handler

Manages graceful degradation when primary models fail.

```
Strategies:
- Try each model in chain sequentially
- Skip models that errored in last 5 minutes
- Track which models are "warm" (recently successful)
- Return best partial response if all fail
```

#### 12. token-counter

Tracks token usage across all providers.

```
Tracks:
- Input tokens per call
- Output tokens per call
- Total tokens per session
- Total tokens per day/week/month
- Cost estimation per provider
```

#### 13. parallel-batcher

Batches multiple small requests into parallel calls for efficiency.

```
When:
- Queue depth > 3 requests
- Requests are independent (no dependencies)
- Provider supports parallel calls

Effect:
- 3x faster throughput
- Same cost (parallel, not sequential)
```

#### 14. cache-hit-checker

Checks semantic cache before any model call.

```
Cache types:
- Exact match: identical prompt -> instant return
- Semantic match: similar prompt (>95% similarity) -> return cached
- Template match: same structure, different variables -> adapt cached

TTL: 1 hour for fast-changing topics, 24 hours for stable topics
```

---

## Skill Routing Matrix

| Task | Primary | Fallback 1 | Fallback 2 | Free? |
|------|---------|-----------|-----------|-------|
| Code gen | DeepSeek-V3 | CodeLlama | Groq Llama | Near-free |
| Research | Groq Llama 70B | Gemini Flash | DeepSeek | Free |
| Content | GPT-4o-mini | Gemini Flash | Groq Mixtral | Near-free |
| Reasoning | DeepSeek-V3 | Kimi-K2.5 | Gemini Pro | Near-free |
| Local only | Ollama Llama3 | GPT4All | — | Free |
| Free only | Groq Llama 70B | Gemini Flash | GPT4All | Free |
| Fast (<2s) | Groq Llama 70B | Groq Mixtral | Gemini Flash | Free |
| Long ctx | Gemini 1.5 Pro | Kimi-128k | Kimi-K2.5 | Near-free |

---

## Adding Custom Skills

Create a new JSON file in `~/.openclaw/skills/custom/`:

```json
{
  "skill_id": "my-custom-skill",
  "version": "1.0.0",
  "description": "My custom routing skill",
  "trigger_keywords": ["my-trigger"],
  
  "routing": {
    "primary": "groq/llama3-70b-8192",
    "fallback_chain": ["gemini/gemini-2.0-flash-exp", "gpt4all"]
  },
  
  "quality": {
    "min_tokens": 50,
    "max_tokens": 2048
  },
  
  "cost": {
    "max_per_call_usd": 0.001
  }
}
```

Load the new skill:

```bash
openclaw skills --reload
openclaw skills --list  # verify it appears
```

---

## Skill CLI Commands

```bash
# List all skills
openclaw skills --list

# Show skill details
openclaw skills --show code-gen-router

# Test a skill
openclaw skills --test research-router "What is ROAS?"

# Enable/disable skill
openclaw skills --enable long-context-router
openclaw skills --disable local-first-router

# Reload skills from disk
openclaw skills --reload

# Show skill performance stats
openclaw skills --stats

# Export skills config
openclaw skills --export > my_skills_backup.json
```

---

## Performance Monitoring

```bash
# Skill hit rate (how often each skill is triggered)
openclaw skills --stats --metric hit_rate

# Output:
# code-gen-router:    34% of calls
# content-router:     28% of calls
# research-router:    22% of calls
# fast-router:        10% of calls
# long-context-router: 4% of calls
# other:               2% of calls

# Average cost by skill
openclaw skills --stats --metric avg_cost

# Output:
# code-gen-router:     $0.0018/call
# content-router:      $0.0004/call
# research-router:     $0.0000/call (Groq free)
# fast-router:         $0.0000/call (Groq free)
# long-context-router: $0.0089/call
```

---

## Related Repos

| Repo | Purpose |
|------|---------|
| hmz-openclaw | The gateway these skills plug into |
| hmz-ai | Core routing hierarchy |
| hmz-skills-archive | 1,000+ Claude Code skills |

---

## License

MIT

---

*Intelligent routing is not optional. It's the difference between a $500/mo AI bill and a $20/mo AI bill.*
