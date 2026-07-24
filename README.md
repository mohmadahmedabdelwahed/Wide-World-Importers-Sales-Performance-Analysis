# Wide-World-Importers-Sales-Performance-Analysis
**Power BI dashboard | Star-schema data modeling | DAX | Business insight generation**
---

## 1. Project overview
A end-to-end Power BI analysis of Wide World Importers' sales data (2013–2016), built to answer a core business question: **is the company growing profitably, or is revenue growth masking margin erosion?**
The project covers data modeling from raw star-schema tables, Power Query cleaning, DAX measure design, and a 9-page interactive report spanning company performance, product profitability, customer concentration, sales team accountability, and geographic performance.
---

## 2. Business problem
Management needed a single source of truth to answer:
- Is revenue growth translating into profit growth, or is margin quietly eroding?
- Which products, customers, and regions actually drive profitability — not just volume?
- Are sales reps being rewarded for revenue at the expense of margin?
- Where is the company overexposed to concentration risk (one customer, one product, one region)?
---

## 3. Data source & model
**Source:** Wide World Importers sample star schema (Microsoft sample dataset)
| Table | Role | Rows (approx.) |
|---|---|---|
| FactSale | Fact table — line-item sales transactions | ~26,000 |
| DimCustomer | Customer dimension (SCD Type 2) | ~400 |
| DimStockItem | Product dimension (SCD Type 2) | ~670 |
| DimEmployee | Salesperson dimension | ~210 |
| DimCity | Geography (city, state, territory) | ~13,000 |
| DimDate | Calendar table (calendar + fiscal) | 1,460 |

**Model:** star schema, single-direction one-to-many relationships from each dimension to FactSale via surrogate keys.
**Data cleaning (Power Query):**
- Removed malformed header rows from DimCustomer and DimStockItem
- Removed the null placeholder row (Stock Item Key 0) with no valid attributes
- Investigated FactSale rows with Customer Key 0 — confirmed these are **legitimate transactions with no customer identification captured**, not broken joins
---

## 4. KPIs measured
| KPI | Definition |
|---|---|
| Total Revenue | Sum of Total Excluding Tax |
| Total Profit | Sum of Profit |
| Profit Margin % | Profit ÷ Revenue |
| Revenue / Profit / Cost / Profit Margin YoY % | Same-period comparison vs. prior year |
| Average Order Value (AOV) | Revenue per distinct invoice |
| Average Profit per Order | Profit per distinct invoice |
| Average Deal Size per Salesperson | Order-level revenue average, calculated per rep |
| % of Total Volume by Product | Product's share of company-wide quantity |
---
## 5. Key insights
**Profitability trend**
- 2015 was the peak year for both revenue ($3.2M) and profit ($6.3M)
- 2014 showed Profit increasing while margin declined — a warning sign later corrected in 2015–2016

**Profitability trend**

- Revenue grew steadily in 2014-2015 before contracting -9.48% in 2016 — the first decline in the dataset. Margin eroded in 2014 (cost growth outpaced revenue growth), stabilized in 2015, then eroded again modestly in 2016 (-0.44pts) as cost reduction (-9.06%) nearly but not fully matched the revenue decline. This suggests the cost base is largely variable/scalable with revenue, but not perfectly — worth investigating which cost components lag behind revenue changes.

**Product performance**
- 4 products (Halloween Zombie Mask variants) combine high sales volume with **negative profit margin (-5.56%)** — a direct cost/pricing issue worth flagging to management, not just a reporting footnote
- One product (Animal Big Feet Slippers, size M) shows high margin (75%) but very low volume (rank 188) — a clear candidate for a marketing push
- No single SKU dominates profit share — the product base is reasonably diversified, which limits single-product concentration risk

**Sales team performance**
- Highest-revenue rep also shows the *lowest* profit margin and The rep with the best profit margin ranks only 7th in total revenue — suggesting revenue is being won through discounting rather than deal quality

**Customer data quality finding**
- ~34% of revenue is associated with unidentified customers (Customer Key 0). Investigation confirmed these are real transactions with complete order data (product, quantity, date) but no customer record captured — reframing this from "customer concentration risk" to a **process/data-capture gap** worth its own recommendation (e.g., enforcing customer capture at point of sale).

**Geographic performance**
- California leads all states in both revenue and profit while Hawaii is the lowest

**Chilled items**
- Total number of invoices is 8k
- Total sales coming from chilled items is 129k which is 0.6% of total sales
- Taj shand has the highest % of total sold chilled items which is 0.9%
- California is the highest state for chilled items sales with $50,786 , and Hawaii is the lowest at $1,436 sales.

**Note**

13 transactions (0.05% of records) have no recorded delivery date, consistent with orders invoiced near the end of the dataset's time range that had not yet shipped. These are excluded from delivery-time slicers but retained in all revenue/profit calculations. 

## 6. Recommendations
1. Investigate the root cause of negative margins on the Halloween Zombie Mask line — pricing or cost issue
2. Increase marketing spend behind high-margin, low-volume products identified in the Pareto analysis
3. Review sales incentive structure — consider weighting compensation toward margin/profit, not revenue alone
4. Address the customer-identification gap at point of sale to convert the ~34% "unknown" revenue into actionable customer-level data

## 7. Tools & skills demonstrated

- **Power Query** — data cleaning, header correction, handling placeholder/null records
- **Data modeling** — star schema design, relationship cardinality, SCD Type 2 awareness
- **DAX** — CALCULATE and context transition, time intelligence (YoY/MoM), iterator functions (AVERAGEX/SUMX) for re-aggregating from line-item to order grain, ALL() for percentage-of-total calculations
- **Business analysis** — translating raw metrics into decision-relevant findings rather than descriptive reporting
- **Data quality judgment** — identifying and correctly reframing a placeholder/unknown-member trap in the customer dimension rather than either deleting it or misreporting it

---


