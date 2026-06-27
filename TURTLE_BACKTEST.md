# Turtle Filter — Backtest & Forward Test

*Does an asymmetric-payoff "turtle" betting rule beat the market where the straight
model can't? Short answer: **no demonstrated edge** — and the backtest specifically
debunks the intuitive version. This documents the test so we don't re-run the same
hope. Reproduce: `python backtest_turtle.py` (historical) and `python bet_tracker.py`
(live forward test). Generated 2026-06-27.*

---

## The idea

Turtle trading lives on **asymmetric payoff**: small frequent losses, occasional big
wins, where *one good bet covers two bad ones*. You can only get that shape at
**plus-money** prices (decimal ≥ 2.0): at +200 a single winner pays for two losers, so
a 34% hit rate breaks even. Minus-money favourites are the opposite trade — you need
two wins to cover one loss.

This matters because the model's two *real* tendencies point at underdogs:
- it is **under-confident** (its favourites win ~11 pts more than it claims), and
- it is more bullish than a US market on **under-covered** strong squads (the Ghana /
  Ivory Coast profile).

So the hypothesis: **back plus-money underdogs the model rates above the market, skip
the favourites.** This file tests it honestly.

---

## The backtest (28 past fixtures with closing odds)

Leak-free walk-forward (each game scored with ratings known only before it), draw =
loss, flat 1u, graded at the real decimal price. One bet per game at most.

| Strategy | Bets | W-L | ROI |
|---|--:|:--:|--:|
| *Baseline:* flat market favourite | 28 | 18-10 | −3.2% |
| *Baseline:* flat market underdog | 28 | 3-25 | −54.3% |
| Turtle: any side model > market | 27 | 3-24 | **−57.6%** |
| + skip thin squads | 27 | 3-24 | −57.6% |
| + not thin + model ≥30% (live dog) | 8 | 2-6 | 0.0% |
| + not thin + **edge ≥5 pts** | 21 | 1-20 | **−72.6%** |
| **Model-favourite plus-money dog + not thin** | 4 | 2-2 | +17.5% |

### Three findings

1. **The naive turtle is a disaster (−57%).** "Bet any underdog the model likes more
   than the market" just bets longshots — because the model is **diffuse**, it likes
   *almost every* dog, so the rule collapses into the −54% flat-underdog baseline.

2. **Selecting *bigger* edges makes it actively worse (−72.6%, 1-20).** This is the
   important one. The model's *largest* disagreements with the market are its *worst*
   bets — they are maximal **miscalibration**, not maximal value. "Bet where the model
   screams value" is exactly backwards here.

3. **The only non-losing pockets are tiny and noise-driven.** The "live dog" floor
   (model ≥30%) lands at break-even on 8 bets, propped up by a single 5.75 longshot.
   The "model-favourite plus-money" cut is +17.5% — but on **4 bets (2-2)**, and even
   there the two **winners had +1 pt edges** (true slight leans) while the two
   **losers had +12/+16 pt edges** (the diffuse picks). Same pattern as #2, inside a
   4-bet sample. Note these "winners" don't actually beat the vig — they won on
   variance, not +EV.

---

## The live forward test

`bet_tracker.py` now logs a **`turtle`** strategy — plus-money picks (decimal ≥ 2.0)
on covered (non-thin) squads, locked at the DraftKings price **before kickoff**. This
is the model-favourite-plus-money rule from the backtest, run prospectively with no
hindsight.

**Record so far: 2-5, −32.9%** (3 pending). Small and red — consistent with the
backtest. It will update as knockout games settle; see `BET_TRACKER.md`.

---

## Conclusion

**The turtle *structure* is sound; this model has no underdog-*selection* skill to feed
it.** Asymmetric payoff is the right shape, but the model can't pick *which* plus-money
dogs to back — its underdog enthusiasm is diffuseness, and the more enthusiastic it is,
the worse the bet. The least-bad rule is the narrow one (plus-money sides the model
*outright favours*, small edge, covered squad), but it is a 4-bet hypothesis, not an
edge, and the live version is 2-5.

This is the same spine as the rest of the project: **no demonstrated game-level edge
over a sharp book.** The turtle test didn't find a backdoor — it found a new way to
lose (chasing the biggest model/market gaps) and ruled it out.

*Reproduce: `python backtest_turtle.py` · live record in `BET_TRACKER.md`
(`python bet_tracker.py`). Related: [[model-vs-draftkings-tracker]], MODEL_PERFORMANCE.md §5/§7.*
