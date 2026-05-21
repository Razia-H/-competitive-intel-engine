╔══════════════════════════════════════════════════════════════════════════╗
║              DATA MAPPING — Token/JSON Flow Node to Node                ║
╚══════════════════════════════════════════════════════════════════════════╝

NODE 1: User Input / Scheduler
  EMITS → {
    "competitors": ["Salesforce", "HubSpot", "SAP", "Microsoft"],
    "industry": "Enterprise CRM",
    "your_company": "Acme Corp",
    "date": "2025-05-21",
    "run_id": "uuid-xxxx"
  }

NODE 2: NewsAPI — Fetch Per Competitor (loop)
  URL: https://newsapi.org/v2/everything
  PARAMS → {
    "q": "{{competitor_name}}",
    "from": "{{yesterday_date}}",
    "sortBy": "relevancy",
    "pageSize": 5,
    "apiKey": "{{newsapi_key}}"
  }
  RETURNS → {
    "articles": [
      {
        "title": "Salesforce announces new AI feature...",
        "description": "...",
        "url": "https://...",
        "publishedAt": "2025-05-21T08:00:00Z",
        "source": {"name": "TechCrunch"}
      }
    ]
  }

NODE 3: OpenRouter API — News Analyst Agent (per competitor)
  SENDS → {
    "model": "anthropic/claude-haiku-4-5",
    "messages": [
      {"role":"system","content":"<NEWS ANALYST PROMPT>"},
      {"role":"user","content":"COMPETITOR: {{name}}\nARTICLES:\n{{articles}}"}
    ]
  }
  RETURNS → {
    "competitor_name": "Salesforce",
    "date_analysed": "2025-05-21",
    "news_volume": 5,
    "sentiment": "POSITIVE|NEUTRAL|NEGATIVE|MIXED",
    "sentiment_score": 72,
    "key_developments": [
      {
        "headline": "Salesforce launches Einstein AI Suite",
        "significance": "HIGH|MEDIUM|LOW",
        "category": "PRODUCT|PRICING|PARTNERSHIP|LEGAL|PERSONNEL|FINANCIAL",
        "strategic_implication": "Direct competitive threat to our AI roadmap",
        "source": "TechCrunch",
        "url": "https://..."
      }
    ],
    "threat_level": "HIGH|MEDIUM|LOW|MONITOR",
    "competitor_momentum": "ACCELERATING|STABLE|DECLINING",
    "analyst_note": "1-sentence summary"
  }

NODE 4: OpenRouter API — Executive Briefing Writer
  SENDS → {
    "model": "anthropic/claude-haiku-4-5",
    "messages": [
      {"role":"system","content":"<EXECUTIVE BRIEFING PROMPT>"},
      {"role":"user","content":"{{all_competitor_briefs_combined}}"}
    ]
  }
  RETURNS → {
    "briefing_date": "2025-05-21",
    "your_company": "Acme Corp",
    "industry": "Enterprise CRM",
    "executive_summary": "2 sentences",
    "threat_index": 68,
    "market_pulse": "ACTIVE|QUIET|VOLATILE|SHIFTING",
    "top_threat": "Salesforce — Einstein AI Suite launch",
    "competitor_rankings": [
      {"rank":1,"name":"Salesforce","threat_level":"HIGH","momentum":"ACCELERATING"},
      {"rank":2,"name":"Microsoft","threat_level":"MEDIUM","momentum":"STABLE"}
    ],
    "cross_competitor_themes": [
      "All 4 competitors investing heavily in AI features",
      "Pricing pressure emerging from Microsoft and HubSpot"
    ],
    "strategic_recommendations": [
      {
        "priority": "URGENT|HIGH|MEDIUM",
        "action": "Accelerate AI feature roadmap announcement",
        "rationale": "Salesforce Einstein launch shifts customer expectations",
        "owner": "Product + Marketing"
      }
    ],
    "items_to_watch": ["Salesforce Q2 earnings", "HubSpot pricing announcement"],
    "no_news_competitors": ["SAP"]
  }

NODE 5: Google Sheets — Add Row
  MAPS → {
    Column A (Run_ID):              {{run_id}},
    Column B (Date):                {{briefing_date}},
    Column C (Industry):            {{industry}},
    Column D (Threat_Index):        {{threat_index}},
    Column E (Market_Pulse):        {{market_pulse}},
    Column F (Top_Threat):          {{top_threat}},
    Column G (Executive_Summary):   {{executive_summary}},
    Column H (Cross_Themes):        {{cross_competitor_themes}},
    Column I (Recommendations):     {{strategic_recommendations}},
    Column J (Items_To_Watch):      {{items_to_watch}},
    Column K (Competitors_Tracked): {{competitor_count}},
    Column L (Delivered_To):        [HUMAN FILLS IN],
    Column M (Actions_Taken):       [HUMAN FILLS IN]
  }
