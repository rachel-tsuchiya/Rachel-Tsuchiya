# FX Hedging Model Specification

**Scenario:** 27 — LNG Marketer  
**Course:** FIN 321  
**Stage:** 2 — Model Specification  
**Status:** Initial Draft

## 1. Problem Statement

Our U.S.-based liquefied natural gas (LNG) company expects to receive EUR 21,500,000 from a German utility in 91 days. Because the payment is denominated in euros, our company faces foreign exchange risk when converting the receivable into U.S. dollars.

The objective of this model is to compare three hedging strategies: a forward contract, a money-market hedge, and a currency put option. The model will calculate the expected USD proceeds under each strategy and evaluate how changes in the EUR/USD exchange rate affect the company's financial outcome.

## 2. Model Inputs

The model will include the following inputs:

| Input | Value | Unit |
|---|---|---|
| Named Range | Placeholder Value | Unit |
| `FC_AMT` | 21,500,000 | EUR |
| `S0_in` | 1.1653 | USD/EUR |
| `F0_in` | 1.1653 | USD/EUR |
| `R_USD` | 5.30% | Annual |
| `R_FC` | 3.00% | Annual |
| `K_PUT` | 1.1653 | USD/EUR |
| `K_CALL` | 1.1653 | USD/EUR |
| `PREM_PUT` | 0.0147 | USD/EUR |
| `PREM_CALL` | 0.0199 | USD/EUR |
| `T_DAYS` | 91 | Days |

All values are indicative modeling inputs. The spot rate, interest rates, and option strike prices are illustrative placeholders rather than verified market quotes. They will be replaced or verified using timestamped market data in Stage 4.

The missing values will be researched and verified using appropriate market-data sources during Stage 4.

## 3. Workbook Architecture

The Excel workbook will contain eight worksheets, organized as follows:

1. **Cover:** Project title, Scenario 27 (LNG Marketer), author, date, and a brief description of the FX exposure.
2. **Legend/Key:** Explanation of input formatting, named ranges, units, formula conventions, and model terminology.
3. **Inputs:** Centralized input values, including the EUR receivable, spot and forward rates, interest rates, option strikes, premiums, and settlement period. All ten required named ranges will be defined here.
4. **Forward:** Calculation of USD proceeds from selling the EUR receivable at the 91-day forward rate, including any transaction costs.
5. **Money Market:** Calculation of EUR borrowing, conversion into USD at the current spot rate, and investment of USD proceeds through settlement.
6. **Options:** EUR put and call option payoff calculations, upfront premiums, and net USD proceeds across different settlement exchange rates. The put hedge will be evaluated as the primary protective option for the EUR receivable.
7. **Sensitivity:** Comparison of unhedged, forward, money-market, and option outcomes across EUR/USD settlement rates from -5% to +5% in 1% increments, including a comparison chart.
8. **Notes & Assumptions:** Documentation of model assumptions, interest-rate conventions, data sources, limitations, and validation checks.

All calculation worksheets will reference the centralized named ranges on the Inputs worksheet to ensure consistency and simplify future updates.

## 4. Assumptions and Constraints

The model will use the following assumptions and constraints:

1. **Settlement and Receivable:** The German utility is assumed to pay the full EUR 21,500,000 receivable exactly 91 days after the valuation date. Credit risk and payment delays are excluded from the base model.

2. **Interest-Rate Convention:** Both EUR and USD annual interest rates will use simple interest with an ACT/360 day-count convention. The 91-day interest factor will be calculated as `1 + Annual Rate × (91/360)`. The same convention will be used consistently in money-market calculations and covered interest rate parity checks.

3. **Exchange-Rate Quotation:** All exchange rates will be expressed in USD per EUR. A higher exchange rate means the euro has appreciated against the dollar; a lower rate means the euro has depreciated.

4. **Forward Contract:** The company is assumed to sell the full EUR receivable at the indicative 91-day forward rate of 1.1653 USD/EUR. The forward contract settles on the same date as the receivable.

5. **Money-Market Hedge:** The company can borrow euros and invest U.S. dollars at the stated annual rates. The base model assumes these rates are available for the full 91-day period, with no borrowing restrictions or early repayment penalties.

6. **Currency Options:** The put and call premiums are quoted in USD per EUR and are paid upfront. The protective EUR put is the relevant hedge for the receivable; the EUR call is included for comparison and model completeness. The model will separately show the premium paid today and its settlement-date value using the USD interest rate, so costs are compared at a consistent point in time.

7. **Transaction Costs:** The base model assumes zero additional transaction costs because actual bid-ask spreads, commissions, and bank fees have not yet been supplied. A separate transaction-cost assumption may be added once reliable figures are available. Option premiums are not treated as zero-cost transactions.

