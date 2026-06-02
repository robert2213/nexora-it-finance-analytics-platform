# Power BI Visual Specifications
## Nexora IT Financial Command Center

---

## Page 1 — CIO Executive Summary

**Purpose:** Single-page view for the CIO operating review. Provides the complete financial picture in under 60 seconds.

---

### Slicer Panel (left column, stacked vertically)

| Slicer | Field | Width | Type |
|---|---|---|---|
| Year | dim_date[year] | 180px | Dropdown |
| Month | dim_date[month_name] | 180px | Dropdown |
| Business Unit | dim_business_unit[business_unit_name] | 180px | List (multi-select) |
| Forecast Cycle | fact_forecast[forecast_cycle] | 180px | Dropdown |

**Sync behavior:** All four slicers sync to all pages via Sync Slicers.

---

### Row 1 — KPI Card Strip

| Visual # | Visual Type | Measure | Label | Format | Position |
|---|---|---|---|---|---|
| 1.1 | KPI Card | [YTD Actuals] | YTD Actuals | $ #,##0.0M | Top row, card 1 |
| 1.2 | KPI Card | [YTD Budget] | YTD Budget | $ #,##0.0M | Top row, card 2 |
| 1.3 | KPI Card | [YTD Variance] | YTD Variance | $ #,##0.0M | Top row, card 3 |
| 1.4 | KPI Card | [YTD Variance %] | Variance % | 0.0% | Top row, card 4 |
| 1.5 | KPI Card | [Year-End Projection] | Year-End Projection | $ #,##0.0M | Top row, card 5 |
| 1.6 | KPI Card | [Risk Flag] | Risk Status | Text | Top row, card 6 |

**Conditional formatting on KPI Card 1.3 (YTD Variance):**
- Positive value (over budget): font color `#D9534F` (red)
- Negative value (under budget): font color `#5CB85C` (green)

**Conditional formatting on KPI Card 1.6 (Risk Flag):**
- "High Risk": background `#D9534F`, white text
- "Medium Risk": background `#F0AD4E`, white text
- "On Track": background `#5CB85C`, white text

**Tooltip on all KPI cards:**
- Show: Measure value, YoY change `[YoY Growth %]`, prior year value `[Prior Year Actuals]`

---

### Row 2 — Trend and Breakdown Visuals

#### Visual 1.7 — Monthly Actuals vs Budget Trend (Line and Clustered Column)
| Property | Value |
|---|---|
| Visual Type | Line and Clustered Column Chart |
| Column Y axis | [Total Actuals] |
| Line Y axis | [Total Budget] |
| X axis | dim_date[month_name] |
| Legend | Actuals (column), Budget (line) |
| Color — Actuals | `#1E88E5` (blue) |
| Color — Budget | `#F0AD4E` (amber dashed) |
| Data labels | Off (too crowded at monthly level) |
| Tooltip | Month, Actuals, Budget, Variance $, Variance % |
| Drill-through | Right-click > Drill Through > Drill-through Detail |
| Interaction | Clicking a month filters all other visuals on the page |
| Width | ~45% of canvas |
| Height | ~35% of canvas |

#### Visual 1.8 — Spend by Business Unit (Clustered Bar)
| Property | Value |
|---|---|
| Visual Type | Clustered Bar Chart |
| Y axis | dim_business_unit[business_unit_name] |
| X axis | [Total Actuals] |
| Color | Single color `#1E88E5` |
| Data labels | On — show values in $ millions |
| Sort | Descending by [Total Actuals] |
| Tooltip | Business Unit, Actuals, Budget, Variance $ |
| Drill-through | Yes — right-click to detail page |
| Width | ~25% of canvas |
| Height | ~35% of canvas |

#### Visual 1.9 — Spend by GL Category (Donut Chart)
| Property | Value |
|---|---|
| Visual Type | Donut Chart |
| Legend | dim_gl_account[gl_category] |
| Values | [Total Actuals] |
| Detail labels | Category name + percentage |
| Colors | Use categorical palette (see Theme section) |
| Tooltip | GL Category, Actuals $, % of total |
| Interaction | Clicking a slice filters other visuals on page |
| Width | ~25% of canvas |
| Height | ~35% of canvas |

