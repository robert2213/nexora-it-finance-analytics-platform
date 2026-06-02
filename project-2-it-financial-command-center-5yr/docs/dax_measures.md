# DAX Measures

```DAX
Total Actuals = SUM(fact_actuals[amount])
Total Budget = SUM(fact_budget[amount])
Total Forecast = SUM(fact_forecast[amount])
YTD Actuals = TOTALYTD([Total Actuals], dim_date[date])
YTD Budget = TOTALYTD([Total Budget], dim_date[date])
YTD Variance = [YTD Actuals] - [YTD Budget]
YTD Variance % = DIVIDE([YTD Variance], [YTD Budget])
Full-Year Budget = CALCULATE([Total Budget], ALL(dim_date[month_number]))
Full-Year Forecast = CALCULATE([Total Forecast], ALL(dim_date[month_number]))
Remaining Forecast = [Full-Year Forecast] - [YTD Actuals]
Year-End Projection = [YTD Actuals] + [Remaining Forecast]
Forecast Variance = [Full-Year Forecast] - [Full-Year Budget]
Forecast Variance % = DIVIDE([Forecast Variance], [Full-Year Budget])
Actuals vs Forecast = [Total Actuals] - [Total Forecast]
Forecast Accuracy % = 1 - ABS(DIVIDE([Actuals vs Forecast], [Total Forecast]))
External Labor Spend = SUM(fact_external_labor[amount])
Cloud Spend = SUM(fact_cloud_spend[amount])
Vendor Spend = SUM(fact_vendor_spend[amount])
Headcount = SUM(fact_headcount[filled_positions])
Open Positions = SUM(fact_headcount[open_positions])
Vacancy Rate = DIVIDE([Open Positions], SUM(fact_headcount[approved_positions]))
Cost per FTE = DIVIDE([YTD Actuals], [Headcount])
YoY Growth % = DIVIDE([Total Actuals] - CALCULATE([Total Actuals], SAMEPERIODLASTYEAR(dim_date[date])), CALCULATE([Total Actuals], SAMEPERIODLASTYEAR(dim_date[date])))
MoM Growth % = DIVIDE([Total Actuals] - CALCULATE([Total Actuals], DATEADD(dim_date[date], -1, MONTH)), CALCULATE([Total Actuals], DATEADD(dim_date[date], -1, MONTH)))
Run Rate = AVERAGEX(VALUES(dim_date[year_month]), [Total Actuals]) * 12
Risk Flag = IF([Forecast Variance %] > 0.05, "High", IF([Forecast Variance %] > 0.02, "Medium", "Low"))
```
