# Prompt log

## 2026-10-09

**What I asked:** Build the repository skeleton, tailor AGENTS.md from the baseline and my resume, write CLAUDE.md, .gitignore and this log, and put my resume into RESUME.md without changing what it says. Show every file before I commit anything.

**What was produced:** The directory skeleton with one-line READMEs in empty folders, README.md as a one-line placeholder (none existed), CLAUDE.md, .gitignore, AGENTS.md tailored to marketing and digital analytics, RESUME.md as Markdown, and this entry.

**What was wrong and how it was caught:** My first message ended before the resume text, and the model noticed the gap, built only the parts that did not depend on it, and asked for the resume. The resume then arrived pasted twice; the two copies read as identical in wording and differ only in spacing, so one was used. The resume has no name or contact header, so none was added. The AGENTS.md data-to-never-paste list was inferred from the resume's roles, so I need to read it and edit it to match what I actually handle.

## 2026-10-09 (second entry, same day)

**What I asked:** Add a header to RESUME.md with my name, email address and LinkedIn link.

**What was produced:** A header at the top of RESUME.md: my name as the title, then the email and the LinkedIn link on one line. Nothing else in RESUME.md changed.

**What was wrong and how it was caught:** Nothing wrong that I found. I checked the top of the file and that the rest was unchanged.

## 2026-10-09 (third entry, same day)

**What I asked:** Remove my email address from the RESUME.md header, because the repository is public, and help me create the repository and commit.

**What was produced:** RESUME.md with the header reduced to my name and LinkedIn link, and steps for creating the repository and committing on github.com.

**What was wrong and how it was caught:** Nothing wrong that I found. I checked that the email appears nowhere else in the repository.

## Stage 2 — FX Hedging Model Specification: AI Review

**Project:** FIN 321, Scenario 27 — LNG Marketer  
**AI Tool:** ChatGPT  
**Review Date:** November 6, 2026

### Purpose
I used ChatGPT to review and improve my initial FX hedging model specification. My goal was to make the document detailed enough for an AI assistant or another analyst to build the Excel workbook accurately in Stage 3.

### Prompt Summary
I asked ChatGPT to review my Stage 2 specification against the assignment requirements, identify missing components, and guide me through revising each section in GitHub.

### AI Feedback
ChatGPT identified several areas for improvement:

1. The original inputs table used general descriptions rather than the required Excel named ranges.
2. The workbook architecture needed separate worksheets for each hedging strategy.
3. The assumptions needed more precise interest-rate conventions and premium timing.
4. The calculation flow needed explicit formulas and a covered interest rate parity check.
5. The sensitivity analysis and validation rules needed specific formulas and measurable tests.
6. The model outputs needed clearer definitions for financial comparisons and decision-making.

### Revisions Made
Based on this feedback, I revised Sections 2–8 of `capabilities/fx-hedging/spec.md`. I added all ten required named ranges, expanded the workbook architecture to eight worksheets, specified the ACT/360 interest convention, and documented the forward, money-market, put-option, and call-option calculations. I also added 11 sensitivity scenarios, validation checks, and detailed output requirements.

### Specific Before-and-After Improvement
**Before:** The original specification listed inputs such as 'EUR Receivable,' 'Spot Exchange Rate,' and 'EUR Interest Rate' without standardized Excel names.

**After:** I replaced these descriptions with named ranges such as `FC_AMT`, `S0_in`, `R_FC`, and `R_USD`, and added the missing `K_CALL` input. This makes the specification easier to implement consistently in Excel and reduces the risk of formula-reference errors.

### Reflection
This review helped me understand that a financial model specification needs more than general descriptions. Explicit inputs, formulas, assumptions, and validation rules make the model easier to build, audit, and reproduce. I reviewed and committed the revisions to GitHub in preparation for Stage 3.


## Stage 2 — Final Specification Revision

**AI Tool:** ChatGPT  
**Date:** November 6, 2026  
**Task:** Condensing the FX Hedging Model Specification

### Prompt Summary
I asked ChatGPT to help condense my Stage 2 FX Hedging Model Specification after discovering that my original document was approximately eight pages long, exceeding the professor's 2–3-page guideline.

### AI Assistance
ChatGPT reviewed my specification and identified repetitive explanations and areas where the writing could be more concise. It helped me create a shortened version while preserving the eight required sections, ten named ranges, workbook architecture, hedging calculations, sensitivity analysis, and validation rules.

### Revisions Made
I reviewed the condensed specification and replaced my original `spec.md` file with the revised version. The updated document is approximately three pages long using 12-point font in Google Docs, meeting the assignment's length guideline.

### Reflection
This revision helped me understand the importance of balancing technical detail with clarity. Although my original specification contained extensive explanations, I learned that a concise and organized document can communicate the same essential information more effectively. The final specification provides a clearer blueprint for developing my Excel hedging model in Stage 3.