---

### Row 3 — Supporting Analysis

#### Visual 1.10 — Top 5 Variance Drivers (Table)
| Property | Value |
|---|---|
| Visual Type | Table |
| Columns | dim_cost_center[cost_center_name], dim_gl_account[gl_category], [Total Actuals], [Total Budget], [YTD Variance], [YTD Variance %] |
| Sort | [YTD Variance] descending (most over budget first) |
| Conditional formatting | [YTD Variance] — red bars for positive, green bars for negative |
| Row limit | Top 5 (use Top N filter on dim_cost_center) |
| Tooltip | Full cost center name, owner, GL description |
| Drill-through | Click row > Drill-through Detail |
| Width | ~50% of canvas |
| Height | ~25% of canvas |

#### Visual 1.11 — Executive Commentary (Text Box)
| Property | Value |
|---|---|
| Visual Type | Text Box |
| Content | Static text — update monthly with key insight bullets |
| Font | Segoe UI, 11pt |
| Background | `#1C2B3A` (dark blue-grey) |
| Font Color | White |
| Border | 1px `#2D4A6A` |
| Example Content | "Cloud Platform Engineering (CC 104018) is tracking 8.2% over YTD budget, driven by Azure Storage and Compute consumption growth. External labor contracts in Data Engineering expire Q3 2026 — renewal review recommended." |
| Width | ~45% of canvas |
| Height | ~25% of canvas |

---

## Page 2 — Budget vs Actuals

**Purpose:** Month-by-month tracking of budget execution. Primary tool for finance review meetings.

---

### Slicers

| Slicer | Field | Notes |
|---|---|---|
| Year | dim_date[year] | Synced |
| Month (through) | dim_date[month_name] | Synced — sets YTD cutoff |
| Business Unit | dim_business_unit[business_unit_name] | Synced |
| Cost Center | dim_cost_center[cost_center_name] | Local — not synced |
| GL Category | dim_gl_account[gl_category] | Local — not synced |

---

### Row 1 — KPI Cards

| Visual | Measure | Format |
|---|---|---|
| 2.1 | [YTD Actuals] | $ #,##0.0M |
| 2.2 | [YTD Budget] | $ #,##0.0M |
| 2.3 | [YTD Variance] | $ #,##0.0M — conditional color |
| 2.4 | [YTD Variance %] | 0.0% — conditional color |
| 2.5 | [Budget Status] | Text — conditional background |

---

### Row 2 — Primary Chart

#### Visual 2.6 — Monthly Actuals vs Budget (Line and Clustered Column)
| Property | Value |
|---|---|
| Visual Type | Line and Clustered Column Chart |
| Column | [Total Actuals] by dim_date[month_name] |
| Line | [Total Budget] by dim_date[month_name] |
| Secondary Y axis | Off — use same scale |
| Constant line | None |
| Data labels | Off |
| Zoom slider | On — allows user to zoom to specific month range |
| Tooltip | Month, Actuals, Budget, Variance $, Variance %, YoY Actuals |
| Drill-through | Right-click > Drill-through Detail |
| Width | ~70% of canvas |
| Height | ~35% of canvas |

---

### Row 3 — Breakdown Matrices

#### Visual 2.7 — Variance by Cost Center (Matrix)
| Property | Value |
|---|---|
| Visual Type | Matrix |
| Rows | dim_cost_center[cost_center_name] |
| Columns | dim_date[month_name] |
| Values | [YTD Variance] |
| Subtotals | Row totals on — Column totals off |
| Conditional formatting | Background color scale — red (high positive) → white → green (negative) |
| Drill-through | Click row header > Drill-through Detail |
| Width | ~48% of canvas |
| Height | ~35% of canvas |

