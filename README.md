# 📊 Retail Business Intelligence Capstone

An end-to-end Business Intelligence project for a fictional retail chain **SleekMart**, covering data extraction with Python, data modeling in Power BI, and an interactive executive dashboard — built to answer real business questions about revenue, profitability, and performance.

---

## 📌 Project Overview

This project simulates a complete BI pipeline for a multi-store retail business. The goal was to transform raw transactional data into actionable insights that help business stakeholders monitor performance across stores, employees, customers, and products.

### Business Requirements
1. Track monthly revenue per store and category
2. Identify top-performing customers
3. Determine product profitability
4. Analyze employee impact on store performance
5. Calculate Average Order Value and Repeat Purchase Rate
6. Calculate Gross Margin

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **Python** | Data extraction and quality validation → CSV |
| **Power BI** | Data modeling, DAX measures, and dashboard |

---

## 🗄️ Data Model

The project uses a **Star Schema** with `orders` as the central fact table, connected to 6 dimension tables:

```
orders (fact)
├── customers      — customer demographics and contact info
├── employees      — employee details, job title, manager hierarchy
├── stores         — store locations across multiple US cities
├── products       — product catalog with retail and supplier pricing
├── suppliers      — supplier information
└── dates          — date dimension (day, month, quarter, week)
```

Plus a separate `orderitems` table for line-item detail (quantity, unit price per order).

![Data Model](Screenshot%202025-11-28%20192630.png)

---

## 🔄 Project Workflow

### Step 1 — Python: Data Extraction & Validation
- Extracted all raw data from the source and exported it to **9 CSV files**
- Performed **Data Quality Validation** to check for nulls, duplicates, and data type consistency before loading into Power BI

### Step 2 — Power BI: Data Modeling
- Imported all CSV files into Power BI
- Built a **Star Schema** with proper one-to-many relationships between the fact table and all dimension tables
- Created a dedicated `KPI_measures` table to organize all DAX calculations

### Step 3 — DAX Measures
Created 7 business KPIs:

```dax
Orders          = COUNTROWS(orders)
Revenue         = SUMX(orderitems, orderitems[quantity] * orderitems[unitprice])
Cost            = SUMX(orderitems, orderitems[quantity] * RELATED(products[supplierprice]))
Profit          = [Revenue] - [Cost]
GrossMargin%    = DIVIDE([Profit], [Revenue])
Avg Order Value = DIVIDE([Revenue], [Orders])
Repeat Customers = CALCULATE(DISTINCTCOUNT(orders[customerid]), ...)
```

### Step 4 — Interactive Dashboard
Built a single-page executive dashboard with full interactivity.

![Dashboard](Screenshot%202025-11-28%20222835.png)

---

## 📊 Dashboard Components

| Visual | Purpose |
|--------|---------|
| **5 KPI Cards** | Total Orders, Revenue, Avg Order Value, Gross Margin %, Repeat Customers |
| **Bar Chart** | Revenue by category |
| **Line Chart** | Revenue trend by month |
| **Donut Chart** | Revenue share by store |
| **Matrix — Top Employees** | Orders, Revenue, Profit per employee |
| **Matrix — Top Customers** | Orders, Revenue, Profit per customer |
| **Matrix — Top Products** | Profit ranking per product |
| **4 Slicers** | Filter by Employee, Customer, Product Name, and Date |

---

## 📈 Key Results

| Metric | Value |
|--------|-------|
| Total Orders | **300** |
| Total Revenue | **$522K** |
| Average Order Value | **$1.74K** |
| Gross Margin | **5.02%** |
| Repeat Customers | **75** |
| Total Profit | **$26,179** |

**Top insights:**
- **Beauty** is the highest-revenue category, followed by Foods and Home Decor
- Revenue is **evenly distributed** across stores — no single store dominates (all between 9-12%)
- **Doll** is the most profitable product ($1,505 profit), followed by Perfume and Laptop

---

## 📁 Repository Structure

```
retail_business_intelligence_capstone/
│
├── data/
│   ├── customers.csv
│   ├── employees.csv
│   ├── orders.csv
│   ├── orderitems.csv
│   ├── products.csv
│   ├── stores.csv
│   ├── suppliers.csv
│   └── dates.csv
│
├── python/
│   └── extraction_validation.py   # Data extraction & quality checks
│
├── powerbi/
│   └── capstone_dashboard.pbix    # Power BI report file
│
├── screenshots/
│   ├── data_model.png
│   └── dashboard.png
│
└── docs/
    └── business_requirements.md
```

---

## 💡 What I Learned

- Building a full Star Schema data model from multiple CSV sources
- Writing complex DAX measures for real business KPIs (Gross Margin, Repeat Customers, AOV)
- Using Python for data extraction and quality validation before loading
- Designing an executive dashboard that answers specific business questions
- Organizing a BI project with proper documentation and structure

---

## 👤 Author

**Mohamed Amer**
- 📧 mo.abdo.amer123@gmail.com
- 💼 [LinkedIn](https://www.linkedin.com/in/mohamed-amer-217342376)
- 🐙 [GitHub](https://github.com/moabdoamer123-cmd)
