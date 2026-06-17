# Model vs DraftKings — Stage-of-Elimination Props

*Generated 2026-06-17. DraftKings 7-way 'Stage of Elimination' markets (`downloads/elim.txt`, a fixed pre-tournament snapshot) de-vigged and compared to the model's live elimination distribution (100,000 MC, 20 results locked). Stages map 1:1 (Last 32→R32, Runner-Up→Final, Outright Winner→Champion). **Only teams yet to kick off are scored** — once a team plays, its pre-game line is stale vs a model that knows the result, so it drops out. As the tournament runs the clean set shrinks; right now it is **7 teams** (Tunisia, Ghana, Uzbekistan, Croatia, England, Panama, Colombia).*

## Headline: the model is more *diffuse* than the market

Across clean teams the model pushes probability into the **tails** more than DraftKings does. That manufactures a long list of nominal '+EV' bets that mostly reflect the model being **less sharp than a sharp book**, not real value:

- **Model > market on early exits for favourites** (under-confidence in favourites): Colombia exit-group 28% vs 13%, England exit-R32 31% vs 21%.
- **Model < market on the modal exit for minnows** (over-rating weak sides): Tunisia group-exit 67% vs 86%, Uzbekistan 56% vs 67%.

Both are the model's known miscalibration (see RESULTS_TRACKER.md), so the exact-stage exotics are noise, not edge.

## Cleanest signal — model vs market 'to qualify' (reach Last 32+)

*Reliable shallow output; +edge = model more bullish on advancing. **A large +pp on a weak side (Tunisia, Uzbekistan) is the model over-rating minnows — a fade, not a bet.** Genuine edge needs an under-covered but genuinely strong side (Ghana). Sort sign alone does not pick a bet.*

| Team | Grp | Model qualify | Market (de-vig) | Edge (pp) |
|---|:--:|--:|--:|--:|
| Tunisia | F | 33% | 14% | +19 |
| Ghana | L | 69% | 54% | +15 |
| Uzbekistan | K | 44% | 33% | +11 |
| Croatia | L | 78% | 80% | -2 |
| England | L | 93% | 96% | -3 |
| Panama | L | 29% | 34% | -5 |
| Colombia | K | 72% | 87% | -14 |

## Credible edges (under-covered side advances further — the CIV thesis)

| Bet | Model | Market (de-vig) | Price | Read |
|---|--:|--:|---|---|
| **Ghana to reach R16+** (qualify) | 69% qualify | ~54% | R16-exit +800 | African side, model +15pp on advancing — Ivory Coast profile; still unplayed |

**DR Congo — edge now partially realized, dropped from the clean screen.** The other half of this thesis has kicked off: DR Congo held Portugal 1-1 (06-17), and the model's qualify jumped to ~67% (vs the pre-game DK line ~46%). Because their line is now stale they no longer appear above; the live bet is tracked in `MODEL_VS_DRAFTKINGS.md`.

Cleanest expression is the **to-qualify / reach-Last-32+** market, not the exact-stage exotic. Ghana remains a thesis-test, not a lock.

## Fades (model miscalibration, not value)

- England **to exit early** (exit-group 7% vs 4%, exit-R32 31% vs 21%) — under-confidence in the lone clean favourite.
- Tunisia / Uzbekistan **to advance** — over-rating minnows; thin/backfilled Elo.

## Full +EV screen (clean teams, Group/R32/R16/QF only)

*Listed for completeness — treat as model diffuseness unless it also fits the under-covered-strong-side read above.*

| Team | Exit stage | Model | Market (dv) | Price | EV/$1 |
|---|:--:|--:|--:|---|--:|
| Tunisia | R16 | 7% | 3% | +3500 | +164% |
| Tunisia | R32 | 22% | 10% | +850 | +112% |
| Colombia | Group | 28% | 13% | +550 | +80% |
| Ghana | QF | 8% | 4% | +2000 | +72% |
| Tunisia | QF | 3% | 1% | +6500 | +67% |
| Uzbekistan | QF | 4% | 2% | +4000 | +64% |
| England | Group | 7% | 4% | +2000 | +55% |
| Ghana | R16 | 17% | 10% | +800 | +53% |
| Uzbekistan | R16 | 10% | 6% | +1400 | +48% |
| England | R32 | 31% | 21% | +320 | +31% |

## Caveats
- SF/Final/Champion edges excluded (knockout coin-flips + thin squads = noise).
- Teams that have already played are excluded (stale lines).
- 'Credible' edges are the thesis under test (n tiny); the market may simply know these squads are weaker than their rating.

*Reproduce: `python compare_elim.py` (reads `downloads/elim.txt`, live n=100000).*
