# I Built a World Cup Predictor in a Weekend. Here's the Honest Scorecard.

*What I learned trying to forecast the 2026 World Cup — including the part where the betting market quietly beat me.*

---

I didn't set out to build a crystal ball. I set out to answer a smaller, more annoying question: **how much of "predicting football" is actually just knowing which team is better?**

It turns out the answer is *almost all of it* — and getting to that answer taught me more than any clever model ever could. This is the story of what I built, how fast it came together, and how it's actually performing now that the 2026 World Cup is underway. The good calls, the embarrassing misses, and the one result that flipped my whole thesis on its head.

Every number below is reproducible from the code and the results file in the repo. No cherry-picking — the trackers log the misses by construction.

---

## The version I almost shipped (and why I'm glad I didn't)

My first instinct was the fun, complicated one: simulate the match. I built a whole multi-agent engine where LLM "players" make decisions minute by minute — a striker decides to shoot, a center-back decides to step up, a referee hands out cards, a commentator narrates the whole thing. Twenty-two agents, a physics-based resolution engine, the works. It's genuinely cool to watch.

Then I did the boring, important thing: I checked whether any of it actually *helped me predict the result*.

It didn't. Not a little — at all. When I ran walk-forward cross-validation (scoring each game using only what was knowable *before* kickoff), the optimal weight on the entire simulation was essentially **zero**. A pure team-strength number predicted just as well as the elaborate 22-agent match engine.

So I made the most important decision of the project: **I ripped simulation out of the prediction path entirely.** The predictor became instant and analytic — no Monte Carlo for a single game, no LLM, no per-match hand-tuning. The fancy simulator still exists, but only as a *storytelling* engine for generating match narratives. For actually forecasting? Strength is king.

That's the lesson I keep coming back to: **the hard part of building something isn't adding capability. It's having the discipline to delete the parts that feel impressive but don't work.**

---

## What the predictor actually is

Stripped down, it's three ideas stacked on top of each other:

1. **A dynamic Elo rating that learns from results.** I seeded it with about 250 historical internationals, and every 2026 result nudges the ratings (weighted by goal difference, with home advantage and a recency decay so stale form fades).

2. **A squad-strength prior.** Each team's "true" rating is anchored to the quality of its best XI, using FIFA-scale player ratings. This matters enormously for teams we have little match data on — they lean on squad quality until real results accumulate. (Think of it as "regularized Elo.")

3. **Honest calibration.** I shrink the probabilities toward the base rate by a factor I tuned with cross-validation, then derive expected goals and scorelines from a simple Poisson model on the rating gap.

That's it. No neural network. No 200-feature pipeline. A read on who's stronger, learning as the tournament goes. The entire prediction is three lines:

```python
from match_engine.elo import default_model

# Builds the ratings from ~250 historical results + every 2026 game so far.
model = default_model()

# Win / draw / loss for a single match — instant, no simulation, no API call.
p_home, p_draw, p_away = model.strength_probs("Brazil", "France", neutral=True)
#  →  (0.28, 0.35, 0.37)   a near-coin-flip the model is honest about
```

No Monte Carlo, no LLM, no per-game tuning — just a regularized Elo lookup. That speed is the whole point: I can forecast every remaining fixture, or roll the entire tournament forward 100,000 times for title odds, in seconds.

Before I let it touch a single 2026 game, I validated it on 294 historical fixtures. The headline: it beat a naive baseline (RPS 0.205 vs 0.231), and — the part I actually cared about — the **cross-validated optimism was 0.001.** In plain English: the edge was real, not me fooling myself by overfitting. That number was my permission slip to take everything that followed seriously.

---

## How it's doing now: 55 games in

The World Cup group stage is the first time the model has faced genuinely unseen games, in public, with no chance to fudge anything after the fact. Here's the live scorecard.

| Metric (55 games, walk-forward) | Model | Naive baseline |
|---|--:|--:|
| Top-pick accuracy | **63%** (37/59) | — |
| Accuracy on decisive games | **86%** (37/43) | — |
| Brier score (lower is better) | **0.546** | 0.667 |
| Log-loss | **0.93** | — |
| Pre-tournament validation (294 games, RPS) | **0.205** | 0.231 |

*Walk-forward means every prediction was made using only data available before that game — the model never saw its own result.*

**It picks winners well.** Top-pick accuracy is **63% (37 of 59)**, and its Brier score (0.546) is comfortably ahead of the naive baseline (0.667). On games that actually had a winner, it's *excellent* — **86% recall** on both home and away wins. Counting only decisive games, it went **37 of 43**, and it almost never confused a home win for an away win. As a "which side wins" engine, it's genuinely strong.

