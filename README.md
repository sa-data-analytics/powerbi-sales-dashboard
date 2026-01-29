# PowerBi-Sales-Dashboard
Sales Performance Dashboard - Power BI

A clean, professional Sales Performance Dashboard built using Power BI, Python‑generated synthetic data, and DAX measures.
This project demonstrates skills in data modeling, time‑intelligence DAX, visualization design, and dashboard storytelling.

**Project Overview**
This dashboard provides insights into:
- Total Sales
- Total Orders
- Total Quantity Sold
- Average Order Value (AOV)
- Sales Trends Over Time
- Sales by Category
- Sales by Region
- Top 5 Products
- Month‑to‑Date (MTD) & Year‑to‑Date (YTD) performance
- YoY Growth %
  
##The dataset was generated using Python to simulate realistic sales transactions.

**Key Skills Demonstrated**

***Power BI***
- Data modeling
- Relationships
- Time intelligence
- KPI design
- Visual storytelling
- Professional layout formatting

***DAX***
- MTD, YTD, YoY calculations
- Aggregations
- CALCULATE, DATEADD, DATESMTD, DATESYTD
- SUMX for row‑level calculations

***DAX Measures***
/* ============================
   CORE SALES MEASURES
   ============================ */

Total Sales =
SUMX ( sales_data, sales_data[Quantity] * sales_data[UnitPrice] )

Total Orders =
DISTINCTCOUNT ( sales_data[OrderID] )

Total Quantity =
SUM ( sales_data[Quantity] )

Average Order Value =
DIVIDE ( [Total Sales], [Total Orders] )


/* ============================
   TIME INTELLIGENCE
   (Requires 'Date' table)
   ============================ */

Sales MTD =
CALCULATE (
    [Total Sales],
    DATESMTD ( 'Date'[Date] )
)

Sales YTD =
CALCULATE (
    [Total Sales],
    DATESYTD ( 'Date'[Date] )
)

Sales LY =
CALCULATE (
    [Total Sales],
    DATEADD ( 'Date'[Date], -1, YEAR )
)

Sales MTD LY =
CALCULATE (
    [Sales MTD],
    DATEADD ( 'Date'[Date], -1, YEAR )
)

Sales YTD LY =
CALCULATE (
    [Sales YTD],
    DATEADD ( 'Date'[Date], -1, YEAR )
)


/* ============================
   GROWTH METRICS
   ============================ */

YoY Growth % =
DIVIDE (
    [Total Sales] - [Sales LY],
    [Sales LY]
)

MTD Growth % =
DIVIDE (
    [Sales MTD] - [Sales MTD LY],
    [Sales MTD LY]
)

YTD Growth % =
DIVIDE (
    [Sales YTD] - [Sales YTD LY],
    [Sales YTD LY]
)


/* ============================
   CATEGORY / REGION ANALYSIS
   ============================ */

Sales by Category =
[Total Sales]

Sales by Region =
[Total Sales]

Sales per Product =
[Total Sales]


/* ============================
   DATE TABLE (Required)
   ============================ */

Date =
ADDCOLUMNS (
    CALENDAR ( DATE(2024,1,1), DATE(2024,12,31) ),
    "Year", YEAR([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "Month Number", MONTH([Date]),
    "Year-Month", FORMAT([Date], "YYYY-MM")
)

***Python***
- Synthetic data generation
- Randomized customer, product, region, and date logic
- CSV export for BI consumption

