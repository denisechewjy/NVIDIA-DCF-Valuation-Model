# NVIDIA DCF Valuation Model
<img width="1751" height="515" alt="Screenshot 2026-10-06 154203" src="https://github.com/user-attachments/assets/60b3d230-8c62-41ce-b133-6e64f96cf069" />

## Motivation
I built this model to learn DCF valuation hands-on using a real, high-profile company. NVIDIA was a natural choice as it is a leader in artificial intelligence chips, controlling roughly 90% of the data center GPU market and driving a valuation above US$5 trillion. Additionally, its rapid revenue growth driven by AI/data centre demand makes it an interesting and challenging subject to value, precisely because standard assumptions (stable margins, predictable growth) don't apply cleanly. Working through the calendarization, scenario construction, and terminal value mechanics on a live company made the concepts stick in a way that theory alone wouldn't.

## Introduction
This project is a Discounted Cash Flow (DCF) valuation model for NVIDIA Corporation (NASDAQ: NVDA), built in Microsoft Excel. It estimates NVIDIA's intrinsic value by projecting future free cash flows and discounting them back to the present. 

This model relies on consensus analyst estimates and is designed to be dynamic. It allows users to toggle between base, conservative, and optimistic cases to test how different inputs — like the WACC or terminal growth rate — impact the implied share price.

While this model provides a baseline valuation, real-world valuation often requires digging deeper into management models and segment-specific revenue streams. 

## Model Overview
The workbook contains four sheets:
| Sheet | Purpose |
| ----------- | ----------- |
| IS | Historical NVIDIA Income Statements (FY2018–FY2026) |
| CFS | Historical Cash Flow Statements (FY2018–FY2026) |
| WACC | Weighted Average Cost of Capital calculations |
| DCF Model | Core valuation — projections, FCF build, terminal value, implied price |

## Methodology and Formulas
### Calendarization
`CY = (11/12) × FY(t+1) + (1/12) × FY(t)`
  
NVIDIA's fiscal year ends in late January (~Jan 31). All historical and projected financials are converted to a calendar year ending December 31 using the above formula.



### Unlevered Free Cash Flow (FCF) 
`EBIAT + D&A − CapEx − Change in NWC`

### 

### Key Assumptions
| Parameter | Conservative | Street/Base | 	Optimistic | 
| ----------- | ----------- | ----------- | ----------- |
| WACC | 	14.95% | 14.45% | 12.50% |
| Terminal Growth Rate | 2.0% | 2.5% | 3.0% |
| Revenue Growth (CY2030) | ~10% | ~15% | ~20% |
| Effective Tax Rate | Trending to 17% by CY2030 

- **Beta**: 2.22 (5-year monthly vs S&P 500)
- **Risk-Free Rate**: 5.275% (10-year US Treasury)
- **Market Risk Premium**: 4.14%
- **Diluted Shares Outstanding**: ~24,150M (post 10:1 split, June 2024)

## Conclusion


## Scenario Analysis
The model supports three scenarios toggled via dropdown switches on the DCF sheet:
- **Conservative** : Higher discount rate, lower terminal growth, below-consensus revenue ramp.
- **Street/Base**: Consensus analyst estimates for revenue and EBIT, mid-range WACC and TGR.
- **Optimistic**: Lower discount rate reflecting re-rating potential, above-consensus growth.

## Limitations & Disclaimer
- This model is built for educational and analytical purposes only.
- Consensus estimates beyond CY2028 have sparse analyst coverage (3–5 analysts) and carry significant uncertainty.
- NVIDIA operates in a rapidly evolving AI/semiconductor industry; realized results may differ materially from projections.

## Data Sources
- **Historical financials**: NVIDIA 10-K filings (SEC EDGAR).
- **Consensus revenue & EBIT estimates (FY2027–FY2031)**: Wall Street consensus (FactSet/Bloomberg; calendarized to CY).
- **Risk-free rate**: US 10-Year Treasury yield.
- **Beta**: 5-year monthly regression vs S&P 500.
- **Cash & debt**: NVIDIA FY2026 balance sheet (as of latest quarter Jul 26, 2026).