#### Visual 2.8 — Variance by GL Category (Bar Chart)
| Property | Value |
|---|---|
| Visual Type | Clustered Bar Chart |
| Y axis | dim_gl_account[gl_category] |
| X axis | [YTD Variance] |
| Colors | Conditional — positive bars red, negative bars green |
| Zero line | Show reference line at zero |
| Data labels | On — show variance in $K |
| Tooltip | GL Category, Description, Actuals, Budget, Variance, Variance % |
| Width | ~48% of canvas |
| Height | ~35% of canvas |

---

## Page 3 — Forecast & Projection

**Purpose:** Compare 3+9, 6+6, and 9+3 forecast scenarios and track year-end projection accuracy.

---

### Slicers

| Slicer | Field | Notes |
|---|---|---|
| Year | dim_date[year] | Synced |
| Business Unit | dim_business_unit[business_unit_name] | Synced |
| Forecast Cycle | fact_forecast[forecast_cycle] | Local — key for this page |
| Cost Center | dim_cost_center[cost_center_name] | Local |

---

### Row 1 — KPI Cards

| Visual | Measure | Format |
|---|---|---|
| 3.1 | [Full-Year Budget] | $ #,##0.0M |
| 3.2 | [Full-Year Forecast] | $ #,##0.0M |
| 3.3 | [Forecast Variance] | $ #,##0.0M — conditional |
| 3.4 | [Forecast Variance %] | 0.0% — conditional |
| 3.5 | [Forecast Accuracy %] | 0.0% |
| 3.6 | [Remaining Forecast] | $ #,##0.0M |

---

### Row 2 — Forecast Comparison

#### Visual 3.7 — Forecast Cycle Comparison (Clustered Column)
| Property | Value |
|---|---|
| Visual Type | Clustered Column Chart |
| X axis | fact_forecast[forecast_cycle] (3+9, 6+6, 9+3) |
| Y axis | [Full-Year Forecast] |
| Reference line | [Full-Year Budget] as a constant line |
| Color | Each cycle a distinct color from the theme palette |
| Data labels | On — show $ millions |
| Tooltip | Forecast Cycle, Full-Year Forecast, Budget, Forecast Variance |
| Width | ~35% of canvas |
| Height | ~35% of canvas |

#### Visual 3.8 — Actuals + Forecast Full-Year View (Area Chart)
| Property | Value |
|---|---|
| Visual Type | Area Chart |
| X axis | dim_date[month_name] |
| Y axis values | [Total Actuals] (solid fill), [Total Forecast] (lighter fill) |
| Reference line | Full-Year Budget as horizontal line |
| Colors | Actuals: `#1E88E5`, Forecast: `#90CAF9` (lighter blue) |
| Tooltip | Month, Actuals, Forecast, Budget, Projection |
| Note | Actuals cover Jan–current month; Forecast covers remaining months |
| Width | ~60% of canvas |
| Height | ~35% of canvas |

---

### Row 3 — Risk and Opportunity

#### Visual 3.9 — Risk/Opportunity Flag Table
| Property | Value |
|---|---|
| Visual Type | Table |
| Columns | dim_cost_center[cost_center_name], [Full-Year Forecast], [Full-Year Budget], [Forecast Variance], [Forecast Variance %], [Risk Flag] |
| Sort | [Forecast Variance] descending |
| Conditional formatting on Risk Flag | Color by risk level (Red/Yellow/Green) |
| Conditional formatting on Forecast Variance % | Data bars |
| Width | ~60% of canvas |
| Height | ~30% of canvas |

#### Visual 3.10 — Year-End Projection vs Budget (Gauge)
| Property | Value |
|---|---|
| Visual Type | Gauge |
| Value | [Year-End Projection] |
| Minimum | 0 |
| Maximum | [Full-Year Budget] * 1.15 |
| Target | [Full-Year Budget] |
| Color | Needle color changes based on [Risk Flag] |
| Tooltip | Projection, Budget, Variance |
| Width | ~35% of canvas |
| Height | ~30% of canvas |

