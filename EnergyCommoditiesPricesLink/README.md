# How European Gas Price Shocks Spread to Asian LNG and Coal Markets (2017–2026)

An econometric analysis of price transmission between European gas (TTF), Asian LNG (JKM), Asian coal (Newcastle) and crude oil (Brent), using cointegration, a VECM, Granger causality and impulse responses.

## 1. Key findings
- **European gas leads Asian LNG.** TTF Granger-causes JKM throughout 2017–2026, with a weaker feedback from JKM to TTF.
- **Gas–coal transmission is a crisis-era phenomenon.** Before 2021, TTF shocks had no significant effect on Asian coal. From 2021, the full chain appears: TTF → JKM, TTF → coal, and JKM ↔ coal.
- **Since 2021, a one-standard-deviation TTF shock raises Asian coal prices by about 1.3%, with 90% of the effect within 4 trading days.**
- **Brent is the external long-run driver:** it does not adjust to deviations from equilibrium, while TTF, JKM and coal do.
- **In 2022, Europe paid more than Asia for LNG:** the JKM–TTF spread fell to about −$16/MMBtu (30-day average) as Europe replaced lost Russian pipeline gas.

## 2. Data
| Series | Market | Unit | Source |
|---|---|---|---|
| TTF | European gas (Netherlands) | €/MWh | investing.com |
| JKM | Asian LNG (Japan/Korea) | $/MMBtu | investing.com |
| Newcastle coal | Asian coal | $/t | investing.com |
| Brent | Crude oil | $/bbl | investing.com |
| EUR/USD | Exchange rate | $ per € | ECB API |

- **Period:** 23.10.2017 (the earliest date in the downloaded TTF series) to 23.10.2026, daily.
- **Preparation:**
  - outer merge of all series on date;
  - forward-fill of short gaps (max. 3 days) caused by different holiday calendars;
  - TTF converted to $ with EUR/USD, and to $/MMBtu (÷ 3.412) for the spread analysis.
- **Data challenges solved:** the source files used different number formats (comma vs dot decimals) and different date formats (day-first vs month-first), which caused mismatched dates when merging. Each file is therefore loaded with an explicit format.

## 3. Method
1. **ADF test:** log prices are non-stationary and log returns are stationary, so the series are integrated of order one, I(1).
2. **Cointegration (Engle-Granger and Johansen):** all pairs share long-run relationships, so a vector error correction model is appropriate.
3. **VECM** on log prices (6 lags, selected by AIC/FPE): captures both short-run dynamics and long-run adjustment.
4. **Granger causality:** tests which market leads which.
5. **Impulse responses:** measure the size and speed of transmission after a TTF shock.
6. **Robustness check:** the model is re-estimated separately for 2017–2020 and 2021–2026.

## 4. Results

### Price growth (base 100)
![Energy commodities price growth]('/Users/jeanmiccheltia/Downloads/Screenshot 2026-10-28 at 19.14.59.png')

All four prices moved together until 2021. During the energy crisis, TTF rose about 16-fold at its 2022 peak, far more than JKM (about 8-fold), coal (about 4.5-fold) and Brent (about 2-fold). Prices fell back in 2023, but TTF and JKM rose again in 2026.

### JKM–TTF spread
![JKM minus TTF spread]('/Users/jeanmiccheltia/Downloads/Screenshot 2026-10-28 at 19.15.20.png')

Asia normally pays a small premium for LNG (about $0–4/MMBtu). From early 2022 the spread turned sharply negative, reaching about −$16/MMBtu on a 30-day average (below −$30 on single days), as Europe outbid Asia for LNG cargoes. It returned to positive in early 2023, with short negative dips since then around winter and early spring.

### Impulse responses: 2017–2020 vs 2021–2026
![Impulse responses by period]('/Users/jeanmiccheltia/Downloads/Screenshot 2026-10-28 at 19.15.49.png')

- **JKM** responds in both periods, but the effect roughly doubled after 2021 (about 4.2% vs 2.2% after 30 trading days) and comes much faster.
- **Coal** shows virtually no response before 2021. Since 2021 it rises to about 1.3% within 4–5 trading days and then stays there.

## 5. Robustness check
The 2021–2022 energy crisis may have changed how markets interact, so the full model was re-estimated separately for two periods.

| Test | 2017–2020 | 2021–2026 |
|---|---|---|
| TTF → JKM | Significant | Significant |
| TTF → Coal | Not significant | Significant |
| JKM ↔ Coal | Not significant | Significant |
| Coal response to a TTF shock | ≈ 0 | +1.3% within 4 trading days |

The link between European gas and Asian LNG holds in both periods, but transmission to Asian coal only appears from 2021. The full-sample result is therefore driven by the crisis period.

## 6. Limitations
- **Sample period:** the analysis starts in October 2017, the first date of the daily TTF series used. The pre-2021 sample (about 3 years 2 months) is shorter than the post-2021 sample (about 5 years 10 months).
- **Shock size:** impulse responses use one-standard-deviation shocks. TTF was far more volatile after 2021, so part of the larger response reflects larger shocks, not only stronger transmission.
- **Daily noise:** European and Asian markets close at different times, forward-filled holidays create artificial zero-change days, and continuous futures series include monthly contract rolls.
- **Missing fundamentals:** traded volumes, LNG shipments and gas storage levels were not included, although they likely affect prices.

## 7. Conclusion
European gas prices consistently lead Asian LNG prices, and since the 2021–2022 energy crisis, gas price shocks also spread quickly into Asian coal prices through fuel switching. Brent acts as the external long-run anchor.

## 8. Further work
- **Storage and seasonality:** since 2025, TTF has traded above JKM around late winter and early spring, when European gas storage is low. Adding storage data (AGSI) would test whether low storage now keeps European prices structurally high.
- **Renewables and gas dependence:** this leads to a follow-up project analysing whether renewable growth in Europe can reduce the dependence of power prices on gas.

## How to run
1. Install the required libraries:
   ```
   pip install pandas numpy matplotlib seaborn statsmodels
   ```
2. Place the data files in the `data/` folder.
3. Run the notebook `gas_coal_analysis.ipynb` from top to bottom.
