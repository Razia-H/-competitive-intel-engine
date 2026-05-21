# AI Competitive Intelligence Briefing Engine
### Agentic AI Portfolio Project | Claude (OpenRouter) + NewsAPI + Google Sheets

## What It Does
Monitors up to 4 competitors daily using NewsAPI, analyses each with a
dedicated AI agent, and synthesises findings into an executive briefing
with threat scores, strategic recommendations, and items to watch —
delivered in under 2 minutes.

## Stack
- AI Agents: Claude Haiku via OpenRouter API
- News Data: NewsAPI.org (free tier — 100 requests/day)
- Dashboard: Google Sheets
- Delivery: Browser UI (demo) / Slack + Email (production)

## The 2-Agent Pipeline

| Agent | Role | Runs |
|-------|------|------|
| News Analyst | Analyses articles per competitor, scores threat level | Once per competitor |
| Executive Briefing Writer | Synthesises all analyses into executive briefing | Once at end |

## Threat Index Scoring

| Score | Market Pulse | Meaning |
|-------|-------------|---------|
| 0–24 | QUIET | Routine activity, no urgency |
| 25–49 | ACTIVE | Notable developments, monitor |
| 50–74 | VOLATILE | Significant moves, response needed |
| 75–100 | SHIFTING | Major disruption, act now |

## Why NewsAPI Over Web Scraping
NewsAPI provides structured, reliable data from 80,000+ sources via
a single API call. Web scraping is brittle — sites change structure,
add bot detection, and require JavaScript rendering. For a system
that runs daily without human intervention, NewsAPI is the correct
production choice.

## How to Run the Demo
1. Get free NewsAPI key at newsapi.org/register
2. Get OpenRouter key at openrouter.ai/keys
3. Download app/competitive-intel-engine.html
4. Open in Notepad → replace YOUR_OPENROUTER_KEY_HERE and YOUR_NEWSAPI_KEY_HERE
5. Save → open in Chrome (drag and drop or Ctrl+O)
6. Enter your company, industry, and competitor names
7. Click Generate Intelligence Briefing

## Portfolio Defense Points
1. Per-competitor agents beat multi-competitor prompts — 100% focus per competitor
2. NewsAPI over scraping — production reliability over fragile DIY solutions
3. Threat indexing enables executive action — not just summarisation
