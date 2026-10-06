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
  
NVIDIA's fiscal year ends in late January (~Jan 31). All historical financials are converted to a calendar year ending December 31 using the above formula. The formula reflects that approximately 11 months of a calendar year fall within NVIDIA's next fiscal year and 1 month within the current one.

### Discount Period - Mid-Year Convention
Rather than discounting each year's FCF as if it were received entirely at year-end, the model uses the mid-year convention: cash flows are assumed to be received evenly throughout the year, so each year is discounted at its midpoint (0.5, 1.5, 2.5 … years from valuation date). This produces a more realistic PV than end-of-year discounting.

### Unlevered Free Cash Flow (FCF) 
`EBIAT = EBIT x (1 - Tax Rate)`
  
`FCF = EBIAT + Depreciation & Amortization − CapEx − Change in Net Working Capital`

Each projection year's free cash flow.

### Terminal Value
`Terminal Value = FCF × (1 + g) / (WACC − g)`
  where g is the Terminal Growth Rate and WACC is the discount rate.
    
The terminal value is calculated using the Gordon Growth Model, applied to the final projection year's normalised FCF.

### Present Value of Terminal Value
`PV of TV = TV / (1 + WACC)^n`
  where n is the mid-year discount period for Year 5. 
    
The Terminal Value above is an undiscounted lump sum at the end of Year 5. It must be discounted back to today at the same mid-year-adjusted discount period as the final projection year.

### Enterprise Value
`Sum of present value of FCF + Present Value of Terminal Value`

### Implied Share Price
`Enterprise Value + Cash & Short-term Investments - Total Debt / Diluted Shares Outstanding`

### Key Assumptions
| Parameter | Conservative | Street/Base | 	Optimistic | 
| ----------- | ----------- | ----------- | ----------- |
| WACC | 	14.95% | 14.45% | 12.50% |
| Terminal Growth Rate | 2.0% | 2.5% | 3.0% |
| Revenue Growth (CY2030) | ~10% | ~15% | ~20% |
| Effective Tax Rate | Trending to 17% by CY2030 

- **Beta**: 2.22 (5-year monthly of NVDA vs S&P 500)
- **Risk-Free Rate**: 5.275% (10-year US Treasury at time of model build)
- **Market Risk Premium**: 4.14% (Damodaran implied ERP for the US market)
- **Cost of Equity (CAPM)**: ~14.45% (Cost of Equity = Risk Free Rate + (Beta x Market Risk Premium))
- **Cost of Debt**: 2.4% (Derived from NVDA's interest expense relative to total debt)
- **Diluted Shares Outstanding**: ~24,150M (post 10:1 split, June 2024)
- **Capital Structure**: ~99% equity (NVIDIA's market cap (~$5.6T) dwarfs its debt ($32B), making the debt weight negligible)

### Terminal Growth Rate
- Conservative (2.0%): Approximately zero real growth - only inflation keeps revenue growing
- Street (2.5%): Anchored to long-run US nominal GDP growth
- Optimistic (3.0%): Anchored to long-run global nominal GDP growth
- TGR must stay below WACC for the Gordon Growth Model to be mathematically valid, and should never meaningfully exceed long-run nominal GDP — otherwise the model implies NVIDIA eventually becomes larger than the entire economy.

## Scenario Analysis
The model supports three scenarios toggled via dropdown switches on the DCF sheet:
- **Conservative** : Higher discount rate, lower terminal growth, below-consensus revenue ramp.
- **Street/Base**: Consensus analyst estimates for revenue and EBIT, mid-range WACC and TGR.
- **Optimistic**: Lower discount rate reflecting re-rating potential, above-consensus growth.

## EBIT Margins
Projected EBIT margins (~65%) are derived from consensus EBIT estimates as a percentage of consensus revenue for each year and held approximately constant in the out-years. This is conservative relative to NVIDIA's recent margin expansion trajectory.

## Tax Rate
- Historical weighted average over the past 8 quarters: ~15%.
- NVIDIA's own guidance points to a normalized rate of ~17% as its global footprint and profitability grow.
- The model linearly interpolates from ~15% in CY2026 to ~17% by CY2030.

## Depreciation & Amortization and CapEx
Both are projected as a percentage of revenue, using a 3-year rolling historical average held constant across the projection period. 

## Net Working Capital (NWC)
NWC is projected as a percentage of revenue using a 3-year rolling average. The change in NWC (cash consumed by working capital investment) is then derived year-over-year. A negative change means NWC is growing (cash outflow); a positive change means NWC is shrinking (cash inflow).

## Conclusion
Building this model from scratch reinforced how sensitive a DCF valuation is to a small number of key inputs — WACC and terminal growth rate in particular affecting implied stock price. For a company growing as rapidly as NVIDIA, the terminal value dominates the valuation (accounting for the majority of EV), which means near-term earnings precision matters far less than getting the long-run assumptions right.  

The exercise also highlighted the importance of methodological rigour: errors like discounting with the wrong period, using an undiscounted terminal value in the EV bridge, or confusing a margin with a growth rate are easy to introduce and hard to spot — but they compound significantly. Verifying every formula against its economic intent, not just its output, is as important as the modelling itself.  

NVIDIA remains a genuinely difficult company to value. Its revenue has grown from ~$10B in FY2022 to over $130B in FY2026 on the back of AI infrastructure demand, and whether that trajectory continues, plateaus, or reverses depends on factors — competition, export controls, AI adoption rates, next-generation product cycles. 

## Limitations
- Consensus estimates beyond CY2028 have sparse analyst coverage (3–5 analysts) and carry significant uncertainty.
- NVIDIA operates in a rapidly evolving AI/semiconductor industry; realized results may differ materially from projections.

## Data Sources
- **Historical financials**: NVIDIA 10-K filings (SEC EDGAR).
- **Consensus revenue & EBIT estimates (FY2027–FY2031)**: Wall Street consensus (FactSet/Bloomberg; calendarized to CY).
- **Risk-free rate**: US 10-Year Treasury yield.
- **Beta**: 5-year monthly regression vs S&P 500.
- **Cash & debt**: NVIDIA FY2026 balance sheet (as of latest quarter Jul 26, 2026).
