+++
title = "MyFinance: A self-hosted personal finance dashboard"
date = 2025-09-21T11:44:42+02:00
draft = false
tags = ["personal finance", "dashboard", "self-hosted", "fastapi", "react", "sqlite", "machine learning", "data engineering", "financial analytics", "full stack"]
categories = ["Programming", "Data Engineering", "Personal Projects"]
+++

I wanted a personal finance tool that's fast, local, and practical. Something that ingests messy bank CSVs, learns from my corrections, and gives me decision-ready views without a monthly spreadsheet ritual. So I built MyFinance: a Docker-first FastAPI + React app that parses bank data, categorizes transactions, and surfaces useful trends. All privately, on my own machine.

## TL;DR
- **Problem**: Spreadsheets don't scale with inconsistent bank exports and manual cleanup.
- **Solution**: A self-hosted dashboard that ingests CSVs, learns categories, and visualizes trends.
- **Stack**: React + Tailwind, FastAPI + SQLAlchemy, SQLite, Pandas, light ML.
- **AI factor**: Used Windsurf with Claude 3.7/4 to accelerate drafts, and shipped via a lightweight AI workflow designed to avoid regressions.
- **Workflow in short**: One conversation per feature, update the CHANGELOG at stable points, seed new chats with README + CHANGELOG for shared context, and restart with a refined first prompt instead of an endless fix-break loop.
- **Why**: A playground to sharpen full-stack and data-engineering skills with AI as an accelerator.
- **Status**: Core functionality deployed. Next up: budget tracking, goal setting, flexible CSV header recognition, and automatic recurring payment identification.

## Quick Demo
{{< figure src="/images/ideas/myfinance.gif" caption="MyFinance in action - see the code on <a href=\"https://github.com/LeandroOrdonez/myfinance\">GitHub</a>." >}}

## 1. Why I Built It
Spreadsheets are fine until you're juggling:
- Inconsistent headers across banks
- Decimal commas, delimiters, and locale quirks
- Repeating the same categorization work every month
- Charts that require pivot-table gymnastics

I wanted "drop a CSV → get insights" without sacrificing privacy.

### Deliberate practice goals
- **Full-stack habits**: Typed APIs, tests and refactors, Dockerized dev, predictable builds.
- **Data engineering**: Resilient CSV parsing (ING/KBC), locale/decimal handling, idempotent imports, background aggregation.
- **Modeling & analytics**: Outlier-resistant stats (winsorization), Financial Health metrics, projection guardrails that cap expenses relative to income.
- **ML in product**: Retrieval-based category suggestions with a feedback loop rather than heavy retraining.
- **AI as accelerator**: Windsurf + Claude for boilerplate and design spikes; ship only patterns that survive tests and simplicity checks.

## 2. What It Does
MyFinance follows three simple principles:
1. **Data In**: Ingest raw CSVs (ING & KBC supported; add others with a small parser).
2. **Smarts On Top**: Auto-categorization improves with every confirmed correction.
3. **Insights Out**: Dashboards that answer "Where did my money go?" in seconds.

## 3. Architecture, in 10 Seconds

{{< figure src="/images/ideas/my-finance-arch.png" caption="MyFinance architecture" >}}

- **React + Tailwind**: Quick UI building blocks, minimal CSS overhead.
- **FastAPI**: Type hints, async, and automatic docs.
- **SQLite**: Zero-config, durable via Docker volume.
- **Pandas**: For CSV wrangling.
- **Light ML**: Text embeddings + k-NN for category suggestions.

One `docker-compose up -d` brings up frontend (:3000) and API (:8000).

## 4. Feature Highlights
- **Transaction import** with header/locale tolerance
- **Category suggestions** that learn from your corrections
- **Analytics**:
  - Monthly trends, essential vs. discretionary, category breakdowns
  - Financial Health scores (savings rate, emergency fund, investment rate, etc.)
  - Projections with realistic guardrails
- **Projections**:
  - Uses historical patterns with outlier-resistant stats
  - Adds a realism guardrail: caps expenses to a historical expense-to-income ratio (with a hard ceiling) to prevent runaway compounding
- **Anomaly detection**:
  - Flags statistical and behavioral outliers to review unusual transactions

## 5. Category Suggestions (Light ML)
A pragmatic approach: learn from past confirmations and suggest categories for similar new transactions. Each confirmation makes future suggestions a bit smarter, no heavyweight retraining loops.

## 6. Challenges and Fixes
- **Bank CSV variability**: Strict header detection with explicit per-bank parsers (ING, KBC); extend by adding new parsers
- **Decimal commas**: Sanitize only numeric columns before parsing
- **Async uploads**: Stream to a temp file with a 5 MB cap; parsing happens inline in the request handler
- **Cold start**: Newly imported transactions with an assigned category are upserted into the suggestion index
- **Frontend state**: A single `useTransactions()` hook manages fetches and local state (no react-query caching)

## 7. AI Workflow: From Vibe Coding to Reliable Shipping
Early on, "vibe coding" made it fast to add features, but sometimes a new feature quietly broke an older one. To counter that, I adopted a lightweight workflow that kept the speed while reducing regressions:

1. Start a separate conversation per major feature.
2. Keep a CHANGELOG and ask the model to update it when a feature reaches a stable state.
3. Seed every new conversation with the repo's README and the latest CHANGELOG for shared context and constraints.
4. When quality drifts, restart with a refined initial prompt instead of dragging into a fix-break-fix loop.

I still used AI for velocity (drafting CRUD, TS types, UI scaffolding, design alternatives), but shipped only what passed simplicity checks, guardrails, and tests. This combo (clear context, clean restarts, and tiny feedback loops) kept progress steady without sacrificing reliability.

## 8. Want the Internals?
If you enjoy the nuts and bolts (parsers, detection, persistence), the repository's README covers the architecture and guardrails. The CHANGELOG tracks incremental improvements and design decisions.

## 9. Lessons Learned
- **AI velocity needs structure**: Separate chats per feature, seed with `README.md` + `CHANGELOG.md`, and restart with a refined prompt when drift appears.
- **Context beats prompt tricks**: Keeping docs current improved first-response quality more than long prompts.
- **Ship explicitness early**: Strict per-bank CSV parsers avoided silent misparses.
- **Guardrails pay for themselves**: Upload limits, duplicate checks, and projection caps turned edge cases into non-events.
- **Learn incrementally**: Simple embeddings + upserts (including manual edits) improved suggestions faster than heavier ML at this scale.

## 10. Roadmap
- Budgets per category
- Financial goals tracking
- Flexible CSV header recognition
- Recurring charge detection
- Multi-currency support
- Desktop app (?)
- Mobile app (?)

## 11. Wrapping Up
MyFinance turned spreadsheet fatigue into a practical side project, and a place to sharpen software development and data-engineering skills with AI as an accelerator.

Code is here: [github.com/LeandroOrdonez/myfinance](https://github.com/LeandroOrdonez/myfinance). Ideas and PRs welcome. If you're exploring AI in your workflow, I'm happy to compare notes.

— Leandro Ordoñez • September 2025