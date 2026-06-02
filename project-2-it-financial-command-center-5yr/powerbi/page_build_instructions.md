# Page Build Instructions
## Nexora IT Financial Command Center

Build pages in the sequence listed below. The Drill-through Detail page is built first so all other pages can reference it during construction.

---

## Before You Start — Global Settings

### Canvas Size
1. View > Page View > Actual Size
2. For each page: right-click the page tab > **Page Settings**
   - Page size: Custom → Width: **1280**, Height: **720**
   - Canvas background: Click the paint bucket → Color: `#0D1B2A`
   - Transparency: 0%

### Apply Theme Before Building Any Visuals
1. View > Themes > Browse for themes
2. If you have a custom theme JSON, browse for it
3. Otherwise set manually:
   - Default font: Segoe UI
   - Data colors (primary): `#1E88E5`, `#90CAF9`, `#F0AD4E`, `#5CB85C`, `#D9534F`, `#00B0F0`, `#FF9900`, `#7E57C2`, `#26A69A`, `#EF5350`

### Navigation Bar (Copy to Every Page)
1. On Page 1 (after building all 9 pages), insert navigation buttons
2. Insert > Buttons > Blank
3. Create 8 buttons labeled: `Exec Summary` | `Budget/Act` | `Forecast` | `Ext Labor` | `Vendors` | `Cloud` | `Headcount` | `Projects`
4. Set each button: Format > Action > Type: Page Navigation > Destination: [page name]
5. Style: Fill color `#2D4A6A`, text white, active page button fill `#1E88E5`
6. Group and copy this nav bar to all pages

### Page Header (Copy to Every Page)
1. Insert > Text Box
2. Text: `NEXORA IT FINANCIAL COMMAND CENTER`
3. Font: Segoe UI, 14pt Bold, white
4. Background: `#0D1B2A`
5. Position: top-left, full width, height 50px
6. Add subtitle text box (smaller, right-aligned): reporting period and page name

---

## Build Order

1. Drill-through Detail (Page 9)
2. CIO Executive Summary (Page 1)
3. Budget vs Actuals (Page 2)
4. Forecast & Projection (Page 3)
5. Headcount (Page 7)
6. External Labor (Page 4)
7. Vendor Spend (Page 5)
8. Cloud Spend (Page 6)
9. Project Spend (Page 8)

---

## Page 9 (Build First): Drill-through Detail

### Why Build First
Other pages will right-click > Drill through > this page. It must exist before you can configure drill-through from other pages.

### Canvas Setup
- Background: `#0D1B2A`
- Add a **Back button**: Insert > Buttons > Back — position top-left, label "← Back"

### Step 1: Set Up Drill-through Fields
1. Right-click the page tab > Drill through
2. In the Drill through panel on the right, add these fields to the **Drill through filters** well:
   - `dim_cost_center[cost_center_name]`
   - `dim_business_unit[business_unit_name]`
   - `dim_vendor[vendor_name]`
   - `dim_project[project_name]`
   - `dim_gl_account[gl_category]`
   - `dim_date[year]`
3. Check "Keep all filters" = ON

### Step 2: Context Card Strip
Add 4 KPI cards at the top showing which filters are active:
- Card 1: Title = "Cost Center" — No measure needed, just a label
- Card 2: `[Transaction Count]` — Label: "Transactions"
- Card 3: `[Total Actuals]` — Label: "Total Amount"
- Card 4: `[Avg Transaction Amount]` — Label: "Avg per Transaction"

Format all cards: Background `#1C2B3A`, no border, white text

### Step 3: Main Transaction Table
1. Insert > Table visual
2. Add these fields in order:
   - `fact_actuals[transaction_date]` — rename to "Date"
   - `dim_date[month_name]` — rename to "Month"
   - `dim_date[year]` — rename to "Year"
   - `dim_business_unit[business_unit_name]` — rename to "Business Unit"
   - `dim_cost_center[cost_center_name]` — rename to "Cost Center"
   - `dim_gl_account[gl_category]` — rename to "GL Category"
   - `dim_gl_account[gl_description]` — rename to "GL Description"
   - `dim_vendor[vendor_name]` — rename to "Vendor"
   - `dim_project[project_name]` — rename to "Project"
   - `fact_actuals[scenario]` — rename to "Scenario"
   - `fact_actuals[amount]` — rename to "Amount"
   - `fact_actuals[notes]` — rename to "Notes"

