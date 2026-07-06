# Model Calibration — 2026 World Cup (walk-forward)

*Generated 2026-07-06. 87 tournament games, each predicted with ratings as of its own date (no leakage). Calibration asks: when the model said X%, did it happen X%? Brier/log-loss are 3-way (lower better); ECE = expected calibration error (0 = perfect).*

## Headline

- **Top-pick accuracy:** 58/87 = **67%**
- **Brier (3-way):** 0.526  (naive 1/3 baseline = 0.667)
- **Log-loss:** 0.904
- **ECE:** 0.095  (some miscalibration)

## Reliability curve (all outcomes)

*Each row: predictions whose probability fell in that band, vs how often the outcome actually happened. `pred ≈ actual` = calibrated.*

| Prob band | n | Mean pred | Actual | Bar (pred=│ actual=█) |
|---|--:|--:|--:|---|
| 10–20% | 34 | 17% | 15% | `███│················` |
| 20–30% | 121 | 25% | 18% | `████·│··············` |
| 30–40% | 26 | 34% | 19% | `████···│············` |
| 40–50% | 32 | 45% | 62% | `█████████│██········` |
| 50–60% | 31 | 55% | 74% | `███████████│███·····` |
| 60–70% | 16 | 65% | 69% | `█████████████│······` |
| 70–80% | 1 | 74% | 100% | `███████████████│████` |

## Favourite-confidence view (the betting-relevant one)

*Bucket games by how confident the model was in its pick, then its actual win rate. If actual ≥ pred, the model is well-calibrated-or-underconfident — good for value betting.*

| Model said | Games | Won | vs claimed |
|---|--:|--:|---|
| 40–45% | 13 | 69% | +27 pts |
| 45–50% | 19 | 58% | +10 pts |
| 50–55% | 19 | 79% | +26 pts |
| 55–60% | 12 | 67% | +9 pts |
| 60–70% | 16 | 69% | +3 pts |
| 70–101% | 1 | 100% | +26 pts |

## Read
- The model's picks won **67%** overall while claiming **52%** on average — a **+15 pt** gap, i.e. the model is **under-confident** in its favourites.
- Under-confidence is the *good* direction for betting: the model's favourites win more than its numbers say, so a fair-priced bet on them carries value.
- Caveat: 55 games is a small sample and these are all **group-stage** games, where the draw blind spot inflates Brier; knockout (binary advance) calibration will be measured separately.

*Reproduce: `python analyze_calibration.py` (walk-forward over data/results.csv).*
