# Time Intelligence DAX – Day 1

This document contains DAX snippets for common time intelligence calculations in Power BI. Each snippet is accompanied by comments to help you understand its purpose and functionality.

```DAX
-- Calculate the total sales amount
Total Sales = SUM(Sales[SalesAmount])

-- Calculate Year-to-Date (YTD) sales
-- This aggregates sales from the start of the year up to the current date
Sales YTD = 
CALCULATE(
    [Total Sales],
    DATESYTD('Calendar'[Date])
)

-- Calculate sales for the same period in the previous year
-- Useful for year-over-year comparisons
Sales LY = 
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR('Calendar'[Date])
)

-- Calculate Month-to-Date (MTD) sales
-- This aggregates sales from the start of the current month up to the current date
Sales MTD = 
CALCULATE(
    [Total Sales],
    DATESMTD('Calendar'[Date])
)

-- Calculate sales for the previous month
-- Useful for month-over-month comparisons
Sales PM = 
CALCULATE(
    [Total Sales],
    PREVIOUSMONTH('Calendar'[Date])
)

-- Calculate the variance in sales compared to the same period last year
-- This shows the absolute difference in sales year-over-year
Sales YoY Variance = 
[Sales YTD] - [Sales LY]

-- Calculate the year-over-year sales growth percentage
-- This shows the relative growth or decline in sales as a percentage
Sales YoY % = 
DIVIDE([Sales YoY Variance], [Sales LY])
```

### Notes:
- Replace `'Calendar'[Date]` with the appropriate date column from your model.
- Ensure your date table is marked as a "Date Table" in Power BI for these functions to work correctly.
- These calculations are commonly used in dashboards to analyze trends and performance over time.
- The `DIVIDE` function is used to handle division safely, avoiding errors when the denominator is zero.
- Customize these measures as needed to fit your specific business requirements.