# Google Sheets — Competitive Intelligence Dashboard Schema

## Tab Name: COMPETITIVE_INTELLIGENCE_LOG

| Col | Header | Type | Filled By |
|-----|--------|------|-----------|
| A | Run_ID | Text | System |
| B | Date | Date | System |
| C | Industry | Text | System |
| D | Threat_Index | Number 0-100 | System |
| E | Market_Pulse | Dropdown | System |
| F | Top_Threat | Text | System |
| G | Executive_Summary | Long Text | System |
| H | Cross_Themes | Text | System |
| I | Recommendations | Text | System |
| J | Items_To_Watch | Text | System |
| K | Competitors_Tracked | Number | System |
| L | Delivered_To | Text | Human |
| M | Actions_Taken | Text | Human |

## Dropdown Options

**Column E — Market_Pulse:**
QUIET, ACTIVE, VOLATILE, SHIFTING

## Conditional Formatting — Column D (Threat Index)
- 0–24: Background #C8E6C9 (Green)
- 25–49: Background #FFF9C4 (Yellow)
- 50–74: Background #FFE0B2 (Orange)
- 75–100: Background #FFCDD2 (Red)

## Human-in-the-Loop Rules
- Threat Index 0–24: No action needed, file for reference
- Threat Index 25–49: Share with relevant team leads
- Threat Index 50–74: Schedule response meeting within 48 hours
- Threat Index 75–100: Escalate to CEO immediately, convene war room
