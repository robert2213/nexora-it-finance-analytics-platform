# Power BI Build Checklist
## Nexora IT Financial Command Center

---

## Phase 1 — Data Model

### Step 1: Open Power BI Desktop
- [ ] Launch Power BI Desktop (version 2.120+ recommended)
- [ ] Create a new file: `Nexora_IT_Financial_Command_Center.pbix`
- [ ] Save immediately to your local working folder

---

### Step 2: Import All CSV Files

Go to **Home > Get Data > Text/CSV** and import each file in this order:

**Dimension Tables (import first):**
- [ ] `dim_date.csv`
- [ ] `dim_business_unit.csv`
- [ ] `dim_cost_center.csv`
- [ ] `dim_gl_account.csv`
- [ ] `dim_vendor.csv`
- [ ] `dim_project.csv`
- [ ] `dim_employee.csv`

**Fact Tables (import second):**
- [ ] `fact_actuals.csv`
- [ ] `fact_budget.csv`
- [ ] `fact_forecast.csv`
- [ ] `fact_headcount.csv`
- [ ] `fact_external_labor.csv`
- [ ] `fact_vendor_spend.csv`
- [ ] `fact_cloud_spend.csv`
- [ ] `fact_project_spend.csv`

---

### Step 3: Power Query Transformations

Open **Transform Data** (Power Query Editor) and apply the following for each table:

#### dim_date
- [ ] Set `date_key` → **Whole Number**
- [ ] Set `date` → **Date**
- [ ] Set `year`, `month_number`, `quarter_number` → **Whole Number**
- [ ] Set `month_name`, `quarter_name`, `year_month` → **Text**
- [ ] Confirm no blank rows
- [ ] Name table: `dim_date`

#### dim_business_unit
- [ ] Set `business_unit_key` → **Text**
- [ ] Set all other columns → **Text**
- [ ] Name table: `dim_business_unit`

#### dim_cost_center
- [ ] Set `cost_center_key` → **Text**
- [ ] Set `business_unit_key` → **Text**
- [ ] Set all other columns → **Text**
- [ ] Name table: `dim_cost_center`

#### dim_gl_account
- [ ] Set `gl_account_key` → **Whole Number**
- [ ] Set `gl_category`, `gl_description` → **Text**
- [ ] Name table: `dim_gl_account`

#### dim_vendor
- [ ] Set `vendor_key` → **Text**
- [ ] Set all other columns → **Text**
- [ ] Name table: `dim_vendor`

#### dim_project
- [ ] Set `project_key` → **Text**
- [ ] Set all other columns → **Text**
- [ ] Name table: `dim_project`

#### dim_employee
- [ ] Set `employee_key` → **Text**
- [ ] Set date columns → **Date**
- [ ] Set numeric columns → **Whole Number** or **Decimal**
- [ ] Name table: `dim_employee`

#### fact_actuals
- [ ] Set `date_key` → **Whole Number**
- [ ] Set `cost_center_key`, `business_unit_key`, `vendor_key`, `project_key`, `scenario` → **Text**
- [ ] Set `gl_account_key` → **Whole Number**
- [ ] Set `amount` → **Fixed Decimal Number** (currency)
- [ ] Set `transaction_date` → **Date**
- [ ] Remove or keep `notes` column as **Text**
- [ ] Name table: `fact_actuals`

#### fact_budget
- [ ] Set `date_key` → **Whole Number**
- [ ] Set key columns → **Text** (cost_center_key, business_unit_key, gl_account_key)
- [ ] Set `gl_account_key` → **Whole Number**
- [ ] Set `amount` → **Fixed Decimal Number**
- [ ] Name table: `fact_budget`

#### fact_forecast
- [ ] Set `date_key` → **Whole Number**
- [ ] Set key columns → **Text**
- [ ] Set `gl_account_key` → **Whole Number**
- [ ] Set `amount` → **Fixed Decimal Number**
- [ ] Set `forecast_cycle` → **Text**
- [ ] Name table: `fact_forecast`

