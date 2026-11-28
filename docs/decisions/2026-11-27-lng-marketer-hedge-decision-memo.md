# CFO Decision Memo — FX Hedging Strategy

**To:** Chief Financial Officer, LNG Marketer  
**From:** Rachel Tsuchiya 
**Date:** November 27, 2026  
**Subject:** Hedging Recommendation for €21.5 Million Receivable

## 1. Executive Summary

The LNG marketer is scheduled to receive €21.5 million from a German utility in 91 days, exposing the company to potential fluctuations in the EUR/USD exchange rate. A depreciation of the euro would reduce the U.S. dollar value of this receivable, creating uncertainty in future cash flows and financial planning.

Based on the November 19, 2026 market-data assumptions, I recommend pursuing a **91-day forward contract**, conditional on confirmation of the bank's indicative exchange rate of 1.1653 USD/EUR. At this rate, the company would secure $25,053,950 in USD proceeds, eliminating exchange-rate uncertainty on the receivable.

The forward hedge provides approximately $1.40 million more than the modeled money-market hedge and outperforms the unhedged and protective put strategies across the tested ±5% EUR/USD scenarios. Unlike the protective put, the forward also requires no upfront option premium.

However, the bank's indicative forward rate is substantially higher than the covered interest parity (CIP) implied rate of approximately 1.10021 USD/EUR. This discrepancy warrants further investigation before execution, particularly because the interest-rate benchmarks used in the model are one-year proxies for a 91-day exposure.

**Recommendation:** Request a firm, executable 91-day forward quote for the full €21.5 million receivable. If the bank confirms the quoted terms, the forward is the preferred strategy because it offers the highest modeled USD proceeds while providing certainty over the company's future cash flow.

## 2. Financial Analysis and Hedge Comparison

Using the November 19, 2026 market observations, the LNG marketer's €21.5 million receivable was evaluated under four strategies: remaining unhedged, entering a forward contract, establishing a money-market hedge, and purchasing a protective EUR put option.

The analysis assumes a 91-day settlement period, ACT/360 simple interest, and a baseline future spot rate equal to the observed rate of 1.0967 USD/EUR.

| Strategy | USD Proceeds at Baseline | Primary Advantage | Primary Limitation |
|---|---:|---|---|
| Unhedged | $23,579,050.00 | Retains full upside from EUR appreciation | Exposed to exchange-rate depreciation |
| Forward hedge | $25,053,950.00 | Locks in USD proceeds with no upfront option premium | Gives up potential upside; bank quote must be confirmed |
| Money-market hedge | $23,654,524.73 | Creates predictable USD proceeds through borrowing and investing | Requires financing and uses proxy interest rates |
| Protective EUR put | $23,259,309.06 | Protects against EUR depreciation while retaining upside | Requires an upfront premium |

The forward hedge generates approximately **$1,399,425 more than the money-market hedge** and **$1,474,900 more than remaining unhedged at the baseline exchange rate**.

The protective EUR put guarantees a modeled minimum of $23,259,309 after accounting for the premium's financing cost. Although the put preserves upside from euro appreciation, its cost reduces net proceeds compared with remaining unhedged when the euro does not depreciate.

A EUR call option was also evaluated as a reference calculation. However, a call is primarily appropriate for hedging a future EUR payable rather than the company's EUR receivable. Therefore, it is not included among the recommended receivable hedges.

Overall, the forward hedge offers the strongest combination of modeled USD proceeds and cash-flow certainty, provided the bank's indicative terms are executable.

## 3. Sensitivity Analysis

To evaluate the impact of exchange-rate fluctuations, the hedging strategies were tested across 11 future EUR/USD scenarios ranging from −5% to +5% around the baseline spot rate of 1.0967 USD/EUR.

The table below highlights three representative scenarios:

| Strategy | EUR −5% | Baseline | EUR +5% |
|---|---:|---:|---:|
| Future EUR/USD rate | 1.041865 | 1.096700 | 1.151535 |
| Unhedged | $22,400,097.50 | $23,579,050.00 | $24,758,002.50 |
| Forward hedge | $25,053,950.00 | $25,053,950.00 | $25,053,950.00 |
| Money-market hedge | $23,654,524.73 | $23,654,524.73 | $23,654,524.73 |
| Protective EUR put | $23,259,309.06 | $23,259,309.06 | $24,438,261.56 |

The forward hedge produces the highest USD proceeds across all 11 tested scenarios. Its fixed rate of 1.1653 USD/EUR exceeds even the +5% future spot rate of 1.151535 USD/EUR.

The money-market hedge also eliminates exchange-rate uncertainty, but its modeled proceeds remain approximately $1.40 million below the forward. The protective put provides a minimum USD value while preserving the potential to benefit from euro appreciation, although the upfront premium reduces net proceeds.

While the forward is the strongest strategy within the tested range, it sacrifices potential gains if the euro appreciates significantly beyond the modeled scenarios. The protective put would surpass the forward's net proceeds only if the future EUR/USD rate exceeded approximately 1.180172.

## 4. Covered Interest Parity and Execution Considerations

Covered interest parity provides a theoretical forward exchange rate based on the current spot rate and interest-rate differential between the United States and the euro area.

Using the November 19 market-data assumptions and ACT/360 simple interest, the CIP-implied forward rate is approximately **1.10021 USD/EUR**, compared with the bank's indicative quote of **1.1653 USD/EUR**. The discrepancy of approximately **0.06509 USD/EUR** exceeds the model's validation tolerance and produces a WARNING.

This difference is financially significant and should not be interpreted as evidence of an immediately executable arbitrage opportunity. The model uses a one-year U.S. Treasury yield and 12-month Euribor as proxies for the company's 91-day financing rates. These benchmarks differ in maturity, credit characteristics, and market conventions. Furthermore, the bank's forward quote is indicative rather than confirmed.

Before executing a hedge, the company should obtain a firm forward bid for the full €21.5 million receivable, verify the settlement date, assess counterparty credit and collateral requirements, and compare the quote against maturity-matched borrowing and investment rates. The company should also confirm any transaction fees or other contractual costs.

If the quoted forward rate is unavailable or materially less favorable when confirmed, the CFO should reassess the forward against a properly priced money-market hedge and protective put using consistent, executable market inputs.

## 5. Final Recommendation and Conclusion

Based on the independent AI validation, Excel workbook results, and sensitivity analysis, I recommend that the LNG marketer **prioritize a 91-day forward hedge for its €21.5 million receivable**, subject to confirmation of executable market terms.

At the indicative forward rate of 1.1653 USD/EUR, the company would secure $25,053,950 in future USD proceeds, outperforming the modeled alternatives across the tested exchange-rate scenarios. This strategy also aligns with the company's objective of reducing foreign exchange exposure and improving cash-flow predictability.

However, the substantial discrepancy between the indicative forward quote and the CIP-implied rate requires additional due diligence. The CFO should not authorize execution solely on the basis of the modeled results.

Before proceeding, management should obtain a binding bank quote, verify transaction costs and settlement terms, and compare the executable forward rate against updated money-market and option alternatives using maturity-matched market data.

If the quoted forward terms are confirmed, the company should execute the forward hedge to protect its USD cash flows. If the terms change materially, management should reevaluate the available strategies before committing.

Ultimately, the objective is not simply to maximize projected proceeds, but to select a hedge that balances **cash-flow certainty, financial value, execution feasibility, and risk management**.
