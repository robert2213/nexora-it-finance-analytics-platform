# Power BI Build Guide

1. Open Power BI Desktop.
2. Import all CSV files from the `/data` folder.
3. Confirm data types: dates as date, keys as text, amount fields as decimal numbers.
4. Mark `dim_date` as the date table using the `date` column.
5. Create one-to-many relationships from dimensions to fact tables.
6. Keep cross-filter direction single.
7. Create the DAX measures from `dax_measures.md`.
8. Build dashboard pages using `dashboard_requirements.md`.
9. Add slicers for Year, Month, Business Unit, Cost Center, Vendor, Forecast Cycle, GL Category, and Project.
10. Create a drill-through page using transaction-level actuals.
11. Add executive commentary boxes to summarize variance drivers and recommended actions.
12. Validate totals by comparing Actuals, Budget, Forecast, Cloud Spend, Vendor Spend, External Labor, and Headcount.
