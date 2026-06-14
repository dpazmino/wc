# Predictions vs Actual — Tracker

*Model predictions (current model: shrink 0.25, DRAW_BASE 0.45) vs actual results for
games played so far. W/D/L = first team's Win / Draw / Loss %. "Brier" = squared error
for that game (lower is better; a blind 1/3-1/3-1/3 guess scores 0.667).*

| Match | Predicted W/D/L | Pick | Actual | Hit | Brier |
|---|---|---|---|:--:|--:|
| Mexico vs South Africa | 53/23/25 | Mexico | 2-0 (Mexico) | ✅ | 0.34 |
| South Korea vs Czechia | 31/27/42 | Czechia | 2-1 (South Korea) | ❌ | 0.72 |
| Canada vs Bosnia | 43/26/31 | Canada | 1-1 (Draw) | ❌ | 0.82 |
| USA vs Paraguay | 54/22/24 | USA | 4-1 (USA) | ✅ | 0.32 |
| Qatar vs Switzerland | 23/22/55 | Switzerland | 1-1 (Draw) | ❌ | 0.97 |
| Brazil vs Morocco | 49/24/26 | Brazil | 1-1 (Draw) | ❌ | 0.89 |

## Scoreboard
- **Top-pick accuracy: 2 / 6** (Mexico, USA)
- **Avg Brier (model): 0.676**  vs  **naive 1/3 baseline: 0.667**
- **Draws: 3 / 6** (50%, vs an expected ~27%)

## Honest read
On these six games the model is **marginally worse than a blind guess** (Brier 0.676 vs 0.667) — no spin. But the cause is specific and instructive:

- **The draw cluster did the damage.** 3 of 6 were draws (50% vs ~27% expected). The model never rates a draw as the single most likely outcome, so a draw-heavy run tanks the hit rate, and confident favourites that drew (Qatar–Switzerland, Brier 0.97) score terribly.
- **The directional reads were mostly sound.** The favoured team only *outright lost* once — the South Korea upset (a near-even game the market also misread). The other three "misses" were draws where the favourite didn't lose.
- **Six games is far too small to judge a model.** The honest measure is the 269-fixture backtest, where the production model scores **RPS 0.207 vs the 0.231 base rate** — a real, cross-validated edge. A six-game cold streak (driven by variance-heavy draws) can't overturn that, just as a six-game hot streak wouldn't prove it.

## Caveat already being acted on
The draw issue is the same one surfaced earlier: the model under-predicted draws, which we partially corrected (`DRAW_BASE` 0.28 → 0.45). These six results pre-date or coincide with that fix; the recalibrated model should fare better as more games are logged. We keep tracking.

*Updated through Brazil–Morocco (June 13). New rows added as results come in.*