---

## Page 4 — External Labor

**Purpose:** Track contractor spend, headcount, rates, and contract expiry risk.

---

### Slicers

| Slicer | Field | Notes |
|---|---|---|
| Year | dim_date[year] | Synced |
| Business Unit | dim_business_unit[business_unit_name] | Synced |
| Risk Level | fact_external_labor[risk_level] | Local |
| Vendor | dim_vendor[vendor_name] | Local |
| Project | dim_project[project_name] | Local |

---

### Row 1 — KPI Cards

| Visual | Measure | Format |
|---|---|---|
| 4.1 | [External Labor Spend] | $ #,##0.0M |
| 4.2 | COUNTROWS(fact_external_labor) | # — Contractor Engagements |
| 4.3 | AVERAGE(fact_external_labor[hourly_rate]) | $ #,##0 — Avg Hourly Rate |
| 4.4 | [External Labor Risk Count] | # — High Risk Contracts |
| 4.5 | [YoY Growth %] (filtered to External Labor) | 0.0% — YoY Change |

---

### Row 2 — Trend and Volume

#### Visual 4.6 — External Labor Spend Trend (Line Chart)
| Property | Value |
|---|---|
| Visual Type | Line Chart |
| X axis | dim_date[year_month] |
| Y axis | [External Labor Spend] |
| Secondary line | COUNTROWS(fact_external_labor) on secondary axis |
| Tooltip | Month, Spend, Headcount, Avg Rate |
| Width | ~55% of canvas |
| Height | ~30% of canvas |

#### Visual 4.7 — Spend by Vendor (Clustered Bar)
| Property | Value |
|---|---|
| Visual Type | Clustered Bar Chart |
| Y axis | dim_vendor[vendor_name] |
| X axis | [External Labor Spend] |
| Filter | Only vendors where vendor_category = "External Labor" |
| Data labels | On |
| Sort | Descending |
| Width | ~40% of canvas |
| Height | ~30% of canvas |

---

### Row 3 — Risk and Detail

#### Visual 4.8 — Contract End Date Risk Table
| Property | Value |
|---|---|
| Visual Type | Table |
| Columns | fact_external_labor[resource_name], fact_external_labor[role], dim_vendor[vendor_name], dim_cost_center[cost_center_name], dim_project[project_name], fact_external_labor[hourly_rate], fact_external_labor[contract_end_date], fact_external_labor[risk_level] |
| Sort | contract_end_date ascending (soonest first) |
| Conditional formatting | risk_level — Red (High), Yellow (Medium), Green (Low) |
| Tooltip | Full contractor details |
| Drill-through | Target: Drill-through Detail |
| Width | ~65% of canvas |
| Height | ~35% of canvas |

#### Visual 4.9 — Labor by Cost Center (Bar Chart)
| Property | Value |
|---|---|
| Visual Type | Clustered Bar Chart |
| Y axis | dim_cost_center[cost_center_name] |
| X axis | [External Labor Spend] |
| Data labels | On |
| Tooltip | Cost Center, Owner, Spend, Contractor Count |
| Width | ~30% of canvas |
| Height | ~35% of canvas |

---

## Page 5 — Vendor Spend

**Purpose:** Strategic vendor analysis — concentration, growth, and renewal risk.

---

### Slicers

| Slicer | Field | Notes |
|---|---|---|
| Year | dim_date[year] | Synced |
| Business Unit | dim_business_unit[business_unit_name] | Synced |
| Vendor Category | dim_vendor[vendor_category] | Local |
| Vendor Tier | dim_vendor[vendor_tier] | Local |

---

### Row 1 — KPI Cards

| Visual | Measure | Format |
|---|---|---|
| 5.1 | [Vendor Spend] | $ #,##0.0M — Total Vendor Spend |
| 5.2 | DISTINCTCOUNT(fact_vendor_spend[vendor_key]) | # — Active Vendors |
| 5.3 | [YoY Growth %] on vendor spend | 0.0% — YoY Growth |
| 5.4 | Top vendor % of total | 0.0% — Concentration Risk |

