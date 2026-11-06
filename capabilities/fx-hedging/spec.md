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

The Sensitivity worksheet will evaluate how changes in the future EUR/USD spot rate affect USD proceeds under each hedging strategy.

**1. Scenario Range:** The model will generate 11 future spot-rate scenarios, ranging from -5% to +5% relative to the baseline exchange rate, in 1% increments. The baseline will be the current spot rate (`S0_in`) unless a separately documented forward-based reference rate is selected.

**2. Scenario Formula:** For each percentage change (`Change_Pct`), the future spot rate will be calculated as:

`ST = S0_in * (1 + Change_Pct)`

The scenario percentages will be -5%, -4%, -3%, -2%, -1%, 0%, +1%, +2%, +3%, +4%, and +5%.

**3. Strategy Calculations:** For each future spot-rate scenario, the model will calculate:

- Unhedged proceeds: `FC_AMT * ST`
- Forward hedge: `FC_AMT * F0_in`
- Money-market hedge: `FC_AMT / (1 + R_FC * T_DAYS/360) * S0_in * (1 + R_USD * T_DAYS/360)`
- Put hedge: `FC_AMT * MAX(ST, K_PUT) - FC_AMT * PREM_PUT * (1 + R_USD * T_DAYS/360)`

Any documented transaction costs will be deducted consistently to calculate net USD proceeds.

**4. Comparison Table:** The Sensitivity worksheet will display the percentage change, future spot rate, and net USD proceeds for all four strategies in each of the 11 scenarios. It will also calculate the difference between each hedge's proceeds and the unhedged proceeds.

**5. Visualization:** A line chart will plot future EUR/USD spot rates on the horizontal axis and net USD settlement proceeds on the vertical axis. Separate lines will represent the unhedged position, forward hedge, money-market hedge, and put option hedge.

**6. Expected Behavior:** The unhedged proceeds should increase as the euro appreciates. Forward and money-market proceeds should remain constant across scenarios. The put hedge should establish a downside floor after premium costs while retaining upside potential when the euro appreciates above the strike price.

**7. Interpretation:** The model will identify which strategy produces the highest net USD proceeds in each scenario and discuss the trade-off between certainty, premium costs, and upside participation. Scenario outcomes will be treated as sensitivity tests, not exchange-rate forecasts.

## 7. Validation Rules

The workbook will include automated validation checks to ensure that inputs, calculations, and outputs are accurate and consistent. Each check will display a PASS, WARNING, or FAIL status on the Notes & Assumptions worksheet.

**1. Input Validation:** Confirm that `FC_AMT` and `T_DAYS` are positive, that `S0_in`, `F0_in`, `K_PUT`, and `K_CALL` are greater than zero, and that `PREM_PUT` and `PREM_CALL` are nonnegative. Interest factors `1 + R_USD*T_DAYS/360` and `1 + R_FC*T_DAYS/360` must be positive to prevent invalid calculations. Missing or nonnumeric inputs will trigger FAIL.

**2. Currency and Unit Consistency:** Verify that exchange rates are expressed in USD/EUR, option premiums in USD/EUR, and interest rates as annual decimal values. All strategy outputs must be in USD at the 91-day settlement date. The model will flag inconsistent labels or units for review.

**3. Forward Hedge Check:** Verify that `Forward_USD = FC_AMT * F0_in` before transaction costs. Forward proceeds must remain unchanged across all 11 future spot-rate scenarios. Any variation will trigger FAIL.

**4. Money-Market Hedge Check:** Verify that `EUR_Borrowed * (1 + R_FC*T_DAYS/360) = FC_AMT`, within a numerical tolerance of EUR 0.01. Money-market proceeds must also remain constant across sensitivity scenarios when the input rates remain fixed.

**5. Put Option Check:** Verify that `Put_USD = FC_AMT * MAX(ST, K_PUT) - Put_Premium_FV` before additional transaction costs. Below the put strike, net proceeds must remain at the protected floor. Above the strike, net proceeds must increase with the future spot rate.

