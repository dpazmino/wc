# Predicting the 2026 World Cup — Model Performance Report

*A running, honest scorecard of a transparent strength model's predictions across the 2026
World Cup. Updated through 2026-06-25 (55 group-stage games). This is the evidence base — wins
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

On 294 historical fixtures, walk-forward (each game scored with ratings known only *before*
it), via `backtest.py --cv`:

| Model | RPS ↓ | Brier ↓ | beats base rate? |
|---|--:|--:|:--:|
| Base-rate prior | 0.231 | 0.662 | — |
| **Production (`pred`)** | **0.205** | **0.608** | ✅ |

**Cross-validated optimism: 0.001** — the edge is real, not overfit. This is the credibility
floor: the model was validated *before* a single 2026 game was scored.

---

## 3. In-tournament accuracy (55 games)

From `RESULTS_TRACKER.md` (walk-forward — the prediction never saw its own result):

- **Top-pick accuracy: 36 / 55 = 65%**
- **Brier (3-way): 0.540** vs **0.667** naive baseline
- **Log-loss: 0.923**

It has beaten the baseline every step of the tournament.

---

## 4. The headline finding: the model is *under-confident*

From `MODEL_CALIBRATION.md` (walk-forward reliability on the 55 games):

| Model said its pick would win… | It actually won | Gap |
|---|--:|--:|
| 40–45% | 67% | **+24 pts** |
| 45–50% | 67% | +19 pts |
| 50–55% | 69% | +16 pts |
| 55–60% | 67% | +9 pts |
| 60–70% | 60% | −5 pts |
| **Overall** | **65%** (claimed 53%) | **+12 pts** |

**The model's favourites win ~12 points more often than it claims.** That's the single most
useful, quantified result of the project — and it's the *good* direction for a bettor: the
model systematically **undervalues its own picks**, so a fairly-priced bet on them carries
value. (ECE = 0.092, so it's not perfectly calibrated — the flip side is that it under-weights
draws, see §6.)

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

---

## 6. Where it failed (the honest part)

A credible scorecard shows the misses:

- **The draw blind spot.** The model assigns draws ~22% but the group stage ran ~25–30% draws.
  14 of 55 games were draws; the model picked a side in nearly all of them, so most of its
  misses are "favourite controlled the game, drew anyway." This is the main thing inflating its
  Brier — and it's a *calibration* gap, not a ranking error (the favourite was usually the
  stronger side).
- **Dead rubbers.** Germany, already qualified, rotated and lost 2-1 to a motivated Ecuador.
  The model rated Germany on its full squad and got it wrong — the market's lower number had
  correctly priced the rotation. **The model has no concept of "nothing to play for."**
- **The disciplined bet lost first.** Our `model_ev` betting filter (only bet when model prob >
  the price's break-even) is 0-1 — its lone bet was that dead-rubber Germany game. A real,
  identifiable failure mode, not noise.
- **It can't separate the title contenders.** Argentina / England / France / Germany have sat
  within ~0.5% of each other for a week; the "leader" rotates on Monte-Carlo noise. The model
  is honest that the top of the field is a coin-flip — which is correct, but not a bold call.

---

## 7. The betting record (prospective, no hindsight)

`BET_TRACKER.md` logs every pick + real DraftKings price **before kickoff**, graded as games
finish. Three strategies (flat 1-unit, draw = loss):

| Strategy | Record | Net | ROI |
|---|:--:|--:|--:|
| All model picks | 14-3 | +4.86u | +29% |
| User's "−127 rule" | 3-1 | +2.65u | +66% |
| Disciplined "model_ev" | 0-1 | −1.00u | −100% |

**Caveat we keep front and centre:** these are tiny samples (1–17 bets). The +29% ROI is
riding the model's strong group-stage favourites and *will* regress. The point of the ledger is
an honest forward test, not a victory lap — the real verdict needs ~30+ graded bets.

---

## 8. Reproducibility (everything is checked in)

- **Predictions & results:** `data/results.csv` (scores + de-vigged DK closing odds),
  `RESULTS_TRACKER.md`.
- **Calibration:** `analyze_calibration.py` → `MODEL_CALIBRATION.md`.
- **Forecasts over time:** git history (`docs/` committed at 31/43/47/53/55-result checkpoints).
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

*Generated 2026-06-25. Regenerate the inputs (`analyze_calibration.py`, `bet_tracker.py`,
`gen_live_forecast.py`) and this report stays current.*