#### fact_headcount
- [ ] Set `date_key` → **Whole Number**
- [ ] Set `cost_center_key`, `business_unit_key` → **Text**
- [ ] Set `approved_positions`, `filled_positions`, `open_positions` → **Whole Number**
- [ ] Set `vacancy_rate` → **Decimal Number**
- [ ] Set `monthly_labor_cost` → **Fixed Decimal Number**
- [ ] Name table: `fact_headcount`

#### fact_external_labor
- [ ] Set `date_key` → **Whole Number**
- [ ] Set `cost_center_key`, `business_unit_key`, `vendor_key`, `project_key` → **Text**
- [ ] Set `hourly_rate` → **Fixed Decimal Number**
- [ ] Set `hours` → **Whole Number**
- [ ] Set `amount` → **Fixed Decimal Number**
- [ ] Set `contract_end_date` → **Date**
- [ ] Set `risk_level` → **Text**
- [ ] Name table: `fact_external_labor`

#### fact_vendor_spend
- [ ] Set `date_key` → **Whole Number**
- [ ] Set key columns → **Text**
- [ ] Set `gl_account_key` → **Whole Number**
- [ ] Set `amount` → **Fixed Decimal Number**
- [ ] Name table: `fact_vendor_spend`

#### fact_cloud_spend
- [ ] Set `date_key` → **Whole Number**
- [ ] Set `cost_center_key`, `business_unit_key`, `vendor_key`, `project_key` → **Text**
- [ ] Set `service_category` → **Text**
- [ ] Set `amount` → **Fixed Decimal Number**
- [ ] Name table: `fact_cloud_spend`

#### fact_project_spend
- [ ] Set `date_key` → **Whole Number**
- [ ] Set key columns → **Text**
- [ ] Set `gl_account_key` → **Whole Number**
- [ ] Set `amount` → **Fixed Decimal Number**
- [ ] Set `spend_type` (Capex/Opex) → **Text**
- [ ] Name table: `fact_project_spend`

- [ ] **Close & Apply** all Power Query changes

---

### Step 4: Mark the Date Table

In the **Model view**:
- [ ] Select `dim_date`
- [ ] Go to **Table tools > Mark as date table**
- [ ] Set the date column to `date`
- [ ] Click OK — Power BI will validate the table

---

### Step 5: Create Relationships

In **Model view**, create the following relationships. All relationships are **one-to-many** (dimension → fact), **single cross-filter direction**.

#### dim_date (1) → fact tables (many)

| From | To | Join Key |
|---|---|---|
| dim_date[date_key] | fact_actuals[date_key] | date_key |
| dim_date[date_key] | fact_budget[date_key] | date_key |
| dim_date[date_key] | fact_forecast[date_key] | date_key |
| dim_date[date_key] | fact_headcount[date_key] | date_key |
| dim_date[date_key] | fact_external_labor[date_key] | date_key |
| dim_date[date_key] | fact_vendor_spend[date_key] | date_key |
| dim_date[date_key] | fact_cloud_spend[date_key] | date_key |
| dim_date[date_key] | fact_project_spend[date_key] | date_key |

#### dim_cost_center (1) → fact tables (many)

| From | To | Join Key |
|---|---|---|
| dim_cost_center[cost_center_key] | fact_actuals[cost_center_key] | cost_center_key |
| dim_cost_center[cost_center_key] | fact_budget[cost_center_key] | cost_center_key |
| dim_cost_center[cost_center_key] | fact_forecast[cost_center_key] | cost_center_key |
| dim_cost_center[cost_center_key] | fact_headcount[cost_center_key] | cost_center_key |
| dim_cost_center[cost_center_key] | fact_external_labor[cost_center_key] | cost_center_key |
| dim_cost_center[cost_center_key] | fact_vendor_spend[cost_center_key] | cost_center_key |
| dim_cost_center[cost_center_key] | fact_cloud_spend[cost_center_key] | cost_center_key |
| dim_cost_center[cost_center_key] | fact_project_spend[cost_center_key] | cost_center_key |

#### dim_business_unit (1) → fact tables (many)