3. Sort: `fact_actuals[transaction_date]` — Descending
4. Format amount column: `$#,##0.00`, right-aligned
5. Column widths: Date 90px, Amount 110px, all others auto
6. Row totals: Off (too many rows)
7. Enable "Export data" in visual header settings

### Step 4: Conditional Formatting on Amount
- Select Amount column > Conditional formatting > Background color
- Scale: white (low) → `#1E88E5` (high)

### Tooltip
None needed — this page IS the detail.

---

## Page 1: CIO Executive Summary

### Slicer Panel (Left Column — 190px wide)

Insert 4 slicers stacked vertically:

**Slicer 1 — Year**
1. Insert > Slicer
2. Field: `dim_date[year]`
3. Style: Dropdown
4. Format: Background `#1A2A3C`, font white, header "Year"
5. Position: x=10, y=70, w=175, h=55

**Slicer 2 — Month**
1. Field: `dim_date[month_name]`
2. Style: Dropdown
3. Header: "Month Through"
4. Position: x=10, y=135, w=175, h=55

**Slicer 3 — Business Unit**
1. Field: `dim_business_unit[business_unit_name]`
2. Style: List (multi-select)
3. Header: "Business Unit"
4. Position: x=10, y=200, w=175, h=150

**Slicer 4 — Forecast Cycle**
1. Field: `fact_forecast[forecast_cycle]`
2. Style: Dropdown
3. Header: "Forecast Cycle"
4. Position: x=10, y=360, w=175, h=55

**Sync All Slicers:**
- View > Sync Slicers
- For each slicer, enable Sync on pages: 1, 2, 3, 4, 5, 6, 7, 8 (all except drill-through)

### Row 1: KPI Cards (6 cards)

Position cards from x=195 to x=1270, y=65, height=90.
Divide width: each card is approximately 178px wide with 8px gap.

**Card 1 — YTD Actuals**
1. Insert > Card visual
2. Field/Measure: `[YTD Actuals]`
3. Format > Callout value: Font 24pt Bold, white
4. Format > Category label: "YTD Actuals", 10pt, `#B0BEC5`
5. Background: `#1C2B3A`
6. No border

**Card 2 — YTD Budget**
- Measure: `[YTD Budget]`
- Label: "YTD Budget"

**Card 3 — YTD Variance**
- Measure: `[YTD Variance]`
- Label: "YTD Variance"
- Conditional formatting on value:
  - Format > Callout value > Conditional formatting > Font color
  - Rules: If value > 0 → `#D9534F` (red), if value < 0 → `#5CB85C` (green), else white

**Card 4 — YTD Variance %**
- Measure: `[YTD Variance %]`
- Label: "Variance %"
- Same conditional color as Card 3

**Card 5 — Year-End Projection**
- Measure: `[Year-End Projection]`
- Label: "Year-End Projection"

**Card 6 — Risk Flag**
- Measure: `[Risk Flag]`
- Label: "Risk Status"
- Conditional background:
  - Format > Background > Conditional formatting > Rules:
    - "High Risk" → `#D9534F`
    - "Medium Risk" → `#F0AD4E`
    - "On Track" → `#5CB85C`

### Row 2: Three Visuals Side by Side

**Visual A — Monthly Trend (Line and Clustered Column)**
Position: x=195, y=165, w=580, h=260

