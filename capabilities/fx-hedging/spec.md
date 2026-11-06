# FX Hedging Model Specification

**FIN 321 | Scenario 27: LNG Marketer | Stage 2 | Status: Revised specification**

## 1. Problem Statement

A U.S. LNG marketer will receive **EUR 21,500,000 in 91 days** from a German utility. EUR depreciation reduces the USD value of this receivable. Build an auditable Excel model comparing **unhedged, forward, money-market, and protective EUR put** settlement-date USD proceeds; show a EUR call separately as a reference for EUR purchases.

## 2. Model Inputs

All ten inputs reside on the **Inputs** tab as Excel named ranges:

| Named range | Value | Units |
|---|---:|---|
| `FC_AMT` | 21,500,000 | EUR |
| `S0_in` | 1.1653* | USD/EUR spot |
| `F0_in` | 1.1653 | USD/EUR forward |
| `R_USD` | 5.30%* | annual decimal rate |
| `R_FC` | 3.00%* | annual decimal EUR rate |
| `K_PUT` | 1.1653* | USD/EUR |
| `K_CALL` | 1.1653* | USD/EUR |
| `PREM_PUT` | 0.0147 | USD/EUR |
| `PREM_CALL` | 0.0199 | USD/EUR |
| `T_DAYS` | 91 | days |

*Illustrative placeholders, **not verified quotes**. In Stage 4, replace or verify spot, interest rates, and strikes using dated sources; record source URLs, quote timestamps, and bid/ask conventions. Scenario figures are indicative, not executable quotes.*

## 3. Workbook Architecture

Eight tabs: **Cover** (scenario and purpose); **Legend/Key** (units and formatting); **Inputs** (ten named ranges and source notes); **Forward** (contract proceeds); **Money Market** (EUR borrowing/USD investing); **Options** (put hedge and separate call reference); **Sensitivity** (11 scenarios, table, chart); **Notes & Assumptions** (conventions, sources, validation statuses, decision summary). Formulas reference Inputs, not duplicated hard-coded values.

## 4. Assumptions and Constraints

Full EUR payment occurs on day 91; ignore credit risk and delays. Quote FX as **USD per EUR**. Apply **simple interest, ACT/360**, consistently: `t = T_DAYS/360`. Assume borrowing/investing at the listed rates, forward settlement aligned with receivable, and put/call premiums paid today. Compound each premium to settlement using the USD rate for comparable day-91 results. Base-case additional transaction costs are **zero** until documented fees/spreads are available; disclose any later costs separately. The **put** hedges a EUR receivable; the **call** is a purchase-side reference, not a receivable hedge.

## 5. Calculation Flow

`ST` = scenario settlement spot (USD/EUR); `t = T_DAYS/360`. Rates are stored as decimals (5.30% = 0.053). Amounts below are settlement-date USD unless labeled otherwise.

```text
Unhedged_USD = FC_AMT * ST
Forward_USD = FC_AMT * F0_in
EUR_Borrowed = FC_AMT / (1 + R_FC*t)
USD_Invested = EUR_Borrowed * S0_in
MoneyMarket_USD = USD_Invested * (1 + R_USD*t)
Put_Premium_Today = FC_AMT * PREM_PUT
Put_Premium_FV = Put_Premium_Today * (1 + R_USD*t)
Put_USD = FC_AMT * MAX(ST,K_PUT) - Put_Premium_FV
Call_Premium_FV = FC_AMT * PREM_CALL * (1 + R_USD*t)
Call_Payoff = FC_AMT * MAX(ST-K_CALL,0)
Call_Purchase_USD = FC_AMT*ST - Call_Payoff + Call_Premium_FV
Parity_Forward = S0_in*(1 + R_USD*t)/(1 + R_FC*t)
Parity_Difference = F0_in - Parity_Forward
```

EUR receivable repays the EUR loan at maturity. The forward yields **$25,053,950 gross** at the scenario quote. Deduct separately disclosed transaction costs from the relevant net proceeds; never mix call purchase **cost** with receivable **proceeds**.

## 6. Sensitivity Analysis

Generate **11 changes: −5%, −4%, …, 0%, …, +4%, +5%**; for each, `ST = S0_in*(1 + Change_Pct)`. Show `Change_Pct`, `ST`, and net USD proceeds for unhedged, forward, money market, and put, plus each hedge's USD difference versus unhedged. Plot settlement spot (x-axis) against USD proceeds (y-axis). Unhedged varies linearly; forward and money market remain flat; the put has a premium-adjusted floor and upside above its strike. These are stress scenarios, **not forecasts**.

## 7. Validation Rules

Display **PASS / WARNING / FAIL** on Notes & Assumptions. **FAIL** for missing/non-numeric inputs; nonpositive `FC_AMT`, `T_DAYS`, spot/forward/strikes or interest factors; negative premiums; broken formulas; or nonfinite USD outputs. Check that EUR loan repayment equals `FC_AMT` within **EUR 0.01**, forward/money-market results are constant across scenarios, put payoff has a floor, call payoff is nonnegative, and exactly 11 scenarios appear in 1% steps. Check USD/EUR units and day-91 timing. **WARNING** if `ABS(Parity_Difference) > 0.005 USD/EUR`; investigate quote timing, spreads, and rate assumptions rather than assuming an error. Resolve FAILs and document WARNINGs.

## 8. Model Outputs

Provide labeled exposure/inputs; forward gross and net USD; EUR borrowed, USD invested, maturity repayment and money-market net USD; put strike, premium today/FV, exercise outcome and net USD; separate call purchase-cost reference; 11-row comparison and line chart; parity and validation statuses. Summarize **net proceeds, downside protection, upside potential, premium/transaction costs, limitations, and a conditional CFO recommendation**. Identify all placeholders and later market-data timestamps/sources. All comparable strategy proceeds are in **settlement-date USD**.
