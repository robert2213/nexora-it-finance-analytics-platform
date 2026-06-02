# DAX Measure Script
## Nexora IT Financial Command Center

All measures live in a dedicated table named `_Measures`.

### How to Create the Measures Table
1. Home > Enter Data
2. Table name: `_Measures`
3. Add one column named `placeholder`, leave it empty, click Load
4. In Report view, right-click `_Measures` > New Measure for each entry below
5. After all measures are created, right-click the `placeholder` column > Delete

Copy each measure exactly as written. Build them in section order — later sections depend on earlier ones.

---

## Section 1: Base Aggregations

These are the foundation. Create these first.

```DAX
Total Actuals =
SUM ( fact_actuals[amount] )
```

```DAX
Total Budget =
SUM ( fact_budget[amount] )
```

```DAX
Total Forecast =
SUM ( fact_forecast[amount] )
```

```DAX
External Labor Spend =
SUM ( fact_external_labor[amount] )
```

```DAX
Cloud Spend =
SUM ( fact_cloud_spend[amount] )
```

```DAX
Vendor Spend =
SUM ( fact_vendor_spend[amount] )
```

```DAX
Project Spend =
SUM ( fact_project_spend[amount] )
```

---

## Section 2: Budget Measures

```DAX
Full-Year Budget =
CALCULATE (
    [Total Budget],
    ALL ( dim_date[month_number] )
)
```

```DAX
YTD Budget =
TOTALYTD ( [Total Budget], dim_date[date] )
```

```DAX
Budget by BU =
CALCULATE ( [Total Budget], ALLEXCEPT ( dim_business_unit, dim_business_unit[business_unit_name] ) )
```

---

## Section 3: Actuals Measures

```DAX
YTD Actuals =
TOTALYTD ( [Total Actuals], dim_date[date] )
```

```DAX
Prior Year Actuals =
CALCULATE ( [Total Actuals], SAMEPERIODLASTYEAR ( dim_date[date] ) )
```

```DAX
Monthly Actuals =
CALCULATE (
    [Total Actuals],
    ALLEXCEPT ( dim_date, dim_date[year_month] )
)
```

---

## Section 4: Forecast Measures

```DAX
Full-Year Forecast =
CALCULATE (
    [Total Forecast],
    ALL ( dim_date[month_number] )
)
```

```DAX
YTD Forecast =
TOTALYTD ( [Total Forecast], dim_date[date] )
```

```DAX
Remaining Forecast =
[Full-Year Forecast] - [YTD Actuals]
```

```DAX
Year-End Projection =
[YTD Actuals] + [Remaining Forecast]
```

```DAX
Forecast Accuracy % =
1 - ABS ( DIVIDE ( [Total Actuals] - [Total Forecast], [Total Forecast], 0 ) )
```

```DAX
Actuals vs Forecast =
[Total Actuals] - [Total Forecast]
```

---

## Section 5: Variance Measures

```DAX
YTD Variance =
[YTD Actuals] - [YTD Budget]
```

```DAX
YTD Variance % =
DIVIDE ( [YTD Variance], [YTD Budget], 0 )
```

```DAX
Forecast Variance =
[Full-Year Forecast] - [Full-Year Budget]
```

```DAX
Forecast Variance % =
DIVIDE ( [Forecast Variance], [Full-Year Budget], 0 )
```

```DAX
Monthly Variance =
[Total Actuals] - [Total Budget]
```

```DAX
Monthly Variance % =
DIVIDE ( [Monthly Variance], [Total Budget], 0 )
```

```DAX
Budget Status =
IF (
    [YTD Variance %] > 0.05, "Over Budget",
    IF ( [YTD Variance %] < -0.03, "Under Budget", "On Track" )
)
```

---

## Section 6: Time Intelligence Measures

```DAX
YoY Growth % =
DIVIDE (
    [Total Actuals] - CALCULATE ( [Total Actuals], SAMEPERIODLASTYEAR ( dim_date[date] ) ),
    CALCULATE ( [Total Actuals], SAMEPERIODLASTYEAR ( dim_date[date] ) ),
    0
)
```

```DAX
MoM Growth % =
DIVIDE (
    [Total Actuals] - CALCULATE ( [Total Actuals], DATEADD ( dim_date[date], -1, MONTH ) ),
    CALCULATE ( [Total Actuals], DATEADD ( dim_date[date], -1, MONTH ) ),
    0
)
```

```DAX
Run Rate =
AVERAGEX ( VALUES ( dim_date[year_month] ), [Total Actuals] ) * 12
```

```DAX
QTD Actuals =
TOTALQTD ( [Total Actuals], dim_date[date] )
```

```DAX
Prior Quarter Actuals =
CALCULATE (
    [Total Actuals],
    DATEADD ( DATESQTD ( dim_date[date] ), -1, QUARTER )
)
```

```DAX
Rolling 3 Month Actuals =
CALCULATE (
    [Total Actuals],
    DATESINPERIOD ( dim_date[date], LASTDATE ( dim_date[date] ), -3, MONTH )
)
```

