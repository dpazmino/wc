# Model vs DraftKings — Stage-of-Elimination Props

*Generated 2026-06-18. DraftKings 7-way 'Stage of Elimination' markets (`downloads/elim.txt`, a fixed pre-tournament snapshot) de-vigged and compared to the model's live elimination distribution (100,000 MC, 23 results locked). Stages map 1:1 (Last 32→R32, Runner-Up→Final, Outright Winner→Champion). **Only teams yet to kick off are scored** — once a team plays, its pre-game line is stale vs a model that knows the result, so it drops out. As the tournament runs the clean set shrinks; right now it is **1 teams** (Tunisia).*

> ⚠️ **Screen nearly exhausted.** Only 1 unplayed team(s) still carry a usable DK line (Tunisia). The thesis bets this screen surfaced — **Ghana** and **DR Congo** — have kicked off (Ghana won 1-0 vs Panama, DR Congo drew Portugal 1-1) and are now tracked live in `MODEL_VS_DRAFTKINGS.md`. This report adds little until fresh DK lines replace `downloads/elim.txt`.

## Headline: the model is more *diffuse* than the market

The model pushes probability into the **tails** more than DraftKings does, so it manufactures nominal '+EV' on longshot exits everywhere — which reflects the model being **less sharp than a sharp book**, not real value (its known miscalibration: under-confident on favourites, over-rating minnows; see RESULTS_TRACKER.md). Two shapes recur across the run:

- **Model > market on early exits for favourites** — e.g. while still clean, Colombia exit-group 28% vs 13%, England exit-R32 31% vs 21%.
- **Model < market on the modal exit for minnows** — e.g. Tunisia group-exit 67% vs 86%.

Either way the exact-stage exotics are noise, not edge.

## Cleanest signal — model vs market 'to qualify' (reach Last 32+)

*Reliable shallow output; +edge = model more bullish on advancing. **A large +pp on a weak side (e.g. Tunisia) is the model over-rating minnows — a fade, not a bet.** Genuine edge needs an under-covered but genuinely strong side. Sort sign alone does not pick a bet.*

| Team | Grp | Model qualify | Market (de-vig) | Edge (pp) |
|---|:--:|--:|--:|--:|
| Tunisia | F | 33% | 14% | +19 |

## Credible edges (CIV thesis — under-covered side advances)

- **Ghana to qualify** — placed pre-tournament (model 69% vs DK ~54%); has kicked off, now **85%** model qualify. *Realized/live — tracked in `MODEL_VS_DRAFTKINGS.md`.*
- **DR Congo to qualify** — placed pre-tournament (model 59% vs DK ~46%); has kicked off, now **67%** model qualify. *Realized/live — tracked in `MODEL_VS_DRAFTKINGS.md`.*

The to-qualify market is the clean expression; both are thesis-tests, not locks.

## Fades (model miscalibration, not value)

- Over-rated minnows **to advance** (e.g. Tunisia, Uzbekistan) — thin/backfilled Elo.
- Favourites **to exit early** — the model's under-confidence, not a real signal.

## Full +EV screen (clean teams, Group/R32/R16/QF only)

*Listed for completeness — treat as model diffuseness unless it also fits the under-covered-strong-side read above.*

| Team | Exit stage | Model | Market (dv) | Price | EV/$1 |
|---|:--:|--:|--:|---|--:|
| Tunisia | R16 | 8% | 3% | +3500 | +172% |
| Tunisia | R32 | 22% | 10% | +850 | +109% |
| Tunisia | QF | 3% | 1% | +6500 | +67% |

## Caveats
- SF/Final/Champion edges excluded (knockout coin-flips + thin squads = noise).
- Teams that have already played are excluded (stale lines).
- 'Credible' edges are the thesis under test (n tiny); the market may simply know these squads are weaker than their rating.

*Reproduce: `python compare_elim.py` (reads `downloads/elim.txt`, live n=100000).*