1. Insert > Line and Clustered Column Chart
2. Column Y axis: `[Total Actuals]`
3. X axis: `dim_date[month_name]` — sorted by `dim_date[month_number]`
4. Line Y axis: `[Total Budget]`
5. Format:
   - Column color: `#1E88E5`
   - Line color: `#F0AD4E`, line style dashed, width 2px
   - X axis: white labels, gridlines off
   - Y axis: $ format, white labels
   - Title: "Monthly Actuals vs Budget", white, 12pt
   - Legend: on, bottom
   - Data labels: off

**Visual B — Spend by Business Unit (Bar Chart)**
Position: x=785, y=165, w=240, h=260

1. Insert > Clustered Bar Chart
2. Y axis: `dim_business_unit[business_unit_name]`
3. X axis: `[Total Actuals]`
4. Format:
   - Bar color: `#1E88E5`
   - Sort: descending by `[Total Actuals]`
   - Data labels: on, $ value
   - Title: "Spend by Business Unit"
   - Y axis labels: white, 10pt
   - X axis: hidden (labels replace it)

**Visual C — Spend by GL Category (Donut)**
Position: x=1035, y=165, w=235, h=260

1. Insert > Donut Chart
2. Legend: `dim_gl_account[gl_category]`
3. Values: `[Total Actuals]`
4. Format:
   - Detail labels: Category name + percentage
   - Legend: on, right
   - Title: "Spend by GL Category"
   - Colors: use theme categorical palette

### Row 3: Table + Commentary

**Visual D — Top 5 Variance Drivers (Table)**
Position: x=195, y=435, w=640, h=270

1. Insert > Table
2. Columns:
   - `dim_cost_center[cost_center_name]` — "Cost Center"
   - `dim_gl_account[gl_category]` — "GL Category"
   - `[Total Actuals]` — "Actuals"
   - `[Total Budget]` — "Budget"
   - `[YTD Variance]` — "Variance $"
   - `[YTD Variance %]` — "Variance %"
3. Filter on visual: Top N — field: `dim_cost_center[cost_center_name]`, Top 5 by `[YTD Variance]`
4. Sort: `[YTD Variance]` descending
5. Conditional formatting on `[YTD Variance]`:
   - Background: Rules — > 0 → red scale, < 0 → green scale

**Visual E — Executive Commentary (Text Box)**
Position: x=845, y=435, w=425, h=270

1. Insert > Text Box
2. Background: `#1C2B3A`
3. Font: Segoe UI, 11pt, white
4. Content (update monthly — this is a template):
   ```
   Executive Commentary

   ▲ Cloud Platform Engineering (CC104018) is +8.2% over YTD
   budget. Primary driver: Azure Storage and Compute growth
   in PRJ007 (Data Lakehouse Buildout).

   ▲ Data Engineering (CC104023) is +6.0% over YTD budget.
   Capgemini contractor ramp-up is the key pressure point.

   ► 23 High-risk external labor contracts expire in the next
   90 days. Immediate review recommended.

   ▼ Cybersecurity (CC110101) is 3.0% favorable — delayed
   CrowdStrike rollout. Expect Q4 variance reversal.
   ```

### Drill-through Setup
- Right-click on Visual A (trend chart) and Visual D (table) > Edit interactions
- Ensure these visuals CAN trigger drill-through (they do by default)

### Tooltip Setup for Visual A (Monthly Trend)
1. Select Visual A > Format > Tooltips
2. Tooltip page: Create a new page (see Tooltip section below) or use default
3. Add fields to tooltip: Month, `[Total Actuals]`, `[Total Budget]`, `[YTD Variance]`, `[YoY Growth %]`

---

## Page 2: Budget vs Actuals

### Additional Slicers (Local — Not Synced)

Add 2 local slicers below the synced ones:

**Cost Center Slicer**
- Field: `dim_cost_center[cost_center_display]`
- Style: Dropdown
- Position below synced slicers

**GL Category Slicer**
- Field: `dim_gl_account[gl_category]`
- Style: List

### Row 1: KPI Cards (5 cards)
Same setup as Page 1. Cards: `[YTD Actuals]`, `[YTD Budget]`, `[YTD Variance]`, `[YTD Variance %]`, `[Budget Status]`

