# Yield Curve Sector Dashboard

A web app that tracks the shape of the yield curve and maps it to sector performance, so you can see which sectors are favored as the curve steepens or flattens.

This repository contains the full product requirements, theory framework, and backend data specification. It is written to be fed directly into an AI app builder (e.g. Grok Build) to generate a working prototype.

## Repo structure

- `REQUIREMENTS.md` — product scope, features, user flows, and acceptance criteria
- `THEORY.md` — the macro framework: curve shapes, sector sensitivities, and the indicators to watch
- `BACKEND_DATA.md` — data sources, schemas, refresh cadence, and API contracts
- `PROMPT_FOR_BUILDER.md` — a ready-to-paste master prompt for the builder

## One-line summary

Dashboard that ingests Treasury (and Canadian) yield data, classifies the curve regime, and surfaces which sectors historically outperform under that regime — with live charts and a watchlist of supporting indicators.