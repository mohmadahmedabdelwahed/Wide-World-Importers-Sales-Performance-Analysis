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

