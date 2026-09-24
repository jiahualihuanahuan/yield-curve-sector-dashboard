# Master Prompt for the Builder

Copy everything below the line into Grok Build (or any AI app builder).

---

Build a single-page web dashboard called **Yield Curve Sector Dashboard**.

## What it does
It tracks the shape of the US and Canadian yield curves and maps the current regime to which equity sectors historically outperform. The user opens it and immediately sees: the curve, the regime in plain English, which sectors are favored, and the supporting indicators that confirm or contradict the signal.

## Read these specs first (they are in this repo)
- `REQUIREMENTS.md` — features, UX, acceptance criteria
- `THEORY.md` — the macro framework and sector sensitivity map
- `BACKEND_DATA.md` — data sources, schemas, API contract, caching

## Implementation guidance
1. **Frontend**: React + TypeScript, responsive, dark mode. One main page with four panels: Yield Curve, Sector Sensitivity, Supporting Indicators, Regime History.
2. **Backend**: a small API (Node/Python) that fetches from FRED + Stooq (free, no key where possible), caches daily, and exposes `GET /api/dashboard` per `BACKEND_DATA.md`.
3. **Regime classifier**: implement the logic in `THEORY.md` — steepening/flattening/inverted/bull/bear steepener, with a driver (short vs long end).
4. **Charts**: lightweight-charts or recharts. Show curves, spread sparklines, and sector performance.
5. **Data honesty**: every number shows its as-of timestamp and source. Surface the caveats from `THEORY.md` §6.
6. **No keys in client code.** All external calls go through the backend.
7. **MVP scope**: features in `REQUIREMENTS.md` §3. Stretch (watchlist/alerts) can be stubbed.

## Deliverable
A runnable app (local dev + one-command deploy) with sample/fallback data so it renders even before live feeds are wired. Include a short README on how to run it.

## Tone
Educational, not financial advice. Plain language, tooltips on jargon.