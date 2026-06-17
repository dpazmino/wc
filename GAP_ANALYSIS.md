# Gap Analysis — Match Predictor

**Purpose:** an honest inventory of what this project has versus a production-grade
real-world football **predictor** (FiveThirtyEight SPI, Opta/Stats Perform, bookmaker
models, Dixon–Coles / bivariate-Poisson). Each gap is rated by severity for prediction
quality and points at the relevant code.

Severity: **Critical** (bounds real-world accuracy today) · **High** · **Medium** · **Low**.

> **Status:** the predictor works. On 254 real fixtures it beats a base-rate prior
> *out-of-sample* (cross-validated RPS 0.211 vs 0.232). The match **simulation has been
> removed from the prediction path** — it added no predictive value — and now serves only
> as the match-narrative engine. What remains is about improving accuracy and
> production-readiness, not making it function.

---

## Executive summary

The predictor is now a **strength model**: dynamic Elo (learned from results, recency-decayed,
regularised toward squad strength) → calibrated by shrinking toward the base rate → optionally
anchored to market odds. It is analytic, instant, and needs no API key. It is validated with
the standard toolkit (walk-forward, RPS, ECE/reliability, k-fold CV).

The three gaps that now matter most — all about **inputs**, not method:

1. **No betting-market data.** The market is the single strongest public predictor, and both
   the anchor (`predict.py --odds`) and the benchmark (`backtest.py`) are built — but
   `data/results.csv` carries **no odds**, so neither runs on real data. This is the highest-ROI
   gap and the only way to know whether the model beats the market (the real bar).
2. **Thin / shallow data.** 254 results is enough to beat a base rate but sparse for Elo
   (~5 games/team). No lineups, injuries, form-beyond-Elo, venue, rest, or head-to-head.
   `ingest_results.py` is ready to pull thousands from a public database.
3. **Rating *inputs* are subjective.** Elo learns from results, but its **seed and low-data
   fallback are FIFA "overall"** — a game rating, not a predictive metric. No age/form/minutes
   weighting; thin squads (Iran/Iraq/Qatar/Egypt/South Africa < 11 players) stay noisy.

Everything else (Dixon–Coles, tournament odds, context factors, uncertainty, engineering) is
capability/polish on top of a working core.

---

## What the project now has

**Prediction (sim-free):**
- `predict.py` — strength W/D/L (Elo `strength_probs` → shrink → optional market anchor) +
  independent-Poisson xG/scorelines. Instant, no API.
- `match_engine/elo.py` — dynamic Elo: goal-difference weighted, home-field advantage,
  squad-seeded, **recency decay** (idle ratings regress toward the prior), regularised toward
  the squad prior by games played.
- `match_engine/ratings.py` — squad strength (`team_rating`, `outcome_probs`), shared
  `combine_probs` (blend+shrink), `BASE_PRIOR`. Seeds Elo and is the low-data fallback.
- `match_engine/odds.py` — de-vig decimal odds (proportional/power) + market `anchor`.
- `backtest.py` — analytic, no cache: scores prior / squad / elo (walk-forward) / strength /
  **pred** (production) and the market; **RPS**, Brier, log-loss, **ECE**; `--sweep` (tune
  shrink), `--cv` (k-fold cross-validate), `--reliability` (calibration curves).
- `data/results.csv` — 254 real results, 2014–2025; `ingest_results.py` to import thousands.

**Simulation (narrative engine, off the prediction path):**
- `match_engine/` LLM / offline / hybrid match engine, box-score-calibrated (`calibrate.py`),
  48-team scheduler with knockouts/ET/shootouts. Used by `run_match.py` — not by `predict.py`.

**Validation result (254 fixtures, walk-forward):**
`pred` RPS 0.211 / Brier 0.622 / ECE 0.017 — beats prior (0.232), squad (0.217), elo (0.215),
strength (0.216). Cross-validated RPS 0.211 with optimism ~0.000 (one stable hyperparameter).

---

## Gaps remaining, by category

