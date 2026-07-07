# Quarter-finals — Match Predictions

*Strength model (shrink 0.25) **anchored 50/50 to the de-vigged DraftKings closing moneyline** where odds are available (rows marked *model-only* have none yet). Knockout metric is **P(advance) = P(win) + ½·P(draw)** — a level game is treated as a coin-flip shootout. Host nations (USA, Mexico, Canada) get Elo home-field advantage when they play; all other ties are neutral. W/D/L = first team's Win / Draw / Loss % over 90 minutes (post-anchor).*

## Summary

| Match | Date (ET) | W/D/L | xG | To advance | Verdict | Result |
|---|---|---|---|---|---|---|
| France vs Morocco | Thu Jul 10, 4:00 PM | 54 / 22 / 24 | 1.6–1.0 | **France 65%** | Slight edge France · *model-only* | — |
| Spain vs Belgium | Fri Jul 11, 12:00 PM | 40 / 29 / 30 | 1.4–1.2 | **Spain 55%** | Slight edge Spain · *model-only* | — |
| Norway vs England | Fri Jul 11, 5:00 PM | 25 / 23 / 52 | 1.1–1.5 | **England 64%** | Slight edge England · *model-only* | — |

## Detail

### France vs Morocco — Thu Jul 10, 4:00 PM
- Model **54.2 / 21.5 / 24.2** (W/D/L) · xG 1.63–0.97.
- **To advance:** France 65% · Morocco 35% → **France**.

### Spain vs Belgium — Fri Jul 11, 12:00 PM
- Model **40.4 / 29.4 / 30.2** (W/D/L) · xG 1.45–1.15.
- **To advance:** Spain 55% · Belgium 45% → **Spain**.

### Norway vs England — Fri Jul 11, 5:00 PM
- Model **24.7 / 23.0 / 52.3** (W/D/L) · xG 1.07–1.53.
- **To advance:** Norway 36% · England 64% → **England**.

*Anchored 50/50 to DraftKings where odds exist (`apply_odds.HIST`). Regenerate: `python gen_ko_preds.py qf`. Log results to `data/results.csv` after kickoff (knockout: log the score for Elo, track the advancer separately).*