**6. Call Option Check:** Verify that the call payoff equals `FC_AMT * MAX(ST - K_CALL, 0)` and is never negative. The call-purchase calculation must be labeled as a reference for buying EUR, not as a direct hedge for the EUR receivable.

**7. Covered Interest Rate Parity (CIRP) Check:** Calculate `Parity_Forward = S0_in * (1 + R_USD*T_DAYS/360) / (1 + R_FC*T_DAYS/360)` and compare it with `F0_in`. Calculate `Parity_Difference = F0_in - Parity_Forward`. A discrepancy greater than 0.005 USD/EUR will trigger WARNING for investigation of market timing, interest-rate assumptions, or transaction spreads. This tolerance is an illustrative review threshold, not a universal market standard.

**8. Sensitivity Check:** Confirm that the Sensitivity worksheet includes exactly 11 scenarios from -5% to +5% in 1% increments, with no missing values or formula errors. The model will verify that the unhedged position changes proportionally with the future spot rate.

**9. Output and Error Handling:** All required outputs must be numeric, finite, and labeled in USD. The workbook will flag missing inputs, broken references, division-by-zero errors, and negative option premiums. Any FAIL status must be resolved before the model is considered ready for decision-making. WARNING statuses must be documented and investigated.

## 8. Model Outputs

The final workbook will display:

The completed Excel workbook will provide clearly labeled financial outputs to support the CFO's evaluation of foreign exchange hedging alternatives for the EUR 21,500,000 receivable.

**1. Exposure Summary:** The Cover worksheet will display the EUR receivable, 91-day settlement period, current spot rate, indicative forward rate, and primary currency risk. The Inputs worksheet will contain the ten required named ranges with values, units, and data-source notes.

**2. Forward Hedge Results:** The Forward worksheet will show the contracted exchange rate, gross USD proceeds, applicable transaction costs, and net USD settlement proceeds. At the indicative rate of 1.1653 USD/EUR, gross proceeds should equal USD 25,053,950.

**3. Money-Market Hedge Results:** The Money Market worksheet will display the EUR amount borrowed today, USD converted and invested today, EUR loan repayment at maturity, and net USD investment proceeds at settlement. The implied effective exchange rate will be calculated as net USD proceeds divided by `FC_AMT`.

**4. Currency Option Results:** The Options worksheet will show the EUR put strike, premium per euro, total upfront premium, premium future value, exercise decision, and net USD settlement proceeds. A separate call-option reference calculation will display its strike, premium, payoff, and EUR purchase cost without presenting it as a hedge for the receivable.

**5. Sensitivity Comparison Table:** The Sensitivity worksheet will present 11 scenarios from -5% to +5% in 1% increments. Each row will show the future EUR/USD spot rate and net USD proceeds for the unhedged position, forward hedge, money-market hedge, and protective put. Additional columns will calculate each hedge's dollar advantage or disadvantage relative to remaining unhedged.

**6. Sensitivity Chart:** A line chart will compare the four strategies, with future EUR/USD spot rates on the horizontal axis and net USD settlement proceeds on the vertical axis. The chart will clearly distinguish fixed-proceeds hedges from strategies that retain exchange-rate upside.

**7. Validation Summary:** The Notes & Assumptions worksheet will display PASS, WARNING, or FAIL results for input integrity, calculation consistency, option payoff behavior, sensitivity completeness, and covered interest rate parity. Any unresolved warnings or failures will be documented.

**8. Decision Summary:** The workbook will provide a concise comparison of net proceeds, downside protection, upside participation, upfront costs, and major limitations for each strategy. A final recommendation will be based on the model results and the company's preference for cash-flow certainty versus potential upside. No strategy will be labeled universally superior without considering the assumptions and market conditions.

All financial outputs will use USD at the 91-day settlement date unless explicitly labeled otherwise. The model will distinguish illustrative inputs from verified market data and identify the valuation date and sources once those figures are obtained in Stage 4.
