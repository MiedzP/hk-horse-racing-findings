# Hong Kong horse racing: what we tested and what held up

## Key note
Nothing held up as a betting edge. Some tests were statistically significant, but in the wrong direction (draw bias on 2013–2020, tongue-tie changes, family stack version 1), or they did not reproduce (draw bias 1997–2005 failed on 2016–18; the 2016 walk-forward gain is one year of six on a reused window). Betting directly lost money, and not betting was the only choice the data supported.

## Summary
No variable, model, or betting rule beat the market's final win odds on data it wasn't tuned on.
The market is the strongest predictor we could build here. The closest candidates are a jockey
edge and late odds movement, and neither reaches a clear positive result.

## Data
- 1997–2005 results (gdaley/hkracing): ~6,300 races with ratings, weights, gear, sectional positions.
- 2008–09 season (frederickmau): ~730 races with jockey, draw, going, final odds.
- 2013–2020 results (jeffreymuller): ~6,300 races with draw, weights, jockey/trainer IDs, final odds, tip index.
- 2015–2017 results with full notebook features (~1,100 races).
- 2016–2018 odds snapshots (mexwell): ~1,500 races, odds captured 8–37 hours before the off.
- Raw datasets are not included here; they are third-party files under their own licences.

## Baselines
- The market's favourite wins 30–32% of the time at average odds of ~3.
- Backing the favourite loses 10–23% per unit in every dataset (all intervals below zero).
- The overround is about 1.23 per race, consistent with a 17.5% win takeout.

## What was tested (log-loss gain over the market, positive = better; 95% interval)
| Test | Result | Verdict |
|---|---|---|
| Stats model with all features, 2015–17 | ~ +0.21 nats worse | No edge |
| Stats model, 1997–2005 holdout | ~ +0.17–0.20 worse | No edge |
| Pooled model, 2019–20 holdout | +0.19 worse | No edge |
| Market-anchored residual model | +0.003 [−0.010, +0.016] | No edge |
| Family stack v1 / v2 | +0.03 / +0.01 | Not better |
| Late odds movement (8 h → final) | +0.0035 [−0.0024, +0.0092] | Not significant |
| Early odds movement | −0.0030 | Worse |
| Gear changes | −0.0014 [−0.0033, +0.0005] | No edge |
| Blinkers added | +0.0010 [+0.00002, +0.0019] | Marginal, not counted |
| Tongue tie added | −0.0023 [−0.0043, −0.0002] | Worse |
| Sectional history | −0.0003 [−0.0016, +0.0010] | No edge |
| Pace/trip features | no change | No edge |
| Speed figures (fallback par) | −0.005 stats-only, −0.0007 market | Negligible |
| Horse ratings (1997–2005) | ≈ 0 | No edge |
| Draw bias, 1997–2005 | +0.0001 [+0.00002, +0.0002] | Failed confirmation |
| Draw bias, 2016–18 | −0.0005 [−0.0011, +0.00005] | Worse |
| Draw bias, 2013–2020 holdout | −0.0032 [−0.0053, −0.0011] | Worse |
| Jockey edge, 1997–2005 | +0.0003 [−0.0005, +0.0011] | Not significant |
| Jockey edge, 2008–09 | +0.0004 [−0.0011, +0.0019] | Not significant |
| Jockey edge, 2018–20 | +0.0003 [−0.0001, +0.0006] | Not significant |
| Tipster index (2013–2020) | 0 | No information |
| Weight vs field (2013–2020) | +0.0004 [−0.0002, +0.0012] | Not significant |
| Walk-forward, Bayesian-shrunk history, 2015–2020 | mean ≈ −0.0002 across years | No edge |
| Walk-forward, 2016 alone | +0.0033 [+0.0003, +0.0063] | One year of six; not clean |

## Betting rules
- Favourite (flat): −10% to −23% per unit.
- Rule search chosen on training years, tested once: −30% on holdout (overfit).
- Thesis-style gradient boosting with Kelly sizing, 2017 test: −38% to −41% per unit.
- Benter-style combination: fundamental weight fitted to 0; no bets qualify.
- Kelly with shrinkage toward the market: no horse reaches p·odds ≥ 1; no bets.

## What the literature says
- Benter (1994): combining a fundamental model with public odds adds information only when the
  fundamental model is strong enough. Reported gain ~0.009 nats, unverified here.
- Penn undergraduate thesis (2025): claims non-favourite profits with Kelly sizing; method and
  full text not accessible to us.
- Politecnico di Torino master's thesis (2023): simulations only, no real race data. Learning
  strategies lose money early; the value of learned information is hard to quantify.
- Takeout theory: with a takeout (R > 1), bettors should bet only a fraction of the bankroll, and
  not at all when the game is unfavourable enough. Our market is unfavourable at every price.

## Conclusion
- Every variable tested so far is already priced by the market, or too small to matter.
- The largest effect that appears consistently is a jockey edge of about 0.0003 nats per race.
  Even if real, it is far below the takeout and would need roughly 80,000 races to confirm.
- A +1% return over the market would need roughly 78,000 bets to confirm at 95% confidence.
- Confirming any edge needs data we don't have: odds captured near the off, scratchings and
  jockey changes with timestamps, and many more races.

## Limits of this study
- Several test windows were reused after they were first used, so later results are less clean.
- Many variables were tried; without correction, a few intervals would be expected to exclude zero by chance.
- Final odds were used throughout; odds available before the off would change the picture.