| From | To | Join Key |
|---|---|---|
| dim_business_unit[business_unit_key] | fact_actuals[business_unit_key] | business_unit_key |
| dim_business_unit[business_unit_key] | fact_budget[business_unit_key] | business_unit_key |
| dim_business_unit[business_unit_key] | fact_forecast[business_unit_key] | business_unit_key |
| dim_business_unit[business_unit_key] | fact_headcount[business_unit_key] | business_unit_key |
| dim_business_unit[business_unit_key] | fact_external_labor[business_unit_key] | business_unit_key |
| dim_business_unit[business_unit_key] | fact_cloud_spend[business_unit_key] | business_unit_key |
| dim_business_unit[business_unit_key] | fact_project_spend[business_unit_key] | business_unit_key |

#### dim_vendor (1) → fact tables (many)

| From | To | Join Key |
|---|---|---|
| dim_vendor[vendor_key] | fact_external_labor[vendor_key] | vendor_key |
| dim_vendor[vendor_key] | fact_vendor_spend[vendor_key] | vendor_key |
| dim_vendor[vendor_key] | fact_cloud_spend[vendor_key] | vendor_key |

#### dim_gl_account (1) → fact tables (many)

| From | To | Join Key |
|---|---|---|
| dim_gl_account[gl_account_key] | fact_actuals[gl_account_key] | gl_account_key |
| dim_gl_account[gl_account_key] | fact_budget[gl_account_key] | gl_account_key |
| dim_gl_account[gl_account_key] | fact_vendor_spend[gl_account_key] | gl_account_key |
| dim_gl_account[gl_account_key] | fact_project_spend[gl_account_key] | gl_account_key |

#### dim_project (1) → fact tables (many)

| From | To | Join Key |
|---|---|---|
| dim_project[project_key] | fact_external_labor[project_key] | project_key |
| dim_project[project_key] | fact_cloud_spend[project_key] | project_key |
| dim_project[project_key] | fact_project_spend[project_key] | project_key |

- [ ] Verify: No circular relationships in model view
- [ ] Verify: All active relationships shown with solid lines
- [ ] Verify: Inactive relationships (if any) shown as dashed lines

---

### Step 6: Create a Measures Table

- [ ] In **Report view**, go to **Enter Data**
- [ ] Create a blank table named `_Measures` with one column and no rows
- [ ] Delete the auto-generated column
- [ ] This keeps all DAX measures organized in one place

---

## Phase 2 — DAX Measures

Create all measures inside the `_Measures` table. Build in dependency order — base measures first, then calculated measures that reference them.

### Tier 1 — Base Aggregations

```DAX
Total Actuals =
SUM(fact_actuals[amount])

Total Budget =
SUM(fact_budget[amount])

Total Forecast =
SUM(fact_forecast[amount])

External Labor Spend =
SUM(fact_external_labor[amount])

Cloud Spend =
SUM(fact_cloud_spend[amount])

Vendor Spend =
SUM(fact_vendor_spend[amount])

Project Spend =
SUM(fact_project_spend[amount])
```

### Tier 2 — Headcount Base

```DAX
Headcount =
SUM(fact_headcount[filled_positions])

Approved Positions =
SUM(fact_headcount[approved_positions])

Open Positions =
SUM(fact_headcount[open_positions])

Monthly Labor Cost =
SUM(fact_headcount[monthly_labor_cost])
```

### Tier 3 — YTD Measures

```DAX
YTD Actuals =
TOTALYTD([Total Actuals], dim_date[date])

YTD Budget =
TOTALYTD([Total Budget], dim_date[date])

YTD Forecast =
TOTALYTD([Total Forecast], dim_date[date])

YTD External Labor =
TOTALYTD([External Labor Spend], dim_date[date])

YTD Cloud Spend =
TOTALYTD([Cloud Spend], dim_date[date])

YTD Vendor Spend =
TOTALYTD([Vendor Spend], dim_date[date])
```

### Tier 4 — Variance Measures

```DAX
YTD Variance =
[YTD Actuals] - [YTD Budget]

YTD Variance % =
DIVIDE([YTD Variance], [YTD Budget], 0)

Forecast Variance =
[Full-Year Forecast] - [Full-Year Budget]

Forecast Variance % =
DIVIDE([Forecast Variance], [Full-Year Budget], 0)

Actuals vs Forecast =
[Total Actuals] - [Total Forecast]
```

### Tier 5 — Full-Year and Projection

