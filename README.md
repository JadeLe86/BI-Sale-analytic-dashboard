# 📊 Executive Sales Analytics Dashboard — Power BI Portfolio Project

> A consulting-grade Business Intelligence solution for Small & Medium Enterprises — transforming fragmented Excel reporting into a real-time executive analytics system.

---

## 🧭 Project Overview

This project demonstrates a **full-stack BI consulting deliverable** built to solve a real-world problem faced by growing SMEs: sales data scattered across multiple Excel files, reports prepared manually every month, and business leaders making decisions on 3-week-old information.

The solution is a **4-page Power BI Executive Dashboard** backed by a governed star schema data model, a DAX measure library with time-intelligence, and an automated insight framework that surfaces 15+ strategic observations without any manual analysis.

**Live Demo:** [Open Portfolio in Browser](./sales_analytics_portfolio.html) &nbsp;|&nbsp; [Phiên bản tiếng Việt](./sales_analytics_portfolio_vi.html)

---

## 🎯 Business Problem Solved

| Pain Point | Before | After |
|---|---|---|
| Reporting effort | 3–4 days/month manual work | < 4 hours, automated |
| Data freshness | 3-week-old PDF reports | Daily refresh |
| Data sources | 6 disconnected Excel files | 1 unified data model |
| Executive visibility | None (ad-hoc requests only) | Real-time dashboard |
| Strategic insights | Manual, delayed | 15+ auto-generated |

---

## 🏗️ Solution Architecture

```
Excel Files (6 sources)
        │
        ▼
  SQL Staging Layer  ←── ETL / Power Query / Data Cleansing
        │
        ▼
  Star Schema Data Model
  ┌─────────────────────────────────────┐
  │         FactSales (Center)          │
  │  SalesID · DateKey · CustomerKey    │
  │  ProductKey · RegionKey · Amount    │
  │  CostAmount · Profit · Discount     │
  └──────┬──────────┬──────────┬────────┘
         │          │          │
    DimDate    DimCustomer  DimProduct
    DimRegion
        │
        ▼
  Power BI Dashboard (4 Pages)
  ┌───────────────────────────────────┐
  │  Page 1 · Executive Overview      │
  │  Page 2 · Customer Analytics      │
  │  Page 3 · Product Analytics       │
  │  Page 4 · Regional Performance    │
  └───────────────────────────────────┘
```

---

## 📁 Repository Contents

```
📂 project-root/
├── 📄 README.md                          ← You are here
├── 🌐 sales_analytics_portfolio.html     ← Full interactive portfolio (English)
├── 🌐 sales_analytics_portfolio_vi.html  ← Full interactive portfolio (Vietnamese)
```

The HTML files are **fully self-contained** — open them directly in any browser. No server, no dependencies, no installation required. Charts render via Chart.js CDN.

---

## 📐 Data Model — Star Schema

### Fact Table

**`FactSales`** — Core transaction records

| Field | Type | Description |
|---|---|---|
| SalesID | PK | Unique transaction identifier |
| DateKey | FK | Links to DimDate |
| CustomerKey | FK | Links to DimCustomer |
| ProductKey | FK | Links to DimProduct |
| RegionKey | FK | Links to DimRegion |
| SalesAmount | Decimal | Gross revenue |
| CostAmount | Decimal | Cost of goods sold |
| Profit | Decimal | Pre-calculated margin |
| Quantity | Integer | Units sold |
| Discount | Decimal | Discount applied |

### Dimension Tables

**`DimDate`** — Full date intelligence (Year, Quarter, Month, Week, Fiscal periods, IsHoliday)

**`DimCustomer`** — CustomerName, Segment (B2B/B2C), Industry, Tier, AcquisitionDate

**`DimProduct`** — ProductName, Category, SubCategory, Brand, StandardCost, ListPrice

**`DimRegion`** — RegionName, Country, Province, SalesTerritory, Manager, TargetRevenue

---

## 📏 KPI Framework

### Financial KPIs
| KPI | DAX Formula |
|---|---|
| Total Revenue | `SUM(FactSales[SalesAmount])` |
| Total Profit | `SUM(FactSales[Profit])` |
| Profit Margin % | `DIVIDE([Total Profit], [Total Revenue], 0)` |
| Average Order Value | `DIVIDE([Total Revenue], [Total Orders], 0)` |

