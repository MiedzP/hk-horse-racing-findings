# Hong Kong horse racing: what we tested and what held up

Findings from testing whether racing data can beat the market's final win odds in Hong Kong.

**Short answer:** no variable, model, or betting rule beat the market on data it wasn't tuned on.

See [FINDINGS.md](FINDINGS.md) for the data, every test with its interval and verdict, the betting results, and the limits of the study.

## Notes
- The raw race datasets are not included. They are third-party files under their own licences.
- Several test windows were reused after first use, so later results are less clean. See the limits section.

## Key note: what was and wasn't statistically significant
- **Nothing held up as a betting edge.** No variable, model, or rule beat the market's final odds on a test window that held up.
- **Some tests were significant, but in the wrong direction or not reproducible.** The draw-bias test on 2013–2020 and tongue-tie changes were significantly worse than the market. The draw result that looked positive on 1997–2005 failed on the 2016–18 confirmation. The one significant gain, in the 2016 walk-forward year, is one year of six and uses a window that was reused.
- **Betting directly lost money.** Backing the favourite lost 10–23% per unit, and every rule tested, including the Kelly-based ones, lost money on untouched windows.
- **Best reading:** the market was the strongest predictor available. Not betting was the only choice the data supported.