---

### Row 2 — Top Vendor Analysis

#### Visual 5.5 — Top 10 Vendors by Spend (Clustered Bar)
| Property | Value |
|---|---|
| Visual Type | Clustered Bar Chart |
| Y axis | dim_vendor[vendor_name] |
| X axis | [Vendor Spend] |
| Top N filter | Top 10 by [Vendor Spend] |
| Colors | Color by dim_vendor[vendor_tier] — Strategic: dark blue, Preferred: medium blue, Transactional: light blue |
| Data labels | On — $ millions |
| Sort | Descending |
| Tooltip | Vendor, Category, Tier, Spend, YoY Growth % |
| Drill-through | Yes |
| Width | ~45% of canvas |
| Height | ~40% of canvas |

#### Visual 5.6 — Vendor YoY Growth (Bar Chart — current vs prior year)
| Property | Value |
|---|---|
| Visual Type | Clustered Bar Chart |
| Y axis | dim_vendor[vendor_name] |
| X1 | [Vendor Spend] (current year) |
| X2 | [Prior Year Actuals] filtered to vendor spend |
| Top N | Top 10 vendors |
| Tooltip | Vendor, Current Year Spend, Prior Year Spend, Growth $ and % |
| Width | ~50% of canvas |
| Height | ~40% of canvas |

---

### Row 3 — Concentration and Category

#### Visual 5.7 — Vendor Concentration (Treemap)
| Property | Value |
|---|---|
| Visual Type | Treemap |
| Group | dim_vendor[vendor_name] |
| Values | [Vendor Spend] |
| Detail | dim_vendor[vendor_category] |
| Color | Proportional — larger = darker |
| Tooltip | Vendor, Spend, % of Total Vendor Spend |
| Width | ~50% of canvas |
| Height | ~30% of canvas |

#### Visual 5.8 — Spend by Vendor Category (Donut)
| Property | Value |
|---|---|
| Visual Type | Donut Chart |
| Legend | dim_vendor[vendor_category] |
| Values | [Vendor Spend] |
| Labels | Category + % |
| Tooltip | Category, Spend, % |
| Width | ~25% of canvas |
| Height | ~30% of canvas |

#### Visual 5.9 — Strategic Vendor Table
| Property | Value |
|---|---|
| Visual Type | Table |
| Columns | dim_vendor[vendor_name], dim_vendor[vendor_category], dim_vendor[vendor_tier], [Vendor Spend], [YoY Growth %] |
| Filter | Strategic tier only |
| Sort | [Vendor Spend] descending |
| Conditional formatting | [YoY Growth %] — color scale |
| Width | ~22% of canvas |
| Height | ~30% of canvas |

---

## Page 6 — Cloud Spend

**Purpose:** Track Azure vs AWS consumption, growth trends, and optimization opportunities by service category.

---

### Slicers

| Slicer | Field | Notes |
|---|---|---|
| Year | dim_date[year] | Synced |
| Business Unit | dim_business_unit[business_unit_name] | Synced |
| Provider | dim_vendor[vendor_name] filtered to Cloud | Local |
| Service Category | fact_cloud_spend[service_category] | Local |
| Project | dim_project[project_name] | Local |

---

### Row 1 — KPI Cards

| Visual | Measure | Format |
|---|---|---|
| 6.1 | [Cloud Spend] | $ #,##0.0M — Total Cloud |
| 6.2 | [YTD Cloud Spend] | $ #,##0.0M — YTD Cloud |
| 6.3 | [Cloud Spend YoY %] | 0.0% — YoY Growth |
| 6.4 | [Cloud Spend] Azure only | $ #,##0.0M — Azure |
| 6.5 | [Cloud Spend] AWS only | $ #,##0.0M — AWS |