## Stage 3 — FX Hedging Model Build and Audit

**Course:** FIN 321  
**Scenario:** 27 — LNG Marketer  
**AI Tool:** ChatGPT  
**Date:** November 13, 2026

### Purpose
I used ChatGPT to help build and audit an Excel-based foreign exchange hedging model using the specifications developed in Stage 2. The objective was to create a functional workbook that compares the financial outcomes of different hedging strategies for a €21,500,000 receivable due in 91 days.

### Prompt Summary
I asked ChatGPT to use my Stage 2 model specification to generate an Excel workbook containing ten named ranges, eight worksheets, formula-driven hedging calculations, a sensitivity analysis, and validation checks. After generating the workbook, I asked ChatGPT to guide me through auditing the calculations and identifying any discrepancies.

### AI Assistance
ChatGPT helped develop the workbook architecture, implement formulas for the forward hedge, money-market hedge, protective EUR put, and EUR call reference, and create 11 exchange-rate sensitivity scenarios with a comparison chart. It also guided me through five audit checks to verify the workbook's calculations and expected behavior.

### Audit Findings
1. **Forward Hedge:** Verified that the formula-driven proceeds equal $25,053,950.00.
2. **Money-Market Hedge:** Confirmed that the borrowing, conversion, and investment calculations produce $25,198,514.60 in settlement proceeds.
3. **Currency Options:** Verified the put and call premium calculations, option payoffs, and net results against the expected figures.
4. **Sensitivity Analysis:** Confirmed that all 11 scenarios were included and that the four strategies responded appropriately to exchange-rate changes.
5. **Validation Rules:** Confirmed that the covered interest rate parity check displayed a WARNING while the remaining checks displayed PASS.

### Revisions and Limitations
The audit identified a discrepancy between the indicative forward rate and the forward rate implied by the illustrative interest rates. Rather than changing the assumptions to eliminate the warning, I retained the discrepancy and documented it for further investigation. The model still uses illustrative spot and interest-rate inputs, which will need to be verified or replaced with sourced market data in Stage 4.

### Reflection
This process helped me understand how AI can support financial modeling while still requiring human oversight. By reviewing the formulas and testing the model's results, I gained a better understanding of how different hedging strategies affect USD cash flows. I also learned that identifying and documenting a model warning is an important part of financial analysis rather than something that should automatically be corrected without investigation.

## Stage 4 — Market Data and Workbook Population (November 19–20, 2026)

**AI Tool Used:** ChatGPT (OpenAI)

**Purpose:** To collect and document market observations, populate the existing FX hedging workbook, calculate covered interest parity, and validate the updated model for Scenario 27 — LNG Marketer.

**Key Prompts and AI Assistance:**

1. Requested step-by-step assistance finding the November 19, 2026 EUR/USD spot rate and one-year USD and EUR interest rates.
2. Used ChatGPT to organize market-data values, source links, observation dates, and modeling limitations.
3. Requested guidance calculating the covered interest parity (CIP) implied forward rate and interpreting the discrepancy with the scenario's bank forward quote.
4. Followed ChatGPT's instructions to update the Excel workbook's named inputs without changing the existing formulas.
5. Used AI-generated expected results to check the forward, money-market, currency-options, and sensitivity worksheets.
6. Documented workbook validation results and the CIP warning in the market-data memo.

**Human Verification and Decisions:**

- Selected November 19, 2026 as the market observation date.
- Recorded the EUR/USD spot rate of 1.0967, USD rate of 4.62%, and EUR rate of 3.343%, using the identified historical sources.
- Retained the original scenario's 91-day maturity, indicative forward quote, and option premiums.
- Set both option strikes to 1.0967 USD/EUR as an at-the-money modeling assumption.
- Manually updated the workbook and confirmed that all hedge calculations remained formula-driven.
- Verified all 11 sensitivity scenarios and the chart.
- Confirmed that CIP displayed WARNING while all other validation checks displayed PASS.
- Saved and committed the updated workbook and market-data memo to GitHub.

**Limitations and Lessons Learned:**

The one-year interest-rate benchmarks are proxies for a 91-day exposure and do not represent executable corporate borrowing or investment rates. The option strikes were assumed rather than obtained as bank quotes. The bank's indicative forward quote differs materially from the CIP-implied rate, so the discrepancy was documented rather than suppressed. AI-assisted calculations were checked against the Excel workbook, but the historical market observations and their precise publication timestamps require independent source verification.

**Deliverables:**

- `capabilities/fx-hedging/model.xlsx`
- `data/2026-11-19-lng-marketer-market-data-memo.md`
- `prompt-log.md`
