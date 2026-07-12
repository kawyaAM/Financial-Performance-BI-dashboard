# Financial Performance & Business Intelligence Dashboard

## Overview
An interactive dashboard analyzing 15 years (2009–2023) of financial performance across 12 major public companies, built to answer: **How has each company performed over time, and how do they compare?**

## Business Question
- How has revenue and profitability evolved across companies and industries from 2009 to 2023?
- Which companies are the strongest performers, and how does their growth compare?
- Are there notable trends, anomalies, or shifts worth investigating (e.g. around 2020)?

## Data Source
- **Dataset:** [Financial Statements of Major Companies (2009–2023)](https://www.kaggle.com/datasets/rish59/financial-statements-of-major-companies2009-2023) (Kaggle)
- **Scope:** 12 companies (AAPL, AMZN, GOOG, MSFT, NVDA, PYPL, MCD, INTC, AIG, BCS, PCG, SHLDQ) across Tech, Finance, Food, and Manufacturing sectors
- **Fields:** Revenue, Net Income, Gross Profit, EBITDA, Market Cap, Cash Flow (Operating/Investing/Financing), and key ratios (ROE, ROA, ROI, Net Profit Margin, Current Ratio, Debt/Equity)

## Tools & Method

**Excel (Power Query)**
- Cleaned raw data: fixed inconsistent category labels (e.g. "BANK" vs "Bank"), trimmed whitespace, corrected data types
- Built a Revenue Growth % calculated column using conditional row-comparison logic (sorted by Company, then Year)

**Power BI**
- Modeled the data as a **star schema**: `Financial_Statements` (fact table) linked to `Dim_company` and `Dim_Date` dimension tables via one-to-many relationships
- Built custom **DAX measures**, including a hand-built year-over-year growth calculation (`FILTER`/`ALL`/`MAX` pattern, used in place of `DATEADD` since Year is stored as a whole number rather than a true date type)
- Designed an interactive dashboard: KPI cards, revenue trend line, company comparison bar chart, YoY growth chart, and a company slicer for cross-filtering

## Key Insights
1. **Overall growth:** Combined revenue across all 12 companies grew substantially from 2009 through 2022, reflecting broad multi-sector expansion over the period.
2. **Apple leads the group:** AAPL is the top revenue generator among the 12 companies, closely followed by Amazon — together they account for a disproportionate share of total revenue in the dataset.
3. **Profitability:** Average net profit margin across all companies and years sits around 13.7%, though this varies meaningfully by sector (e.g. tech vs. finance vs. manufacturing) — a natural next area to drill into.

## Data Quality Notes
- Identified and corrected inconsistent category labels during cleaning (data quality issue, not a business signal)
- Noted a sharp anomaly in 2023 figures (a steep single-year drop for at least one company) that appears to reflect incomplete or partial-year reporting in the source dataset rather than an actual business event — flagged rather than smoothed over, since honest handling of messy real-world data is part of the analysis

## Skills Demonstrated
- Data cleaning & transformation (Power Query / Excel)
- Data modeling (star schema design, fact/dimension tables)
- DAX (time-intelligence workarounds, custom growth measures)
- Dashboard design & interactivity (slicers, cross-filtering, KPI cards)
- Data quality auditing and transparent reporting of limitations

## Files in This Repository
- `financial_statements_cleaned.xlsx` — cleaned source data with Excel-based Revenue Growth % calculation
- `financial_dashboard.pbix` — Power BI file with full data model, DAX measures, and dashboard
- Dashboard screenshot (`.png`)
