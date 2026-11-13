# Stage 3 — LNG Marketer Build and Audit Analysis

**Course:** FIN 321  
**Scenario:** 27 — LNG Marketer  
**Date:** November 12, 2026  
**Workbook:** `capabilities/fx-hedging/model.xlsx`  
**Status:** Manual workbook audit completed; illustrative inputs require Stage 4 verification.

## Purpose and method

I inspected the AI-assisted Excel workbook against the Stage 2 model specification for a EUR 21,500,000 receivable due in 91 days. In Excel, I checked the calculated values and formulas on the Forward, Money Market, and Options sheets, reviewed all 11 sensitivity scenarios and the chart, and inspected the validation statuses on Notes & Assumptions. The results below describe my observed checks; they are not a claim of an independent line-by-line review of every workbook formula.

## Audit findings

### Finding 1 — Forward hedge calculation: PASS

**Test:** Inspect the forward-proceeds cell and confirm it contains a formula rather than a hardcoded result.  
**Expected:** EUR 21,500,000 × 1.1653 USD/EUR = **USD 25,053,950.00**.  
**Observed:** The Forward sheet displayed **USD 25,053,950.00** and used a formula.  
**Assessment/action:** PASS. This confirms the base-case forward amount under the indicative bank quote. Retain the quote as an assumption until Stage 4 source documentation is complete.

### Finding 2 — Money-market hedge calculations: PASS

**Test:** Inspect the EUR borrowing, USD conversion/investment, and USD maturity-proceeds cells and their formulas.  
**Expected:** Borrow **EUR 21,338,185.43**; convert to approximately **USD 24,865,387.48** today; receive **USD 25,198,514.60** at maturity using 3.00% EUR and 5.30% USD annual simple rates on ACT/360. The EUR borrowing plus interest repays EUR 21,500,000.  
**Observed:** The workbook's three money-market values matched the displayed expected results and used formulas.  
**Assessment/action:** PASS for the inspected formula-driven calculation. The interest rates are illustrative; Stage 4 must replace or verify them with dated sources and clarify whether the chosen benchmarks represent executable borrowing/investment rates.

### Finding 3 — Currency options and hedge direction: PASS

**Test:** Inspect seven put and call outputs and confirm formula use at a future spot rate of 1.1653 USD/EUR.  
**Expected put:** Upfront premium **USD 316,050.00**; premium accumulated to maturity **USD 320,284.19**; net receivable proceeds **USD 24,733,665.81**.  
**Expected call reference:** Upfront premium **USD 427,850.00**; premium accumulated to maturity **USD 433,582.00**; call payoff **USD 0.00**; EUR purchase cost **USD 25,487,532.00**.  
**Observed:** All seven displayed values matched expectations and used formulas.  
**Assessment/action:** PASS. The EUR put protects the receivable; the EUR call calculation is a separate EUR-purchase reference, not an alternative receivable hedge. Keep that labeling explicit.

### Finding 4 — Sensitivity scenarios and chart: PASS

**Test:** Inspect the Sensitivity sheet for 11 future-spot scenarios from −5% to +5% in 1% increments and compare the four strategy lines.  
**Expected:** Unhedged proceeds rise with EUR/USD; forward and money-market proceeds remain flat; the protective put establishes a downside floor and retains upside above its strike.  
**Observed:** All 11 scenarios appeared and the chart followed the expected patterns.  
**Assessment/action:** PASS for the inspected scenario coverage and chart behavior. These are sensitivity tests, not forecasts.

### Finding 5 — Covered interest rate parity discrepancy: WARNING (expected)

**Test:** Review the Notes & Assumptions validation results and the covered interest rate parity (CIRP) comparison.  
**Expected:** Parity-implied forward ≈ **1.172024 USD/EUR** versus indicative forward **1.165300 USD/EUR**; difference ≈ **−0.006724 USD/EUR**. Its absolute value exceeds the model's illustrative **0.005 USD/EUR** warning threshold.  
**Observed:** CIRP displayed **WARNING**, and all other displayed validation checks showed **PASS**.  
**Assessment/action:** Expected warning, not a confirmed formula defect. Do not override it simply to obtain all PASS statuses. In Stage 4, investigate timing, rate-tenor consistency, bid–ask spreads, and source dates before interpreting the difference.

## Limitations and next steps

This audit used the Stage 2 illustrative spot rate, interest rates, and option strikes. It verified displayed results and formula presence but did not establish executable market prices or fully stress-test every input. In Stage 4, document dated sources for market inputs, retain the scenario's bank forward and premium quotes, confirm option strikes, and rerun the validation and sensitivity checks after updating the data. The model should not be used for an actual hedging decision until those steps are completed.

## AI assistance and review

ChatGPT assisted with workbook construction, benchmark calculations, and audit-report drafting. I opened the workbook in Excel and reported the results of the five manual checks described above. I remain responsible for verifying the calculations, assumptions, and submitted files.
