# Polo Shirt Product Performance Analysis

Diagnosing a 48% return rate using SQL segmentation and root cause analysis.

---

## The Question

A fashion e-commerce brand is seeing 48% of polo shirt orders returned. That is not a logistics problem and it is not a sizing chart problem. Those explanations are guesses. This analysis starts from the data.

**Business problem:** PoloMax is experiencing a critically high return rate (48.09%) and mediocre customer satisfaction (3.02 average rating). Profitability is declining. The root cause is unknown.

**Objective:** Determine whether the return rate is systemic across the product line or isolated to specific variants, and identify exactly what is driving it.

---

## Key Finding

The return rate is not a company-wide problem. It is a single-variant problem.

Segmenting 5,120 transactions by color, size, and timeframe isolated the issue to the Black colorway, which consistently received the lowest customer ratings (2.98 average) across all locations. Return rates were uniform across cities at approximately 48%, which ruled out a logistics or regional fulfillment explanation. The problem was in the product itself.

The Black variant has a manufacturing defect — most likely in the fabric or dye process.

---

## Why Segmentation Is the Method

Aggregate return rates are misleading. A 48% return rate across all products looks catastrophic. The same 48% rate concentrated in one color variant out of several is a solvable, specific problem. The difference between those two conclusions is segmentation.

**The diagnostic logic:**

1. If the return rate varies by location, the problem is logistics.
2. If the return rate varies by size, the problem is the sizing chart.
3. If the return rate is uniform across locations and sizes but concentrated in one color, the problem is the product variant.

All three were tested. The data pointed to option 3.

---

## Analysis

**Tool:** SQL (MySQL)

**Key queries:**

Return rate by location — tested whether any city or region showed an outlier rate. Result: uniform at approximately 48% everywhere, ruling out logistics.

```sql
SELECT Location,
       ROUND((SUM(CASE WHEN Return_Status = 'Returned' THEN 1 ELSE 0 END) * 100.0 / COUNT(*)), 2) AS Return_Rate
FROM tshirts
GROUP BY Location;
```

Average rating by color variant — identified Black as the consistent low-rated outlier.

```sql
SELECT Color,
       ROUND(AVG(Price), 2) AS Avg_Price,
       ROUND(AVG(Rating), 2) AS Avg_Rating
FROM tshirts
GROUP BY Color;
```

Timeframe segmentation — confirmed the Black variant issue persists across time periods, ruling out a temporary batch defect.

---

## Recommendations

**Immediate:** Pause Black variant sales to stop brand damage from accumulating.

**Short term:** Audit the Black colorway production process. Likely causes are fabric quality or dye process failure.

**Inventory strategy:** Expand the Red product line. Red drives the highest revenue at approximately £964K and the highest customer satisfaction. It is the product that works.

**Target outcome:** Reducing the return rate to 25% is projected to improve profit margin by 23%.

---

## Files

- `polo_tshirt_cleaned_dataset.csv` — 5,120 transaction records.
- `polo_shirt_sql_queries.sql` — Full query library.
- `PoloMax_Product_Analysis.pdf` — Stakeholder presentation.
- `SQL_POLO_SHIRT_ANALYSIS_REPORT.docx` — Detailed written report.

---

## Tools

SQL (MySQL), Power BI, root cause analysis, data segmentation
