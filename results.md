# Predictions vs Actual — Tracker

*Model predictions (walk-forward: each game scored with ratings as of its own date, so the
prediction never "sees" its own result). W/D/L = first team's Win / Draw / Loss %.
Brier = squared error for that game (lower is better; a blind 1/3-1/3-1/3 guess = 0.667).*

| Match | Predicted W/D/L | Pick | Actual | Hit | Brier |
|---|---|---|---|:--:|--:|
| Mexico vs South Africa | 53/23/25 | Mexico | 2-0 (Mexico) | ✅ | 0.34 |
| South Korea vs Czechia | 31/27/42 | Czechia | 2-1 (South Korea) | NP | 0.72 |
| Canada vs Bosnia | 43/26/31 | Canada | 1-1 (Draw) | NP | 0.82 |
| USA vs Paraguay | 54/22/24 | USA | 4-1 (USA) | ✅ | 0.32 |
| Qatar vs Switzerland | 23/22/55 | Switzerland | 1-1 (Draw) | ❌ | 0.97 |
| Brazil vs Morocco | 49/24/26 | Brazil | 1-1 (Draw) | ❌ | 0.89 |
| Haiti vs Scotland | 27/24/49 | Scotland | 0-1 (Scotland) | ✅ | 0.39 |
| Australia vs Türkiye | 24/24/51 | Türkiye | 2-0 (Australia) | ❌ | 0.89 |
| Germany vs Curaçao | 68/17/15 | Germany | 7-1 (Germany) | ✅ | 0.16 |
| Netherlands vs Japan | 48/25/27 | Netherlands | 2-2 (Draw) | ❌ | 0.87 |

## Scoreboard (10 games)
- **Top-pick accuracy: 4 / 10** (Mexico, USA, Scotland, Germany)
- **Avg Brier (model): 0.636**  vs  **naive 1/3 baseline: 0.667**  → model now **beats** the baseline
- **Draws: 4 / 10** · **Outright upsets: 2 / 10** (South Korea, Australia)

## Honest read
After a rough first six, the model has **recovered to ahead of a blind guess** (Brier 0.636 vs 0.667). The turn came from two clean calls:
- **Haiti–Scotland** — leaned Scotland (49%), Scotland won 1-0 (Brier 0.39).
- **Germany–Curaçao** — Germany (68%) won **7-1** (Brier 0.16). This also **vindicated the market over the model**: when we DraftKings-anchored it, DK had Curaçao at ~3% vs the model's 15%, and the blowout proved the model was over-rating a debutant. The anchored 79% was the better number.

Still-true caveats:
- **The draw problem persists** — 4 of 10 are draws (Netherlands–Japan the latest), still above the ~25–27% the model expects. The single biggest source of misses.
- **Top-pick accuracy (4/10) is still modest** — proper scoring (Brier) rewards the model's calibration even when the headline pick misses.
- **Small sample.** The real measure remains the 269-fixture backtest (RPS 0.207 vs 0.231). Ten games is trending the right way but proves little on its own.

*Updated through the June 14 games (Germany–Curaçao, Netherlands–Japan).*
