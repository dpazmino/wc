# Model Calibration — 2026 World Cup (walk-forward)

*Generated 2026-06-29. 73 tournament games, each predicted with ratings as of its own date (no leakage). Calibration asks: when the model said X%, did it happen X%? Brier/log-loss are 3-way (lower better); ECE = expected calibration error (0 = perfect).*

## Headline

- **Top-pick accuracy:** 47/73 = **64%**
- **Brier (3-way):** 0.530  (naive 1/3 baseline = 0.667)
- **Log-loss:** 0.910
- **ECE:** 0.083  (some miscalibration)

## Reliability curve (all outcomes)

*Each row: predictions whose probability fell in that band, vs how often the outcome actually happened. `pred ≈ actual` = calibrated.*

| Prob band | n | Mean pred | Actual | Bar (pred=│ actual=█) |
|---|--:|--:|--:|---|
| 10–20% | 28 | 17% | 14% | `███│················` |
| 20–30% | 101 | 24% | 20% | `████·│··············` |
| 30–40% | 23 | 33% | 17% | `███····│············` |
| 40–50% | 25 | 45% | 60% | `█████████│██········` |
| 50–60% | 28 | 55% | 71% | `███████████│██······` |
| 60–70% | 13 | 66% | 69% | `█████████████│······` |
| 70–80% | 1 | 74% | 100% | `███████████████│████` |

## Favourite-confidence view (the betting-relevant one)

*Bucket games by how confident the model was in its pick, then its actual win rate. If actual ≥ pred, the model is well-calibrated-or-underconfident — good for value betting.*

| Model said | Games | Won | vs claimed |
|---|--:|--:|---|
| 40–45% | 11 | 64% | +21 pts |
| 45–50% | 14 | 57% | +10 pts |
| 50–55% | 16 | 75% | +22 pts |
| 55–60% | 12 | 67% | +9 pts |
| 60–70% | 13 | 69% | +4 pts |
| 70–101% | 1 | 100% | +26 pts |

## Read
- The model's picks won **64%** overall while claiming **52%** on average — a **+12 pt** gap, i.e. the model is **under-confident** in its favourites.
- Under-confidence is the *good* direction for betting: the model's favourites win more than its numbers say, so a fair-priced bet on them carries value.
- Caveat: 55 games is a small sample and these are all **group-stage** games, where the draw blind spot inflates Brier; knockout (binary advance) calibration will be measured separately.

*Reproduce: `python analyze_calibration.py` (walk-forward over data/results.csv).*
