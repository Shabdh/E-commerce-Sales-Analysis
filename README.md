# E-commerce Sales and Profit Analysis

A beginner portfolio project using SQL, Excel and reproducible Python scripts.

**Data disclosure:** This is synthetic practice data, not records from a real company. It was generated with seed 42. Prices, costs, discounts, order timing and customer IDs are invented. Findings demonstrate an analysis workflow and do not establish real market trends.

## Start here

1. Open `Ecommerce_Dashboard.xlsx` in Excel. The Dashboard shows KPIs and three editable charts. The Orders tab contains filterable records and calculated columns.
2. Read `REPORT.md` to understand the findings and recommendations.
3. Read `sql/01_clean.sql` and `sql/02_analysis.sql` to understand the cleaning and queries.
4. Open `dashboard.png` for a quick preview or portfolio screenshot.

The workbook and CSV files can be inspected without running code. No Power BI installation is needed. A native Power BI `.pbix` file is not included.

## Business questions

- Which month generates the most sales?
- Which categories generate the most profit?
- Which region leads sales, and does it also lead profit?
- Which products sell the most units and generate the most profit?
- How does profitability vary across discount levels?
- Which products contribute to loss-making orders?

## Data and definitions

Period: 1 January–31 December 2025. Currency: INR. The dataset contains 1,200 orders, 296 distinct customers, nine products and three categories. **One row represents one order containing one product with one or more units.** Consequently, the order ID is unique. Real multi-product orders would require an order-line ID and distinct order counts.

| Field | Meaning |
|---|---|
| order_id | Unique synthetic order ID |
| order_date | ISO date, YYYY-MM-DD |
| customer_id | Synthetic customer ID; customers can repeat |
| region | North, South, East, West or Unknown |
| category / product | Product classification and name |
| quantity | Units in the order |
| unit_price | List price per unit, INR |
| discount_rate | Fraction of list price deducted; 0.10 means 10% |
| unit_cost | Product cost per unit, INR |
| shipping_cost | Cost per order, INR |
| gross_sales | quantity × unit_price |
| sales | gross_sales × (1 − discount_rate), rounded to two decimals |
| product_cost | quantity × unit_cost |
| profit | sales − product_cost − shipping_cost |
| month | Calendar month key, YYYY-MM |

Profit is contribution after product and shipping costs, **not accounting net profit**. Taxes, returns, salaries, marketing and other overheads are excluded. Profit margin = total profit / total sales. Average order value = total sales / distinct orders. Never average individual order margins to calculate the overall margin.

## Cleaning process

The generator creates 1,220 raw rows. SQL removes 20 exact duplicate rows, normalizes 15 lowercase/padded region values and labels 10 missing regions `Unknown`. Missing regions are retained so totals stay complete. A unique index rejects conflicting duplicate IDs rather than silently dropping them. Dates are generated as valid ISO dates. The script validates row counts, numeric ranges, unique IDs and aggregate sales.

## Reproduce the analysis

From this project folder, run:

```bash
python3 scripts/run_analysis.py
```

Only Python's standard library is required. This command regenerates the sample data and overwrites the included SQLite database and CSV/JSON query results. It does **not** refresh the workbook or the written report. Read the Excel refresh instructions below before using changed data.

To explore the existing database using a SQLite client:

```sql
SELECT product, SUM(profit) AS profit
FROM orders
GROUP BY product
ORDER BY profit DESC;
```

`sql/02_analysis.sql` contains seven named queries. Their exported results are in `results/`. The database includes both raw and cleaned tables.

## Excel use and refresh

- The Dashboard summarizes all 1,200 rows. Filtering the Orders table does not filter Dashboard KPIs or charts.
- Edit existing Orders input cells A:K to recalculate dependent formulas and charts. L:P are calculated columns.
- Dashboard formulas use fixed rows 5:1204. To append data, extend the Orders table, copy formulas in L:P and extend all Dashboard source ranges. Add any new categories, regions, discount values or months to the relevant summary and chart ranges.
- Written findings and PNG screenshots are snapshots. Update them after changing data.
- Excel-compatible formulas were recalculated and checked during generation. Native Excel and Power BI application testing was not performed.

## Optional Power BI extension

Import `data/clean_orders.csv`. Set `order_date` to Date, IDs to Text, quantity to Whole Number, discount_rate to Decimal Number and monetary fields to Decimal Number. Use the measures in `powerbi_measures.dax`. Create KPI cards, a month sales line chart, category profit bars and region/category slicers. Sort the YYYY-MM month key ascending. This is a guided extension, not a claim that a Power BI dashboard is already built.

## Put it on GitHub

1. Unzip this project and create a repository named `ecommerce-sales-analysis`.
2. Upload the extracted project files, with README.md at the repository root.
3. Add your name and any changes you independently make. Keep the synthetic-data disclosure.
4. Include the dashboard image and link to your repository in the internship application.

Suggested description: “Portfolio analysis of 1,200 synthetic e-commerce orders using SQL and Excel, with reproducible data cleaning, profitability metrics and an editable dashboard.”

Before presenting it, be able to explain duplicates, missing values, margin, average order value, the difference between sales and profit, and why synthetic discount patterns do not prove real customer behavior.

## Files

- `Ecommerce_Dashboard.xlsx`: formula-driven dashboard and order details
- `dashboard.png`: dashboard screenshot
- `data/`: raw CSV, clean CSV and SQLite database
- `sql/`: cleaning and business analysis queries
- `results/`: reproducible query output tables and JSON
- `scripts/run_analysis.py`: seeded generation, SQL execution and validation
- `REPORT.md`: findings, recommendations and limitations
- `powerbi_measures.dax`: optional Power BI measures

Generated with AI assistance. Review the code and add your own analysis before describing the work in an interview.