For Cards 6.4 and 6.5 use:
```DAX
Azure Spend = CALCULATE([Cloud Spend], dim_vendor[vendor_name] = "Microsoft Azure")
AWS Spend = CALCULATE([Cloud Spend], dim_vendor[vendor_name] = "AWS")
```

---

### Row 2 — Provider and Trend Analysis

#### Visual 6.6 — Azure vs AWS Monthly Trend (Line Chart)
| Property | Value |
|---|---|
| Visual Type | Line Chart |
| X axis | dim_date[year_month] |
| Line 1 | [Azure Spend] — color `#00B0F0` (Azure blue) |
| Line 2 | [AWS Spend] — color `#FF9900` (AWS orange) |
| Markers | On |
| Tooltip | Month, Azure Spend, AWS Spend, Total, YoY change |
| Width | ~60% of canvas |
| Height | ~35% of canvas |

#### Visual 6.7 — Cloud Spend by Service Category (Stacked Bar)
| Property | Value |
|---|---|
| Visual Type | Stacked Bar Chart |
| Y axis | dim_date[year] |
| X axis | [Cloud Spend] |
| Legend | fact_cloud_spend[service_category] |
| Colors | Compute, Storage, Network, Analytics, Database — each unique color |
| Tooltip | Year, Category, Spend, % of total |
| Width | ~35% of canvas |
| Height | ~35% of canvas |

---

### Row 3 — Cost Center and Project Allocation

#### Visual 6.8 — Cloud Spend by Cost Center (Matrix)
| Property | Value |
|---|---|
| Visual Type | Matrix |
| Rows | dim_cost_center[cost_center_name] |
| Columns | dim_vendor[vendor_name] (Azure, AWS) |
| Values | [Cloud Spend] |
| Subtotals | Row totals on |
| Conditional formatting | Background color scale by spend amount |
| Width | ~55% of canvas |
| Height | ~30% of canvas |

#### Visual 6.9 — Cloud Spend by Project (Bar Chart)
| Property | Value |
|---|---|
| Visual Type | Clustered Bar Chart |
| Y axis | dim_project[project_name] |
| X axis | [Cloud Spend] |
| Sort | Descending |
| Data labels | On |
| Tooltip | Project, Owner, Category, Cloud Spend |
| Width | ~40% of canvas |
| Height | ~30% of canvas |

---

## Page 7 — Headcount

**Purpose:** Workforce analytics — approved vs filled positions, vacancy rate, and labor cost trend.

---

### Slicers

| Slicer | Field | Notes |
|---|---|---|
| Year | dim_date[year] | Synced |
| Business Unit | dim_business_unit[business_unit_name] | Synced |
| Cost Center | dim_cost_center[cost_center_name] | Local |

---

### Row 1 — KPI Cards

| Visual | Measure | Format |
|---|---|---|
| 7.1 | [Approved Positions] | # — Total Approved |
| 7.2 | [Headcount] | # — Total Filled |
| 7.3 | [Open Positions] | # — Open Roles |
| 7.4 | [Vacancy Rate] | 0.0% — Vacancy Rate |
| 7.5 | [Monthly Labor Cost] | $ #,##0.0M |
| 7.6 | [Cost per FTE] | $ #,##0 — Cost per FTE |

---

### Row 2 — Workforce Trend

#### Visual 7.7 — Headcount Trend (Line and Clustered Column)
| Property | Value |
|---|---|
| Visual Type | Line and Clustered Column Chart |
| X axis | dim_date[year_month] |
| Column | [Approved Positions] |
| Line | [Headcount] |
| Secondary line | [Vacancy Rate] on right Y axis |
| Colors | Approved: `#90CAF9`, Filled: `#1E88E5`, Vacancy: `#D9534F` |
| Tooltip | Month, Approved, Filled, Open, Vacancy %, Labor Cost |
| Width | ~60% of canvas |
| Height | ~35% of canvas |

