# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

TTCC (Training Team Command Center) 2026 is a static single-page dashboard application for managing training programs across regional markets. It has no build step — the entire app lives in `public/index.html`.

## Development

No build tools, no package manager. Edit `public/index.html` directly and open it in a browser to test.

**Deployment (Vercel):**
```bash
npm i -g vercel
vercel
```

Or push to GitHub — Vercel auto-deploys on every push via the GitHub integration.

## Architecture

The entire application is a single ~3,150-line `public/index.html` structured in three sections:

1. **CSS** (lines ~1–362): Design tokens and component styles
2. **HTML** (lines ~363–1191): App shell, sidebar, all views/modals, and the separate Coordinator UI
3. **JavaScript** (lines ~1192–end): All logic (~1,950 lines), including constants, role-based rendering, data operations, and API calls

### Role System

Three user roles gate access to views:
- **L1 (Training Architect & Builder):** Full admin — all views including Team Management, Team Execution, and Data Management
- **L2 (Regional Training Specialist):** Mission Control, Roadmap, Strategy, Calendar, My Work
- **L3 (Training Coordinator):** Separate simplified coordinator UI for task tracking and progress logging

### Key Data Entities

- **Initiatives** — Training programs with status, progress %, owner, Mountain Peak (market), strategy tags, and quarter/year
- **Sessions** — Training events with date, trainer, capacity
- **Tasks** — Coordinator work items with priority/status
- **OKRs** — Quarterly objectives and key results
- **Users** — Team members with role and region
- **Progress Logs** — Private per-coordinator progress notes

### Core Constants (defined near line 1192)

- `MP_CODES` — Eight markets: Qatar, UAE, Bahrain, Kuwait, Oman, UK, Riyadh, Jeddah
- `STRATEGY_TAGS` — Nine pillars: AI + Automations, Cost Efficiency, Kitchen Optimization, People/Upskilling, Productivity, Quality, Streamlining, Impact Metrics, Others
- `ROLES` — L1/L2/L3 definitions with view permissions

### Backend

The app calls a **Google Apps Script** API (URL entered by users at login) for data persistence. The backend URL and auth token are entered at the login screen under "Apps Script URL". All data read/write goes through this API; there is no local database.

### Views

| View | Roles | Purpose |
|------|-------|---------|
| Mission Control | L1, L2 | KPIs, roadmap progress, active initiatives |
| 2026 Roadmap | L1, L2 | Gantt-style initiative timeline |
| Strategy Canvas | L1, L2 | 9 pillars with completion tracking |
| Analytics | L1, L2 | Charts: completion rates, performance, learning hours |
| Heatmap | L1 | Competency coverage: Mountain Peak × Strategy |
| Calendar | L1, L2 | 2026 training session planner |
| OKRs | L1, L2 | Objectives & Key Results tracking |
| My Work | L1, L2 | Personalized responsibilities dashboard |
| Data Management | L1 | Full initiative registry with CSV import/export |
| Team Management | L1 | User administration |
| Team Execution | L1 | Coordinator live progress overview |
| Coordinator App | L3 | Simplified task + progress UI |

### CSV Import/Export

Data Management supports Notion-compatible CSV format for bulk initiative import/export. Parse logic is in the JS section.