**It is, charmingly, too humble.** This is my favorite finding. When the model says its pick has, say, a 40–45% chance to win, those picks actually win **67%** of the time. Across the board, its favorites win about **10 percentage points more often than it claims.** The model systematically *undervalues its own picks.* It's a forecaster with impostor syndrome.

**It is honest about what it doesn't know.** Argentina, England, France, and Germany have sat within half a percent of each other for the title for a week. The "leader" reshuffles on Monte-Carlo noise. The model refuses to pretend the top of the field is anything but a coin flip — which is correct, even if it isn't a bold headline.

---

## The call I'm proud of

A model that just echoes the betting market is worthless — the only place you can possibly have an edge is where you *disagree* with it. So I went hunting for a structural disagreement, and I found a candidate: US betting markets over-weight familiar, glamorous teams and **under-cover strong-but-unfashionable African and Asian squads** stacked with players from top European leagues. My model, which only sees squad strength, should be more bullish on exactly those teams — and right to be.

It played out almost exactly as the thesis predicted. The model was more confident than the market on **Ghana, Ivory Coast, and Algeria** to advance — and all three came through. The signature call: **Ghana, which the market priced at a 54% chance to qualify, clinched it by holding England to a 0-0 draw.** The under-covered-side thesis went roughly 4-for-5.

That felt great. And then the data made me be careful about *why* it felt great.

---

## The result that humbled me

Here's the part most people would quietly leave out. I'm putting it in the headline of the lesson instead, because it's the most interesting thing I learned.

The edge I found was real — but it lived in the **"will this team advance" market**, a season-long, reputation-driven read. It was emphatically **not** a game-by-game edge. And I can prove the difference, because I logged every single bet with its real DraftKings price *before kickoff.*

My disciplined betting filter — "only bet when the model's probability beats the price's break-even point," the rule an actual sharp bettor would use — is **0 for 3.** Every single time the model was confident enough to *disagree with the market on a specific game*, the market was right. Germany (a dead rubber the model badly misread), Sweden (drew), Paraguay (drew). Three swings, three misses.

The only betting strategy that's in the black is "blindly back every model pick," and that's just a coarse ride on the under-confidence I mentioned earlier — and it's regressing toward break-even as I write this.

| Betting strategy (every pick logged pre-kickoff) | Record | ROI |
|---|:--:|--:|
| Back every model pick | 15–6 | +9.5% |
| Bet the "−127 or longer" rule | 3–4 | −5% |
| Disciplined "value" filter (model prob > break-even) | **0–3** | **−100%** |

*The one positive line is the undisciplined one. Every time the model was confident enough to disagree with the sharp price, it lost.*

So the real, defensible conclusion is this: **a transparent strength model — even a well-calibrated one that beats a baseline and finds a structural market edge — does not have a game-level edge over a sharp betting market.** Where we disagreed on a single match, the book won. That's not the clickbait version. It's the true one, and I have the timestamped tickets to back it up.

---

## Where it falls on its face

For completeness, the misses, because a scorecard that only shows wins isn't a scorecard:

- **Draws are its blind spot.** The model assigns draws about 22%, but the group stage ran closer to 25–30%. It almost always picks a side, so most of its losses are "the favorite controlled the game and drew anyway." Sixteen of 59 games were draws — that's the single biggest drag on its score.
- **It has no concept of "nothing to play for."** Germany, already qualified, rotated its squad and lost 2-1 to a motivated Ecuador. The model rated Germany on its full-strength XI and walked right into it. The market's lower number had correctly priced the rotation; my model can't even *see* the situation.

---

## What I'd actually tell you

If you take one thing from this, don't let it be a betting tip. Let it be the shape of the project:

**Build the simplest thing that could possibly work. Validate it honestly, out-of-sample, before you trust a word of it. Then keep score in public, misses included.**

The flashy 22-agent simulator was a dead end for prediction, and the unglamorous "who's stronger" number quietly did all the real work. The model is a strong winner-picker, it's endearingly under-confident, it found a genuine edge on under-covered teams — and it cannot beat a sharp bookmaker game to game. All of those things are true at once, and the only reason I can say them with a straight face is that I wrote down every prediction before I knew the result.

The knockouts are next. The format turns binary — advance or go home, penalties always crown a winner — and that should actually *flatter* the model, because its worst enemy, the draw, stops counting against it. A 1-1 that the favorite wins on penalties becomes a hit instead of a miss.

I'll keep score. Honestly. Whichever way it goes.

---

*Everything in this piece — the predictions, the calibration curves, the betting ledger with its pre-kickoff prices — is checked into the repo and regenerates from a one-line command. The trackers include the misses by design, because a scorecard you can edit after the fact isn't a scorecard.*
