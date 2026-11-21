# Stage 4 — LNG Marketer Market-Data Memo

**Scenario:** 27 — LNG Marketer  
**Market observation date:** November 19, 2026  
**Exposure:** EUR 21,500,000 receivable in 91 days

## 1. Market Inputs and Sources

| Named Range | Value | Source | Notes |
|---|---|---|---|
| `FC_AMT` | EUR 21,500,000 | Scenario 27 | Contractual euro receivable |
| `S0_in` | 1.0967 USD/EUR | ExchangeRates.org.uk, historical EUR/USD | Reported November 19 daily close; provider closing convention applies |
| `F0_in` | 1.1653 USD/EUR | Scenario 27 bank quote | Indicative 91-day forward; retained unchanged |
| `R_USD` | 4.62% | U.S. Treasury, 1-year constant-maturity yield | Government yield proxy for USD investment |
| `R_FC` | 3.343% | 12-month Euribor historical fixing | Interbank benchmark proxy for EUR borrowing |
| `K_PUT` | To be set | Stage 4 modeling convention | Strike at or near live spot |
| `K_CALL` | To be set | Stage 4 modeling convention | Strike at or near live spot |
| `PREM_PUT` | 0.0147 USD/EUR | Scenario 27 | Bank-provided indicative premium; held fixed |
| `PREM_CALL` | 0.0199 USD/EUR | Scenario 27 | Bank-provided indicative premium; held fixed |
| `T_DAYS` | 91 | Scenario 27 | ACT/360 convention |

## 2. Source Links and Timing

- EUR/USD historical exchange rate: https://www.exchangerates.org.uk/EUR-USD-exchange-rate-history.html
- U.S. Treasury historical yield curve: https://home.treasury.gov/resource-center/data-chart-center/interest-rates
- Historical Euribor rates: https://euriborrates.com/euribor-rates/2026-11-19

All three market observations are dated November 19, 2026. The EUR/USD figure is a provider-reported daily close, the Treasury yield is a daily published observation, and Euribor is a daily benchmark fixing. These observations do not necessarily share an identical fixing time. Exact retrieval timestamps remain to be documented.

## 3. Rate Selection and Limitations

The one-year U.S. Treasury yield is used as a transparent, publicly available proxy for the company's USD investment rate. The 12-month Euribor fixing is used as a proxy for its EUR borrowing rate.

Both have longer maturities than the company's 91-day exposure. They are not executable corporate deposit or borrowing quotes, and the difference in instruments introduces a basis mismatch.

The scenario's indicative bank forward and option premiums remain unchanged. Option strikes will be set at or near the observed spot rate, consistent with Stage 4 instructions.

## 4. Covered Interest Parity

Using the November 19, 2026 market inputs and the ACT/360 simple-interest convention:

CIP-implied forward = 1.0967 × [1 + 0.0462 × (91/360)] / [1 + 0.03343 × (91/360)] = 1.100210 USD/EUR.

The scenario's indicative bank forward quote is 1.165300 USD/EUR. The discrepancy (bank forward minus CIP-implied forward) is +0.065090 USD/EUR, exceeding the model's illustrative tolerance of 0.005 USD/EUR. Therefore, the CIP validation status is WARNING.

This discrepancy should not automatically be interpreted as an executable arbitrage opportunity. The calculation uses one-year benchmark rates as proxies for 91-day corporate borrowing and investing, and the scenario's bank forward is indicative rather than a verified executable quote. The mismatch warrants investigation rather than an adjustment to force the validation check to PASS.

## 5. Workbook Population and Validation

The FX hedging workbook (`capabilities/fx-hedging/model.xlsx`) was updated using the November 19, 2026 market observations.

The following inputs were revised:

- `S0_in`: 1.0967 USD/EUR
- `R_USD`: 4.62%
- `R_FC`: 3.343%
- `K_PUT`: 1.0967 USD/EUR
- `K_CALL`: 1.0967 USD/EUR

The original scenario inputs, including the EUR 21,500,000 receivable, 91-day maturity, 1.1653 USD/EUR indicative forward quote, and bank-provided option premiums, were retained.

**Workbook validation results:**

- **Forward hedge — PASS:** USD proceeds remained $25,053,950.00, calculated using an Excel formula.
- **Money-market hedge — PASS:** All three calculations matched the expected results and remained formula-driven.
- **Currency options — PASS:** All seven option calculations matched expected results and remained formula-driven.
- **Sensitivity analysis — PASS:** All 11 exchange-rate scenarios recalculated correctly, and the chart continued to display the expected hedge behavior.
- **Input and formula validation — PASS:** All validation checks passed except covered interest parity.
- **Covered interest parity — WARNING:** The indicative bank forward quote exceeded the theoretical CIP-implied rate by approximately 0.06509 USD/EUR, above the model's 0.005 USD/EUR tolerance.

The CIP warning was retained rather than changing the market inputs to force a passing result. The discrepancy reflects limitations associated with indicative bank pricing, different benchmark instruments, and the use of one-year interest-rate proxies for a 91-day exposure.

The updated workbook was saved and committed to GitHub.
