# Model vs DraftKings — Disagreement Tracker

**Purpose.** DraftKings is a sharp book; on most games the strength model and DK agree on
the favourite, so there is no edge to be had. Edge can only exist where they **disagree on
the favourite**. This file isolates exactly those games and scores the model *only* on them —
the honest test of whether the model has a real, exploitable edge over DK.

**The thesis being tested.** DraftKings is a US book, so its prices absorb US public money,
which over-weights *familiar* sides (CONMEBOL names, hyped squads, historical powers) and
under-covers strong-but-unglamorous African/Asian squads with European-league talent. The
model sees only squad strength, so it should be "right" when it is **more bullish on an
under-covered side** that DK has shaded down on reputation. (Origin: Côte d'Ivoire–Ecuador.)

**What counts as a clean disagreement** (a real edge candidate):
- Model and DK pick **different favourites** (by the moneyline side, ignoring the draw).
- The gap is **strength-driven**, not because DK knows something the model doesn't (injuries,
  rotation, dead-rubber motivation).
- It is a **single-match moneyline**, not an outright/futures (DK is sharpest there) and not a
  minnow longshot or deep-run tail (those are the *model* being wrong, not DK).

A push (the match ends in a draw) scores as **neither** — a side bet on the favourite loses,
but it is not evidence either model belongs.

---

## 🎯 Disagreement scorecard (the headline)

*Only games where model and DK picked different favourites. This is the edge measure.*

| Date | Match | Model fav | DK fav | Result | Winner of the call |
|---|---|---|---|---|:--:|
| 06-13 | Côte d'Ivoire vs Ecuador | Ivory Coast (47%) | Ecuador (37%) | 1–0 Ivory Coast | **model ✅** |

**Record: model 1–0 DK** (n = 1). *Far too small to claim an edge — one clean call that fit
the thesis. Needs a sample.*

---

## Full comparison log

*Every game for which we have both a model pick and a DK line. "Agree" games can't generate
edge — they're here only to show how often the two diverge (rarely).*

| Date | Match | Model fav | DK fav | Agree? | Result | Note |
|---|---|---|---|:--:|---|---|
| 06-13 | Germany vs Curaçao | Germany | Germany | ✅ | 7–1 GER | both right |
| 06-13 | Netherlands vs Japan | Netherlands | Netherlands | ✅ | 2–2 | push (draw) |
| 06-13 | **Côte d'Ivoire vs Ecuador** | **Ivory Coast** | **Ecuador** | ❌ | **1–0 CIV** | **model ✅ / DK ✗** |
| 06-15 | Spain vs Cape Verde | Spain | Spain | ✅ | 0–0 | push (draw) |
| 06-15 | Saudi Arabia vs Uruguay | Uruguay | Uruguay | ✅ | 1–1 | push (draw) |
| 06-15 | Belgium vs Egypt | Belgium | Belgium | ✅ | 1–1 | push (draw) |
| 06-15 | Iran vs New Zealand | Iran | Iran | ✅ | 2–2 | push (draw) |

**Agreement rate: 6 / 7 games** — the model is not a contrarian engine; it mostly mirrors the
sharp line. That is the central caveat to any "model beats DK" story.

### Pending (model + DK pick logged, not yet played)
| Date | Match | Model fav | DK fav | Agree? |
|---|---|---|---|:--:|
| 06-13 | Sweden vs Tunisia | Sweden | Sweden | ✅ |
| 06-16 | France vs Senegal | France | France | ✅ |
| 06-16 | Iraq vs Norway | Norway | Norway | ✅ |
| 06-16 | Argentina vs Algeria | Argentina | Argentina | ✅ |

### DK line not captured (model pick known, market unknown — backfill if available)
These early results predate the logged slates, so we can't tell whether they were
agreements or disagreements. **Two are model misses on upsets — if DK favoured the winner,
they were disagreements where *DK* beat the model**, which the scorecard must count.

| Date | Match | Model fav | Result | If DK line found… |
|---|---|---|---|---|
| 06-11 | Mexico vs South Africa | Mexico | 2–0 MEX | |
| 06-11 | South Korea vs Czechia | Czechia | 2–1 KOR (upset) | did DK favour South Korea? |
| 06-12 | Canada vs Bosnia | Canada | 1–1 | |
| 06-12 | USA vs Paraguay | USA | 4–1 USA | |
| 06-13 | Qatar vs Switzerland | Switzerland | 1–1 | |
| 06-13 | Brazil vs Morocco | Brazil | 1–1 | |
| 06-13 | Haiti vs Scotland | Scotland | 0–1 SCO | |
| 06-14 | Australia vs Turkey | Türkiye | 2–0 AUS (upset) | did DK favour Australia? |

---

## Elimination-market edge tests (stage-of-elimination props)

*A second market, scored separately from the moneyline scorecard. DraftKings 7-way
"stage of elimination" props (`downloads/elim.txt`), de-vigged and compared to the model's
live elimination distribution — see `MODEL_VS_DK_ELIMINATION.md` for the full screen. The
**headline finding is that the model is more diffuse than DK** (fat tails → nominal +EV
everywhere), so most of the screen is miscalibration, not edge. Only spots that also fit the
under-covered-but-strong (Ivory Coast) profile count as genuine tests.*

| Logged | Bet | Model | DK (de-vig) | Result | Verdict |
|---|---|---|---|---|:--:|
| 06-16 | **Ghana to qualify** (reach Last 32+) | 69% | ~54% | TBD — won 1-0 vs Panama (3 pts, 2 to play) | on track |
| 06-16 | **DR Congo to qualify** (reach Last 32+) | 59% | ~46% | TBD — drew Portugal 1-1 (1 pt, 2 to play) | on track |

Both are the CIV thesis restated for the qualify market: an under-covered African side the
model rates a stronger advancer than a US book does. **Thesis-tests, not locks** — the market
may simply know the squad is weaker than its rating. **Both opened well on 06-17** — Ghana beat
Panama, DR Congo took a point off Portugal — but neither has clinched; mark the final result
once their group completes (Ghana plays England/Croatia, DR Congo plays Colombia/Uzbekistan).

**Fades logged for honesty** (model miscalibration, *not* edge, so not bets): Tunisia/Uzbekistan
to advance (over-rating minnows); Argentina/France/Portugal to exit early (under-confidence in
favourites).

## How this gets maintained
1. When new DK moneylines arrive, run `python predict.py A B --odds-american <h> <d> <a>`
   (or compare the de-vigged market to the model) and record both favourites.
2. If the favourites **differ**, it's a disagreement → add it to the scorecard; otherwise it
   goes in the full log only.
3. After the match, mark who was right. A draw is a push (neither).
4. Watchlist for likely disagreements (Ivory Coast profile — under-covered, model-bullish):
   **Ivory Coast, Ghana, Senegal, Egypt, Algeria, Iran.** Their single matches are where to
   look first.

*Seeded 2026-06-15. The edge is unproven (n = 1); this file exists to find out if it's real.*
