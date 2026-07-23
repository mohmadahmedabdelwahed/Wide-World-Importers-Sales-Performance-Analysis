# Wide-World-Importers-Sales-Performance-Analysis
**Power BI dashboard | Star-schema data modeling | DAX | Business insight generation**
---

## 1. Project overview
A end-to-end Power BI analysis of Wide World Importers' sales data (2013–2016), built to answer a core business question: **is the company growing profitably, or is revenue growth masking margin erosion?**

The project covers data modeling from raw star-schema tables, Power Query cleaning, DAX measure design, and an 8-page interactive report spanning company performance, product profitability, customer concentration, sales team accountability, and geographic performance.
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
| Revenue / Profit YoY %  / Profit Margin % | Same-period comparison vs. prior year |
| Average Order Value (AOV) | Revenue per distinct invoice |
| Average Profit per Order | Profit per distinct invoice |
| Average Deal Size per Salesperson | Order-level revenue average, calculated per rep |
| % of Total Volume by Product | Product's share of company-wide quantity |
---
## 5. Key insights
**Profitability trend**
- 2015 was the peak year for both revenue ($3.2M) and profit ($6.3M)
- 2014 showed Profit increasing while margin declined — a warning sign later corrected in 2015–2016
- Q1 and June consistently show the strongest margins; Q4 and August the weakest
- Growth is decreasing, but margin has stabilized (2016) Revenue grew 13.93% YoY and profit grew 13.96% YoY in 2016 — both slower than prior-year growth rates (2014–2015), indicating decelerating growth, worth investigating (market saturation, competition, fewer new customers acquired)
- Profit Margin YoY moved only +0.03 percentage points — effectively flat, not a meaningful increase. The more accurate read: margin held steady despite slowing growth
- This is a positive contrast to 2014, where revenue grew while margin eroded (see above). By 2016, revenue and profit are growing in lockstep again — the company avoided a repeat of the 2014 pattern, even as top-line growth itself slowed down

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


