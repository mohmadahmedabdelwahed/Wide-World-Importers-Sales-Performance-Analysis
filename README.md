# Wide-World-Importers-Sales-Performance-Analysis
**Power BI dashboard | Star-schema data modeling | DAX | Business insight generation**
---

## 1. Project overview
### This project is an end-to-end sales analysis of the Wide World Importers dataset (2013–2016) using Power BI.
The main goal was to answer an important business question:
Is the company growing in a healthy and profitable way, or is revenue increasing while profit margins are shrinking?

The project includes:

- Data cleaning using Power Query
- Building a star schema data model
- Creating DAX measures and KPIs
- Designing a 9-page interactive dashboard

The analysis covers overall business performance, product profitability, customer behavior, sales team performance, and geographic trends.
---

## 2. Business problem
Management wanted a clear view of the business and answers to questions such as:

- Is revenue growth leading to higher profits?
- Which products, customers, and regions generate the most profit?
- Are sales representatives focusing on revenue at the expense of profitability?
- Is the business relying too heavily on a small number of products, customers, or locations?
---

## 3. Data source & model
**Source:** Wide World Importers Sample Dataset (Microsoft)
| Table | Role | Rows (approx.) |
|---|---|---|
| FactSale | Fact table — line-item sales transactions | ~26,000 |
| DimCustomer | Customer dimension | ~400 |
| DimStockItem | Product dimension | ~670 |
| DimEmployee | Salesperson dimension | ~210 |
| DimCity | Geography (city, state, territory) | ~13,000 |
| DimDate | Calendar table (calendar + fiscal) | 1,460 |

**Model:** star schema, single-direction one-to-many relationships from each dimension to FactSale via surrogate keys.
**Data cleaning (Power Query):**
- Removed invalid header rows from DimCustomer and DimStockItem
- Removed the null placeholder row (Stock Item Key 0) with no valid attributes
- Investigated sales records linked to Customer Key 0 and confirmed they were valid transactions with missing customer details rather than data model issues.
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
- 2015 was the strongest year, generating both the highest revenue ($3.2M) and profit ($6.3M).
- In 2014, profit increased but profit margin decreased, suggesting costs were growing faster than revenue.
- Revenue continued to grow in 2015 before declining by 9.48% in 2016.
- Although costs also decreased in 2016, they did not fall enough to fully offset the revenue decline, leading to a slight margin reduction.
- This suggests that most costs move with revenue, but some expenses may not scale down efficiently and should be investigated further.

**Product performance**
- Four Halloween Zombie Mask products generated high sales volume but had negative profit margins (-5.56%), indicating potential pricing or cost issues.
- Animal Big Feet Slippers (Size M) had a very high profit margin (75%) but low sales volume (rank 188), making it a strong candidate for additional marketing.
- Profit contribution is spread across many products, reducing dependence on a single product line.

**Sales team performance**
- The salesperson with the highest revenue generated one of the lowest profit margins.
- The salesperson with the highest profit margin ranked only seventh in revenue.

This suggests some sales growth may be driven by heavy discounting rather than profitable deals.

**Customer data quality finding**
- Around 34% of total revenue came from transactions linked to unknown customers.
- Analysis confirmed these transactions were legitimate sales with complete order information, but customer details were not captured.

This points to a process issue rather than a reporting issue and highlights an opportunity to improve customer data collection.

- Only 13 transactions (0.05% of records) were missing delivery dates.
- These were likely orders created near the end of the dataset period and had not yet been shipped.
- They were excluded from delivery-time analysis but included in all revenue and profit calculations.

**Geographic performance**
- California generated the highest revenue and profit.
- Hawaii recorded the lowest revenue and profit.

**Chilled items Analysis**
- Total number of invoices is 8k
- Chilled items contributed approximately $129K in sales, representing only 0.6% of total sales.
- Taj Shand had the highest share of chilled item sales at 0.9%.
- California recorded the highest chilled-item sales ($50,786), while Hawaii recorded the lowest ($1,436).

**Note**

13 transactions (0.05% of records) have no recorded delivery date, consistent with orders invoiced near the end of the dataset's time range that had not yet shipped. These are excluded from delivery-time slicers but retained in all revenue/profit calculations. 

## 6. Recommendations
- Review pricing and cost structure for the Halloween Zombie Mask product line.
- Increase marketing efforts for high-margin products with low sales volume.
- Adjust sales incentives to reward profitability in addition to revenue generation.
- Improve customer information capture during the sales process to reduce unidentified transactions and enable better customer analysis.

## 7. Tools & skills demonstrated

- **Power Query** — data cleaning, header correction, handling placeholder/null records
- **Data modeling** — star schema design, Relationship management
- **DAX** — CALCULATE and context transition, time intelligence (YoY), iterator functions (AVERAGEX) for re-aggregating from line-item to order grain, ALL() for percentage-of-total calculations
- **Business analysis** — Turning data into actionable business recommendations and identifying performance drivers and profitability issues
- **Data quality judgment** — Investigating missing and placeholder records and distinguishing real business issues from data-modeling issues

---