```DAX
Full-Year Budget =
CALCULATE(
    [Total Budget],
    ALL(dim_date[month_number])
)

Full-Year Forecast =
CALCULATE(
    [Total Forecast],
    ALL(dim_date[month_number])
)

Remaining Forecast =
[Full-Year Forecast] - [YTD Actuals]

Year-End Projection =
[YTD Actuals] + [Remaining Forecast]
```

### Tier 6 — Rate and Efficiency

```DAX
Vacancy Rate =
DIVIDE([Open Positions], [Approved Positions], 0)

Cost per FTE =
DIVIDE([YTD Actuals], [Headcount], 0)

Forecast Accuracy % =
1 - ABS(DIVIDE([Actuals vs Forecast], [Total Forecast], 0))

Run Rate =
AVERAGEX(VALUES(dim_date[year_month]), [Total Actuals]) * 12
```

### Tier 7 — Time Intelligence

```DAX
YoY Growth % =
DIVIDE(
    [Total Actuals] - CALCULATE([Total Actuals], SAMEPERIODLASTYEAR(dim_date[date])),
    CALCULATE([Total Actuals], SAMEPERIODLASTYEAR(dim_date[date])),
    0
)

MoM Growth % =
DIVIDE(
    [Total Actuals] - CALCULATE([Total Actuals], DATEADD(dim_date[date], -1, MONTH)),
    CALCULATE([Total Actuals], DATEADD(dim_date[date], -1, MONTH)),
    0
)

Prior Year Actuals =
CALCULATE([Total Actuals], SAMEPERIODLASTYEAR(dim_date[date]))

Prior Year Cloud Spend =
CALCULATE([Cloud Spend], SAMEPERIODLASTYEAR(dim_date[date]))

Cloud Spend YoY % =
DIVIDE(
    [Cloud Spend] - [Prior Year Cloud Spend],
    [Prior Year Cloud Spend],
    0
)
```

### Tier 8 — Risk and Status Flags

```DAX
Risk Flag =
IF(
    [Forecast Variance %] > 0.05, "High Risk",
    IF([Forecast Variance %] > 0.02, "Medium Risk", "On Track")
)

External Labor Risk Count =
CALCULATE(
    COUNTROWS(fact_external_labor),
    fact_external_labor[risk_level] = "High"
)

Budget Status =
IF(
    [YTD Variance %] > 0.05, "Over Budget",
    IF([YTD Variance %] < -0.03, "Under Budget", "On Track")
)
```

### Tier 9 — Format Helpers (optional but recommended)

```DAX
YTD Variance Color =
IF([YTD Variance] > 0, "#D9534F", "#5CB85C")

Forecast Risk Color =
SWITCH(
    [Risk Flag],
    "High Risk", "#D9534F",
    "Medium Risk", "#F0AD4E",
    "#5CB85C"
)
```

- [ ] Format all currency measures as **$ #,##0** or **$ #,##0.0M** for KPI cards
- [ ] Format all percentage measures as **0.0%**
- [ ] Format headcount measures as **#,##0**
- [ ] Add descriptions to each measure (right-click > Description)

---

## Phase 3 — Dashboard Build Order

Build pages in this sequence to manage slicer and cross-filter dependencies correctly.

| Build Order | Page Name | Primary Fact Table |
|---|---|---|
| 1 | Drill-through Detail | fact_actuals |
| 2 | CIO Executive Summary | fact_actuals, fact_budget, fact_forecast |
| 3 | Budget vs Actuals | fact_actuals, fact_budget |
| 4 | Forecast & Projection | fact_forecast, fact_budget, fact_actuals |
| 5 | Headcount | fact_headcount |
| 6 | External Labor | fact_external_labor |
| 7 | Vendor Spend | fact_vendor_spend |
| 8 | Cloud Spend | fact_cloud_spend |
| 9 | Project Spend | fact_project_spend |

Build the drill-through detail page first so other pages can reference it immediately during testing.

---

### Global Slicers (add to every page using Sync Slicers)

Go to **View > Sync Slicers** and sync the following slicers across all pages:

| Slicer | Field | Type |
|---|---|---|
| Year | dim_date[year] | Dropdown |
| Month | dim_date[month_name] | Dropdown |
| Business Unit | dim_business_unit[business_unit_name] | List or Dropdown |
| Cost Center | dim_cost_center[cost_center_name] | Dropdown |
| Forecast Cycle | fact_forecast[forecast_cycle] | Dropdown |

