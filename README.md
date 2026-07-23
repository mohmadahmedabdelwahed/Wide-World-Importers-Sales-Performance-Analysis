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
| Total Revenue | Sum of Total Excluding Tax (net of sales tax — see methodology note) |
| Total Profit | Sum of Profit |
| Profit Margin % | Profit ÷ Revenue |
| Revenue / Profit YoY % | Same-period comparison vs. prior year |
| Average Order Value (AOV) | Revenue per distinct invoice |
| Average Profit per Order | Profit per distinct invoice |
| Average Deal Size per Salesperson | Order-level revenue average, calculated per rep |
| % of Total Volume by Product | Product's share of company-wide quantity |
| Average Delivery Time | Days between invoice date and delivery date |

