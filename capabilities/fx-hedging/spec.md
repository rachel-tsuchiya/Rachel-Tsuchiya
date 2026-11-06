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

The Excel workbook will contain five worksheets:

- **Inputs:** Centralized assumptions, exchange rates, interest rates, and transaction costs.
- **Calculations:** Formulas for the unhedged position and three hedging strategies.
- **Sensitivity:** Exchange-rate scenarios and their impact on USD proceeds.
- **Validation:** Formula checks, unit consistency, and error flags.
- **Dashboard:** Summary comparison of hedge outcomes and financial recommendations.

## 4. Assumptions and Constraints

The model assumes that the German utility will pay the full EUR receivable after 91 days. Interest rates will be expressed annually and converted to the 91-day period using a documented day-count convention.

The forward exchange rate is assumed to remain available for the specified settlement date. Option premiums are assumed to be paid upfront, and transaction costs will be included where applicable.

## 5. Calculation Flow

**Unhedged Position:**

USD Proceeds = EUR Receivable × Future Spot Rate

**Forward Hedge:**

USD Proceeds = EUR Receivable × Forward Rate − Transaction Costs

**Money-Market Hedge:**

EUR Borrowed Today = EUR Receivable ÷ (1 + EUR Interest Rate × 91/360)

USD Invested Today = EUR Borrowed Today × Current Spot Rate

USD Proceeds = USD Invested Today × (1 + USD Interest Rate × 91/360) − Transaction Costs

**Currency Put Option:**

USD Proceeds = EUR Receivable × MAX(Future Spot Rate, Put Strike Price) − Option Premium Cost − Transaction Costs

Option Premium Cost = EUR Receivable × Put Premium per EUR

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
