# The Unlaunched List

[![token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/c/token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/bapenven-ctrl/token-radar-01/rank.svg)](https://make.fun/c/token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/bapenven-ctrl/token-radar-01/reward.svg)](https://make.fun/c/token-radar-01)

An entry for the [token-radar-01](https://make.fun/c/token-radar-01) bounty on
[make.fun](https://make.fun): 191 pre-token protocols ranked by comps-calibrated
value, held-out tested, with a farm verdict each.

## What it does

`main.ts` reads the sealed snapshot of DeFi protocols and writes a ranked board
(`board.json`) plus a static dashboard (`dashboard/`) and a dossier
(`dossier.json`):

- **191 pre-token protocols** — the full 40-protocol watchlist plus 151 early
  launch candidates beyond the watchlist, every one rankable from the snapshot.
- **Comps-calibrated value model** — implied value = TVL × the median
  market-cap/TVL multiple of the protocol's category (fitted from 128 live-token
  protocols in the snapshot) × 7-day growth × a maturity factor for time without
  a token. No protocol names are hard-coded in the model.
- **Held-out validation, shown honestly** — two-way held-out tests
  (Spearman ρ ≈ 0.46 / 0.43, within 2× on 18/64 protocols, median error ≈ 90%)
  are displayed in the dashboard's KPI strip and model panel: the model fixes
  scale (TVL alone errs by ~465%), not precise pricing.
- **A farm verdict per row** — Farm first / Farm / Watch / Early watch, plus a
  6-step farm plan with cost and time for every protocol.
- **Live-token tab** — the 24 protocols in the snapshot that already have a token
  are kept separate, with market cap shown as fact.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input <path-to-snapshot.json>
```

Requires Node 22+, standard library only. Two runs write byte-identical output.

## Layout

- `main.ts` — entrypoint: builds the board, dashboard data and dossier.
- `lib/model.ts` — the comps-1 value model and farm-plan generator.
- `vendor/makefun-board.ts` — dossier builder from the kit (unchanged).
- `dashboard/` — static page (no network, no framework): board, per-protocol
  detail with recompute check, filters, and a model sandbox.
- `screenshots/` — board, detail, and filtered views of the dashboard.

## License

MIT — see [LICENSE](LICENSE).