8. **Market Data and Limitations:** The spot rate, interest rates, and option strike prices currently serve as illustrative placeholders. They must be verified or replaced with sourced, timestamped market data in Stage 4. Results are conditional on these assumptions and should not be interpreted as executable market quotes.

## 5. Calculation Flow

The model will use the ten named inputs defined in Section 2. All rates are quoted in USD per EUR, and all net proceeds will be compared at the 91-day settlement date. `ST` represents the future EUR/USD spot rate in each sensitivity scenario; it is a calculated scenario variable, not an additional required input.

**1. Unhedged Position**

`Unhedged_USD = FC_AMT * ST`

This represents the USD value of the receivable if the company waits until settlement and converts the euros at the prevailing spot rate.

**2. Forward Hedge**

`Forward_USD = FC_AMT * F0_in`

At the indicative forward rate, the gross locked-in proceeds are EUR 21,500,000 × 1.1653 = USD 25,053,950. Any separately documented transaction costs will be deducted to calculate net proceeds. The forward result must remain constant across all future spot-rate scenarios.

**3. Money-Market Hedge**

`YEAR_FRAC = T_DAYS / 360`

`EUR_Borrowed = FC_AMT / (1 + R_FC * YEAR_FRAC)`

`USD_Invested = EUR_Borrowed * S0_in`

`MoneyMarket_USD = USD_Invested * (1 + R_USD * YEAR_FRAC)`

At settlement, the EUR receivable repays the EUR loan, including interest. The USD investment matures into the hedged proceeds. Borrowing and investment rates must be stored as decimal values (for example, 5.30% = 0.053). Documented transaction costs are deducted separately.

**4. Currency Put Option**

`Put_Premium_Today = FC_AMT * PREM_PUT`

`Put_Premium_FV = Put_Premium_Today * (1 + R_USD * YEAR_FRAC)`

`Put_USD = FC_AMT * MAX(ST, K_PUT) - Put_Premium_FV`

The put provides a minimum conversion rate while preserving the ability to benefit from euro appreciation. The premium is accumulated to settlement using the USD rate to make all strategy proceeds comparable at the same date.

**5. Currency Call Option — Reference Calculation**

`Call_Premium_Today = FC_AMT * PREM_CALL`

`Call_Premium_FV = Call_Premium_Today * (1 + R_USD * YEAR_FRAC)`

`Call_Payoff = FC_AMT * MAX(ST - K_CALL, 0)`

`Call_Purchase_USD = FC_AMT * ST - Call_Payoff + Call_Premium_FV`

The call-purchase formula represents the net USD cost of purchasing EUR at settlement with call protection; it is not a hedge for the company's EUR receivable. The model will label this separately and will not compare this purchase cost directly with the receivable's USD proceeds.

**6. Covered Interest Rate Parity Check**

`Parity_Forward = S0_in * (1 + R_USD * YEAR_FRAC) / (1 + R_FC * YEAR_FRAC)`

`Parity_Difference = F0_in - Parity_Forward`

The model will compare the quoted forward rate against the parity-implied rate. Any material discrepancy will be flagged for review of interest-rate assumptions, bid-ask spreads, and market-data timing.

**7. Transaction Costs and Comparison Basis**

The base case assumes zero additional transaction costs because no reliable fee quotes are provided. If transaction costs are introduced, they must be explicitly documented and deducted consistently. The final comparison will use net USD settlement-date proceeds for the unhedged position, forward hedge, money-market hedge, and put hedge.

## 6. Sensitivity Analysis

The model will evaluate future EUR/USD exchange rates from −5% to +5% of the baseline rate, using 1% increments.

For each scenario, the workbook will calculate the USD proceeds for the unhedged position, forward hedge, money-market hedge, and put option.

## 7. Validation Rules

The workbook will verify that:

- The EUR receivable and settlement period are positive.
- Exchange rates and interest rates use consistent units.
- The forward hedge produces fixed USD proceeds across exchange-rate scenarios.
- The money-market hedge produces fixed USD proceeds when borrowing and investment rates are held constant.
- The put option provides downside protection while allowing upside participation.
- All formulas reference centralized input cells.

## 8. Model Outputs

The final workbook will display:

- Net USD proceeds under each hedging strategy.
- A comparison table showing hedge outcomes.
- A sensitivity analysis across 11 exchange-rate scenarios.
- A chart comparing the three hedging strategies and the unhedged position.
- Validation results and warnings.
- A summary identifying the most appropriate strategy under the stated assumptions.
