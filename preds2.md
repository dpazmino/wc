# 2026 FIFA World Cup — Forecast (v2, improved model)

*Generated 2026-06-13. Strength model with the re-validated calibration (shrink **0.25**) and corrected draw rate (**DRAW_BASE 0.45**), over **100,000** Monte-Carlo simulations of the real 48-team draw using the **official 2026 knockout bracket**. Host nations (USA/Mexico/Canada) get home advantage in group games; knockout ties are strength-weighted coin flips.*

## 🏆 Title odds (top 18)

| # | Team | Grp | Win group | Qualify | Reach final | **Title** | ±95% |
|---|------|:--:|:--:|:--:|:--:|:--:|:--:|
| 1 | England | L | 55% | 93% | 16% | **9.2%** | ±0.2 |
| 2 | France | I | 53% | 91% | 15% | **8.7%** | ±0.2 |
| 3 | Germany | E | 57% | 92% | 14% | **8.5%** | ±0.2 |
| 4 | Portugal | K | 54% | 91% | 13% | **7.5%** | ±0.2 |
| 5 | Argentina | J | 52% | 91% | 12% | **7.1%** | ±0.2 |
| 6 | Spain | H | 52% | 91% | 12% | **6.9%** | ±0.2 |
| 7 | Brazil | C | 50% | 89% | 11% | **6.1%** | ±0.1 |
| 8 | Netherlands | F | 45% | 88% | 10% | **5.6%** | ±0.1 |
| 9 | Belgium | G | 55% | 92% | 10% | **5.2%** | ±0.1 |
| 10 | Uruguay | H | 32% | 82% | 6% | **2.8%** | ±0.1 |
| 11 | Switzerland | B | 39% | 82% | 6% | **2.8%** | ±0.1 |
| 12 | Norway | I | 24% | 76% | 5% | **2.3%** | ±0.1 |
| 13 | Croatia | L | 24% | 77% | 5% | **2.1%** | ±0.1 |
| 14 | Sweden | F | 27% | 77% | 5% | **2.0%** | ±0.1 |
| 15 | Austria | J | 24% | 75% | 4% | **1.8%** | ±0.1 |
| 16 | Ivory Coast | E | 23% | 74% | 4% | **1.7%** | ±0.1 |
| 17 | Colombia | K | 23% | 72% | 4% | **1.6%** | ±0.1 |
| 18 | Turkey | D | 30% | 77% | 4% | **1.6%** | ±0.1 |

## Favourites' bracket (chalk on the official template)

**Group winners (by strength, incl. host advantage):** Mexico, Switzerland, Brazil, USA, Germany, Netherlands, Belgium, Spain, France, Argentina, Portugal, England.

```mermaid
flowchart LR
  classDef champ fill:#ffd700,stroke:#b8860b,stroke-width:3px,color:#000;
  subgraph R0["Round of 16"]
    direction TB
    r0_Germany["Germany"]
    r0_France["France"]
    r0_Czechia["Czechia"]
    r0_Netherlands["Netherlands"]
    r0_Brazil["Brazil"]
    r0_Norway["Norway"]
    r0_Japan["Japan"]
    r0_England["England"]
    r0_Croatia["Croatia"]
    r0_Spain["Spain"]
    r0_Algeria["Algeria"]
    r0_Belgium["Belgium"]
    r0_Argentina["Argentina"]
    r0_Turkey["Turkey"]
    r0_Switzerland["Switzerland"]
    r0_Portugal["Portugal"]
  end
  subgraph R1["Quarter-finals"]
    direction TB
    r1_France["France"]
    r1_Netherlands["Netherlands"]
    r1_Spain["Spain"]
    r1_Belgium["Belgium"]
    r1_Brazil["Brazil"]
    r1_England["England"]
    r1_Argentina["Argentina"]
    r1_Portugal["Portugal"]
  end
  subgraph R2["Semi-finals"]
    direction TB
    r2_France["France"]
    r2_Spain["Spain"]
    r2_England["England"]
    r2_Portugal["Portugal"]
  end
  subgraph R3["Final"]
    direction TB
    r3_France["France"]
    r3_England["England"]
  end
  subgraph RC["Champion"]
    champ["🏆 England"]
  end
  r0_Germany --> r1_France
  r0_France --> r1_France
  r0_Czechia --> r1_Netherlands
  r0_Netherlands --> r1_Netherlands
  r0_Brazil --> r1_Brazil
  r0_Norway --> r1_Brazil
  r0_Japan --> r1_England
  r0_England --> r1_England
  r0_Croatia --> r1_Spain
  r0_Spain --> r1_Spain
  r0_Algeria --> r1_Belgium
  r0_Belgium --> r1_Belgium
  r0_Argentina --> r1_Argentina
  r0_Turkey --> r1_Argentina
  r0_Switzerland --> r1_Portugal
  r0_Portugal --> r1_Portugal
  r1_France --> r2_France
  r1_Netherlands --> r2_France
  r1_Spain --> r2_Spain
  r1_Belgium --> r2_Spain
  r1_Brazil --> r2_England
  r1_England --> r2_England
  r1_Argentina --> r2_Portugal
  r1_Portugal --> r2_Portugal
  r2_France --> r3_France
  r2_Spain --> r3_France
  r2_England --> r3_England
  r2_Portugal --> r3_England
  r3_France --> champ
  r3_England --> champ
  class champ champ;
```

**Champion (chalk): England.**

## Caveats
- Title odds are the forecast; the chalk bracket is the single most likely path (its exact probability of occurring is tiny — real tournaments are upset-heavy).
- Knockout now uses the **official 2026 bracket template** (group-position R32 pairings + real tree); best-thirds are matched to FIFA-allocated slots.
- Draw rate is calibrated to ~25% (from ~22%); a residual ~2.6pp under-prediction remains, left in place so home advantage still helps underdogs.
- ~11 backfilled teams use real squads with **estimated** overalls; Elo self-corrects as results are logged.

*Reproduce: `python tournament.py -n 100000`*
