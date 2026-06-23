# Prospective Bet Tracker — model picks vs DraftKings

*Updated 2026-06-23. Flat 1-unit stakes; draw = loss (3-way moneyline). Picks + prices locked before kickoff. Three strategies: **all** picks · **rule** (DK price −127 or longer, BE ≤ 56%) · **model_ev** (model prob > break-even). PnL in units.*

## Running record

| Strategy | Bets | Record | Net (u) | ROI | Win% | Avg BE% | Pending |
|---|--:|:--:|--:|--:|--:|--:|--:|
| all | 5 | 5-0 | +3.02 | +60.4% | 100% | 66% | 28 |
| rule (≤−127) | 1 | 1-0 | +1.25 | +125.0% | 100% | 44% | 12 |
| model_ev | 0 | 0-0 | +0.00 | +0.0% | 0% | 0% | 4 |

## Graded (5)

| Kickoff | Match | Pick | DK | BE% | Model% | EV | Rule | Result | PnL |
|---|---|---|--:|--:|--:|--:|:--:|:--:|--:|
| 1st Half4:56 | New Zealand v Egypt | Egypt | -165 | 62 | 58 | -8% |  | ✅ | 0.606 |
| Tomorrow 1:00 PM | Argentina v Austria | Argentina | -190 | 66 | 51 | -22% |  | ✅ | 0.526 |
| Tomorrow 5:00 PM | France v Iraq | France | -1200 | 92 | 70 | -24% |  | ✅ | 0.083 |
| Tomorrow 8:00 PM | Norway v Senegal | Norway | +125 | 44 | 43 | -3% | ✓ | ✅ | 1.250 |
| Tomorrow 11:00 PM | Jordan v Algeria | Algeria | -180 | 64 | 54 | -16% |  | ✅ | 0.556 |

## Pending (28)

| Kickoff | Match | Pick | DK | BE% | Model% | EV | Rule | Result | PnL |
|---|---|---|--:|--:|--:|--:|:--:|:--:|--:|
| Tue Jun 23rd 1:00 PM | Portugal v Uzbekistan | Portugal | -500 | 83 | 66 | -21% |  | · |  |
| Tue Jun 23rd 4:00 PM | England v Ghana | England | -450 | 82 | 60 | -26% |  | · |  |
| Tue Jun 23rd 7:00 PM | Panama v Croatia | Croatia | -185 | 65 | 63 | -2% |  | · |  |
| Tue Jun 23rd 10:00 PM | Colombia v DR Congo | Colombia | -195 | 66 | 43 | -35% |  | · |  |
| Wed Jun 24th 3:00 PM | Switzerland v Canada | Switzerland | +145 | 41 | 41 | -1% | ✓ | · |  |
| Wed Jun 24th 3:00 PM | Bosnia and Herzegovina v Qatar | Bosnia and Herzegovina | -230 | 70 | 44 | -37% |  | · |  |
| Wed Jun 24th 6:00 PM | Scotland v Brazil | Brazil | -245 | 71 | 55 | -23% |  | · |  |
| Wed Jun 24th 6:00 PM | Morocco v Haiti | Morocco | -525 | 84 | 54 | -36% |  | · |  |
| Wed Jun 24th 9:00 PM | Czechia v Mexico | Mexico | -105 | 51 | 43 | -16% | ✓ | · |  |
| Wed Jun 24th 9:00 PM | South Africa v South Korea | South Korea | -160 | 62 | 39 | -37% |  | · |  |
| Thu Jun 25th 4:00 PM | Ecuador v Germany | Germany | -105 | 51 | 65 | +26% | ✓ | · |  |
| Thu Jun 25th 4:00 PM | Curacao v Ivory Coast | Ivory Coast | -650 | 87 | 54 | -38% |  | · |  |
| Thu Jun 25th 7:00 PM | Tunisia v Netherlands | Netherlands | -750 | 88 | 68 | -23% |  | · |  |
| Thu Jun 25th 7:00 PM | Japan v Sweden | Sweden | +320 | 24 | 39 | +62% | ✓ | · |  |
| Thu Jun 25th 10:00 PM | Turkey v USA | USA | +100 | 50 | 45 | -10% | ✓ | · |  |
| Thu Jun 25th 10:00 PM | Paraguay v Australia | Paraguay | +190 | 34 | 45 | +31% | ✓ | · |  |
| Fri Jun 26th 3:00 PM | Norway v France | France | -125 | 56 | 53 | -5% | ✓ | · |  |
| Fri Jun 26th 3:00 PM | Senegal v Iraq | Senegal | -330 | 77 | 53 | -31% |  | · |  |
| Fri Jun 26th 8:00 PM | Uruguay v Spain | Spain | -195 | 66 | 46 | -30% |  | · |  |
| Fri Jun 26th 8:00 PM | Cape Verde v Saudi Arabia | Cape Verde | +130 | 43 | 38 | -12% | ✓ | · |  |
| Fri Jun 26th 11:00 PM | New Zealand v Belgium | Belgium | -450 | 82 | 69 | -16% |  | · |  |
| Fri Jun 26th 11:00 PM | Egypt v Iran | Egypt | +125 | 44 | 41 | -7% | ✓ | · |  |
| Sat Jun 27th 5:00 PM | Panama v England | England | -425 | 81 | 74 | -9% |  | · |  |
| Sat Jun 27th 5:00 PM | Croatia v Ghana | Croatia | -160 | 62 | 40 | -35% |  | · |  |
| Sat Jun 27th 7:30 PM | Colombia v Portugal | Portugal | +105 | 49 | 49 | -0% | ✓ | · |  |
| Sat Jun 27th 7:30 PM | DR Congo v Uzbekistan | DR Congo | +110 | 48 | 43 | -9% | ✓ | · |  |
| Sat Jun 27th 10:00 PM | Jordan v Argentina | Argentina | -525 | 84 | 69 | -18% |  | · |  |
| Sat Jun 27th 10:00 PM | Algeria v Austria | Austria | +155 | 39 | 41 | +4% | ✓ | · |  |

*Reproduce: `python bet_tracker.py` (reads downloads/odds.txt + data/results.csv; ledger in data/bets.csv).*