```DAX
Rolling 12 Month Actuals =
CALCULATE (
    [Total Actuals],
    DATESINPERIOD ( dim_date[date], LASTDATE ( dim_date[date] ), -12, MONTH )
)
```

---

## Section 7: Headcount Measures

```DAX
Approved Positions =
SUM ( fact_headcount[approved_positions] )
```

```DAX
Headcount =
SUM ( fact_headcount[filled_positions] )
```

```DAX
Open Positions =
SUM ( fact_headcount[open_positions] )
```

```DAX
Vacancy Rate =
DIVIDE ( [Open Positions], [Approved Positions], 0 )
```

```DAX
Monthly Labor Cost =
SUM ( fact_headcount[monthly_labor_cost] )
```

```DAX
Cost per FTE =
DIVIDE ( [Monthly Labor Cost], [Headcount], 0 )
```

```DAX
Annualized Labor Cost =
[Monthly Labor Cost] * 12
```

```DAX
Headcount YoY Change =
[Headcount] - CALCULATE ( [Headcount], SAMEPERIODLASTYEAR ( dim_date[date] ) )
```

```DAX
Vacancy Rate Alert =
IF (
    [Vacancy Rate] > 0.15, "High",
    IF ( [Vacancy Rate] > 0.08, "Medium", "Normal" )
)
```

---

## Section 8: External Labor Measures

```DAX
External Labor Spend =
SUM ( fact_external_labor[amount] )
```

```DAX
YTD External Labor =
TOTALYTD ( [External Labor Spend], dim_date[date] )
```

```DAX
Contractor Count =
COUNTROWS ( fact_external_labor )
```

```DAX
Avg Hourly Rate =
AVERAGE ( fact_external_labor[hourly_rate] )
```

```DAX
Total Hours Billed =
SUM ( fact_external_labor[hours] )
```

```DAX
External Labor Risk Count =
CALCULATE (
    COUNTROWS ( fact_external_labor ),
    fact_external_labor[risk_level] = "High"
)
```

```DAX
External Labor YoY % =
DIVIDE (
    [External Labor Spend] - CALCULATE ( [External Labor Spend], SAMEPERIODLASTYEAR ( dim_date[date] ) ),
    CALCULATE ( [External Labor Spend], SAMEPERIODLASTYEAR ( dim_date[date] ) ),
    0
)
```

```DAX
Expiring in 90 Days =
CALCULATE (
    COUNTROWS ( fact_external_labor ),
    fact_external_labor[days_until_expiry] >= 0,
    fact_external_labor[days_until_expiry] <= 90
)
```

```DAX
External Labor % of Total =
DIVIDE ( [External Labor Spend], [Total Actuals], 0 )
```

---

## Section 9: Vendor Measures

```DAX
Vendor Spend =
SUM ( fact_vendor_spend[amount] )
```

```DAX
YTD Vendor Spend =
TOTALYTD ( [Vendor Spend], dim_date[date] )
```

```DAX
Prior Year Vendor Spend =
CALCULATE ( [Vendor Spend], SAMEPERIODLASTYEAR ( dim_date[date] ) )
```

```DAX
Vendor YoY Growth % =
DIVIDE (
    [Vendor Spend] - [Prior Year Vendor Spend],
    [Prior Year Vendor Spend],
    0
)
```

```DAX
Active Vendor Count =
DISTINCTCOUNT ( fact_vendor_spend[vendor_key] )
```

```DAX
Top Vendor Concentration % =
DIVIDE (
    MAXX (
        VALUES ( dim_vendor[vendor_name] ),
        CALCULATE ( [Vendor Spend] )
    ),
    [Vendor Spend],
    0
)
```

```DAX
Strategic Vendor Spend =
CALCULATE (
    [Vendor Spend],
    dim_vendor[vendor_tier] = "Strategic"
)
```

```DAX
Strategic Vendor % =
DIVIDE ( [Strategic Vendor Spend], [Vendor Spend], 0 )
```

---

## Section 10: Cloud Measures

```DAX
Cloud Spend =
SUM ( fact_cloud_spend[amount] )
```

```DAX
YTD Cloud Spend =
TOTALYTD ( [Cloud Spend], dim_date[date] )
```

```DAX
Azure Spend =
CALCULATE ( [Cloud Spend], dim_vendor[vendor_name] = "Microsoft Azure" )
```

```DAX
AWS Spend =
CALCULATE ( [Cloud Spend], dim_vendor[vendor_name] = "AWS" )
```

```DAX
Azure % of Cloud =
DIVIDE ( [Azure Spend], [Cloud Spend], 0 )
```

```DAX
AWS % of Cloud =
DIVIDE ( [AWS Spend], [Cloud Spend], 0 )
```

```DAX
Prior Year Cloud Spend =
CALCULATE ( [Cloud Spend], SAMEPERIODLASTYEAR ( dim_date[date] ) )
```

```DAX
Cloud Spend YoY % =
DIVIDE (
    [Cloud Spend] - [Prior Year Cloud Spend],
    [Prior Year Cloud Spend],
    0
)
```