### 1. Market odds — **Critical** · `odds.py`, `data/results.csv`
Mechanism complete (de-vig, `--odds` anchor, backtest market comparison) but **no odds data**.
Until odds are populated, the market anchor and the "beat the market" benchmark are inert. The
market typically beats strength models, so this is both the biggest accuracy lever and the only
honest success bar. *Done:* the plumbing. *Missing:* the data.

### 2. Real-world data inputs — **Critical** · data pipeline
Beyond results, a real model ingests **lineups, injuries/suspensions, recent form, venue,
rest/travel/congestion, head-to-head, match stakes**. None exist; the model knows only ratings
derived from final scores. 254 results is also thin for Elo — ingest the full public database
(`ingest_results.py`) for density. *Also:* fix the favorite-listed-as-"home" labeling artifact
in `results.csv` (inflates the prior's accuracy metric).

### 3. Rating inputs quality — **High** · `stats_loader.py`, `player_stats.csv`
The Elo **seed and fallback** are FIFA-style "overall" — subjective, not predictive; no age
curve, no form/minutes weighting, no xG-derived player value. Several squads have < 11 rated
players (noisy). Elo learning from results mitigates this for teams that play often, but thin
squads and the seed remain weak.

### 4. Goal / scoreline model — ~~Medium~~ **largely addressed** · `dixoncoles.py`
`match_engine/dixoncoles.py` is a full **Dixon–Coles** model (MLE-fit attack/defence, home
term, low-score `rho`, time-decay, L2-regularised), evaluated out-of-sample in
`backtest.py --dc`. **Finding:** on sparse international data (~5 games/team, no squad prior)
DC is no better than the Elo strength model (time-split test: DC RPS ≈ pred ≈ prior), so the
strength model stays the default and `predict.py` keeps its independent-Poisson scorelines.
*Remaining:* DC would win with denser league data; the W/D/L and scoreline models are still
not forced mutually consistent.

### 5. Tournament-level forecasting — ~~Medium~~ **DONE** · `tournament.py`
`tournament.py` Monte-Carlos the full 2026 format (12 groups → 8 best thirds → 32-team
knockout) driven by `predict.py`, outputting group-win / qualify / per-round / title odds.
*Remaining polish:* the official bracket template (we strength-seed) and host-nation
(USA/Mexico/Canada) home advantage (we treat all venues as neutral).

### 6. Context / situational factors — **Medium (partial)** · `tournament.py`, `predict.py`
**Done:** host-nation home advantage — `tournament.py` gives USA/Mexico/Canada the home Elo
edge in their group games (`predict.py --home` for any home game). **Remaining:** venue
altitude (Mexico City) and heat (2026 US summer), travel/rest/congestion, motivation/stakes,
and availability adjustment for missing key players — all need fixture-level venue/lineup data.

### 7. Uncertainty quantification — ~~Medium~~ **addressed** · `predict.py`, `tournament.py`
**Done:** `predict.py` reports a 95% interval on each win probability from rating uncertainty
(games-based standard error, Monte-Carlo propagated); `tournament.py` reports 95% MC intervals
on title odds. *Remaining polish:* formal rating covariance rather than an independent per-team SE.

### 8. Engineering / pipeline / reproducibility — **Medium (partial)** · repo-wide
**Done:** a pytest suite (`tests/test_prediction.py`, 15 tests) covering odds, Elo, calibration,
scoring metrics, predict, Dixon–Coles, and tournament conservation. **Remaining:** automated
ingest-and-update pipeline (ratings auto-refresh from a live feed), data/model versioning, CI.

### 9. Calibration method — ~~Low~~ **addressed** · `backtest.py`
**Done:** `backtest.py --cal` cross-validates shrink-to-prior against temperature scaling — they
are equivalent here (CV RPS 0.211 each), so the simpler shrink stays. Isotonic would need more
data to pay off.

---

## Resolved since the original analysis

- ✅ **Dynamic, results-driven ratings** — `elo.py` (goal-diff weighted, HFA, squad-seeded,
  regularised, **recency decay**). *(was the #1 Critical gap)*
- ✅ **Validation toolkit** — walk-forward, **RPS**, **ECE/reliability**, **k-fold CV**, market-
  benchmark mechanism. *(was the Critical validation gap)*
- ✅ **Simulation removed from prediction** — CV showed it adds nothing; `predict.py` is now
  strength-only. The sim remains the narrative engine. *(was the "shallow predicting engine" gap)*
- ✅ **Data 109 → 254** + `ingest_results.py` for thousands more.
- ✅ **Poisson scoreline model** replaced sim-derived scorelines.
- ✅ **Tournament Monte-Carlo** — `tournament.py` produces 2026 group/qualify/round/title odds,
  with host-nation home advantage and 95% MC intervals.
- ✅ **Dixon–Coles model** built and evaluated out-of-sample (`dixoncoles.py`, `backtest.py --dc`).
- ✅ **Uncertainty** — rating-CI bands in `predict.py`, MC intervals in `tournament.py`.
- ✅ **Test suite** — `tests/test_prediction.py` (15 tests).
- ✅ **Calibration check** — shrink vs temperature compared (`--cal`); equivalent.

---

## Prioritized roadmap — what's left (all data / infrastructure)

Every *method/capability* gap is now closed. The remaining work is **acquiring data** and
**production infrastructure** — things code alone can't conjure:

1. **Real closing odds** → populate `results.csv` columns 7–9; the anchor and benchmark run
   automatically. The one signal that reliably beats strength models. *(gap #1, data)*
2. **Full-database ingest** → run `ingest_results.py` on the public results CSV for thousands of
   matches; denser, more reliable Elo (and DC would become viable). *(gap #2, data)*
3. **Better rating inputs** → replace/augment the FIFA-overall seed with xG-derived,
   minutes/age-adjusted player value; backfill thin squads. *(gap #3, data)*
4. **Fixture-level context** → venue/altitude/heat, rest/travel, lineups/availability. *(gap #6, data)*
5. **Production pipeline** → automated ingest-and-update of results/odds/ratings, versioning, CI. *(gap #8, infra)*

---

## Summary table

| # | Gap | Severity | Status |
|---|---|---|---|
| 1 | Market odds (anchor + benchmark) | **Critical** | mechanism done; **needs odds data** |
| 2 | Real-world inputs (lineups, form, venue, rest, H2H) + data volume | **Critical** | 254 results + ingest tool; **needs data** |
| 3 | Rating inputs are subjective FIFA overalls; thin squads | **High** | Elo mitigates; **needs better player data** |
| 4 | Dixon–Coles goal model | **Done** | built + OOS-evaluated (`dixoncoles.py`, `--dc`) |
| 5 | Tournament forecasting | **Done** | `tournament.py` (host adv + MC intervals) |
| 6 | Context: venue/altitude/travel/stakes/availability | **Partial** | host advantage done; rest needs fixture data |
| 7 | Uncertainty / intervals | **Done** | rating CIs (predict) + MC CIs (tournament) |
| 8 | Data pipeline / tests / versioning | **Partial** | test suite done; pipeline/CI remain |
| 9 | Calibration method | **Done** | shrink vs temperature compared (`--cal`) |

---

## Bottom line

This is a **working, honestly-validated, base-rate-beating predictor** built on a clean
separation: **team strength predicts, the simulation narrates.** Every method and capability
gap is now closed — dynamic Elo with recency decay, calibrated probabilities, walk-forward +
RPS + ECE + reliability + cross-validation, a Dixon–Coles reference model, tournament odds with
host advantage and confidence intervals, uncertainty bands, and a test suite.

What remains is **not code** — it is **data and infrastructure**: real betting odds (#1), more
and richer match/player data (#2, #3), fixture-level context (#6), and a production ingest
pipeline (#8). Those are the only things now standing between this and a genuinely competitive
real-world predictor, and none of them can be solved by further modeling — only by feeding the
machine real, current data.
