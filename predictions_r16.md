# Round of 16 — Match Predictions

*Strength model (shrink 0.25) **anchored 50/50 to the de-vigged DraftKings closing moneyline** where odds are available (rows marked *model-only* have none yet). Knockout metric is **P(advance) = P(win) + ½·P(draw)** — a level game is treated as a coin-flip shootout. Host nations (USA, Mexico, Canada) get Elo home-field advantage when they play; all other ties are neutral. W/D/L = first team's Win / Draw / Loss % over 90 minutes (post-anchor).*

## Summary

| Match | Date (ET) | W/D/L | xG | To advance | Verdict | Result |
|---|---|---|---|---|---|---|
| Canada vs Morocco *(host Canada at home)* | Sat Jul 4, 1:00 PM | 33 / 30 / 37 | 1.2–1.4 | **Morocco 52%** | Toss-up · *model-only* | — |
| Paraguay vs France | Sat Jul 4, 5:00 PM | 17 / 18 / 65 | 0.7–1.9 | **France 74%** | France favoured · *model-only* | — |
| Brazil vs Norway | Sun Jul 5, 4:00 PM | 48 / 25 / 27 | 1.5–1.1 | **Brazil 60%** | Slight edge Brazil · *model-only* | — |
| Mexico vs England *(host Mexico at home)* | Sun Jul 5, 8:00 PM | 26 / 23 / 51 | 1.0–1.6 | **England 62%** | Slight edge England · *model-only* | — |
| Portugal vs Spain | Mon Jul 6, 3:00 PM | 32 / 34 / 34 | 1.2–1.4 | **Spain 51%** | Toss-up · *model-only* | — |
| USA vs Belgium *(host USA at home)* | Mon Jul 6, 8:00 PM | 32 / 30 / 39 | 1.2–1.4 | **Belgium 53%** | Toss-up · *model-only* | — |

## Detail

### Canada vs Morocco — Sat Jul 4, 1:00 PM  *(host Canada at home)*
- Model **33.3 / 29.9 / 36.8** (W/D/L) · xG 1.21–1.39.
- **To advance:** Canada 48% · Morocco 52% → **Morocco**.

### Paraguay vs France — Sat Jul 4, 5:00 PM
- Model **17.2 / 18.1 / 64.7** (W/D/L) · xG 0.70–1.90.
- **To advance:** Paraguay 26% · France 74% → **France**.

### Brazil vs Norway — Sun Jul 5, 4:00 PM
- Model **48.0 / 24.6 / 27.4** (W/D/L) · xG 1.49–1.11.
- **To advance:** Brazil 60% · Norway 40% → **Brazil**.

### Mexico vs England — Sun Jul 5, 8:00 PM  *(host Mexico at home)*
- Model **25.9 / 23.4 / 50.7** (W/D/L) · xG 1.04–1.56.
- **To advance:** Mexico 38% · England 62% → **England**.

### Portugal vs Spain — Mon Jul 6, 3:00 PM
- Model **31.5 / 34.4 / 34.1** (W/D/L) · xG 1.24–1.36.
- **To advance:** Portugal 49% · Spain 51% → **Spain**.

### USA vs Belgium — Mon Jul 6, 8:00 PM  *(host USA at home)*
- Model **31.6 / 29.8 / 38.5** (W/D/L) · xG 1.21–1.39.
- **To advance:** USA 47% · Belgium 53% → **Belgium**.

*Anchored 50/50 to DraftKings where odds exist (`apply_odds.HIST`). Regenerate: `python gen_ko_preds.py r16`. Log results to `data/results.csv` after kickoff (knockout: log the score for Elo, track the advancer separately).*