**Budget Status card:**
- Conditional background: "Over Budget" → `#D9534F`, "Under Budget" → `#5CB85C`, "On Track" → `#1E88E5`

### Row 2: Monthly Trend (Full Width)

**Visual A — Monthly Actuals vs Budget**
Position: x=195, y=165, w=1075, h=240

1. Line and Clustered Column Chart
2. Column: `[Total Actuals]` by `dim_date[month_name]`
3. Line: `[Total Budget]` by `dim_date[month_name]`
4. Enable **Zoom Slider**: Format > X axis > Zoom slider > On
5. Title: "Monthly Actuals vs Budget"

### Row 3: Two Matrices Side by Side

**Visual B — Variance by Cost Center (Matrix)**
Position: x=195, y=415, w=620, h=285

1. Insert > Matrix
2. Rows: `dim_cost_center[cost_center_name]`
3. Columns: `dim_date[month_name]`
4. Values: `[YTD Variance]`
5. Format > Row subtotals: on; Column subtotals: off
6. Conditional formatting on Values:
   - Background: diverging scale → center at 0
   - Low color: `#5CB85C` (green), Center: white, High color: `#D9534F` (red)
7. Sort rows by descending subtotal variance

**Visual C — Variance by GL Category (Bar)**
Position: x=825, y=415, w=445, h=285

1. Clustered Bar Chart
2. Y axis: `dim_gl_account[gl_category]`
3. X axis: `[YTD Variance]`
4. Format:
   - Conditional formatting on bars:
     - Rules: Value > 0 → `#D9534F`, Value < 0 → `#5CB85C`
   - X axis: add constant line at 0
   - Data labels: on, show values in $K
   - Sort: descending by `[YTD Variance]`

### Drill-through on Both Visuals B and C
- Right-click any row in the matrix or bar → Drill through → Drill-through Detail
- This works automatically once dim_cost_center[cost_center_name] and dim_gl_account[gl_category] are set as drill-through fields on Page 9

---

## Page 3: Forecast & Projection

