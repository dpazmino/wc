# Round of 16 — Match Predictions

*Strength model (shrink 0.25) **anchored 50/50 to the de-vigged DraftKings closing moneyline** where odds are available (rows marked *model-only* have none yet). Knockout metric is **P(advance) = P(win) + ½·P(draw)** — a level game is treated as a coin-flip shootout. Host nations (USA, Mexico, Canada) get Elo home-field advantage when they play; all other ties are neutral. W/D/L = first team's Win / Draw / Loss % over 90 minutes (post-anchor).*

## Summary

| Match | Date (ET) | W/D/L | xG | To advance | Verdict | Result |
|---|---|---|---|---|---|---|
| Canada vs Morocco *(host Canada at home)* | Sat Jul 4, 1:00 PM | 26 / 28 / 46 | 1.1–1.5 | **Morocco 60%** | Slight edge Morocco | **Morocco** ✅ hit (0–3) |
| Paraguay vs France | Sat Jul 4, 5:00 PM | 11 / 16 / 73 | 0.7–1.9 | **France 81%** | France strong | **France** ✅ hit (0–1) |
| Brazil vs Norway | Sun Jul 5, 4:00 PM | 49 / 25 / 25 | 1.4–1.2 | **Brazil 62%** | Slight edge Brazil | **Norway** ❌ miss (1–2) |
| Mexico vs England *(host Mexico at home)* | Sun Jul 5, 8:00 PM | 28 / 26 / 46 | 1.0–1.6 | **England 59%** | Slight edge England | **England** ✅ hit (2–3) |
| Portugal vs Spain | Mon Jul 6, 3:00 PM | 27 / 29 / 44 | 1.2–1.4 | **Spain 58%** | Slight edge Spain | **Spain** ✅ hit (0–1) |
| USA vs Belgium *(host USA at home)* | Mon Jul 6, 8:00 PM | 34 / 27 / 39 | 1.1–1.5 | **Belgium 53%** | Toss-up | **Belgium** ✅ hit (1–4) |
| Argentina vs Egypt | Tue Jul 7, 12:00 PM | 59 / 19 / 21 | 1.8–0.8 | **Argentina 69%** | Argentina favoured · *model-only* | — |
| Switzerland vs Colombia | Tue Jul 7, 4:00 PM | 37 / 32 / 31 | 1.4–1.2 | **Switzerland 53%** | Toss-up · *model-only* | — |

**Model on advancement so far: 5/6 correct (83%)** across the 6 decided tie(s) of 8. ✅ = the model's P(advance) favourite went through; ❌ = it was knocked out (a shootout loss by the favourite counts as a miss). Grade is on **advancement**, not the 90' score.

## Detail

### Canada vs Morocco — Sat Jul 4, 1:00 PM  *(host Canada at home)*
- Model+market **26.0 / 27.8 / 46.2** (W/D/L) · xG 1.11–1.49.
- **To advance:** Canada 40% · Morocco 60% → **Morocco**.  *(model-only had Canada 47%; market trimmed it.)*
- **Result:** **Morocco** advanced (0–3) — model ✅ correct.

### Paraguay vs France — Sat Jul 4, 5:00 PM
- Model+market **11.2 / 16.2 / 72.6** (W/D/L) · xG 0.67–1.93.
- **To advance:** Paraguay 19% · France 81% → **France**.  *(model-only had Paraguay 26%; market trimmed it.)*
- **Result:** **France** advanced (0–1) — model ✅ correct.

### Brazil vs Norway — Sun Jul 5, 4:00 PM
- Model+market **49.2 / 25.5 / 25.4** (W/D/L) · xG 1.39–1.21.
- **To advance:** Brazil 62% · Norway 38% → **Brazil**.  *(model-only had Brazil 60%; market lifted it.)*
- **Result:** **Norway** advanced (1–2) — model ❌ wrong (favourite eliminated).

### Mexico vs England — Sun Jul 5, 8:00 PM  *(host Mexico at home)*
- Model+market **27.8 / 25.9 / 46.3** (W/D/L) · xG 0.99–1.61.
- **To advance:** Mexico 41% · England 59% → **England**.  *(model-only had Mexico 36%; market lifted it.)*
- **Result:** **England** advanced (2–3) — model ✅ correct.

### Portugal vs Spain — Mon Jul 6, 3:00 PM
- Model+market **27.4 / 28.5 / 44.1** (W/D/L) · xG 1.17–1.43.
- **To advance:** Portugal 42% · Spain 58% → **Spain**.  *(model-only had Portugal 46%; market trimmed it.)*
- **Result:** **Spain** advanced (0–1) — model ✅ correct.

### USA vs Belgium — Mon Jul 6, 8:00 PM  *(host USA at home)*
- Model+market **33.7 / 27.4 / 38.9** (W/D/L) · xG 1.09–1.51.
- **To advance:** USA 47% · Belgium 53% → **Belgium**.  *(model-only had USA 44%; market lifted it.)*
- **Result:** **Belgium** advanced (1–4) — model ✅ correct.

### Argentina vs Egypt — Tue Jul 7, 12:00 PM
- Model **59.2 / 19.3 / 21.4** (W/D/L) · xG 1.76–0.84.
- **To advance:** Argentina 69% · Egypt 31% → **Argentina**.

### Switzerland vs Colombia — Tue Jul 7, 4:00 PM
- Model **37.0 / 31.9 / 31.0** (W/D/L) · xG 1.37–1.23.
- **To advance:** Switzerland 53% · Colombia 47% → **Switzerland**.

*Anchored 50/50 to DraftKings where odds exist (`apply_odds.HIST`). Regenerate: `python gen_ko_preds.py r16`. Log results to `data/results.csv` after kickoff (knockout: log the score for Elo, track the advancer separately).*
