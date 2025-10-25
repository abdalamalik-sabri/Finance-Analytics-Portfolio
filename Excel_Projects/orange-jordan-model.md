# 📊 Orange Jordan — Integrated 3-Statement Model

**Deliverable:** `orange-3-statement-model.xlsx` with linked statements, dashboards, and valuation scenarios + `orange-jordan-dashboard.pdf` snapshot.

## 🎯 Objective
Build a driver-based forecast for Orange Jordan that ties together income statement, balance sheet, and cash flow projections to evaluate dividend policy, CAPEX investments, and valuation outcomes.

## 🔍 What’s Inside
| Tab | Description |
| --- | --- |
| `Assumptions` | Revenue growth, churn, ARPU, CAPEX, working-capital, and cost structure drivers through 2029. |
| `Income Statement`, `Balance Sheet`, `Cash Flow` | Fully linked statements with circularity checks and dynamic formatting. |
| `Valuation` | Discounted cash-flow (DCF) model with WACC, terminal value, and scenario toggles. |
| `Dashboard` | Executive view of KPIs (revenue, EBITDA, FCF, leverage) plus scenario comparison visuals. |

## 🛠️ Methodology & Tools
- Modeled subscription economics using **top-down market sizing** blended with churn and ARPU assumptions.
- Linked statements with Excel’s dynamic arrays, `SUMPRODUCT`, and `INDEX/XMATCH` to ensure one source of truth.
- Created switchable scenarios (base, stretch, downside) via data validation + `CHOOSE()` logic for instant sensitivity review.
- Designed dashboard elements using sparklines, in-cell charts, and color-coded KPI cards for stakeholder presentations.

## 📚 Data Notes
- Historical financials derived from **Orange Jordan public filings and investor presentations**.
- Forecast drivers mix public telecom benchmarks with analyst consensus ranges.

## 💡 Business Impact
The model quantifies cash generation capacity and supports capital allocation choices (dividends vs reinvestment). Scenario toggles help executives understand how churn, pricing, or CAPEX shifts influence free cash flow and valuation.

## ▶️ How to Use
1. Adjust key drivers in the `Assumptions` tab to reflect updated market intelligence.
2. Review resulting financial statements to ensure balance sheet integrity (automated balance checks provided).
3. Use the `Dashboard` and `Valuation` tabs when briefing leadership—scenario controls update the visuals in real time.
