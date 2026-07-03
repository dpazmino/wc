# MLS Backtest — Phase 3 (club football, results-only)

*Walk-forward, leak-free backtest of the predictor on Major League Soccer. 6,034
MLS matches, seasons 2012 → 2026 (football-data.co.uk `/new/USA.csv`), scored
against the de-vigged **closing** market (100% odds coverage). No squad ratings by
default — clubs seed at a flat prior and the models learn strength from results.
First 400 games are warmup, excluded from scoring.*

## Why MLS is the interesting test

Phase 1–2 (La Liga, `LALIGA_BACKTEST.md`) showed the model is accurate but can't
beat La Liga's sharp closing line — and its disagreements with the market are
noise. The Phase 2 prediction was that **MLS lines are softer** (less volume, less
sharp attention than a big-5 European league), so the beat-the-close screen is the
more interesting test here. MLS also has strong home advantage and frequent
expansion teams (cold-starts), which stress different parts of the model.

## Result (5,634 games scored, K=12 HFA=120)

| Model | Brier | LogLoss | RPS | Accuracy |
|---|--:|--:|--:|--:|
| Base-rate prior | 0.6279 | 1.0437 | 0.2199 | 49.4% |
| Elo | 0.6226 | 1.0378 | 0.2158 | 48.6% |
| Elo + squad seed | 0.6226 | 1.0378 | 0.2158 | 48.6% |
| Dixon–Coles | 0.6208 | 1.0341 | 0.2163 | 49.6% |
| **Market (closing)** | 0.6050 | 1.0109 | **0.2090** | 50.6% |

*(MLS home advantage is large — best Elo needs HFA≈120 Elo pts vs La Liga's 75, and
a low K≈12. Base rate is 49/25/25 H/D/A — half of all MLS games are home wins.)*

## Findings

1. **The model works, but by less than in La Liga.** Elo beats the prior
   (0.2199 → 0.2158), but the margin is smaller — MLS's salary-cap **parity**
   compresses team strength, leaving less signal for a strength model to exploit.

2. **The squad seed does nothing here** (Elo = Elo+seed, identical to 4 dp). In a
   parity league the squad-overall range is tiny (68.7–76.6, vs La Liga's
   67.8–87.6), so seeding cold-starts from squad strength ≈ the flat prior. The
   seed only helps in a **dispersed-talent** league (La Liga), confirming *why* it
   helped there — not a universal win.

3. **Dixon–Coles ≈ Elo here** (0.2163 vs 0.2158 RPS — DC marginally *worse* on RPS,
   slightly better on Brier/accuracy). In La Liga DC clearly beat Elo (0.1974 vs
   0.2005); in MLS parity flattens that advantage too — the attack/defence
   decomposition needs talent dispersion to pay off.

4. **The market still wins on accuracy** (0.2090 vs 0.2158) — but the gap (+0.0068
   RPS) is similar to La Liga's, on a noisier league.

## Beat-the-close screen — a tempting mirage

On the 666 games where the seeded model and the closing line pick a **different
match-winner**, betting the model's side at the closing price:

| League | Bets | ROI | Bootstrap 95% CI | Verdict |
|---|--:|--:|---|---|
| La Liga | 467 | −5.0% | [−18.3%, +8.8%] | no edge |
| **MLS** | 666 | **+5.0%** | **[−6.2%, +16.2%]** | **no *proven* edge** |

The MLS point estimate flips positive (+5% ROI, 227–439) — directionally consistent
with softer MLS lines. **But the bootstrap 95% CI spans zero.** On 666 high-variance
plus-money bets, a +5% ROI is only ~1 standard error from nothing — indistinguishable
from noise. Reporting the point estimate alone would have been a false positive; the
CI is the honest test, and it says **not yet**.

## Bottom line

MLS is *more encouraging* than La Liga — the disagreement ROI is positive rather than
negative, matching the soft-market thesis — but it is **not a proven edge**. The model
remains accurate-but-not-sharper-than-the-close, and the one hint of an exploitable
pocket (soft MLS lines) needs far more data before it clears statistical noise.

## Next steps

- **More data / narrower screen:** re-run as seasons accumulate; try tightening the
  screen to *large* model-vs-market disagreements (where any real edge should be
  strongest) to see if a signal separates from noise.
- **Live soft-line test:** the real MLS edge test is against *current* MLS lines, not
  historical closes — the softest MLS markets are the early/live ones.

## Reproduce

```bash
curl football-data.co.uk/new/USA.csv -> data/raw/mls/USA.csv
python ingest_league.py data/raw/mls/USA.csv --out data/mls_results.csv
python club_seed.py --league mls
python backtest_league.py data/mls_results.csv --warmup 400 --k 12 --hfa 120 --dc --seed
python beat_close.py data/mls_results.csv --seedcsv data/mls_squad_overalls.csv \
    --hfa 120 --k 12 --warmup 400
```
