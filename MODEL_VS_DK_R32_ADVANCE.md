# Model vs DraftKings — R32 To-Qualify (2-way advance) · 2026-06-29

*Pure strength model (shrink 0.25, **un-anchored**) P(advance) = P(win)+½·P(draw) vs the de-vigged DraftKings 2-way "To Qualify" market. Host nations (USA/Mexico/Canada) get Elo home advantage. EV = model P(advance) × raw DK decimal price − 1 (the price still carries vig, so +EV must clear the margin). Edge can only live where the model and market disagree on **who advances** — not in the across-the-board underdog +EV below, which is the model's diffuseness.*

| Match | Kickoff (ET) | Model adv% (H/A) | DK adv% (H/A) | Fav: model / DK |
|---|---|---|---|---|
| Germany vs Paraguay | Today 4:30 PM | 73/27 | 84/16 | Germany / Germany | |
| Netherlands vs Morocco | Today 9:00 PM | 60/40 | 58/42 | Netherlands / Netherlands | |
| Ivory Coast vs Norway | Tomorrow 1:00 PM | 48/52 | 39/61 | Norway / Norway | |
| France vs Sweden | Tomorrow 5:00 PM | 65/35 | 86/14 | France / France | |
| Mexico vs Ecuador (host Mexico) | Tomorrow 9:00 PM | 59/41 | 61/39 | Mexico / Mexico | |
| England vs DR Congo | Wed Jul 1st 12:00 PM | 72/28 | 86/14 | England / England | |
| Belgium vs Senegal | Wed Jul 1st 4:00 PM | 61/39 | 60/40 | Belgium / Belgium | |
| USA vs Bosnia and Herzegovina (host USA) | Wed Jul 1st 8:00 PM | 62/38 | 84/16 | USA / USA | |
| Spain vs Austria | Thu Jul 2nd 3:00 PM | 63/37 | 86/14 | Spain / Spain | |
| Portugal vs Croatia | Thu Jul 2nd 7:00 PM | 60/40 | 69/31 | Portugal / Portugal | |
| Switzerland vs Algeria | Thu Jul 2nd 11:00 PM | 57/43 | 64/36 | Switzerland / Switzerland | |
| Australia vs Egypt | Fri Jul 3rd 2:00 PM | 40/60 | 44/56 | Egypt / Egypt | |
| Argentina vs Cape Verde | Fri Jul 3rd 6:00 PM | 74/26 | 91/9 | Argentina / Argentina | |
| Colombia vs Ghana | Fri Jul 3rd 9:30 PM | 55/45 | 77/23 | Colombia / Colombia | |

## Edge candidates (favourite disagreements)

_None — the model and DK agree on the advancer in all 14/14 ties. The model mirrors the sharp line, so there is **no clean advance-market edge** this round._

## Model–market gap (calibration artifact, NOT edge)

The model assigns the **underdog** more advance equity than the sharp market in every tie below, producing nominal +EV on plus-money longshots. This is the model's known diffuseness (its knockout distribution treats level ties as coin-flips and is flatter than the market) — the same miscalibration as `MODEL_VS_DK_ELIMINATION.md`. Listed for transparency, **not as bets:**

- Germany vs Paraguay: model Germany 73% / Paraguay 27% vs DK Germany 84% / Paraguay 16% → underdog Paraguay nominal EV +62% at +500.
- Ivory Coast vs Norway: model Ivory Coast 48% / Norway 52% vs DK Ivory Coast 39% / Norway 61% → underdog Ivory Coast nominal EV +16% at +145.
- France vs Sweden: model France 65% / Sweden 35% vs DK France 86% / Sweden 14% → underdog Sweden nominal EV +127% at +550.
- England vs DR Congo: model England 72% / DR Congo 28% vs DK England 86% / DR Congo 14% → underdog DR Congo nominal EV +81% at +550.
- USA vs Bosnia and Herzegovina: model USA 62% / Bosnia and Herzegovina 38% vs DK USA 84% / Bosnia and Herzegovina 16% → underdog Bosnia and Herzegovina nominal EV +116% at +475.
- Spain vs Austria: model Spain 63% / Austria 37% vs DK Spain 86% / Austria 14% → underdog Austria nominal EV +143% at +550.
- Portugal vs Croatia: model Portugal 60% / Croatia 40% vs DK Portugal 69% / Croatia 31% → underdog Croatia nominal EV +24% at +210.
- Switzerland vs Algeria: model Switzerland 57% / Algeria 43% vs DK Switzerland 64% / Algeria 36% → underdog Algeria nominal EV +11% at +160.
- Argentina vs Cape Verde: model Argentina 74% / Cape Verde 26% vs DK Argentina 91% / Cape Verde 9% → underdog Cape Verde nominal EV +170% at +950.
- Colombia vs Ghana: model Colombia 55% / Ghana 45% vs DK Colombia 77% / Ghana 23% → underdog Ghana nominal EV +90% at +320.

*Grade on ADVANCEMENT, not 90-minute W/D/L. A favourite that wins on penalties after a level 90' is a hit.*
