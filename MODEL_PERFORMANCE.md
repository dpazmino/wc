# Predicting the 2026 World Cup — Model Performance Report

*A running, honest scorecard of a transparent strength model's predictions across the 2026
World Cup. Updated through 2026-06-26 (65 group-stage games). This is the evidence base — wins
**and** misses — behind the write-up. Every number here is reproducible from the scripts and
`data/results.csv` in this repo.*

---

## 1. What the model is (and isn't)

It is a **pure team-strength predictor** — no match simulation, no LLM, no hand-tuning per game:

- **Dynamic Elo** (`match_engine/elo.py`) that *learns from results* — ~250 historical
  internationals seeded the ratings, and every 2026 result updates them (goal-difference
  weighted, home-field advantage, recency decay).
- **Squad-strength prior** from best-XI FIFA-scale player ratings (`player_stats.csv`) that
  seeds and anchors each team's Elo, so thin-data sides lean on squad quality until results
  accumulate ("regularised Elo").
- **Calibration**: probabilities are shrunk toward the base rate (`shrink=0.25`, tuned by
  walk-forward cross-validation), then expected goals/scorelines come from an independent
  Poisson on the rating gap.

**The most important design decision: we removed simulation from the prediction path.**
Walk-forward cross-validation showed a full 22-agent match simulation added *zero* predictive
value over raw team strength. So predictions are **instant and analytic** — no Monte Carlo for
a single game. (Monte Carlo is used only to roll the *tournament* forward into title/qualify
odds — 100,000 iterations.)

**Honest framing:** this is not a crystal ball. It's a well-calibrated-ish strength model that
beats a naive baseline, finds a specific market edge, and has clearly-identified blind spots.
The story is the *rigor and the edge*, not omniscience.

---

## 2. Out-of-sample validation (before the tournament)

On 328 fixtures, walk-forward (each game scored with ratings known only *before*
it), via `backtest.py --cv`:

| Model | RPS ↓ | Brier ↓ | beats base rate? |
|---|--:|--:|:--:|
| Base-rate prior | 0.232 | 0.661 | — |
| **Production (`pred`)** | **0.201** | **0.598** | ✅ |

**Cross-validated optimism: 0.000** — the edge is real, not overfit. This is the credibility
floor: the model beat the baseline out-of-sample *before* the tournament, and still does as
2026 results accumulate.

---

## 3. In-tournament accuracy (65 games)

From `RESULTS_TRACKER.md` (walk-forward — the prediction never saw its own result):

- **Top-pick accuracy: 41 / 65 = 63%**
- **Brier (3-way): 0.539** vs **0.667** naive baseline
- **Log-loss: 0.92**

It has beaten the baseline every step of the tournament — though the margin is modest, and the
group stage's draw rate (18 of 65) is the ceiling on it (see §6).

---

## 3a. Confusion matrix & F1 (the classifier view)

Treating the model's most-likely pick as a 3-way classifier (`model_f1.py`, same leak-free
walk-forward picks — reproduces the 41/65 above):

```
              PREDICTED
ACTUAL      Home    Draw    Away    tot
  Home        26       0       4     30
  Draw        15       0       3     18
  Away         2       0      15     17
```

| class | precision | recall | F1 | support |
|---|--:|--:|--:|--:|
| Home | 0.60 | 0.87 | 0.71 | 30 |
| Draw | 0.00 | 0.00 | 0.00 | 18 |
| Away | 0.68 | 0.88 | 0.77 | 17 |
| **Macro-F1** | | | **0.494** | |
| **Weighted-F1** | | | **0.530** | 65 |

**Read it correctly — this is a *strong* winner-picker with one structural asterisk:**

- **On games that had a winner it is excellent: ~87% recall on both home and away wins**
  (26/30 and 15/17). Counting only decisive games, the model went **41/47 = 87%** picking the
  right side, and almost never confused a home win for an away win (6 such errors in 47).
- **The Draw row is all zeros because the model never picks "Draw" as its single most-likely
  outcome** — a favourite always edges it (~25–31% on the draw, never the most). So every actual
  draw scores as a miss and Draw F1 = 0, dragging Macro-F1 to 0.49. **This is an argmax artifact,
  not a ranking failure.** The model is a *probabilistic* forecaster; its honest measure is the
  proper scoring in §2–3 (Brier/RPS beat baseline), not a hard-classification F1. It is the same
  draw under-weighting documented in §6, viewed through a classifier lens.

(Full 328-game history for context: Accuracy 51.2%, Macro-F1 0.34 — lower because it's dominated
by tighter qualifiers with the same draw-zeroing; the 65-game WC set is the relevant current test.)

---

## 4. The headline finding: the model is *under-confident*

From `MODEL_CALIBRATION.md` (walk-forward reliability on the 65 games):

| Model said its pick would win… | It actually won | Gap |
|---|--:|--:|
| 40–45% | 60% | **+18 pts** |
| 45–50% | 58% | +11 pts |
| 50–55% | 73% | +20 pts |
| 55–60% | 67% | +9 pts |
| 60–70% | 67% | +1 pts |
| **Overall** | **63%** (claimed 53%) | **+11 pts** |

**The model's favourites win ~11 points more often than it claims.** That's the single most
useful, quantified result of the project — and it's the *good* direction for a bettor: the
model systematically **undervalues its own picks**, so a fairly-priced bet on them carries
value. (ECE = 0.076, so it's not perfectly calibrated — the flip side is that it under-weights
draws, see §6.) **But note the crucial distinction in §7:** this broad under-confidence is real,
yet it did *not* translate into a moneyline edge over a sharp book.

---

