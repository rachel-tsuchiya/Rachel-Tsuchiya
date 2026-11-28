Hi! My name is Rachel Tsuchiya and I am a senior-standing student at the University of Hawaii at Manoa. I am currently studying Marketing and Finance at the Shidler College of Business.
I am passionate about consumer behavior, brand strategy, and creating meaningful connections between brands and their audiences. 

## FIN 321 — FX Hedging Project

### Scenario 27: LNG Marketer

This project evaluates foreign exchange hedging strategies for an LNG marketer expecting to receive €21.5 million in 91 days. The analysis compares an unhedged position, forward contract, money-market hedge, and EUR currency options to determine how the company can manage exchange-rate exposure and protect its future USD cash flows.

The project follows a five-stage workflow involving financial analysis, capability specification, Excel modeling, market-data integration, and independent AI validation.

### Project Deliverables

| Stage | Deliverable | Link |
|---|---|---|
| 2 | FX Hedging Capability Specification | [View Specification](capabilities/fx-hedging/spec.md) |
| 3 | Excel Hedging Model | [View Workbook](capabilities/fx-hedging/model.xlsx) |
| 4 | Market-Data Memo | [View Market Data](data/2026-11-19-lng-marketer-market-data-memo.md) |
| 5 | Independent AI Analysis | [View AI Output](analysis/2026-11-27-lng-marketer-independent-ai-output.md) |
| 5 | Validation Analysis | [View Validation](analysis/2026-11-27-lng-marketer-validation-analysis.md) |
| 5 | CFO Decision Memo | [View Decision Memo](docs/decisions/2026-11-27-lng-marketer-hedge-decision-memo.md) |

### Key Findings

Using the November 19, 2026 market-data assumptions, the forward hedge produced the highest modeled USD proceeds of **$25,053,950**, compared with approximately $23.65 million for the money-market hedge.

The analysis identified a significant discrepancy between the bank's indicative forward rate of 1.1653 USD/EUR and the covered interest parity implied rate of approximately 1.10021 USD/EUR.

The final recommendation is to pursue the forward hedge **only if the bank confirms executable terms**, with further due diligence required before implementation.

### AI Validation and Documentation

The project includes an independent AI calculation of the hedge outcomes, comparison against the Excel workbook, manual verification of key formulas, and documentation of modeling assumptions and limitations.

A record of AI-assisted development is maintained in the [Project Prompt Log](prompt-log.md).
