# Coach-vs-Coach Tactical Matchups — Round of 32

*How each pair of coaches' **styles** clash, scored from the tactical profiles in `team_tactics.py` / `coach_prompts.py` (transparent keyword counts on five axes: press height, directness, width, counter focus, set-piece threat).*

> ⚠ **Descriptive, not predictive.** This is a tactical lens for the narrative simulation — it explains *how* a game might be fought, not who wins. The full sim models all of this and adds ~0 over scalar team strength (`docs/GAP_ANALYSIS.md`), and unit style-matchups showed no out-of-sample edge (`player_match/`). For who advances, use `predict.py` / `docs/predictions_r32.md`.

### South Africa vs Canada
- **South Africa** (South Africa's manager): low block, direct / vertical, wide / crossing, counter-attacking, set-piece threat
- **Canada** (Jesse Marsch): high press, direct / vertical, wide / crossing, counter-attacking, set-piece threat
- **Tactical clash:**
  - **South Africa plays direct into Canada's high line** — balls in behind can turn Canada's aggression into space for South Africa to attack.
  - **Canada's high press vs South Africa's low block** — Canada owns territory and pins South Africa back; South Africa looks to spring out. Whether Canada can break a packed block is the question.
  - **Canada's counter vs South Africa's low block** — South Africa sits and absorbs; Canada needs the transition moment, or it's a patience game.

### Brazil vs Japan
- **Brazil** (Brazil's manager): high press, possession / patient, wide / crossing, counter-attacking, balanced setpiece
- **Japan** (Hajime Moriyasu): low block, direct / vertical, wide / crossing, counter-attacking, set-piece threat
- **Tactical clash:**
  - **Brazil's high press vs Japan's low block** — Brazil owns territory and pins Japan back; Japan looks to spring out. Whether Brazil can break a packed block is the question.
  - **Brazil's counter vs Japan's low block** — Japan sits and absorbs; Brazil needs the transition moment, or it's a patience game.
  - **Japan plays direct into Brazil's high line** — balls in behind can turn Brazil's aggression into space for Japan to attack.
  - **Japan's set-piece threat** could be the separator — a clear dead-ball edge over Brazil.

### Germany vs Paraguay
- **Germany** (Julian Nagelsmann): high press, direct / vertical, wide / crossing, counter-attacking, set-piece threat
- **Paraguay** (Gustavo Alfaro): low block, direct / vertical, wide / crossing, counter-attacking, set-piece threat
- **Tactical clash:**
  - **Germany's high press vs Paraguay's low block** — Germany owns territory and pins Paraguay back; Paraguay looks to spring out. Whether Germany can break a packed block is the question.
  - **Germany's counter vs Paraguay's low block** — Paraguay sits and absorbs; Germany needs the transition moment, or it's a patience game.
  - **Paraguay plays direct into Germany's high line** — balls in behind can turn Germany's aggression into space for Paraguay to attack.

### Netherlands vs Morocco
- **Netherlands** (Ronald Koeman): high press, balanced direct, wide / crossing, balanced counter, set-piece threat
- **Morocco** (Walid Regragui): low block, balanced direct, wide / crossing, counter-attacking, set-piece threat
- **Tactical clash:**
  - **Netherlands's high press vs Morocco's low block** — Netherlands owns territory and pins Morocco back; Morocco looks to spring out. Whether Netherlands can break a packed block is the question.

### Ivory Coast vs Norway
- **Ivory Coast** (Ivory Coast's manager): balanced press, direct / vertical, wide / crossing, balanced counter, set-piece threat
- **Norway** (Stale Solbakken): low block, direct / vertical, wide / crossing, counter-attacking, set-piece threat
- **Tactical clash:** styles are broadly compatible — no sharp stylistic mismatch; likely decided on quality, not shape.

### France vs Sweden
- **France** (Didier Deschamps): low block, direct / vertical, wide / crossing, counter-attacking, set-piece threat
- **Sweden** (Graham Potter): low block, direct / vertical, wide / crossing, counter-attacking, set-piece threat
- **Tactical clash:**
  - **France's counter vs Sweden's low block** — Sweden sits and absorbs; France needs the transition moment, or it's a patience game.
  - **Sweden's counter vs France's low block** — France sits and absorbs; Sweden needs the transition moment, or it's a patience game.
  - **Two low blocks** — likely cagey and low-scoring; whoever blinks first (or wins a set piece) may decide it.

### USA vs Bosnia and Herzegovina
- **USA** (Mauricio Pochettino): balanced press, balanced direct, wide / crossing, counter-attacking, set-piece threat
- **Bosnia and Herzegovina** (Sergej Barbarez): low block, possession / patient, wide / crossing, balanced counter, set-piece threat
- **Tactical clash:**
  - **USA's counter vs Bosnia and Herzegovina's low block** — Bosnia and Herzegovina sits and absorbs; USA needs the transition moment, or it's a patience game.

### Australia vs Egypt
- **Australia** (Australia's manager): low block, direct / vertical, wide / crossing, counter-attacking, set-piece threat
- **Egypt** (Egypt's manager): balanced press, direct / vertical, balanced width, counter-attacking, set-piece threat
- **Tactical clash:**
  - **Egypt's counter vs Australia's low block** — Australia sits and absorbs; Egypt needs the transition moment, or it's a patience game.

### Argentina vs Cape Verde
- **Argentina** (Lionel Scaloni): high press, possession / patient, wide / crossing, balanced counter, set-piece threat
- **Cape Verde** (Bubista): low block, balanced direct, wide / crossing, counter-attacking, set-piece threat
- **Tactical clash:**
  - **Argentina's high press vs Cape Verde's low block** — Argentina owns territory and pins Cape Verde back; Cape Verde looks to spring out. Whether Argentina can break a packed block is the question.

*Reproduce: `python coach_matchup.py` (or `python coach_matchup.py TeamA TeamB` for one pairing).*
