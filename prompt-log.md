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
