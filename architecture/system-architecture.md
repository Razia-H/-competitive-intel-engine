╔══════════════════════════════════════════════════════════════════════════╗
║              AI COMPETITIVE INTELLIGENCE BRIEFING ENGINE                ║
║                     End-to-End System Architecture                      ║
╚══════════════════════════════════════════════════════════════════════════╝

  ┌──────────────────────────────────────┐
  │           INGESTION LAYER            │
  │  ──────────────────────────────────  │
  │  Input: Competitor names list        │
  │  e.g. ["Salesforce","HubSpot","SAP"] │
  │  Trigger: Scheduled daily 6am OR     │
  │  Manual run via browser UI           │
  └──────────────────┬───────────────────┘
                     │
                     ▼
  ┌──────────────────────────────────────┐
  │         DATA COLLECTION LAYER        │
  │  ──────────────────────────────────  │
  │  NewsAPI.org (free tier)             │
  │  · Everything endpoint               │
  │  · Last 24 hours filter              │
  │  · Per competitor query              │
  │  Returns: headlines + snippets       │
  └──────────────────┬───────────────────┘
                     │ RAW NEWS DATA per competitor
                     ▼
╔════════════════════╧═════════════════════════════════════════════════╗
║                    PARALLEL AGENT ROUTER                             ║
║              One agent per competitor (up to 5)                      ║
╠══════════════╦══════════════╦══════════════╦══════════════╗
║ COMPETITOR 1 ║ COMPETITOR 2 ║ COMPETITOR 3 ║ COMPETITOR 4 ║
║              ║              ║              ║              ║
║ News Analyst ║ News Analyst ║ News Analyst ║ News Analyst ║
║ Agent        ║ Agent        ║ Agent        ║ Agent        ║
║              ║              ║              ║              ║
║ OUTPUT:      ║ OUTPUT:      ║ OUTPUT:      ║ OUTPUT:      ║
║ JSON brief   ║ JSON brief   ║ JSON brief   ║ JSON brief   ║
╚══════════════╩══════════════╩══════════════╩══════════════╝
                     │
                     ▼
         ┌───────────────────────────┐
         │  AGENT: EXECUTIVE         │
         │  BRIEFING WRITER          │
         │  ─────────────────────    │
         │  · Synthesises all        │
         │    competitor briefs      │
         │  · Identifies cross-      │
         │    competitor themes      │
         │  · Ranks strategic threats│
         │  · Writes exec briefing   │
         │  · Recommends actions     │
         └─────────────┬─────────────┘
                       │
                       ▼
         ┌───────────────────────────┐
         │  DELIVERY LAYER           │
         │  ─────────────────────    │
         │  · Google Sheets log      │
         │  · Slack message (prod)   │
         │  · Email (prod)           │
         │  · Browser display (demo) │
         └───────────────────────────┘
