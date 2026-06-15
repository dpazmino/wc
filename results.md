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
| Côte d'Ivoire vs Ecuador | 48/25/28 | Ivory Coast | 1-0 (Ivory Coast) | NP | 0.41 |

## Scoreboard (11 games)
- **Top-pick accuracy: 5 / 11** (Mexico, USA, Scotland, Germany, Ivory Coast)
- **Avg Brier (model): 0.616**  vs  **naive 1/3 baseline: 0.667**  → model **ahead** of the baseline
- **Draws: 4 / 11** · **Outright upsets against the model: 2 / 11** (South Korea, Australia)

## Honest read
The model has steadily climbed from a poor start (Brier 0.71 after 7) to **clearly ahead of a blind guess** (0.616 after 11), and top-pick accuracy is up to 5/11.

- **Model beat the market on Côte d'Ivoire–Ecuador.** DraftKings made Ecuador the favourite (37% vs Ivory Coast 29%) and the anchored call was a coin-flip leaning Ecuador — I'd flagged "fade the model here." Instead the model's lean to **Ivory Coast (48%) was right** (1-0). A clean reminder that the market isn't always sharper than the strength model.
- **Germany 7-1 Curaçao** (Brier 0.16) remains the model's best call; **Haiti–Scotland** and **Ivory Coast–Ecuador** were the kind of tight games it's now getting right.
- **Misses are still mostly draws + the two upsets** (South Korea, Australia) where the favoured side controlled play but didn't win.

## Caveats
- 11 games is still a small sample; the real measure is the 269-fixture backtest (RPS 0.207 vs 0.231).
- Pending (predicted, not yet reported): **Sweden vs Tunisia** (Group F).

*Updated through Côte d'Ivoire–Ecuador (June 14).*
