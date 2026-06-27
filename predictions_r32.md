# Round of 32 — Match Predictions

*Strength model (shrink 0.25) **anchored 50/50 to the de-vigged DraftKings closing moneyline** where odds are available (rows marked *model-only* have none yet). Knockout metric is **P(advance) = P(win) + ½·P(draw)** — a level game is treated as a coin-flip shootout. Host nations (USA, Mexico, Canada) get Elo home-field advantage when they play; all other ties are neutral. W/D/L = first team's Win / Draw / Loss % over 90 minutes (post-anchor).*

## Summary

| Match | Date (ET) | W/D/L | xG | To advance | Verdict |
|---|---|---|---|---|---|
| South Africa vs Canada *(host Canada at home)* | Sat Jun 28, 3:00 PM | 22 / 25 / 53 | 1.1–1.5 | **Canada 66%** | Canada favoured |
| Brazil vs Japan | Mon Jun 29, 1:00 PM | 53 / 24 / 23 | 1.6–1.0 | **Brazil 65%** | Brazil favoured |
| Germany vs Paraguay | Mon Jun 29, 4:30 PM | 67 / 19 / 14 | 1.8–0.8 | **Germany 76%** | Germany strong |
| Netherlands vs Morocco | Mon Jun 29, 9:00 PM | 47 / 27 / 26 | 1.5–1.1 | **Netherlands 60%** | Slight edge Netherlands |
| Ivory Coast vs Norway | Tue Jun 30, 1:00 PM | 30 / 28 / 42 | 1.3–1.3 | **Norway 56%** | Slight edge Norway |
| France vs Sweden | Tue Jun 30, 5:00 PM | 64 / 19 / 17 | 1.7–0.9 | **France 74%** | France favoured |
| USA vs Bosnia and Herzegovina *(host USA at home)* | Wed Jul 1, 8:00 PM | 60 / 22 / 18 | 1.5–1.1 | **USA 71%** | USA favoured |
| Australia vs Egypt | Fri Jul 3, 2:00 PM | 28 / 29 / 43 | 1.1–1.5 | **Egypt 57%** | Slight edge Egypt |
| Argentina vs Cape Verde | Fri Jul 3, 6:00 PM | 74 / 15 / 11 | 1.9–0.7 | **Argentina 82%** | Argentina strong |

## Detail

### South Africa vs Canada — Sat Jun 28, 3:00 PM  *(host Canada at home)*
- Model+market **21.8 / 25.3 / 52.9** (W/D/L) · xG 1.10–1.50.
- **To advance:** South Africa 34% · Canada 66% → **Canada**.  *(model-only had South Africa 37%; market trimmed it.)*

### Brazil vs Japan — Mon Jun 29, 1:00 PM
- Model+market **52.9 / 24.3 / 22.7** (W/D/L) · xG 1.55–1.05.
- **To advance:** Brazil 65% · Japan 35% → **Brazil**.  *(model-only had Brazil 62%; market lifted it.)*

### Germany vs Paraguay — Mon Jun 29, 4:30 PM
- Model+market **66.6 / 18.9 / 14.5** (W/D/L) · xG 1.77–0.83.
- **To advance:** Germany 76% · Paraguay 24% → **Germany**.  *(model-only had Germany 73%; market lifted it.)*

### Netherlands vs Morocco — Mon Jun 29, 9:00 PM
- Model+market **46.5 / 27.2 / 26.3** (W/D/L) · xG 1.51–1.09.
- **To advance:** Netherlands 60% · Morocco 40% → **Netherlands**.  *(model-only had Netherlands 60%; market lifted it.)*

### Ivory Coast vs Norway — Tue Jun 30, 1:00 PM
- Model+market **29.7 / 28.0 / 42.4** (W/D/L) · xG 1.27–1.33.
- **To advance:** Ivory Coast 44% · Norway 56% → **Norway**.  *(model-only had Ivory Coast 48%; market trimmed it.)*

### France vs Sweden — Tue Jun 30, 5:00 PM
- Model+market **63.9 / 19.4 / 16.7** (W/D/L) · xG 1.73–0.87.
- **To advance:** France 74% · Sweden 26% → **France**.  *(model-only had France 65%; market lifted it.)*

### USA vs Bosnia and Herzegovina — Wed Jul 1, 8:00 PM  *(host USA at home)*
- Model+market **59.9 / 21.7 / 18.5** (W/D/L) · xG 1.47–1.13.
- **To advance:** USA 71% · Bosnia and Herzegovina 29% → **USA**.  *(model-only had USA 62%; market lifted it.)*

### Australia vs Egypt — Fri Jul 3, 2:00 PM
- Model+market **28.4 / 28.7 / 42.9** (W/D/L) · xG 1.12–1.48.
- **To advance:** Australia 43% · Egypt 57% → **Egypt**.  *(model-only had Australia 40%; market lifted it.)*

### Argentina vs Cape Verde — Fri Jul 3, 6:00 PM
- Model+market **74.1 / 15.0 / 10.9** (W/D/L) · xG 1.86–0.74.
- **To advance:** Argentina 82% · Cape Verde 18% → **Argentina**.  *(model-only had Argentina 74%; market lifted it.)*

*Anchored 50/50 to DraftKings where odds exist (`apply_odds.HIST`). Regenerate: `python gen_ko_preds.py r32`. Log results to `data/results.csv` after kickoff (knockout: log the score for Elo, track the advancer separately).*
