# What Could Actually Improve Predictions — Evidence-Ranked Gap Analysis

*A focused companion to `GAP_ANALYSIS.md` (which inventories production-readiness). This one
asks the narrower question — **what would measurably raise accuracy** — and answers it from the
evidence we now have: a live 2026 track record plus five completed augmentation experiments.
Generated 2026-06-27. Reproduce the numbers with `backtest.py --cv`, `coach_clash.py`, etc.*

---

## Where the model stands (366 results, 65 WC games)

- **Beats the base rate out-of-sample:** `pred` RPS **0.201** vs prior 0.232; CV optimism ~0.000.
- **In-tournament:** 41/65 = 63% top-pick, Brier 0.539, mildly under-confident (ECE 0.076).
- **Loses to the market game-to-game:** on the 28 fixtures with closing odds, **market RPS 0.149
  vs pred 0.177** (pred+market anchor 0.158). That 0.028 gap is *larger* than the 0.031 by which
  the model beats the prior — the market is comfortably better than the model.

---

## The headline: the feature-engineering levers are spent

Five separate attempts to add signal *beyond scalar team strength* have now been built, isolated,
and walk-forward tested. **Every one is an out-of-sample null:**

| Experiment | What it added | Verdict |
|---|---|---|
| Full 22-agent match sim | tactics, players, events in depth | ~0 over strength (`GAP_ANALYSIS.md`) |
| `player_match/` | unit style matchups (attack vs defence…) | NO edge (CV 0.1754 vs 0.1734) |
| `psycho_stress/` | heat/altitude/travel/circadian stress | NO edge (CV worse than baseline) |
| `coach_clash.py` | coach/tactical-style clash | NO edge (in-sample best K=0) |
| Dense-data ingest | thousands of 2023–26 matches | NO improvement (squad-Elo isn't data-hungry) |

Plus a sixth, just measured: **draw recalibration is a non-lever.** The model's draw mass (~22%)
sits below the actual WC draw rate (28%), which *looks* like a gap — but sweeping `DRAW_BASE`
from 0.30→0.60 moves walk-forward RPS by **<0.0002** (0.1695→0.1697, and it gets *worse* past
0.45). Because the model can't discriminate *which* games draw (`analyze_draws.py`), adding draw
mass only shaves win/loss confidence. **Already optimal; leave it.**

**Read this correctly:** six independent probes all say *scalar team strength already absorbs the
signal*. This is strong evidence the model is near the ceiling of what this data and method can
do. The conclusion is not "try a seventh feature" — it's **stop feature-engineering and change the
inputs.**

---

## What could actually move the needle (ranked by evidence)

### 1. Market odds on every game + anchoring — **PROVEN, highest ROI** · data
The market beats the model by 0.028 RPS where we have odds, and anchoring to it (`predict.py
--odds`) demonstrably closes most of that gap. The mechanism is fully built; the only thing
missing is **odds data for more than 28 of 366 fixtures.** This is the single highest-confidence
improvement available, and it's pure data acquisition. *Action:* populate `results.csv` cols 7–9
for every fixture (`apply_odds.py`), then anchor by default.

### 2. Lineup / availability data — **PLAUSIBLE, untested** · data
The one context factor with a real mechanism we *couldn't* test for lack of data: who actually
plays. The model rates full-strength squads, so it misreads **rotation, injuries, suspensions,
and rest** — exactly the `Germany 2-1 Ecuador` dead-rubber miss ([[dead-rubber-model-bias]]).
Unlike style/stress features (tested null), availability changes the *strength input itself*, so
it has a credible path to edge. *Action:* fixture-level XI / availability feed → adjust the
effective squad rating. Unproven until we have the data.

### 3. Better player-rating inputs — **PLAUSIBLE, untested** · data
Elo's seed and low-data fallback are FIFA "overall" — a game rating, not a predictive metric, and
several squads have <11 rated players (Iran/Iraq/Qatar/Egypt/South Africa). xG-derived,
minutes/age-adjusted player values would sharpen the seed and the thin-squad fallback. Bounded
upside (Elo learns from results for teams that play often), but it's the quality floor for
under-covered sides — the very teams where the model's biggest errors and "edges" both live.

### 4. Match-stakes / dead-rubber flag — **NICHE** · data + method
A motivation/phase adjustment for dead rubbers ([[dead-rubber-model-bias]]) addresses a real,
repeated miss — but it fires on few games and is hard to validate on a small sample. Worth a flag,
not a research program.

---

## What NOT to spend time on

- **More feature engineering on style / tactics / context / player-matchups** — six nulls. The
  signal isn't there beyond scalar strength.
- **Retuning draws or shrink** — draw RPS is flat; shrink is stable at 0.25 and the in-tournament
  sweep drift is noise ([[shrink-calibration-hold-025]]). Don't reactively retune.
- **More raw results volume** — already tested null ([[dense-data-ingest-no-help]]).
- **Re-adding the simulation to prediction** — it was removed for adding nothing; nothing has
  changed.

---

## Bottom line

The **method is mature and the feature space is exhausted** — six independent augmentations all
confirm scalar strength absorbs the signal. The remaining accuracy is **not a modeling problem;
it's an inputs problem**, and the order is clear: (1) **market odds everywhere** (proven — the
market beats us by 0.028 RPS), then (2) **lineups/availability** and (3) **xG-based player
ratings** (plausible, change the strength input itself, but unproven until the data exists). None
of these can be conjured by more code on the current data — only by feeding the model better data.

*Related: `GAP_ANALYSIS.md` (production inventory), `MODEL_PERFORMANCE.md` (track record),
`docs/MODEL_VS_DRAFTKINGS.md` (market edge). Augmentation nulls: `player_match/`, `psycho_stress/`,
`coach_clash.py`.*