### Local Slicers
Add **Forecast Cycle** slicer (this page has its own since it's the primary control here):
- Already synced globally — no change needed
- Consider making it a Button slicer (Style: Buttons) for visual appeal

### Row 1: KPI Cards (6 cards)
`[Full-Year Budget]`, `[Full-Year Forecast]`, `[Forecast Variance]`, `[Forecast Variance %]`, `[Forecast Accuracy %]`, `[Remaining Forecast]`

### Row 2: Two Visuals

**Visual A — Actuals + Forecast Area Chart**
Position: x=195, y=165, w=690, h=260

1. Area Chart
2. X axis: `dim_date[month_name]` (ordered by month_number)
3. Y axis values:
   - `[Total Actuals]` — solid fill `#1E88E5` at 70% opacity
   - `[Total Forecast]` — fill `#90CAF9` at 40% opacity
4. Add constant line at `[Full-Year Budget]` value
   - Analytics pane > Constant line → enter [Full-Year Budget] value
5. Title: "Actuals + Forecast — Full Year View"
6. Legend: on, bottom
7. Tooltip: Month, `[Total Actuals]`, `[Total Forecast]`, `[Full-Year Budget]`

**Visual B — Forecast Cycle Comparison (Clustered Column)**
Position: x=895, y=165, w=375, h=260

1. Clustered Column Chart
2. X axis: `fact_forecast[forecast_cycle]`
3. Y axis: `[Full-Year Forecast]`
4. Add Analytics line for `[Full-Year Budget]` as a constant
5. Colors: each cycle bar a distinct color (use theme colors 1, 3, 5)
6. Data labels: on, $ millions
7. Title: "Forecast Cycle Comparison"

### Row 3: Risk Table + Gauge

**Visual C — Risk & Opportunity Table**
Position: x=195, y=435, w=780, h=270

1. Table
2. Columns:
   - `dim_cost_center[cost_center_name]`
   - `[Full-Year Forecast]`
   - `[Full-Year Budget]`
   - `[Forecast Variance]`
   - `[Forecast Variance %]`
   - `[Risk Flag]`
3. Sort: `[Forecast Variance]` descending
4. Conditional formatting on `[Risk Flag]`:
   - Background rules: "High Risk" → `#D9534F`, "Medium Risk" → `#F0AD4E`, "On Track" → `#5CB85C`
5. Conditional formatting on `[Forecast Variance %]`:
   - Data bars (gradient)

**Visual D — Year-End Projection Gauge**
Position: x=985, y=435, w=285, h=270

1. Insert > Gauge
2. Value: `[Year-End Projection]`
3. Minimum: 0
4. Maximum: create a helper measure:
   ```DAX
   Gauge Max = [Full-Year Budget] * 1.15
   ```
5. Target: `[Full-Year Budget]`
6. Needle color: conditional — use `[Risk Flag Color]` measure
7. Title: "Year-End Projection vs Budget"

---

## Page 4: External Labor

### Local Slicers
Add these below the global slicers:
- `fact_external_labor[risk_level]` — Style: Buttons (shows High/Medium/Low as toggle buttons)
- `dim_vendor[vendor_name]` filtered to External Labor vendors — Dropdown
- `dim_project[project_name]` — Dropdown

### Row 1: KPI Cards (5 cards)
`[External Labor Spend]`, `[Contractor Count]`, `[Avg Hourly Rate]`, `[External Labor Risk Count]`, `[External Labor YoY %]`

**External Labor Risk Count card:**
- Conditional background: if value > 20 → `#D9534F`, if > 10 → `#F0AD4E`, else `#1C2B3A`

### Row 2: Two Visuals

**Visual A — External Labor Spend Trend**
Position: x=195, y=165, w=700, h=250

1. Line Chart
2. X axis: `dim_date[year_month]`
3. Y axis (line 1): `[External Labor Spend]`
4. Secondary Y axis (line 2): `[Contractor Count]`
5. Line 1 color: `#1E88E5`, Line 2 color: `#F0AD4E` dashed
6. Markers: on
7. Tooltip: Month, Spend, Count, Avg Rate

**Visual B — Spend by Vendor**
Position: x=905, y=165, w=365, h=250

1. Clustered Bar Chart
2. Y axis: `dim_vendor[vendor_name]`
3. X axis: `[External Labor Spend]`
4. Filter: `dim_vendor[vendor_category]` = "External Labor" OR "Professional Services"
5. Top N: 8 by `[External Labor Spend]`
6. Sort: descending
7. Data labels: on

### Row 3: Contract Risk Table (Full Width)

**Visual C — Contract End Date Risk Table**
Position: x=195, y=425, w=1075, h=280

1. Table
2. Columns:
   - `fact_external_labor[resource_name]` — "Resource"
   - `fact_external_labor[role]` — "Role"
   - `dim_vendor[vendor_name]` — "Vendor"
   - `dim_cost_center[cost_center_name]` — "Cost Center"
   - `dim_project[project_name]` — "Project"
   - `fact_external_labor[hourly_rate]` — "Rate/Hr"
   - `fact_external_labor[hours]` — "Hours"
   - `fact_external_labor[amount]` — "Amount"
   - `fact_external_labor[contract_end_date]` — "Contract End"
   - `fact_external_labor[days_until_expiry]` — "Days to Expiry"
   - `fact_external_labor[risk_level]` — "Risk"
3. Sort: `contract_end_date` ascending (soonest first)
4. Conditional formatting on `risk_level`:
   - Background rules: "High" → `#D9534F`, "Medium" → `#F0AD4E`, "Low" → `#5CB85C`
5. Conditional formatting on `days_until_expiry`:
   - Rules: <= 30 → `#D9534F` font, 31–90 → `#F0AD4E` font, > 90 → white

### Drill-through
- Right-click any resource row → Drill through → Drill-through Detail

---

## Page 5: Vendor Spend

### Local Slicers
- `dim_vendor[vendor_category]` — Dropdown
- `dim_vendor[vendor_tier]` — Buttons (Strategic / Preferred / Transactional)

### Row 1: KPI Cards (4 cards)
`[Vendor Spend]`, `[Active Vendor Count]`, `[Vendor YoY Growth %]`, `[Strategic Vendor %]`

### Row 2: Two Bar Charts Side by Side

**Visual A — Top 10 Vendors by Spend**
Position: x=195, y=165, w=520, h=280

1. Clustered Bar Chart
2. Y axis: `dim_vendor[vendor_name]`
3. X axis: `[Vendor Spend]`
4. Top N filter on visual: Top 10 by `[Vendor Spend]`
5. Color by: `dim_vendor[vendor_tier]`
   - In Format > Data colors: enable "Show all" and assign:
     - Strategic → `#1E88E5`
     - Preferred → `#90CAF9`
     - Transactional → `#B0BEC5`
6. Data labels: on
7. Sort: descending

**Visual B — Vendor YoY Comparison**
Position: x=725, y=165, w=545, h=280

1. Clustered Bar Chart
2. Y axis: `dim_vendor[vendor_name]` (same Top 10 filter)
3. X axis — two series:
   - `[Vendor Spend]` — Current Year
   - `[Prior Year Vendor Spend]`
4. Top N filter: Top 10 by `[Vendor Spend]`
5. Color: Current `#1E88E5`, Prior year `#90CAF9`
6. Legend: on
7. Tooltip: Vendor, Current Spend, Prior Spend, YoY Growth %

### Row 3: Treemap + Donut + Table

**Visual C — Vendor Concentration (Treemap)**
Position: x=195, y=455, w=560, h=250

1. Treemap
2. Group: `dim_vendor[vendor_name]`
3. Values: `[Vendor Spend]`
4. Details: `dim_vendor[vendor_category]`
5. Data labels: on (vendor name + $ value)
6. Tooltip: Vendor, Category, Tier, Spend, % of total vendor spend

**Visual D — Spend by Category (Donut)**
Position: x=765, y=455, w=250, h=250

1. Donut Chart
2. Legend: `dim_vendor[vendor_category]`
3. Values: `[Vendor Spend]`
4. Detail labels: Category + %

**Visual E — Strategic Vendor Table**
Position: x=1025, y=455, w=245, h=250

1. Table
2. Filter on visual: `dim_vendor[vendor_tier]` = "Strategic"
3. Columns: `dim_vendor[vendor_name]`, `[Vendor Spend]`, `[Vendor YoY Growth %]`
4. Sort: `[Vendor Spend]` descending
5. Conditional formatting on `[Vendor YoY Growth %]`: data bars

---

## Page 6: Cloud Spend

### Local Slicers
- `dim_vendor[is_cloud_vendor]` — filtered to "Yes" (pre-filter)
- `fact_cloud_spend[service_category]` — Buttons
- `dim_project[project_name]` — Dropdown

### Row 1: KPI Cards (5 cards)
`[Cloud Spend]`, `[YTD Cloud Spend]`, `[Cloud Spend YoY %]`, `[Azure Spend]`, `[AWS Spend]`

**Azure Spend card color:** font `#00B0F0` (Azure blue)
**AWS Spend card color:** font `#FF9900` (AWS orange)

### Row 2: Azure vs AWS Trend (Full Width)

**Visual A — Azure vs AWS Monthly Trend**
Position: x=195, y=165, w=1075, h=250

1. Line Chart
2. X axis: `dim_date[year_month]` — sorted by year_month
3. Y axis:
   - Line 1: `[Azure Spend]` — color `#00B0F0`, line width 2.5
   - Line 2: `[AWS Spend]` — color `#FF9900`, line style dashed, width 2
4. Markers: on for both
5. Legend: on, bottom — "Microsoft Azure" and "AWS"
6. Zoom slider: on
7. Title: "Azure vs AWS Monthly Spend — 2022 to 2026"
8. Tooltip: Month, Azure, AWS, Total Cloud, YoY %

### Row 3: Three Visuals

**Visual B — Cloud by Service Category (Stacked Bar)**
Position: x=195, y=425, w=420, h=270

1. Stacked Bar Chart
2. Y axis: `dim_date[year]`
3. X axis: `[Cloud Spend]`
4. Legend: `fact_cloud_spend[service_category]`
5. Colors — use 5 distinct colors for Compute, Storage, Network, Analytics, Database
6. Title: "Cloud by Service Category"

**Visual C — Cloud by Cost Center Matrix**
Position: x=625, y=425, w=450, h=270

1. Matrix
2. Rows: `dim_cost_center[cost_center_name]`
3. Columns: `dim_vendor[vendor_name]` (filtered to Azure, AWS only)
4. Values: `[Cloud Spend]`
5. Row subtotals: on
6. Conditional formatting: background scale on values

**Visual D — Cloud by Project (Bar)**
Position: x=1085, y=425, w=185, h=270

1. Clustered Bar Chart
2. Y axis: `dim_project[project_name]`
3. X axis: `[Cloud Spend]`
4. Sort: descending
5. Data labels: on

---

## Page 7: Headcount

### Row 1: KPI Cards (6 cards)
`[Approved Positions]`, `[Headcount]`, `[Open Positions]`, `[Vacancy Rate]`, `[Monthly Labor Cost]`, `[Cost per FTE]`

**Vacancy Rate card:**
- Conditional background: > 0.15 → `#D9534F`, > 0.08 → `#F0AD4E`, else `#1C2B3A`

### Row 2: Trend + BU Bar

**Visual A — Headcount Trend**
Position: x=195, y=165, w=700, h=250

1. Line and Clustered Column Chart
2. X axis: `dim_date[year_month]`
3. Column (grouped): `[Approved Positions]` (color `#90CAF9`), `[Headcount]` (color `#1E88E5`)
4. Line Y2 axis: `[Vacancy Rate]` — color `#D9534F`, dashed
5. Legend: on
6. Tooltip: Month, Approved, Filled, Open, Vacancy %, Labor Cost

**Visual B — Vacancy Rate by Business Unit**
Position: x=905, y=165, w=365, h=250

1. Clustered Bar Chart
2. Y axis: `dim_business_unit[business_unit_name]`
3. X axis: `[Vacancy Rate]`
4. Conditional formatting on bars:
   - Rules: > 0.15 → `#D9534F`, 0.08–0.15 → `#F0AD4E`, < 0.08 → `#5CB85C`
5. Data labels: on — percentage format
6. Add constant line at company average vacancy rate

### Row 3: Detail Table + Labor Cost Area

**Visual C — Headcount Detail Table**
Position: x=195, y=425, w=700, h=280

1. Table
2. Columns:
   - `dim_cost_center[cost_center_name]`
   - `dim_business_unit[business_unit_name]`
   - `[Approved Positions]`
   - `[Headcount]`
   - `[Open Positions]`
   - `[Vacancy Rate]`
   - `[Monthly Labor Cost]`
3. Sort: `[Open Positions]` descending
4. Conditional formatting on `[Vacancy Rate]`: color scale

**Visual D — Monthly Labor Cost Area Chart**
Position: x=905, y=425, w=365, h=280

1. Area Chart
2. X axis: `dim_date[year_month]`
3. Y axis: `[Monthly Labor Cost]`
4. Fill color: `#1E88E5` at 30% opacity
5. Line color: `#1E88E5` solid, width 2
6. Tooltip: Month, Labor Cost, Headcount, Cost per FTE

---

## Page 8: Project Spend

### Local Slicers
- `dim_project[project_status]` — Buttons
- `dim_project[project_category]` — Dropdown
- `fact_project_spend[spend_type]` — Buttons (Capex / Opex)

### Row 1: KPI Cards (5 cards)
`[Project Spend]`, `[Capex Spend]`, `[Opex Spend]`, `[Capex % of Project Spend]`, `[Active Project Count]`

### Row 2: Project Column Chart + Capex Donut

**Visual A — Project Budget vs Actuals vs Forecast**
Position: x=195, y=165, w=830, h=270

1. Clustered Column Chart
2. X axis: `dim_project[project_name]`
3. Y axis — 3 series:
   - `[Total Budget]` — color `#90CAF9`
   - `[Project Spend]` — color `#1E88E5`
   - `[Full-Year Forecast]` — color `#F0AD4E`
4. Legend: on, bottom
5. Data labels: on (toggle if too crowded)
6. Sort: by `[Project Spend]` descending
7. Tooltip: Project, Owner, Category, Status, all three values + variance

**Visual B — Capex vs Opex Donut**
Position: x=1035, y=165, w=235, h=270

1. Donut Chart
2. Legend: `fact_project_spend[spend_type]`
3. Values: `[Project Spend]`
4. Colors: Capex `#1E88E5`, Opex `#90CAF9`
5. Detail labels: type + percentage

### Row 3: Project Detail Table (Full Width)

**Visual C — Project Detail Table**
Position: x=195, y=445, w=1075, h=260

1. Table
2. Columns:
   - `dim_project[project_name]` — "Project"
   - `dim_project[project_category]` — "Category"
   - `dim_project[project_status]` — "Status"
   - `dim_project[project_owner]` — "Owner"
   - `[Project Spend]` — "Actuals"
   - `[Total Budget]` (scoped to project) — "Budget"
   - `[Forecast Variance]` — "Variance $"
   - `[Forecast Variance %]` — "Variance %"
3. Sort: `[Forecast Variance]` descending
4. Conditional formatting on Status:
   - "Active" → background `#5CB85C`, white text
   - "Planned" → background `#F0AD4E`, white text
5. Conditional formatting on Variance %: data bars

---

## Tooltip Pages

Create small pages (220x120px) for use as report tooltips:

### Tooltip Page 1 — Monthly Context
1. Right-click page tab > **Page Information** — enable "Use as a tooltip page"
2. Set page size: 220 x 120
3. Add 2 KPI cards: `[Total Actuals]` (Month label), `[Total Budget]`
4. Add text measure: `[YTD Variance]` and `[YoY Growth %]`
5. Background: `#1C2B3A`, no border
6. On Visual A (Monthly Trend) on each page:
   - Format > Tooltip > Type: Report page > select "Tooltip Page 1"

### Tooltip Page 2 — Vendor Context
1. Enable as tooltip
2. Size: 220x120
3. Fields: Vendor name, Category, Tier, `[Vendor Spend]`, `[Vendor YoY Growth %]`
4. Assign to all vendor-related visuals

### Tooltip Page 3 — Cost Center Context
1. Enable as tooltip
2. Size: 220x120
3. Fields: Cost Center name, Owner, BU, `[Total Actuals]`, `[Open Positions]`, `[Vacancy Rate]`
4. Assign to cost center charts and matrices

---

## Conditional Formatting Reference (Applies Across All Pages)

| Scenario | Field | Rule | Color |
|---|---|---|---|
| Over budget | `[YTD Variance]` | > 0 | `#D9534F` (red) |
| Under budget | `[YTD Variance]` | < 0 | `#5CB85C` (green) |
| High risk | `[Risk Flag]` | "High Risk" | `#D9534F` |
| Medium risk | `[Risk Flag]` | "Medium Risk" | `#F0AD4E` |
| On track | `[Risk Flag]` | "On Track" | `#5CB85C` |
| High vacancy | `[Vacancy Rate]` | > 0.15 | `#D9534F` |
| Medium vacancy | `[Vacancy Rate]` | 0.08–0.15 | `#F0AD4E` |
| Contract high risk | risk_level | "High" | `#D9534F` |
| Contract medium risk | risk_level | "Medium" | `#F0AD4E` |
| Contract low risk | risk_level | "Low" | `#5CB85C` |
| Positive YoY growth | `[YoY Growth %]` | > 0 | `#D9534F` (spend going up = negative) |
