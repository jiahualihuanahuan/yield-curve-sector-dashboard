# Product Requirements

## 1. Goal

Build a single-page web dashboard that answers: **"Given the current yield curve, which sectors should I be watching, and why?"**

The app should be useful for a retail investor or analyst who wants a fast, visual read on rate-driven sector rotation without digging through bond screens.

## 2. Target users

- Retail investors tracking macro rotation
- Analysts who want a quick regime check before digging deeper
- Anyone following Canadian or US rate markets

## 3. Core features (MVP)

### 3.1 Yield curve panel
- Display the current yield curve for US Treasuries (2Y, 5Y, 10Y, 30Y) and Canadian government bonds (2Y, 5Y, 10Y, 30Y).
- Show the key spreads: 10Y−2Y, 10Y−5Y, 30Y−2Y, 2Y10Y (Canada).
- Classify the regime in plain language: **steepening / flattening / inverted / bull steepener / bear steepener**.
- Mini sparkline of each spread over the last 1Y and 5Y.

### 3.2 Sector sensitivity panel
- A table or card grid of sectors with their historical sensitivity to curve shape.
- Each sector card shows: direction of sensitivity (benefits / hurt), confidence, and a one-line rationale.
- Sectors to include: Financials (banks), REITs (equity + mortgage), Utilities, Industrials, Consumer Discretionary, Energy, Healthcare, Consumer Staples, Materials, Small/Mid Caps.
- Color coding: green = favored in current regime, red = hurt, gray = neutral.

### 3.3 Supporting indicators panel
- Real yield (nominal 10Y minus inflation breakeven).
- Credit spread (high-yield minus Treasury, or IG OAS).
- Inflation expectation (5Y breakeven / TIPS).
- USD index and oil price (WTI).
- Each with a small trend arrow and a one-line interpretation.

### 3.4 Regime history
- A timeline of past curve regimes with the sectors that led during each.
- Lets the user sanity-check the framework against history.

### 3.5 Watchlist / alerts (stretch)
- User can save a sector or indicator.
- Optional email/push when a regime flips.

## 4. Non-goals (MVP)

- No trade execution or brokerage integration.
- No portfolio construction or optimization.
- No ML forecasting of the curve — regime classification only.

## 5. UX requirements

- Single page, loads in under 2 seconds on desktop.
- Mobile-responsive.
- Dark mode toggle.
- All numbers show as-of timestamp and data source.
- Plain-language tooltips on every technical term.

## 6. Acceptance criteria

- [ ] Curve regime auto-classifies correctly on load.
- [ ] Sector cards update color when the regime changes.
- [ ] All four supporting indicators render with trend.
- [ ] Data refreshes at least daily without manual action.
- [ ] Works in Chrome, Firefox, Safari; responsive down to 375px width.

## 7. Tech suggestions (non-binding)

- Frontend: React + TypeScript, or a simple static site.
- Backend: a small API that caches market data (to respect rate limits).
- Charts: lightweight library (e.g. lightweight-charts or recharts).
- Hosting: any static host + serverless function is fine.