# Theory Framework

This is the analytical backbone the app surfaces. Keep the language plain; the math stays in the data layer.

## 1. Yield curve basics

The yield curve plots interest rates across maturities. Its **shape** — not just the level — carries information about growth and inflation expectations.

- **Steepening**: the gap between long and short yields widens. Often signals stronger growth, more inflation risk, or heavier government borrowing.
- **Flattening**: the gap narrows. Can signal slowing growth; a deep inversion has preceded most US recessions since the 1960s.
- **Bull steepener**: driven by falling short-term (policy) rates — usually Fed/BoC easing.
- **Bear steepener**: driven by rising long-term yields — growth or inflation optimism.

## 2. Why the shape matters for sectors

Banks borrow short and lend long, so a wider spread expands **net interest margins**. Rate-sensitive, long-duration assets (utilities, equity REITs) get discounted harder when long yields rise. Cyclicals (industrials, discretionary) benefit when credit conditions ease.

## 3. Sector sensitivity map

| Sector | Favored when curve... | Hurt when curve... | Why |
|---|---|---|---|
| Financials / Banks | Steepens | Flattens / inverts | NIM expands with wider spread |
| Mortgage REITs | Steepens (bull) | Bear steepener | Borrow short, invest long; spread drives margin |
| Equity REITs | Bull steepener | Bear steepener | Lower short rates help; rising long yields hurt valuations |
| Utilities | Flattens / long yields fall | Bear steepens | Capital-intensive, long duration, sensitive to discount rate |
| Industrials | Steepens | Flattens | Credit availability and capex improve |
| Consumer Discretionary | Steepens | Flattens | Cyclical demand and credit |
| Energy | Steepens | Flattens | Pricing power, hard assets, inflation hedge |
| Healthcare | Mildly favored in steepening | — | Defensive with upside; catch-up flows |
| Consumer Staples | Mildly favored in steepening | — | Pricing power, durable cash flows |
| Materials | Steepens | Flattens | Commodity/credit cycle |
| Small / Mid Caps | Steepens | Flattens | Higher beta to credit and growth |

Notes:
- Equity REITs and mortgage REITs behave differently; show both.
- Defensive sectors (healthcare, staples) are not pure plays — treat as hedges, not leaders.
- Canadian banks are especially sensitive to the 2Y10Y spread (research shows post-2009 sensitivity increased).

## 4. Supporting indicators to watch

The curve alone is ambiguous. These disambiguate:

1. **Real yield** = nominal 10Y − inflation breakeven. Drives the discount rate on long-duration assets more directly than the nominal curve.
2. **Credit spread** (HY OAS or IG OAS). Widening = banks less willing to lend, economy cooling. Narrowing = risk-on.
3. **Inflation expectation** (5Y breakeven). Tells you whether a bear steepener is growth-driven or inflation-driven — opposite implications for gold, TIPS, and real assets.
4. **USD index**. Strong dollar pressures commodities and EM; weak dollar supports them.
5. **Oil (WTI)**. Direct input to the energy sector and a real-time inflation signal.

## 5. How the app should interpret combinations

- Steepening + rising real yields + widening credit spread → cautious: favor quality financials, watch defensives.
- Steepening + falling real yields + narrowing credit spread → risk-on: cyclicals, small caps, discretionary.
- Flattening + rising inflation expectation → stagflation risk: energy, materials, gold; avoid long-duration defensives.
- Inversion → historically recessionary: defensives (utilities, staples, healthcare), shorten duration.

## 6. Honest caveats (surface these in the UI)

- The curve is a lagging-to-coincident indicator, not a crystal ball. Inversions have false-alarmed.
- Sector sensitivities are historical averages; regimes differ.
- This is educational, not investment advice.
- Canadian data is thinner than US data — flag lower confidence where relevant.