```DAX
Cloud % of Total Actuals =
DIVIDE ( [Cloud Spend], [Total Actuals], 0 )
```

```DAX
Cloud Compute Spend =
CALCULATE ( [Cloud Spend], fact_cloud_spend[service_category] = "Compute" )
```

```DAX
Cloud Storage Spend =
CALCULATE ( [Cloud Spend], fact_cloud_spend[service_category] = "Storage" )
```

```DAX
Cloud Analytics Spend =
CALCULATE ( [Cloud Spend], fact_cloud_spend[service_category] = "Analytics" )
```

---

## Section 11: Project Measures

```DAX
Project Spend =
SUM ( fact_project_spend[amount] )
```

```DAX
Capex Spend =
CALCULATE ( [Project Spend], fact_project_spend[spend_type] = "Capex" )
```

```DAX
Opex Spend =
CALCULATE ( [Project Spend], fact_project_spend[spend_type] = "Opex" )
```

```DAX
Capex % of Project Spend =
DIVIDE ( [Capex Spend], [Project Spend], 0 )
```

```DAX
Active Project Count =
CALCULATE (
    DISTINCTCOUNT ( fact_project_spend[project_key] ),
    dim_project[project_status] = "Active"
)
```

```DAX
Project Variance =
[Project Spend] - CALCULATE ( [Total Budget], USERELATIONSHIP ( fact_project_spend[project_key], dim_project[project_key] ) )
```

---

## Section 12: Risk and Status Measures

```DAX
Risk Flag =
IF (
    [Forecast Variance %] > 0.05, "High Risk",
    IF ( [Forecast Variance %] > 0.02, "Medium Risk", "On Track" )
)
```

```DAX
Risk Flag Color =
SWITCH (
    [Risk Flag],
    "High Risk", "#D9534F",
    "Medium Risk", "#F0AD4E",
    "#5CB85C"
)
```

```DAX
Variance Color =
IF ( [YTD Variance] > 0, "#D9534F", "#5CB85C" )
```

```DAX
KPI Arrow =
IF (
    [YTD Variance %] > 0, "▲",
    IF ( [YTD Variance %] < 0, "▼", "►" )
)
```

```DAX
Transaction Count =
COUNTROWS ( fact_actuals )
```

```DAX
Avg Transaction Amount =
DIVIDE ( [Total Actuals], [Transaction Count], 0 )
```

---

## Measure Formatting Reference

After creating all measures, apply these format strings in the Measure properties pane:

| Measure | Format String |
|---|---|
| Total Actuals | `$#,##0.00` |
| Total Budget | `$#,##0.00` |
| Total Forecast | `$#,##0.00` |
| YTD Actuals | `$#,##0.00` |
| YTD Budget | `$#,##0.00` |
| YTD Variance | `$#,##0.00;($#,##0.00)` |
| Full-Year Budget | `$#,##0.00` |
| Full-Year Forecast | `$#,##0.00` |
| Year-End Projection | `$#,##0.00` |
| YTD Variance % | `0.0%` |
| Forecast Variance % | `0.0%` |
| Forecast Accuracy % | `0.0%` |
| YoY Growth % | `+0.0%;-0.0%;0.0%` |
| MoM Growth % | `+0.0%;-0.0%;0.0%` |
| Cloud Spend YoY % | `+0.0%;-0.0%;0.0%` |
| Vacancy Rate | `0.0%` |
| External Labor % of Total | `0.0%` |
| Azure % of Cloud | `0.0%` |
| Capex % of Project Spend | `0.0%` |
| Headcount | `#,##0` |
| Approved Positions | `#,##0` |
| Open Positions | `#,##0` |
| Contractor Count | `#,##0` |
| Avg Hourly Rate | `$#,##0` |
| Cost per FTE | `$#,##0` |
| External Labor Spend | `$#,##0.00` |
| Cloud Spend | `$#,##0.00` |
| Vendor Spend | `$#,##0.00` |
| Project Spend | `$#,##0.00` |

---

## Measure Organization (Display Folders)

After creating measures, group them in display folders for easier navigation.
In the Measure properties pane, set the **Display folder** field:

| Folder Name | Measures |
|---|---|
| 01 Base | Total Actuals, Total Budget, Total Forecast |
| 02 YTD | YTD Actuals, YTD Budget, YTD Forecast, YTD Variance, YTD Variance % |
| 03 Full Year | Full-Year Budget, Full-Year Forecast, Remaining Forecast, Year-End Projection |
| 04 Variance | Monthly Variance, Monthly Variance %, Budget Status, Forecast Variance, Forecast Variance % |
| 05 Time Intelligence | YoY Growth %, MoM Growth %, Run Rate, QTD Actuals, Rolling 3 Month Actuals |
| 06 Headcount | All headcount measures |
| 07 External Labor | All external labor measures |
| 08 Vendors | All vendor measures |
| 09 Cloud | All cloud measures |
| 10 Projects | All project measures |
| 11 Risk | Risk Flag, Variance Color, KPI Arrow |
