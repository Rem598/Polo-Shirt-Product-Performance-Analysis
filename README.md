# 👕 PoloMax Product Performance Analysis

![Project Status](https://img.shields.io/badge/Status-Complete-green)
![Tools](https://img.shields.io/badge/Tools-SQL_|_Excel_|_Data_Viz-blue)
![Focus](https://img.shields.io/badge/Focus-Product_Strategy-orange)

## 📖 Executive Summary
During my internship as a Product Research Analyst, I analyzed **5,120 customer reviews and transactions** for PoloMax (a fashion e-commerce brand) to diagnose a critical business issue: a **48% product return rate**.

Using SQL for data extraction and exploratory data analysis (EDA), I identified that the high return rate was a systemic product quality issue rather than a logistics failure. My analysis provided data-backed recommendations to pause underperforming SKUs and double down on high-revenue variants.

---

## 📊 Dashboard Preview
![Dashboard](dashboard.png)
*Visual overview of market performance, return rates by location, and rating distribution.*

---

## 🎯 Business Problem
The brand faced declining profitability due to:
* A critically high **Return Rate (48.09%)**.
* Mediocre Customer Satisfaction (**3.02 Avg Rating**).
* Unknown performance drivers across different SKUs (Colors/Sizes).

**Objective:** Analyze sales data to pinpoint the root cause of returns and identify high-value opportunities.

---

## 🛠️ Tech Stack & Skills
* **SQL (MySQL):** Used for data cleaning, aggregation, `CASE` statements, and complex filtering.
* **Data Analysis:** Trend analysis, correlation (Price vs. Rating), and root cause analysis.
* **Data Visualization:** Created dashboard mockups to visualize geographic spread and SKU performance.
* **Strategic Planning:** Translated raw data into actionable business steps (e.g., "Pause Black variant sales").

---

## 🔍 Key Insights & SQL Logic

### 1. The "Black Shirt" Quality Issue
I discovered a strong correlation between color variants and customer ratings. While **Red** shirts were the top revenue drivers (~964k), **Black** shirts consistently received the lowest ratings (2.98), indicating a specific fabric or dye issue.

**SQL Snippet Used:**
```sql
-- Average Price vs. Average Rating by Material (Proxy: Color)
SELECT Color as Material_Proxy, 
       ROUND(AVG(Price), 2) as Avg_Price, 
       ROUND(AVG(Rating), 2) as Avg_Rating 
FROM tshirts 
GROUP BY Color;
