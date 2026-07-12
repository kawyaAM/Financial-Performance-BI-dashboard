# Financial Performance & BI Dashboard

I built this project to practice the full workflow of a data analyst: taking messy real-world financial data, cleaning it properly, and turning it into something people can actually explore. It covers 12 major public companies (Apple, Amazon, Google, Microsoft, Nvidia, PayPal, McDonald's, Intel, AIG, Barclays, PG&E, and Sears) over 15 years, from 2009 to 2023.

## What I wanted to find out
- How has each company's revenue and profitability changed over time?
- Who are the strongest performers, and how do they compare to each other?
- Are there any surprises or anomalies in the data worth digging into?

## The data
Sourced from Kaggle: [Financial Statements of Major Companies (2009–2023)](https://www.kaggle.com/datasets/rish59/financial-statements-of-major-companies2009-2023). It's pulled from real 10-K filings and includes Revenue, Net Income, Gross Profit, EBITDA, Market Cap, cash flow figures, and financial ratios like ROE, ROA, and Debt/Equity.

## How I built it

**Cleaning (Excel / Power Query)**
The raw data had a few issues I had to fix — the "Bank" category was labeled inconsistently (sometimes "BANK", sometimes "Bank"), there was a stray space in one of the column headers, and I had to make sure numeric columns weren't accidentally stored as text. I also built a Revenue Growth % formula that compares each company's revenue to its own prior year — trickier than it sounds since the data isn't sorted with companies grouped together by default.

**Data modeling (Power BI)**
Instead of dumping everything into one flat table, I split the data into a proper star schema: a fact table (`Financial_Statements`) connected to two dimension tables (`Dim_company` and `Dim_Date`). This is the standard way BI tools are supposed to be modeled, and it makes the DAX measures behave correctly when you filter or slice the data.

**DAX measures**
A few standard ones (Total Revenue, Total Net Income, Average Net Profit Margin), plus a custom Year-over-Year Revenue Growth % measure. I originally tried using DAX's built-in `DATEADD` function for this, but it kept failing — turns out `DATEADD` needs a real Date-type column, and mine was just a whole number (Year). I rebuilt the logic manually using `FILTER` and `ALL` instead, which was a good exercise in understanding what these functions are actually doing under the hood rather than just copying a formula.

**Dashboard**
KPI cards up top, a revenue trend line, a company comparison bar chart, a YoY growth chart, and a company slicer so you can click into any single company and see everything update.

## What I found
- Combined revenue across all 12 companies grew steadily from 2009 up through around 2022.
- Apple is the clear revenue leader in this group, with Amazon close behind.
- Average net profit margin across all companies and years sits around 13-14%, though it varies a lot by industry — banks and tech companies don't look anything alike here.
- There's a sharp, unrealistic-looking drop in 2023 figures for at least one company (visible as a steep spike down in the YoY growth chart). I looked into it and it seems to be incomplete data for that year in the source dataset, rather than an actual business event — I decided to leave it in and flag it rather than quietly fix or hide it, since that felt more honest.

## What this project shows I can do
- Clean and fix real, messy data (not a pre-cleaned dataset)
- Build a proper relational data model, not just one flat table
- Write DAX from scratch, including debugging when a "standard" approach doesn't work
- Design a dashboard that's actually interactive, not just static charts
- Notice and investigate a data quality issue instead of ignoring it

## Files in this repo
- `financial_statements_cleaned.xlsx` — cleaned data with the Revenue Growth % formula
- `financial_dashboard.pbix` — the full Power BI file (data model, DAX, dashboard)
- Dashboard screenshot
