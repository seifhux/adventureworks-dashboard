# 🚲 Adventure Works Sales Dashboard

An interactive **Power BI** dashboard that analyzes sales, profit, product, and customer performance for **Adventure Works**, a fictional global bicycle manufacturer. The project turns raw transactional data into a clear view of the business so decision-makers can see what is selling, where, to whom, and how profitably.

> **Tools:** Power BI Desktop · Power Query · DAX · Data Modeling (Star Schema)

---

## 📌 Table of Contents
1. [Project Overview](#-project-overview)
2. [Business Questions](#-business-questions)
3. [Dataset](#-dataset)
4. [Data Model](#-data-model)
5. [Data Preparation](#-data-preparation)
6. [Key DAX Measures](#-key-dax-measures)
7. [Dashboard Pages & Features](#-dashboard-pages--features)
8. [Key Insights](#-key-insights)
9. [How to Run](#-how-to-run)
10. [Repository Structure](#-repository-structure)
11. [Future Improvements](#-future-improvements)
12. [Author](#-author)

---

## 📖 Project Overview

Adventure Works sells bikes, components, clothing, and accessories through multiple regions. This project builds an end-to-end BI solution:

- Cleans and shapes the raw data in **Power Query**
- Builds a **star-schema data model** with fact and dimension tables
- Creates reusable **DAX measures** for revenue, cost, profit, and returns
- Presents the results in an interactive, multi-page **Power BI dashboard** with slicers and drill-through

## ❓ Business Questions

The dashboard is designed to answer:

- What are the total **sales, profit, and profit margin**, and how are they trending over time?
- Which **products and categories** drive the most revenue and profit?
- Which **regions / territories** perform best and worst?
- Who are the **top customers**, and how do customer segments differ?
- What is the **return rate**, and which products are returned most?
- How do results compare **year over year** and **month over month**?

## 🗂 Dataset

The data is the **Adventure Works** sample dataset, organized into these tables:

| Table | Type | Description |
|---|---|---|
| `Sales` | Fact | Order lines: order date, product, customer, territory, quantity |
| `Returns` | Fact | Returned items by date, product, and territory |
| `Products` | Dimension | Product name, cost, price, color, size |
| `Product Categories` / `Subcategories` | Dimension | Product hierarchy |
| `Customers` | Dimension | Customer demographics (name, income, occupation, etc.) |
| `Territories` | Dimension | Region, country, and continent |
| `Calendar` | Dimension | Date table for time intelligence |

## 🧩 Data Model

The model follows a **star schema**: fact tables (`Sales`, `Returns`) connect to dimension tables through one-to-many relationships, with a dedicated `Calendar` table marked as the date table.

```
Customers ─┐
Products ──┼──< Sales >──┬── Calendar
Territories┘             └── Territories
Products ──< Returns
```

> 📷 *Add a screenshot of your model view here:* `![Data Model](images/data_model.png)`

## 🧹 Data Preparation

Performed in **Power Query**:

- Checked data types and fixed incorrectly typed columns
- Removed duplicates and handled null / blank values
- Merged product, subcategory, and category tables into a clean product hierarchy
- Created derived columns (e.g., full customer name, age groups, income brackets)
- Built a complete `Calendar` table (year, quarter, month, month name, weekday)

## 🧮 Key DAX Measures

```DAX
Total Revenue = SUMX(Sales, Sales[OrderQuantity] * RELATED(Products[ProductPrice]))

Total Cost = SUMX(Sales, Sales[OrderQuantity] * RELATED(Products[ProductCost]))

Total Profit = [Total Revenue] - [Total Cost]

Profit Margin % = DIVIDE([Total Profit], [Total Revenue])

Total Orders = DISTINCTCOUNT(Sales[OrderNumber])

Total Returns = SUM(Returns[ReturnQuantity])

Return Rate = DIVIDE([Total Returns], SUM(Sales[OrderQuantity]))

Revenue LY = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR('Calendar'[Date]))

Revenue YoY % = DIVIDE([Total Revenue] - [Revenue LY], [Revenue LY])
```

> Adjust column names to match your own model.

## 📊 Dashboard Pages & Features

**1. Executive Overview**
- KPI cards: Revenue, Profit, Profit Margin, Orders, Return Rate
- Revenue and profit trend over time
- Sales by region / country map

**2. Product Analysis**
- Top and bottom products by revenue and profit
- Category and subcategory breakdown
- Return rate by product

**3. Customer Analysis**
- Top customers by revenue
- Sales by income bracket, occupation, and age group

**Interactive features:** slicers (year, region, category), cross-filtering, drill-down hierarchies, tooltips, and bookmarks.

> 📷 *Add dashboard screenshots here:*
> `![Overview](images/overview.png)`
> `![Products](images/products.png)`
> `![Customers](images/customers.png)`

## 💡 Key Insights

*Replace these with the findings from your own dashboard:*

- **Top category:** [e.g., Bikes account for X% of total revenue]
- **Best region:** [e.g., Australia / United States leads in sales]
- **Trend:** [e.g., Revenue grew X% year over year]
- **Returns:** [e.g., Return rate is X%, concentrated in product Y]
- **Customers:** [e.g., Higher-income customers contribute the most revenue]

## ▶️ How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   ```
2. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free, Windows).
3. Open `AdventureWorks_Dashboard.pbix`.
4. If prompted, update the data source path: **Home → Transform data → Data source settings**.
5. Click **Refresh** to load the data.

## 📁 Repository Structure

```
├── AdventureWorks_Dashboard.pbix   # Power BI report
├── data/                           # Source CSV files
├── images/                         # Screenshots of the dashboard and model
└── README.md
```

## 🚀 Future Improvements

- Add forecasting for sales and profit
- Add row-level security by region
- Connect directly to SQL Server instead of CSV files
- Publish to Power BI Service with scheduled refresh

## 👤 Author

**Seif Hussein Aboelazaim**
Computer Science & AI student at Cairo University (FCAI) · Aspiring Data Scientist
📧 seifhuss74@gmail.com · 🔗 [LinkedIn](https://linkedin.com/in/seifaboelazaim)
