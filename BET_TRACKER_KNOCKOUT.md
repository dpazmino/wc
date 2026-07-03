# Knockout Bet Tracker — model advance-picks vs DraftKings

*Updated 2026-07-03. Flat 1-unit ($100) stakes on the **2-way "To Qualify" market** (no draw
— a level 90' resolves on penalties, and the shootout winner counts). Picks + de-vigged DK
prices from `~/Downloads/advance.txt`; model P(advance) = P(win) + ½·P(draw), un-anchored,
hosts get Elo HFA. Companion to the group-stage `BET_TRACKER.md` (3-way moneyline). Grade is
on **advancement**, not the 90-minute score.*

## R32 running record (11 of 14 ties decided)

| Strategy | Bets | Record | Net (u) | Net ($) | ROI |
|---|--:|:--:|--:|--:|--:|
| **Back the favourite to advance** | 11 | 9-2 | **+0.94** | **+$94** | **+8.6%** |
| Model's "value" underdog (the *don't-bet* list) | 8 | 1-7 | −2.00 | −$200 | −25.0% |

*No third strategy existed: the model and DK agreed on the advancer in **all 14/14 ties**, so
there was **no favourite-disagreement edge** to exploit this round (see
`MODEL_VS_DK_R32_ADVANCE.md`).*

## Why "back the favourite" was fragile despite the profit

Nine correct picks netted +$294; the **two upsets — Germany (−900) and Netherlands (−160),
both lost on penalties — cost −$200.** The heavy favourites (France, England, Spain all at
−1000) pay just **10¢ on the dollar**, so you lay ~$9 to win $1 on the chalk. One more
favourite stumble in the three pending ties (Argentina is −2500) would flip the ROI negative.
Positive here, but on variance, not a durable edge.

## Why the "value" underdogs bled — as the comparison doc warned

`MODEL_VS_DK_R32_ADVANCE.md` listed these underdog +EVs "for transparency, **not as bets**" —
they're the model's **diffuseness** (it treats knockout ties closer to coin-flips than the
sharp market does, manufacturing fake +EV on longshots). Result: 1-7. The single hit
(**Paraguay +500**, +$500) masks it — strip that lucky longshot and it's 0-7, −$700.

## Graded ties (11)

| Kickoff (ET) | Tie | DK fav | Fav price | Advancer | Fav bet | Value-dog bet |
|---|---|---|--:|---|:--:|:--:|
| Mon Jun 29 4:30 | Germany v Paraguay | Germany | −900 | **Paraguay** (pens) | ❌ −1.00 | ✅ Paraguay +500 → +5.00 |
| Mon Jun 29 9:00 | Netherlands v Morocco | Netherlands | −160 | **Morocco** (pens) | ❌ −1.00 | — (no model +EV) |
| Tue Jun 30 1:00 | Ivory Coast v Norway | Norway | −185 | **Norway** | ✅ +0.54 | ❌ Ivory Coast +145 → −1.00 |
| Tue Jun 30 5:00 | France v Sweden | France | −1000 | **France** | ✅ +0.10 | ❌ Sweden +550 → −1.00 |
| Tue Jun 30 9:00 | Mexico v Ecuador | Mexico | −185 | **Mexico** | ✅ +0.54 | — (no model +EV) |
| Wed Jul 1 12:00 | England v DR Congo | England | −1000 | **England** | ✅ +0.10 | ❌ DR Congo +550 → −1.00 |
| Wed Jul 1 4:00 | Belgium v Senegal | Belgium | −175 | **Belgium** | ✅ +0.57 | — (no model +EV) |
| Wed Jul 1 8:00 | USA v Bosnia | USA | −750 | **USA** | ✅ +0.13 | ❌ Bosnia +475 → −1.00 |
| Thu Jul 2 3:00 | Spain v Austria | Spain | −1000 | **Spain** | ✅ +0.10 | ❌ Austria +550 → −1.00 |
| Thu Jul 2 7:00 | Portugal v Croatia | Portugal | −270 | **Portugal** | ✅ +0.37 | ❌ Croatia +210 → −1.00 |
| Thu Jul 2 11:00 | Switzerland v Algeria | Switzerland | −205 | **Switzerland** | ✅ +0.49 | ❌ Algeria +160 → −1.00 |

## Pending (3 — Fri Jul 3)

| Kickoff (ET) | Tie | DK fav | Fav price | Value-dog |
|---|---|---|--:|---|
| Fri Jul 3 2:00 | Australia v Egypt | Egypt | −150 | — (no model +EV on Australia) |
| Fri Jul 3 6:00 | Argentina v Cape Verde | Argentina | −2500 | Cape Verde +950 |
| Fri Jul 3 9:30 | Colombia v Ghana | Colombia | −450 | Ghana +320 |

## Bottom line (both rounds)

The group-stage `BET_TRACKER.md` and this knockout tracker land in the same place:
**betting favourites** squeaks out a small profit on variance (+6% group, +8.6% knockout) at
brutal prices, while **betting the model's disagreements with the market** loses consistently
(group `model_ev` −100%, `turtle` −32%; knockout value-dogs −25%). The model mirrors the sharp
DraftKings line too closely to beat it, and where it deviates (longshots) it's wrong — so
**there was no systematic edge to harvest.** The one honest edge case — model and DK picking
*different* advancers — **never occurred** in the R32.

*Reproduce: read `~/Downloads/advance.txt` + `data/results.csv`; favourite/underdog prices per
tie above. Grade on advancement (a favourite winning on penalties is a hit). Re-run after the
3 pending Jul 3 ties resolve.*
