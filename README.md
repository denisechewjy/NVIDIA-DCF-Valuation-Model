# NVIDIA DCF Valuation Model
<img width="1751" height="515" alt="Screenshot 2026-10-06 154203" src="https://github.com/user-attachments/assets/60b3d230-8c62-41ce-b133-6e64f96cf069" />

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

### Unlevered Free Cash Flow (FCF)** 
`EBIAT + D&A − CapEx − Change in NWC`

### 