Page-specific slicers (not synced):
| Page | Slicer | Field |
|---|---|---|
| Vendor Spend | Vendor | dim_vendor[vendor_name] |
| Cloud Spend | Provider | dim_vendor[vendor_name] (Cloud tier) |
| External Labor | Risk Level | fact_external_labor[risk_level] |
| Project Spend | Project | dim_project[project_name] |
| Budget vs Actuals | GL Category | dim_gl_account[gl_category] |

---

### Page Settings (apply to every page)

- [ ] Page size: **16:9** (1280 x 720 or 1920 x 1080)
- [ ] Canvas background: `#0D1B2A` (dark navy) or `#F5F5F5` (light corporate)
- [ ] Report theme: Apply the Nexora custom theme (see Theme Specifications)

---

## Phase 4 — Validation Checks

After building all pages, complete these validation steps before publishing.

### Financial Totals Validation

| Check | Method |
|---|---|
| Total Actuals ties to source | Build a matrix by year and sum — compare to expected range |
| Total Budget ties to source | Same as above for fact_budget |
| YTD Actuals = sum of months through selected month | Filter to Dec and verify YTD = full year |
| Year-End Projection is reasonable | Should be close to Full-Year Budget in early months |
| Variance % is directionally correct | Positive = over budget, negative = under budget |
| Cloud Spend is subset of Total Actuals | Cloud Spend should be < Total Actuals |
| External Labor Spend cross-checks | Compare to GL 612000 + 612050 in fact_actuals |

### Relationship Validation

| Check | Method |
|---|---|
| No blanks in slicer selections | Select each slicer and check for blank rows |
| dim_date covers all fact dates | Create a measure: COUNTROWS(fact_actuals) — should not change with date slicer |
| No duplicate relationships | Model view: no ambiguous path warnings |

### Visual Validation

| Check | Method |
|---|---|
| KPI cards update with slicer selection | Change year slicer — all cards should update |
| Drill-through works from all source pages | Right-click a data point > Drill through > Detail |
| Tooltips display on hover | Hover over each visual type |
| Conditional formatting renders | Over-budget rows should appear red |
| All visuals render without errors | Check for yellow warning triangles |

---

## Phase 5 — Polish and Publish

- [ ] Add report title text box to each page header
- [ ] Add footer with: `Nexora IT Financial Command Center | Confidential | Data through {latest month}`
- [ ] Add executive commentary text boxes (see Executive Mockups)
- [ ] Add Nexora logo placeholder (top left of each page)
- [ ] Apply consistent font size hierarchy (Title 18pt, Section 14pt, Body 11pt)
- [ ] Verify mobile layout (View > Mobile Layout) for key KPI pages
- [ ] Save final .pbix file
- [ ] Export each page as PNG for portfolio screenshots (File > Export > Export to PDF or use Snipping Tool)
- [ ] Upload screenshots to `project-2-it-financial-command-center-5yr/assets/screenshots/`

---

## Implementation Roadmap

### Phase 1 — Data Model (Day 1, ~2–3 hours)
- Import all 15 CSV files
- Apply all Power Query type corrections
- Mark dim_date as date table
- Build all 30+ relationships
- Validate no errors in model view

### Phase 2 — Measures (Day 1–2, ~2–3 hours)
- Create _Measures table
- Build all 30 DAX measures in tier order
- Spot-check each measure in a card visual
- Format all measure output types

### Phase 3 — Visuals (Day 2–3, ~4–6 hours)
- Build Drill-through Detail page first
- Build remaining 8 pages following visual specifications
- Apply sync slicers across all pages
- Add conditional formatting and tooltips

### Phase 4 — Executive Storytelling (Day 3, ~2–3 hours)
- Add commentary text boxes to each page
- Insert executive insight callouts
- Apply theme, fonts, and colors
- Finalize navigation buttons between pages

### Phase 5 — Portfolio Screenshots (Day 4, ~1–2 hours)
- Final review of all pages
- Export PNG screenshots for each page
- Commit screenshots to GitHub repository
- Update README with screenshot previews

**Total Estimated Build Time: 12–17 hours**
