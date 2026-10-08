# E-commerce Sales and Profit Analysis — Findings

Synthetic portfolio data, calendar 2025. All monetary amounts are INR.

## Overview

| Metric | Result |
|---|---:|
| Orders | 1,200 |
| Distinct customers | 296 |
| Sales after discounts | 5,489,435 |
| Profit after product and shipping costs | 1,171,445 |
| Profit margin | 21.34% |
| Average order value | 4,574.53 |
| Loss-making orders | 79 (6.58%) |

Profit excludes tax, returns and overhead. These are simulated results, not real company performance.

## Findings and proposed actions

**1. October leads sales.** It generates INR 710,310 from 153 orders and INR 158,610 in profit. May has the lowest sales at INR 326,895. For an equivalent real business, compare inventory capacity with high-volume months. Here, month weights in the generator intentionally favor the last quarter, so the pattern is partly designed and cannot demonstrate market seasonality.

**2. Fashion generates the most profit.** It contributes INR 496,425 at a 39.80% margin. Electronics sells more—INR 2,127,855—but has an 18.45% margin. Home has a 13.35% margin. All three categories remain profitable overall. Prioritize investigation of category costs and discount policies before allocating more stock purely on revenue.

**3. Revenue and profit leaders differ by region.** West leads sales at INR 1,428,130, while North leads profit at INR 312,330. Compare product mix and discount levels before changing regional marketing budgets. Ten orders with missing regions remain in an explicit Unknown group and contribute INR 32,520 of sales.

**4. Sneakers generate the most product profit.** They contribute INR 253,000. Backpacks lead unit volume at 389 units. Office chairs generate the most product sales at INR 1,519,925 but only INR 101,485 profit. Sales, unit volume and profit answer different business questions.

**5. The 35% discount group is loss-making.** Its 184 orders generate INR 621,010 sales and a loss of INR 4,240, a −0.68% margin. The no-discount group has a 33.53% margin. Consider product-level discount limits. The data does not measure demand response: discounts are sampled independently, and lower discounts mechanically increase per-order profit when all else is fixed. Do not claim that reducing discounts will preserve sales volume or cause a specific profit uplift.

**6. Losses are concentrated in office-chair orders.** Among only loss-making orders, 33 office-chair orders lose INR 42,200. This is a loss-subset figure; office chairs are profitable in aggregate. A useful review rule is to flag orders where sales fall below product cost plus shipping. The break-even discount for an order is `1 − (quantity × unit_cost + shipping_cost) / (quantity × unit_price)`.

## Validation

- 1,220 raw rows become 1,200 unique orders after removing 20 exact duplicates.
- Fifteen inconsistent region labels are normalized; ten missing labels remain Unknown.
- Sales calculated independently from raw unique orders match SQL totals.
- Monthly sales sum to the overall sales total.
- The Excel sales and profit totals match SQL. Changing a quantity updates the linked sales KPI, and the temporary change is restored.

## Interview explanation

“This is a practice project using synthetic e-commerce data. I studied the cleaning rules, used SQL to compare sales and profitability, and explored the results in an Excel dashboard. The main lesson is that high sales do not always mean high profit. For example, office chairs lead sales, but sneakers lead profit. I also found that the 35% discount group loses money in this sample. These are simulated patterns, so a real pricing decision would need customer demand and cost data.”

Use this explanation only after studying and running the project. Describe your own contributions accurately.
