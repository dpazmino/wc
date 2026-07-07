# Model vs DraftKings — R32 To-Qualify (2-way advance) · 2026-07-06

*Pure strength model (shrink 0.25, **un-anchored**) P(advance) = P(win)+½·P(draw) vs the de-vigged DraftKings 2-way "To Qualify" market. Host nations (USA/Mexico/Canada) get Elo home advantage. EV = model P(advance) × raw DK decimal price − 1 (the price still carries vig, so +EV must clear the margin). Edge can only live where the model and market disagree on **who advances** — not in the across-the-board underdog +EV below, which is the model's diffuseness.*

| Match | Kickoff (ET) | Model adv% (H/A) | DK adv% (H/A) | Fav: model / DK |
|---|---|---|---|---|
| Portugal vs Spain | Today 3:00 PM | 49/51 | 35/65 | Spain / Spain | |
| USA vs Belgium (host USA) | Today 8:00 PM | 47/53 | 54/46 | Belgium / USA |  **⚠ disagree** |
| Argentina vs Egypt | Tomorrow 12:00 PM | 69/31 | 83/17 | Argentina / Argentina | |
| Switzerland vs Colombia | Tomorrow 4:00 PM | 53/47 | 42/58 | Switzerland / Colombia |  **⚠ disagree** |
| France vs Morocco | Thu Jul 9th 4:00 PM | 65/35 | 76/24 | France / France | |
| Norway vs England | Sat Jul 11th 5:00 PM | 36/64 | 36/64 | England / England | |

## Edge candidates (favourite disagreements)

- **USA vs Belgium** — model backs **Belgium** to advance; DK backs the other side. Model USA 47% / Belgium 53% vs DK USA 54% / Belgium 46%. Bet Belgium at +105 (EV +10%).
- **Switzerland vs Colombia** — model backs **Switzerland** to advance; DK backs the other side. Model Switzerland 53% / Colombia 47% vs DK Switzerland 42% / Colombia 58%. Bet Switzerland at +125 (EV +19%).

## Model–market gap (calibration artifact, NOT edge)

The model assigns the **underdog** more advance equity than the sharp market in every tie below, producing nominal +EV on plus-money longshots. This is the model's known diffuseness (its knockout distribution treats level ties as coin-flips and is flatter than the market) — the same miscalibration as `MODEL_VS_DK_ELIMINATION.md`. Listed for transparency, **not as bets:**

- Portugal vs Spain: model Portugal 49% / Spain 51% vs DK Portugal 35% / Spain 65% → underdog Portugal nominal EV +34% at +175.
- Argentina vs Egypt: model Argentina 69% / Egypt 31% vs DK Argentina 83% / Egypt 17% → underdog Egypt nominal EV +71% at +450.
- France vs Morocco: model France 65% / Morocco 35% vs DK France 76% / Morocco 24% → underdog Morocco nominal EV +38% at +295.

*Grade on ADVANCEMENT, not 90-minute W/D/L. A favourite that wins on penalties after a level 90' is a hit.*
