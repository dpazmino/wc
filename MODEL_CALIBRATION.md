# Model Calibration — 2026 World Cup (walk-forward)

*Generated 2026-06-26. 59 tournament games, each predicted with ratings as of its own date (no leakage). Calibration asks: when the model said X%, did it happen X%? Brier/log-loss are 3-way (lower better); ECE = expected calibration error (0 = perfect).*

## Headline

- **Top-pick accuracy:** 37/59 = **63%**
- **Brier (3-way):** 0.546  (naive 1/3 baseline = 0.667)
- **Log-loss:** 0.932
- **ECE:** 0.072  (some miscalibration)

## Reliability curve (all outcomes)

*Each row: predictions whose probability fell in that band, vs how often the outcome actually happened. `pred ≈ actual` = calibrated.*

| Prob band | n | Mean pred | Actual | Bar (pred=│ actual=█) |
|---|--:|--:|--:|---|
| 10–20% | 22 | 17% | 18% | `███│················` |
| 20–30% | 84 | 24% | 19% | `████·│··············` |
| 30–40% | 15 | 33% | 20% | `████···│············` |
| 40–50% | 20 | 45% | 60% | `█████████│██········` |
| 50–60% | 25 | 55% | 68% | `███████████│██······` |
| 60–70% | 11 | 65% | 64% | `█████████████│······` |

## Favourite-confidence view (the betting-relevant one)

*Bucket games by how confident the model was in its pick, then its actual win rate. If actual ≥ pred, the model is well-calibrated-or-underconfident — good for value betting.*

| Model said | Games | Won | vs claimed |
|---|--:|--:|---|
| 40–45% | 9 | 67% | +24 pts |
| 45–50% | 11 | 55% | +7 pts |
| 50–55% | 13 | 69% | +16 pts |
| 55–60% | 12 | 67% | +9 pts |
| 60–70% | 11 | 64% | -1 pts |

## Read
- The model's picks won **63%** overall while claiming **53%** on average — a **+10 pt** gap, i.e. the model is **under-confident** in its favourites.
- Under-confidence is the *good* direction for betting: the model's favourites win more than its numbers say, so a fair-priced bet on them carries value.
- Caveat: 55 games is a small sample and these are all **group-stage** games, where the draw blind spot inflates Brier; knockout (binary advance) calibration will be measured separately.

*Reproduce: `python analyze_calibration.py` (walk-forward over data/results.csv).*
