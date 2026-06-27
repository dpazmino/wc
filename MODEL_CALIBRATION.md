# Model Calibration — 2026 World Cup (walk-forward)

*Generated 2026-06-27. 65 tournament games, each predicted with ratings as of its own date (no leakage). Calibration asks: when the model said X%, did it happen X%? Brier/log-loss are 3-way (lower better); ECE = expected calibration error (0 = perfect).*

## Headline

- **Top-pick accuracy:** 41/65 = **63%**
- **Brier (3-way):** 0.539  (naive 1/3 baseline = 0.667)
- **Log-loss:** 0.922
- **ECE:** 0.076  (some miscalibration)

## Reliability curve (all outcomes)

*Each row: predictions whose probability fell in that band, vs how often the outcome actually happened. `pred ≈ actual` = calibrated.*

| Prob band | n | Mean pred | Actual | Bar (pred=│ actual=█) |
|---|--:|--:|--:|---|
| 10–20% | 24 | 17% | 17% | `███│················` |
| 20–30% | 92 | 24% | 20% | `████·│··············` |
| 30–40% | 18 | 33% | 17% | `███····│············` |
| 40–50% | 22 | 45% | 59% | `█████████│██········` |
| 50–60% | 27 | 55% | 70% | `███████████│██······` |
| 60–70% | 12 | 65% | 67% | `█████████████│······` |

## Favourite-confidence view (the betting-relevant one)

*Bucket games by how confident the model was in its pick, then its actual win rate. If actual ≥ pred, the model is well-calibrated-or-underconfident — good for value betting.*

| Model said | Games | Won | vs claimed |
|---|--:|--:|---|
| 40–45% | 10 | 60% | +18 pts |
| 45–50% | 12 | 58% | +11 pts |
| 50–55% | 15 | 73% | +20 pts |
| 55–60% | 12 | 67% | +9 pts |
| 60–70% | 12 | 67% | +1 pts |

## Read
- The model's picks won **63%** overall while claiming **53%** on average — a **+11 pt** gap, i.e. the model is **under-confident** in its favourites.
- Under-confidence is the *good* direction for betting: the model's favourites win more than its numbers say, so a fair-priced bet on them carries value.
- Caveat: 55 games is a small sample and these are all **group-stage** games, where the draw blind spot inflates Brier; knockout (binary advance) calibration will be measured separately.

*Reproduce: `python analyze_calibration.py` (walk-forward over data/results.csv).*
