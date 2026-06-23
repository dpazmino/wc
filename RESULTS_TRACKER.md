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
| France vs Senegal | 58/20/22 | France | 3-1 (France) | ✅ | 0.27 |
| Iraq vs Norway | 20/20/60 | Norway | 1-4 (Norway) | ✅ | 0.25 |
| Argentina vs Algeria | 56/22/23 | Argentina | 3-0 (Argentina) | ✅ | 0.29 |
| Austria vs Jordan | 58/21/21 | Austria | 3-1 (Austria) | ✅ | 0.26 |
| Portugal vs DR Congo | 61/20/19 | Portugal | 1-1 (Draw) | ❌ | 1.04 |
| England vs Croatia | 53/22/25 | England | 4-2 (England) | ✅ | 0.34 |
| Ghana vs Panama | 59/20/21 | Ghana | 1-0 (Ghana) | ✅ | 0.25 |
| Uzbekistan vs Colombia | 26/23/51 | Colombia | 1-3 (Colombia) | ✅ | 0.36 |
| Czechia vs South Africa | 46/25/29 | Czechia | 1-1 (Draw) | ❌ | 0.86 |
| Switzerland vs Bosnia & Herz. | 48/24/27 | Switzerland | 4-1 (Switzerland) | ✅ | 0.40 |
| Canada vs Qatar (H) | 50/24/26 | Canada | 6-0 (Canada) | ✅ | 0.38 |
| Mexico vs South Korea (H) | 47/26/28 | Mexico | 1-0 (Mexico) | ✅ | 0.43 |
| USA vs Australia (H) | 58/21/21 | USA | 2-0 (USA) | ✅ | 0.26 |
| Scotland vs Morocco | 32/29/39 | Morocco | 0-1 (Morocco) | ✅ | 0.56 |
| Brazil vs Haiti | 65/18/16 | Brazil | 3-0 (Brazil) | ✅ | 0.18 |
| Türkiye vs Paraguay | 46/25/29 | Türkiye | 0-1 (Paraguay) | ❌ | 0.78 |
| Netherlands vs Sweden | 47/25/28 | Netherlands | 5-1 (Netherlands) | ✅ | 0.42 |
| Germany vs Ivory Coast | 54/22/24 | Germany | 2-1 (Germany) | ✅ | 0.32 |
| Ecuador vs Curaçao | 42/27/32 | Ecuador | 0-0 (Draw) | ❌ | 0.81 |
| Tunisia vs Japan | 22/21/57 | Japan | 0-4 (Japan) | ✅ | 0.28 |
| Spain vs Saudi Arabia | 66/18/17 | Spain | 4-0 (Spain) | ✅ | 0.18 |
| Belgium vs Iran | 58/20/22 | Belgium | 0-0 (Draw) | ❌ | 1.02 |
| Uruguay vs Cape Verde | 56/22/22 | Uruguay | 2-2 (Draw) | ❌ | 0.97 |
| New Zealand vs Egypt | 21/21/58 | Egypt | 1-3 (Egypt) | ✅ | 0.26 |
| Argentina vs Austria | 51/23/26 | Argentina | 2-0 (Argentina) | ✅ | 0.36 |
| Norway vs Senegal | 43/26/31 | Norway | 3-2 (Norway) | ✅ | 0.49 |
| France vs Iraq | 70/16/14 | France | 3-0 (France) | ✅ | 0.14 |
| Jordan vs Algeria | 24/22/54 | Algeria | 1-2 (Algeria) | ✅ | 0.32 |

## Scoreboard (43 games)
- **Top-pick accuracy: 27 / 43** (Mexico, USA, Scotland, Germany, Ivory Coast, France, Norway, Argentina, Austria, England, Ghana, Colombia, Switzerland, Canada, Morocco, Brazil, Netherlands, Japan, Spain, Egypt, Algeria)
- **Avg Brier (model): 0.540**  vs  **naive 1/3 baseline: 0.667**  → model **ahead** of the baseline
- **Draws: 13 / 43** · **Outright upsets against the model: 3 / 43** (South Korea, Australia, Paraguay)

## Honest read
The June 16 slate (France, Norway, Argentina all winning as favourites, slate Brier 0.27)
pulled the average from 0.717 back to **0.644 — below the blind 1/3 guess again**, and the
June 17 split (Austria win, Portugal 1-1 DR Congo) held it there.

- **Draws were the whole story, and the group-opener wave has passed.** 9 of 20 games were
  draws (45%, down from the early 53%), heavily clustered in the tight opening round; once
  second games arrived, the favourites started converting (3-1, 4-1, 3-0, 3-1). The model
  assigns draws only ~18–25%, so it lost nine coin-flips it was favoured in during the opener
  glut — a conversion-variance miss, not a ranking error — and is now being rewarded as games
  open up.
- **Group-opener effect.** Opening games are historically tight and low-scoring; the model has
  no tournament-phase adjustment, so it over-converts strength into expected wins right now.
- **Germany 7-1 Curaçao** (Brier 0.16), **Norway 4-1 Iraq** (0.25), and the **Ivory Coast–
  Ecuador** market beat remain the best calls.

## Caveats
- 23 games is still a small sample; the real measure is the 278-fixture backtest (CV RPS 0.210 vs 0.231).
- The draw lean (9/23 = 39%, vs ~22% modelled) was concentrated in the group openers and has
  eased as second games arrived — worth a **DRAW_BASE / draw-mass** look once the group stage
  ends, **not** a strength-rating change. The 278-fixture CV is unmoved, so don't retune off this.
- Pending (predicted, not yet reported): **Sweden vs Tunisia** (Group F).
- **Thesis watch:** both elimination-market bets advancing — **Ghana beat Panama 1-0** (3 pts, the
  qualify thesis on track) and **DR Congo's 1-1 with Portugal** banked a point. Both feed the
  "to qualify" tests in [[model-vs-draftkings-tracker]].
- **Fade vindicated:** Colombia 1-3'd Uzbekistan as DK's −250 implied (71%) — the model's
  diffuse 51% was the worse number, exactly why I flagged Uzbekistan-to-advance as a fade, not edge.

*Updated through the June 22 Group I/J slate (Norway–Senegal … Jordan–Algeria).*
