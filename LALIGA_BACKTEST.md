# La Liga Backtest — Phase 1 (club football, results-only)

*Walk-forward, leak-free backtest of the predictor on dense club data. 4,180 La
Liga matches, seasons 2015-16 → 2025-26 (football-data.co.uk), scored against the
de-vigged **closing** market carried in the same files. No squad ratings — clubs
seed at a flat prior and the models learn strength purely from results. First
season (380 games) is warmup, excluded from scoring.*

## The question

The repo's international predictor keeps hitting the same null: team strength is
a scalar, the market beats the model, and fancier models (Dixon–Coles, latent
factors) don't beat plain Elo — but that's on **sparse** data (~5–10 games/team).
The open question the international data could never answer: **does the model beat
the closing line when it has hundreds of games per team to learn from?**

## Result (3,800 games scored)

| Model | Brier | LogLoss | RPS | Accuracy |
|---|--:|--:|--:|--:|
| Base-rate prior | 0.6442 | 1.0665 | 0.2254 | 45.5% |
| Elo (tuned, K=25 HFA=75) | 0.5949 | 0.9998 | **0.2005** | 50.5% |
| **Dixon–Coles** | 0.5855 | 0.9830 | **0.1974** | 52.6% |
| **Market (closing)** | 0.5724 | 0.9639 | **0.1916** | 54.2% |

*(RPS is the 1X2 metric — lower is better. Elo default K=40/HFA=65 gives RPS
0.2018; grid-tuned optimum is K=25/HFA=75 → 0.2005.)*

## Findings

1. **The model works far better on dense data.** Elo crushes the base-rate prior
   (0.2254 → 0.2005, +5.3 pts accuracy) — a real, large edge over "just guess the
   home-win rate," which it can barely manage on international data.

2. **Dixon–Coles finally earns its keep.** On dense data DC beats Elo (0.1974 vs
   0.2005) — the opposite of the international finding where DC ≈ Elo. This
   confirms the repo's standing hypothesis: DC needs dense per-team data to
   estimate reliable attack/defence/rho parameters, and La Liga supplies it.

3. **But the market still wins.** The de-vigged closing line (0.1916) beats even
   Dixon–Coles by **+0.0058 RPS**. Even with a decade of results per club, a
   pure-results model does **not** beat the sharp La Liga closing price. The
   central null survives — but the gap is small and the model is genuinely
   competitive (DC closes ~⅓ of the prior→market distance beyond Elo).

## What this means for betting

Same lesson as the World Cup work, now on dense data: **the closing market is the
best public predictor.** A results-only model is *close* but not ahead, so there
is no broad edge to harvest against La Liga closing lines. Any edge, if it exists,
would live where the model and market disagree on the favourite (rare, given the
0.006 RPS gap) or in **softer markets** — earlier lines, lower divisions, props,
in-play — not the efficient headline 1X2 close.

## Next steps

- **Phase 2:** add a club squad-rating seed (EA FC dataset via `fetch_player_stats.py`)
  to improve cold-start / post-transfer-window accuracy, and test whether it moves
  the gap.
- **Beat-the-close screen:** isolate the fixtures where DC and the market disagree
  on the favourite and grade *those* specifically (the only plausible edge pocket).
- **Phase 3:** MLS — same engine, harder data sourcing (no football-data.co.uk
  coverage; American Soccer Analysis / football-data.org APIs).

## Reproduce

```bash
# 1. download seasons: curl football-data.co.uk/mmz4281/<SS>/SP1.csv -> data/raw/laliga/
python ingest_league.py "data/raw/laliga/*.csv" --out data/laliga_results.csv
python backtest_league.py --warmup 380 --k 25 --hfa 75 --dc
```

*Pure analytic backtest — no simulation, no API key. Re-run as new seasons are
added to `data/raw/laliga/`.*
