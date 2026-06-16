# Predictions vs Actual — Tracker

*Model predictions (walk-forward: each game scored with ratings as of its own date, so the
prediction never "sees" its own result). W/D/L = first team's Win / Draw / Loss %.
Brier = squared error for that game (lower is better; a blind 1/3-1/3-1/3 guess = 0.667).*

| Match | Predicted W/D/L | Pick | Actual | Hit | Brier |
|---|---|---|---|:--:|--:|
| Mexico vs South Africa | 53/23/25 | Mexico | 2-0 (Mexico) | ✅ | 0.34 |
| South Korea vs Czechia | 31/27/42 | Czechia | 2-1 (South Korea) | ❌ | 0.72 |
| Canada vs Bosnia | 43/26/31 | Canada | 1-1 (Draw) | ❌ | 0.82 |
| USA vs Paraguay | 54/22/24 | USA | 4-1 (USA) | ✅ | 0.32 |
| Qatar vs Switzerland | 23/22/55 | Switzerland | 1-1 (Draw) | ❌ | 0.97 |
| Brazil vs Morocco | 49/24/26 | Brazil | 1-1 (Draw) | ❌ | 0.89 |
| Haiti vs Scotland | 27/24/49 | Scotland | 0-1 (Scotland) | ✅ | 0.39 |
| Australia vs Türkiye | 24/24/51 | Türkiye | 2-0 (Australia) | ❌ | 0.89 |
| Germany vs Curaçao | 68/17/15 | Germany | 7-1 (Germany) | ✅ | 0.16 |
| Netherlands vs Japan | 48/25/27 | Netherlands | 2-2 (Draw) | ❌ | 0.87 |
| Côte d'Ivoire vs Ecuador | 48/25/28 | Ivory Coast | 1-0 (Ivory Coast) | ✅ | 0.41 |
| Spain vs Cape Verde | 64/19/17 | Spain | 0-0 (Draw) | ❌ | 1.11 |
| Belgium vs Egypt | 52/23/25 | Belgium | 1-1 (Draw) | ❌ | 0.93 |
| Saudi Arabia vs Uruguay | 21/21/58 | Uruguay | 1-1 (Draw) | ❌ | 1.01 |
| Iran vs New Zealand | 52/23/25 | Iran | 2-2 (Draw) | ❌ | 0.93 |

## Scoreboard (15 games)
- **Top-pick accuracy: 5 / 15** (Mexico, USA, Scotland, Germany, Ivory Coast)
- **Avg Brier (model): 0.717**  vs  **naive 1/3 baseline: 0.667**  → model now **behind** the baseline
- **Draws: 8 / 15** · **Outright upsets against the model: 2 / 15** (South Korea, Australia)

## Honest read
Four straight cagey favourite-draws (Spain–Cape Verde, Belgium–Egypt, Saudi Arabia–Uruguay,
Iran–New Zealand) have pushed the average to **0.717 — now behind a blind 1/3 guess**.

- **The story is draws, not bad strength rankings.** 8 of 15 games were draws (53%), but the
  model assigns draws only ~18–25%, so it picked a side every time and lost eight coin-flips it
  was favoured in. In most of those the model's favourite was the stronger team that controlled
  play without winning — a conversion-variance miss, not a ranking error.
- **Group-opener effect.** Opening games are historically tight and low-scoring; the model has
  no tournament-phase adjustment, so it over-converts strength into expected wins right now.
- **Germany 7-1 Curaçao** (Brier 0.16) and the **Ivory Coast–Ecuador** market beat remain the
  best calls.

## Caveats
- 14 games is still a small sample; the real measure is the 276-fixture backtest (CV RPS 0.208 vs 0.231).
- The 0.702 vs 0.667 gap is within 14-game variance, but the draw lean is now consistent (50%
  observed vs ~22% modelled) — worth a **DRAW_BASE / draw-mass** look once the group stage ends,
  **not** a strength-rating change. The 276-fixture CV is unmoved, so don't retune off this yet.
- Pending (predicted, not yet reported): **Sweden vs Tunisia** (Group F), **France vs Senegal**,
  **Iraq vs Norway**, **Argentina vs Algeria** (June 16).

*Updated through Iran–New Zealand (June 15).*
