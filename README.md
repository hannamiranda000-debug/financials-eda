# Financials EDA — Profitability & Discount Policy Analysis

An end-to-end financial data analysis of a company's transactional records (2013–2014), built across **Excel, Python, and SQL** to answer one question:

> **Where is the company making money, where is it losing money, and what pricing/discount decisions would improve profitability?**

The same financial data is analyzed three ways — each tool demonstrates a different analytical capability — and all three converge on the same findings and recommendations.

---

## Executive Summary

| Metric | Value |
|---|---|
| Total Revenue | $118,726,350.29 |
| Total Profit | $16,893,702.29 |
| Profit Margin | 14.23% |
| Cost of Goods Sold (COGS) | $101,832,648.00 |
| COGS / Revenue | 85.77% |
| Transactions | 700 |
| Period | 2013–2014 |
| Markets | 5 (Canada, France, Germany, Mexico, USA) |
| Products | 6 (Amarilla, Carretera, Montana, Paseo, Velo, VTT) |

**Headline:** Profitability is thin (14.23% margin) and discount policy is the single largest controllable driver of profit. The **Low discount tier earns ~3x more profit per unit ($23.64) than the High discount tier ($8.51)**. The USA generates the highest revenue but converts worst (11.97% margin). One product — Paseo — drives 28% of total profit.

---

## Key Findings

1. **Margins are thin.** COGS consumes 85.77% of revenue, leaving a 14.23% blended margin.
2. **The USA generates the most revenue but converts worst.** Highest revenue ($25.0M) yet lowest margin (11.97%) of all five markets. The gap is discount structure, not pricing power.
3. **Discount policy is the largest controllable lever.** The Low discount tier earns ~3x more profit per unit than the High tier. This effect is statistically significant in the regression model.
4. **Product concentration risk.** Paseo contributes 28% of total profit ($4.80M of $16.89M) — a single-product dependency worth monitoring.
5. **Seasonal concentration.** Q4 (Oct–Dec) accounts for 45% of annual transaction volume, with October alone at 20%.
6. **France converts best.** Highest margin (15.53%) and highest profit ($3.78M) despite lower revenue than USA.

---

## Recommendations

| Priority | Action | Expected Financial Impact |
|---|---|---|
| 1 | Cap High-discount exposure in the USA; shift volume toward Low tier | +2–3pp margin → ~$500K–750K profit uplift |
| 2 | Reduce High-discount share across all markets; reserve for clearance only | Every 1% shift High → Low adds ~$28K profit |
| 3 | Stop discounting Paseo — it converts at full price | Recovers margin on ~$8M of discounted Paseo revenue |
| 4 | Target 1% COGS reduction via supplier/logistics renegotiation | Adds ~$1.19M directly to profit |
| 5 | Front-load inventory and staffing into Q4 | Reduce stockouts and lost revenue during peak |
| 6 | Replicate France's Low-discount mix in USA and Mexico | Lift lowest-margin markets toward 14%+ |

---

## Project Structure

```
financials-eda/
├── README.md                          ← this file
├── Financials.xlsx                    ← Excel workbook (financial analysis + pivots + recommendations)
├── Financials_Python_EDA.ipynb        ← Python notebook (cleaning + financial EDA + regression)
├── Financials_SQL_Analysis.ipynb      ← SQL notebook (15 senior-level financial queries)
├── financials_output/                 ← Python outputs
│   ├── financials_cleaned.csv
│   ├── country_summary.csv
│   ├── product_summary.csv
│   ├── discount_summary.csv
│   ├── regression_summary.txt
│   └── 8 charts (PNG)
└── sql_output/                        ← SQL outputs
    ├── q01_core_kpis.csv
    ├── q02_country_performance.csv
    └── ... (13 more query results)
```

---

## Tools Used & Why

| Tool | Purpose |
|---|---|
| **Excel** | Financial pivots, cross-tabulations, interactive workbook, recommendations |
| **Python (pandas, statsmodels)** | Data cleaning, distribution analysis, OLS regression |
| **SQL (DuckDB)** | Query-layer financial analysis, window functions, CTEs, joins |
| **Tableau Public** | Interactive financial dashboard (see link below) |

Each tool tells the same financial story. Together they demonstrate the full financial analyst workflow.

---

## Approach

### 1. Financial Data Cleaning
- Stripped currency formatting, handled bracketed negatives and placeholder dashes
- Parsed transaction dates, reconciled totals against the raw file
- Engineered three derived columns: Margin, Discount_Pct, Profit_Outlier

### 2. Financial Analysis
- **Descriptive:** revenue, COGS, profit, margin, skewness, percentiles, outlier flagging
- **Segmented:** by market, product, discount tier, month
- **Cross-tabulated:** Market × Discount, Product × Discount
- **Inferential:** OLS regression `Profit ~ DiscountBand + Country + Product`

### 3. Outputs
- Excel workbook with financial pivots and chart takeaways
- Python notebook with reproducible financial EDA + regression
- SQL notebook with 15 queries covering aggregations, window functions, CTEs, joins

---

## Interactive Dashboard (Tableau Public)

👉 **[Click here to view the interactive Tableau dashboard](PASTE_YOUR_TABLEAU_LINK_HERE)**

![Dashboard preview](tableau_preview.png)

The live dashboard lets you filter by market, product, and discount tier interactively.

---

## Regression Summary

Model: `Profit ~ C(DiscountBand) + C(Country) + C(Product)`

- **R²:** see `financials_output/regression_summary.txt`
- **Discount tier coefficients:** statistically significant (p < 0.05) — confirms discount structure is a genuine driver of profitability
- **Market and Product** are also significant predictors of profit

---

## Limitations

- **Time span:** 2013–2014 only; no multi-year trend
- **No cost inflation data:** price vs volume effects cannot be separated
- **Currency unlabeled:** treated as generic monetary units
- **No customer-level data:** segment analysis is aggregate
- **Discount % assumed linear:** real discount ladders may be non-linear

---

## Next Steps

- Fit a mixed-effects model with month as a random effect
- Build a what-if simulation under alternative discount policies
- Segment margin analysis: which segments subsidize which?
- Cohort 2013 vs 2014 to detect mix shift over time

---

## How to Reproduce

1. Clone the repo
2. Ensure `Financials.csv` is in the root (or update paths)
3. **Python:** open `Financials_Python_EDA.ipynb` in Colab or Jupyter, run top-to-bottom
4. **SQL:** open `Financials_SQL_Analysis.ipynb` in Colab; installs DuckDB automatically
5. **Excel:** open `Financials.xlsx` and refresh pivots if needed

---

## Author

**Hanna Lourdes Miranda**
Financial Data Analyst

- **LinkedIn:** Hanna Miranda
- **Email:** hannamiranda000@gmail.com

---

*Financial data analysis performed with Excel, Python, and SQL. All findings reconciled across the three tools.*
