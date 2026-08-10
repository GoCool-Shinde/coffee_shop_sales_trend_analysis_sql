# ☕ Coffee Shop Sales Trend Analysis (SQL)

Month-over-month analysis of a coffee shop chain's point-of-sale transactions — built entirely in SQL using window functions and modular views to track **revenue, order volume, and units sold** across time.

---

## 📌 Project Overview

This project analyzes raw, transaction-level point-of-sale data from a multi-location coffee shop chain. The goal was to turn a flat transaction log into a set of reusable analytical views that answer three core business questions for **three separate metrics — Sales, Orders, and Quantity**:

1. **What happened?** — Total value for each month
2. **What changed?** — Month-over-month increase/decrease (absolute + % change)
3. **How do two specific months compare?** — Difference between any selected month and the one before it

Each question is answered using SQL views built with window functions (`LAG`), date-truncation logic, and safe division handling — so the results can be queried instantly without re-writing logic every time.

## 🗂️ Dataset

- **Source:** Point-of-sale transaction export from a coffee shop chain
- **Grain:** One row per transaction
- **Key columns:** `Transaction_Id`, `Transaction_Date`, `Quantity`, `Store_Id`, `Store_Location`, `Product_Id`, `Unit_Price`, `Product_Category`, `Product_Type`, `Product_Detail`

## 🧩 Project Structure

| Section | Business Question | Metric |
|---|---|---|
| A1 | Total sales per month | Revenue |
| A2 | Month-on-month sales change (value + %) | Revenue |
| A3 | Sales difference vs. previous month | Revenue |
| B1 | Total number of orders per month | Order Volume |
| B2 | Month-on-month order change (value + %) | Order Volume |
| B3 | Order difference vs. previous month | Order Volume |
| C1 | Total quantity sold per month | Units Sold |
| C2 | Month-on-month quantity change (value + %) | Units Sold |
| C3 | Quantity difference vs. previous month | Units Sold |

Each section is implemented as a `CREATE VIEW`, so results can be pulled with a single `SELECT * FROM <view_name>`.

## 🛠️ Tech Stack

- **Database:** PostgreSQL / SQL Server (T-SQL version included)
- **Core techniques:**
  - Window functions — `LAG() OVER (...)`
  - Date functions — `DATE_TRUNC`, `DATE_PART`, `TO_CHAR` (Postgres) / `DATEFROMPARTS`, `DATEPART`, `FORMAT` (SQL Server)
  - Aggregations — `SUM`, `COUNT`
  - Safe division handling — `NULLIF` to prevent divide-by-zero errors
  - Modular views for reusable, stakeholder-friendly querying

## 📁 Repository Contents

```
├── Coffee_Shop_Transactions.sql       # PostgreSQL — base queries (A1, A2, A3, B1, B2, B3, C1, C2, C3)
├── Coffee_Shop_New.sql                # PostgreSQL — refined version with Month_Number for correct sorting
├── Coffee_Shop_New_SQLServer.sql      # SQL Server (T-SQL) version
├── Coffee_Shop_Transactions.docx      # Project write-up
├── Coffee_Shop_SQL_Project.pptx       # Slide deck walkthrough of each query
└── README.md
```

## 🚀 How to Run

1. Load the transaction data into a table named `Transactions` in your database.
2. Run the script matching your database engine:
   - PostgreSQL → `Coffee_Shop_New.sql`
   - SQL Server → `Coffee_Shop_New_SQLServer.sql`
3. Query any view directly, e.g.:
   ```sql
   SELECT * FROM B; -- month-on-month sales change
   ```

## 📊 Key Insights

- Revenue and order count trends can diverge — a few months show flat order counts but rising revenue, suggesting a shift toward higher-ticket items rather than more foot traffic.
- The modular view structure means the same `LAG`-based pattern can be re-applied to new groupings (by store, product category, etc.) without rewriting the core logic.

## 🔮 Future Improvements

- Add store-level and product-category-level breakdowns
- Build a BI dashboard (Power BI / Tableau) on top of these views
- Automate refresh via a scheduled ETL pipeline

---

**Author:** *[Your Name]*
Feel free to fork, adapt, or reach out with questions!
