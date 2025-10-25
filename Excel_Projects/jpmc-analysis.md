# 🧮 Jordan Phosphate Mines Company (JPMC) Financial Review

**Deliverable:** `jpmc-analysis.xlsx` (ratio diagnostics, WACC model) + executive-ready PDF exports.

## 🎯 Objective
Evaluate JPMC’s recent performance and estimate a grounded weighted-average cost of capital (WACC) to inform valuation and funding decisions.

## 🔍 What’s Inside
| Tab | Description |
| --- | --- |
| `Financials` | Cleaned income statement, balance sheet, and cash flow statements (JOD '000). |
| `Ratios` | Liquidity, profitability, and leverage KPIs benchmarked 2022 vs 2023. |
| `WACC` | CAPM-based cost of equity, after-tax cost of debt, capital structure, and WACC output. |
| `Dashboards` | KPI scorecard with conditional formatting and commentary fields. |

## 🛠️ Methodology & Tools
- Modeled equity cost via **CAPM** using Amman Stock Exchange beta proxies and regional risk premiums.
- Calculated cost of debt from interest coverage + borrowing spreads, adjusting for the corporate tax shield.
- Leveraged Excel functions (`XLOOKUP`, `INDEX/MATCH`, dynamic named ranges) to automate ratio rollups and peer comparisons.
- Applied scenario toggles to stress-test changes in leverage and risk-free assumptions.

## 📊 Key Results
- ROE compressed from **48.3% → 26.5%** as equity expanded faster than net income.
- ROA trended downward (34.6% → 20.8%) due to asset base growth and softer profitability.
- Gross margin stabilized around **~59%**, supporting resilient cash generation.
- JPMC’s blended **WACC ≈ 9.1%**, anchored by low-cost debt and elevated equity risk.

## 📚 Data Notes
- Financial statements sourced from **Jordan Phosphate Mines Company annual reports (2022–2023)**.
- Market data (risk-free rates, beta, market premium) compiled from public ASE and Damodaran datasets.

## 💡 Business Impact
The model identifies whether JPMC is creating value above its capital costs, highlighting levers (pricing discipline, asset utilization, capital structure) for strategic planning and investor communications.

## ▶️ How to Use
1. Open `jpmc-analysis.xlsx` and start with the `Dashboard` tab for headline metrics.
2. Adjust key assumptions in the `WACC` tab (risk-free rate, market premium, tax rate) to evaluate sensitivity.
3. Use the `Ratios` view for board or investor presentations—commentary fields auto-update with threshold logic.
