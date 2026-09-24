# Backend Data Specification

Data is the heart of this app. The frontend should never hit external APIs directly in production — a thin backend caches and normalizes everything.

## 1. Data sources (free / low-cost first)

| Series | Source | Notes |
|---|---|---|
| US Treasury yields (2Y,5Y,10Y,30Y) | FRED (`DGS2`,`DGS5`,`DGS10`,`DGS30`) or Treasury.gov | Daily, free |
| US 10Y-2Y spread | FRED `T10Y2Y` | Pre-computed, convenient |
| Canada bond yields | BoC Valet API or FRED Canada series | Daily |
| Inflation breakeven (5Y, 10Y) | FRED `T5YIE`, `T10YIE` | For real yield |
| High-yield OAS | FRED `BAMLH0A0HYM2` | Credit spread |
| USD index | FRED `DTWEXBGS` or Stooq | |
| WTI crude | FRED `DCOILWTICO` or EIA | |
| Sector ETFs (for performance) | Yahoo Finance / Stooq | XLF, XLRE, XLU, XLI, XLY, XLE, XLV, XLP, XLB, IWM |

Prefer FRED + Stooq for zero-cost, no-key access where possible. Cache aggressively.

## 2. Refresh cadence

- Yields, spreads, breakevens, OAS: **daily** (markets closed weekends/holidays).
- Oil, USD: **daily**.
- Sector ETF prices: **daily** close.
- Regime classification: recomputed on each data refresh.

Store a `last_updated` timestamp per series and show it in the UI.

## 3. Normalized schema

### `yield_observation`
```
{
  "date": "YYYY-MM-DD",
  "market": "US" | "CA",
  "maturity": "2Y" | "5Y" | "10Y" | "30Y",
  "yield_pct": 4.12,
  "source": "FRED"
}
```

### `spread_observation`
```
{
  "date": "YYYY-MM-DD",
  "market": "US" | "CA",
  "spread_name": "10Y-2Y" | "10Y-5Y" | "30Y-2Y",
  "spread_bps": 38,
  "source": "FRED"
}
```

### `indicator_observation`
```
{
  "date": "YYYY-MM-DD",
  "name": "real_yield_10y" | "hy_oas" | "breakeven_5y" | "usd_index" | "wti_oil",
  "value": 1.85,
  "unit": "pct" | "bps" | "index" | "usd_per_bbl",
  "source": "FRED"
}
```

### `sector_performance`
```
{
  "date": "YYYY-MM-DD",
  "ticker": "XLF",
  "name": "Financials",
  "price": 42.1,
  "daily_return_pct": 0.4,
  "ytd_return_pct": 12.3
}
```

### `regime` (derived, not stored raw)
```
{
  "as_of": "YYYY-MM-DD",
  "market": "US",
  "shape": "steepening" | "flattening" | "inverted" | "bull_steepener" | "bear_steepener",
  "driver": "short_end" | "long_end" | null,
  "spread_10y2y_bps": 38,
  "confidence": "high" | "medium" | "low"
}
```

## 4. API contract (backend → frontend)

`GET /api/dashboard` returns:
```
{
  "as_of": "...",
  "curves": { "US": [...], "CA": [...] },
  "spreads": { "US": {...}, "CA": {...} },
  "regime": { "US": {...}, "CA": {...} },
  "indicators": [...],
  "sectors": [...],
  "regime_history": [...]
}
```

`GET /api/series?name=10Y-2Y&market=US&range=5Y` for chart drill-downs.

## 5. Caching & rate limits

- Cache FRED/Stooq responses server-side for 6–24h.
- Never expose API keys to the client.
- Graceful fallback: if a source is down, serve last-known values with a stale flag.

## 6. Storage

- SQLite or Postgres for time series. Keep it simple for MVP.
- A single `observations` table with (series_id, date, value) works; normalize later if needed.

## 7. Testing the data layer

- Unit test the regime classifier against known historical dates (e.g. 2019 inversion, 2020 bull steepener, 2022 bear steepener).
- Snapshot test the `/api/dashboard` payload shape.