#### Visual 7.8 — Vacancy Rate by Business Unit (Bar Chart)
| Property | Value |
|---|---|
| Visual Type | Clustered Bar Chart |
| Y axis | dim_business_unit[business_unit_name] |
| X axis | [Vacancy Rate] |
| Colors | Conditional — >15% red, 5–15% yellow, <5% green |
| Data labels | On — percentage |
| Reference line | Company average vacancy rate |
| Tooltip | BU, Owner, Approved, Filled, Open, Vacancy % |
| Width | ~35% of canvas |
| Height | ~35% of canvas |

---

### Row 3 — Detail Tables

#### Visual 7.9 — Headcount by Cost Center (Table)
| Property | Value |
|---|---|
| Visual Type | Table |
| Columns | dim_cost_center[cost_center_name], dim_business_unit[business_unit_name], [Approved Positions], [Headcount], [Open Positions], [Vacancy Rate], [Monthly Labor Cost] |
| Sort | [Open Positions] descending |
| Conditional formatting | [Vacancy Rate] — color scale |
| Width | ~60% of canvas |
| Height | ~30% of canvas |

#### Visual 7.10 — Labor Cost Trend (Area Chart)
| Property | Value |
|---|---|
| Visual Type | Area Chart |
| X axis | dim_date[year_month] |
| Y axis | [Monthly Labor Cost] |
| Fill color | `#1E88E5` at 30% opacity |
| Tooltip | Month, Labor Cost, Headcount, Cost per FTE |
| Width | ~35% of canvas |
| Height | ~30% of canvas |

---

## Page 8 — Project Spend

**Purpose:** Capital and operating spend by project, with status and owner accountability.

---

### Slicers

| Slicer | Field | Notes |
|---|---|---|
| Year | dim_date[year] | Synced |
| Business Unit | dim_business_unit[business_unit_name] | Synced |
| Project Status | dim_project[project_status] | Local |
| Project Category | dim_project[project_category] | Local |
| Spend Type | fact_project_spend[spend_type] | Local — Capex/Opex |

---

### Row 1 — KPI Cards

| Visual | Measure | Format |
|---|---|---|
| 8.1 | [Project Spend] | $ #,##0.0M — Total Project Spend |
| 8.2 | CALCULATE([Project Spend], fact_project_spend[spend_type]="Capex") | $ #,##0.0M — Capex |
| 8.3 | CALCULATE([Project Spend], fact_project_spend[spend_type]="Opex") | $ #,##0.0M — Opex |
| 8.4 | DIVIDE(Capex, [Project Spend]) | 0.0% — Capex % |
| 8.5 | DISTINCTCOUNT(fact_project_spend[project_key]) | # — Active Projects |

---

### Row 2 — Project Summary

#### Visual 8.6 — Project Budget vs Actuals vs Forecast (Clustered Column)
| Property | Value |
|---|---|
| Visual Type | Clustered Column Chart |
| X axis | dim_project[project_name] |
| Y axis — Column 1 | [Total Budget] allocated to project |
| Y axis — Column 2 | [Project Spend] (actuals) |
| Y axis — Column 3 | [Total Forecast] for project |
| Colors | Budget: `#90CAF9`, Actuals: `#1E88E5`, Forecast: `#F0AD4E` |
| Tooltip | Project, Owner, Category, Status, Budget, Actuals, Forecast, Variance |
| Width | ~65% of canvas |
| Height | ~40% of canvas |

#### Visual 8.7 — Capex vs Opex Donut
| Property | Value |
|---|---|
| Visual Type | Donut Chart |
| Legend | fact_project_spend[spend_type] |
| Values | [Project Spend] |
| Colors | Capex: `#1E88E5`, Opex: `#90CAF9` |
| Tooltip | Spend Type, Amount, % |
| Width | ~30% of canvas |
| Height | ~40% of canvas |

---

### Row 3 — Project Detail