### Customer KPIs
| KPI | DAX Formula |
|---|---|
| Total Customers | `DISTINCTCOUNT(FactSales[CustomerKey])` |
| Revenue Growth % | `DIVIDE(RevCY - RevPY, RevPY, BLANK())` |
| Customer Retention Rate | `[Returning Customers] / [Prior Period Customers]` |

### Time-Intelligence KPIs
| KPI | DAX Formula |
|---|---|
| Revenue YTD | `TOTALYTD([Total Revenue], DimDate[FullDate])` |
| Revenue MTD | `TOTALMTD([Total Revenue], DimDate[FullDate])` |
| Revenue vs Same Period Last Year | `CALCULATE([Total Revenue], SAMEPERIODLASTYEAR(...))` |

---

## 📊 Dashboard Pages

### Page 1 — Executive Overview
Top KPI cards (Revenue · Profit · Margin · Customers · Orders), monthly revenue trend line, revenue vs target gauge, regional map, category bar chart, top 10 customers table, and an auto-generated executive insight panel.

### Page 2 — Customer Analytics
Customer segmentation donut, revenue distribution histogram, top 20 customers ranked bar, Pareto 80/20 analysis, and customer acquisition trend over time.

### Page 3 — Product Analytics
Revenue by product horizontal bar, profit waterfall, ABC classification scatter, and a product performance quadrant matrix (high margin × high revenue).

### Page 4 — Regional Performance
Filled geographic map, regional target attainment bars, multi-line trend comparison, revenue contribution stacked bar, and profit contribution donut.

---

## 💡 Sample Automated Insights

The dashboard generates insights like these automatically — no manual analysis required:

- 📈 **Revenue grew 12.5% YoY** to $4.82M, driven by a 34% surge in the East Region
- 🗺️ **South Region** contributes 48% of total revenue with only 32% of sales headcount
- 👥 **Top 10 customers** generate 35% of total revenue — concentration risk identified
- ⚠️ **Profit margin compressed** by 1.1pp to 25.7% despite revenue growth — cost pressure signal
- 📦 **ABC analysis**: top 6.4% of SKUs drive 72% of sales — long-tail rationalization opportunity
- 🔴 **Customer retention dropped** from 74% to 68% — $290K revenue at risk
- 📅 **September–October** consistently represent 34% of annual revenue — seasonal planning trigger
- 💰 **Discount rate increased** from 9.8% to 14.3% — $217K margin erosion identified

---

## 🛠️ Technology Stack

| Layer | Technology | Purpose |
|---|---|---|
| Visualization | Power BI Desktop & Service | Dashboard, report pages, scheduled refresh |
| Data Modeling | DAX / Power BI Model | Star schema, KPI measures, time-intelligence |
| Data Transformation | Power Query (M) | ETL, cleansing, staging |
| Database | SQL Server / T-SQL | Centralized staging layer |
| Source Data | Microsoft Excel | Original transactional files |
| Security | Row-Level Security (RLS) | Region-scoped data access per manager |
| Automation | Power Automate | Weekly KPI email delivery |

---

## 📈 Business Outcomes

| Metric | Result |
|---|---|
| Reporting time reduction | **~70%** (3 days → < 4 hours) |
| Data freshness | **Daily** (was monthly PDF) |
| Revenue at risk identified | **$290,000** |
| Data sources unified | **6 → 1** |
| Insights auto-generated | **15+** per reporting cycle |

---

## 🔮 Future Enhancements

- [ ] **Predictive Forecasting** — Azure Machine Learning integration for revenue prediction
- [ ] **Churn Prediction** — Embedded Python model to flag at-risk customers
- [ ] **Automated Alerts** — Power Automate weekly KPI digest emails to leadership
- [ ] **Mobile Layout** — Optimized report view for field sales teams
- [ ] **Advanced RLS** — Granular row-level security by territory and product category

---

## 📬 About This Project

This is a **consulting portfolio project** created to demonstrate the end-to-end BI delivery process — from business problem framing and data model design through to dashboard UX, DAX development, and executive communication.

It represents the type of work I deliver for SME clients who need to move beyond Excel and gain real-time visibility into their business performance.

**If you're interested in a similar solution for your business:**

- 🔗 Connect on [LinkedIn] (https://www.linkedin.com/in/thuy-linh-le-2aa7b810a/)
- 📧 Email: linh.ltt06@gmail.com
- 🌐 Portfolio: 

---

## 📄 License

This project is shared for portfolio and educational purposes.  
Feel free to use the structure, methodology, and DAX patterns as reference for your own BI projects.

---

*Built with Power BI · SQL Server · Excel · DAX · HTML/CSS/JavaScript*
