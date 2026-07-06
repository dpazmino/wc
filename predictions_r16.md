# Round of 16 — Match Predictions

*Strength model (shrink 0.25) **anchored 50/50 to the de-vigged DraftKings closing moneyline** where odds are available (rows marked *model-only* have none yet). Knockout metric is **P(advance) = P(win) + ½·P(draw)** — a level game is treated as a coin-flip shootout. Host nations (USA, Mexico, Canada) get Elo home-field advantage when they play; all other ties are neutral. W/D/L = first team's Win / Draw / Loss % over 90 minutes (post-anchor).*

## Summary

| Match | Date (ET) | W/D/L | xG | To advance | Verdict | Result |
|---|---|---|---|---|---|---|
| Canada vs Morocco *(host Canada at home)* | Sat Jul 4, 1:00 PM | 26 / 29 / 45 | 1.2–1.4 | **Morocco 59%** | Slight edge Morocco | — |
| Paraguay vs France | Sat Jul 4, 5:00 PM | 11 / 16 / 72 | 0.7–1.9 | **France 81%** | France strong | — |
| Brazil vs Norway | Sun Jul 5, 4:00 PM | 50 / 25 / 25 | 1.5–1.1 | **Brazil 62%** | Slight edge Brazil | — |
| Mexico vs England *(host Mexico at home)* | Sun Jul 5, 8:00 PM | 28 / 27 / 45 | 1.0–1.6 | **England 59%** | Slight edge England | — |
| Portugal vs Spain | Mon Jul 6, 3:00 PM | 28 / 30 / 42 | 1.2–1.4 | **Spain 57%** | Slight edge Spain | — |
| USA vs Belgium *(host USA at home)* | Mon Jul 6, 8:00 PM | 34 / 29 / 37 | 1.2–1.4 | **Belgium 51%** | Toss-up | — |
| Argentina vs Egypt | Tue Jul 7, 12:00 PM | 59 / 19 / 21 | 1.8–0.8 | **Argentina 69%** | Argentina favoured · *model-only* | — |
| Switzerland vs Colombia | Tue Jul 7, 4:00 PM | 37 / 32 / 31 | 1.4–1.2 | **Switzerland 53%** | Toss-up · *model-only* | — |

## Detail

### Canada vs Morocco — Sat Jul 4, 1:00 PM  *(host Canada at home)*
- Model+market **26.3 / 28.6 / 45.1** (W/D/L) · xG 1.21–1.39.
- **To advance:** Canada 41% · Morocco 59% → **Morocco**.  *(model-only had Canada 48%; market trimmed it.)*

### Paraguay vs France — Sat Jul 4, 5:00 PM
- Model+market **11.2 / 16.3 / 72.4** (W/D/L) · xG 0.70–1.90.
- **To advance:** Paraguay 19% · France 81% → **France**.  *(model-only had Paraguay 26%; market trimmed it.)*

### Brazil vs Norway — Sun Jul 5, 4:00 PM
- Model+market **49.8 / 24.9 / 25.2** (W/D/L) · xG 1.49–1.11.
- **To advance:** Brazil 62% · Norway 38% → **Brazil**.  *(model-only had Brazil 60%; market lifted it.)*

### Mexico vs England — Sun Jul 5, 8:00 PM  *(host Mexico at home)*
- Model+market **28.1 / 26.6 / 45.3** (W/D/L) · xG 1.04–1.56.
- **To advance:** Mexico 41% · England 59% → **England**.  *(model-only had Mexico 38%; market lifted it.)*

### Portugal vs Spain — Mon Jul 6, 3:00 PM
- Model+market **27.7 / 30.5 / 41.8** (W/D/L) · xG 1.24–1.36.
- **To advance:** Portugal 43% · Spain 57% → **Spain**.  *(model-only had Portugal 49%; market trimmed it.)*

### USA vs Belgium — Mon Jul 6, 8:00 PM  *(host USA at home)*
- Model+market **34.1 / 28.9 / 36.9** (W/D/L) · xG 1.21–1.39.
- **To advance:** USA 49% · Belgium 51% → **Belgium**.  *(model-only had USA 47%; market lifted it.)*

### Argentina vs Egypt — Tue Jul 7, 12:00 PM
- Model **59.2 / 19.3 / 21.4** (W/D/L) · xG 1.76–0.84.
- **To advance:** Argentina 69% · Egypt 31% → **Argentina**.

### Switzerland vs Colombia — Tue Jul 7, 4:00 PM
- Model **37.0 / 31.9 / 31.0** (W/D/L) · xG 1.37–1.23.
- **To advance:** Switzerland 53% · Colombia 47% → **Switzerland**.

*Anchored 50/50 to DraftKings where odds exist (`apply_odds.HIST`). Regenerate: `python gen_ko_preds.py r16`. Log results to `data/results.csv` after kickoff (knockout: log the score for Elo, track the advancer separately).*