#### Visual 8.8 — Project Detail Table
| Property | Value |
|---|---|
| Visual Type | Table |
| Columns | dim_project[project_name], dim_project[project_category], dim_project[project_status], dim_project[project_owner], [Project Spend], [Total Budget], [YTD Variance], [Forecast Variance %] |
| Sort | [YTD Variance] descending |
| Conditional formatting | project_status — Active: green badge, Planned: amber badge |
| Conditional formatting | [Forecast Variance %] — data bars |
| Drill-through | Row click > Drill-through Detail |
| Width | ~95% of canvas |
| Height | ~25% of canvas |

---

## Page 9 — Drill-through Detail

**Purpose:** Transaction-level analysis. Reached by right-clicking any data point on pages 1–8 and selecting "Drill through."

---

### Drill-through Setup

- [ ] Right-click the page tab > **Edit > Drill-through fields**
- [ ] Add these drill-through anchor fields:
  - dim_cost_center[cost_center_name]
  - dim_business_unit[business_unit_name]
  - dim_vendor[vendor_name]
  - dim_project[project_name]
  - dim_gl_account[gl_category]
  - dim_date[year]

When a user right-clicks on any of these dimensions in pages 1–8, "Drill through > Drill-through Detail" will appear.

---

### Page Header

#### Visual 9.1 — Context Cards (auto-populated from drill-through)
| Visual | Measure | Notes |
|---|---|---|
| Cost Center | Selected cost center name | Auto-filled from source page |
| Business Unit | Selected BU name | Auto-filled |
| Date Range | Selected year/month | Auto-filled |
| GL Category | Selected GL category | Auto-filled |

---

### Main Table

#### Visual 9.2 — Transaction Detail Table
| Property | Value |
|---|---|
| Visual Type | Table |
| Columns | fact_actuals[transaction_date], dim_date[month_name], dim_date[year], dim_business_unit[business_unit_name], dim_cost_center[cost_center_name], dim_gl_account[gl_category], dim_gl_account[gl_description], dim_vendor[vendor_name], dim_project[project_name], fact_actuals[scenario], fact_actuals[amount], fact_actuals[notes] |
| Sort | fact_actuals[transaction_date] descending |
| Column widths | Adjust transaction_date (80px), amount (100px right-aligned) |
| Formatting on amount | $ #,##0.00 |
| Row count display | On — "Showing X transactions" |
| Export option | Enable "Allow export" in visual settings |
| Width | ~95% of canvas |
| Height | ~65% of canvas |

---

### Supporting Aggregations

#### Visual 9.3 — Mini KPI Strip (above main table)
| Visual | Measure |
|---|---|
| Transaction Count | COUNTROWS(fact_actuals) |
| Total Amount | [Total Actuals] |
| Avg per Transaction | DIVIDE([Total Actuals], COUNTROWS(fact_actuals)) |
| Date Range | MIN(transaction_date) & " – " & MAX(transaction_date) |

---

### Back Button

- [ ] Insert a **Back button** (Insert > Buttons > Back)
- [ ] Position top left
- [ ] Label: "← Back"
- [ ] This returns the user to the source page automatically

---

## Cross-Page Interactions Summary

| Action | Behavior |
|---|---|
| Click any chart element | Filters other visuals on the same page via cross-filtering |
| Right-click a data point | Shows "Drill through > Drill-through Detail" option |
| Click month in trend chart | All page visuals filter to that month |
| Click business unit bar | All page visuals filter to that BU |
| Use year slicer | All synced pages update simultaneously |
| Use Back button on detail page | Returns to the page you drilled through from |
| Hover over any visual | Tooltip card appears with extended context |

---

## Tooltip Specifications (All Pages)

Create custom tooltip pages for key visuals:

### Tooltip Page: Monthly Spend Detail
- Small page (220x120px)
- Show: Month, Actuals, Budget, Variance $, Variance %, YoY change

### Tooltip Page: Vendor Detail
- Show: Vendor name, Category, Tier, Spend, YoY Growth %, Description

### Tooltip Page: Cost Center Detail
- Show: Cost Center name, Owner, BU, Actuals, Budget, Open Positions, Vacancy Rate