## 5. The real edge: beating the market on under-covered teams

A model that just mirrors the betting market is worthless — the edge can only live where they
**disagree**. The thesis (`MODEL_VS_DRAFTKINGS.md`): a US betting market over-weights familiar
sides and **under-covers strong-but-unglamorous African/Asian squads** with European-league
talent. The model, seeing only squad strength, should be right when it's *more bullish* on
those sides.

**It played out:**

| Bet (placed pre-tournament) | DK implied | Model | Outcome |
|---|--:|--:|---|
| **Ghana to qualify** | ~54% | 69% | ✅ **clinched** (drew England 0-0) |
| **Ivory Coast to qualify** | ~74% | higher | ✅ through |
| **Algeria to qualify** | ~67% | higher | ✅ advancing |
| Côte d'Ivoire to *beat* Ecuador | DK favoured Ecuador | model favoured CIV | ✅ 1-0 (the one clean moneyline disagreement — model won) |
| DR Congo to qualify | ~46% | 68%→46% | 🔻 the one that slipped |

The under-covered-African-side thesis went ~4-for-5. **Ghana — backed at the market's 54% and
clinching by holding England — is the signature call.**

**But be precise about *where* the edge lived.** It was in the **qualify / "to advance" market
on under-covered teams** — a structural, season-long read the market shades on reputation. It
was **not** a game-by-game moneyline edge. When the model disagreed with DraftKings on a single
match strongly enough to flag a value bet, **the market won** (see §7). Those are two very
different claims, and conflating them is exactly the overreach a credible write-up should avoid.

---

## 6. Where it failed (the honest part)

A credible scorecard shows the misses:

- **The draw blind spot.** The model assigns draws ~22% but the group stage ran ~28% draws.
  18 of 65 games were draws; the model picked a side in nearly all of them, so most of its
  misses are "favourite controlled the game, drew anyway." This is the main thing inflating its
  Brier — and it's a *calibration* gap, not a ranking error (the favourite was usually the
  stronger side).
- **Dead rubbers.** Germany, already qualified, rotated and lost 2-1 to a motivated Ecuador.
  The model rated Germany on its full squad and got it wrong — the market's lower number had
  correctly priced the rotation. **The model has no concept of "nothing to play for."**
- **The disciplined bet filter is winless.** Our `model_ev` filter (only bet when model prob >
  the price's break-even) is **0-3** — Germany (dead rubber), Sweden (drew), Paraguay (drew).
  Every game where the model was confident enough to *disagree* with the sharp line, the line
  was right. That's the strongest evidence that the model has **no game-level betting edge.**
- **It can't separate the title contenders.** Argentina / England / France / Germany have sat
  within ~0.5% of each other for a week; the "leader" rotates on Monte-Carlo noise. The model
  is honest that the top of the field is a coin-flip — which is correct, but not a bold call.

---

## 7. The betting record (prospective, no hindsight)

`BET_TRACKER.md` logs every pick + real DraftKings price **before kickoff**, graded as games
finish. Three strategies (flat 1-unit, draw = loss):

| Strategy | Record | Net | ROI |
|---|:--:|--:|--:|
| All model picks | 19-8 | +1.83u | +6.8% |
| User's "−127 rule" | 4-6 | −1.55u | **−15.5%** |
| Disciplined "model_ev" | 0-3 | −3.00u | **−100%** |

**This is the most important honest result in the whole project — and it's the opposite of the
clickbait version.** Early on, all three strategies looked great (the "all" ledger was +29%,
the "rule" 3-0). But as the sample grew the two *edge* strategies (`rule`, `model_ev`)
went underwater — `rule` is now **4-6 (−15.5%)** and `model_ev` — the **disciplined** one, the
one a sharp bettor would actually use — is **0-for-3.** The only positive line, "all picks," is a
coarse ride on the model's under-confidence (§4) and has itself regressed from +29% to **+6.8%**
as the games piled up.

**The takeaway:** *a transparent strength model, even a well-calibrated one that beats a
baseline, does not have a game-level edge over a sharp betting market.* Where they disagreed,
the market was right. That's the real, defensible conclusion — and we have every pick logged
with its **pre-kickoff** price to prove we didn't pick this story after the fact.

---

## 8. Reproducibility (everything is checked in)

- **Predictions & results:** `data/results.csv` (scores + de-vigged DK closing odds),
  `RESULTS_TRACKER.md`.
- **Calibration:** `analyze_calibration.py` → `MODEL_CALIBRATION.md`.
- **Confusion matrix & F1:** `model_f1.py` (§3a) — `python model_f1.py`.
- **Forecasts over time:** git history (`docs/` committed at 31/43/47/53/55/65-result checkpoints).
- **Betting:** `bet_tracker.py` + `data/bets.csv` + `BET_TRACKER.md`; `compare_odds.py` for
  model-vs-market.
- **Model & validation:** `predict.py`, `match_engine/elo.py`, `backtest.py --cv`.

Every claim above regenerates from a one-line command. No cherry-picking — the trackers include
the misses by construction.

---

## 9. What's next (knockouts)

The Round of 32 onward is **binary** (advance / out — penalties always produce a winner). We
report `P(advance) = P(win) + ½·P(draw)`, grade on advancement, and score with binary metrics.
**The model should look *better* here**, because its biggest weakness — draws — stops counting
against it: a 1-1 the favourite wins on penalties becomes a *hit*, not a miss. That's the
prediction to test next.

*Generated 2026-06-27. Regenerate the inputs (`analyze_calibration.py`, `bet_tracker.py`,
`gen_live_forecast.py`, `model_f1.py`) and this report stays current.*
