# Validation Tests
## Nexora IT Financial Command Center

Run these tests after building the data model and measures, before building dashboard pages. Each test describes what to check, how to check it, and what the expected result should be.

---

## Test Group 1: Row Count Verification

Before running any measures, confirm that all CSV data loaded completely.

### Test 1.1 — Verify Dimension Table Row Counts

Create a card visual for each: `COUNTROWS(table_name)`

| Table | Expected Rows | Actual Rows | Pass/Fail |
|---|---|---|---|
| dim_date | 60 (5 years × 12 months) | ☐ | ☐ |
| dim_business_unit | 6 | ☐ | ☐ |
| dim_cost_center | 18 | ☐ | ☐ |
| dim_gl_account | 11 | ☐ | ☐ |
| dim_vendor | 18 | ☐ | ☐ |
| dim_project | 10 | ☐ | ☐ |

### Test 1.2 — Verify Fact Table Row Counts

| Table | Notes | Record Your Count |
|---|---|---|
| fact_actuals | Should be several thousand rows (18 cost centers × 11 GL accounts × 60 months ≈ 11,880 max) | ☐ |
| fact_budget | Similar scale to fact_actuals | ☐ |
| fact_forecast | 3× actuals if all 3 forecast cycles are present | ☐ |
| fact_headcount | 18 cost centers × 60 months = 1,080 | ☐ |
| fact_external_labor | Variable — check raw CSV row count matches | ☐ |
| fact_vendor_spend | Check raw CSV matches | ☐ |
| fact_cloud_spend | Check raw CSV matches | ☐ |
| fact_project_spend | 10 projects × months in scope | ☐ |

**How to check:** Open each table in Data view (left sidebar icon) and note row count shown at bottom of screen.

---

## Test Group 2: fact_actuals Reconciliation

### Test 2.1 — Total Actuals Grand Total

**Method:**
1. Insert a Matrix visual on a blank test page
2. Rows: `dim_date[year]`
3. Values: `[Total Actuals]`
4. No slicers — all data

**Expected Result:** Five rows (2022–2026) with values. Sum of all years = Grand Total.

**Manual Verification:**
Open `fact_actuals.csv` in Excel → SUM the `amount` column → result should match the Grand Total card in Power BI within $0.01 (rounding from Fixed Decimal).

| Year | Expected Range | Your Value | Pass/Fail |
|---|---|---|---|
| 2022 | Positive dollar amount | ☐ | ☐ |
| 2023 | Greater than 2022 | ☐ | ☐ |
| 2024 | Greater than 2023 | ☐ | ☐ |
| 2025 | Greater than 2024 | ☐ | ☐ |
| 2026 | Positive amount | ☐ | ☐ |
| Grand Total | Sum of above | ☐ | ☐ |

### Test 2.2 — Actuals by GL Category

**Method:** Matrix with `dim_gl_account[gl_category]` as rows, `[Total Actuals]` as values (no year filter)

**Expected:** 11 rows, one per GL category. All values positive. Internal Labor should be the largest category.

**Validation Check:**
- Internal Labor (GL 611000) should be the largest line item
- Cloud (GL 613050) should show meaningful growth from 2022 to 2026
- No GL categories should appear as blank

### Test 2.3 — Actuals by Business Unit

**Method:** Card: `[Total Actuals]` filtered by each business unit one at a time using a slicer

**Expected:** Sum of all 6 BU totals = Grand Total from Test 2.1

```
BU01 + BU02 + BU03 + BU04 + BU05 + BU06 = Grand Total
```

If this does not equal, a relationship or key mismatch exists between fact_actuals and dim_business_unit.

---

## Test Group 3: fact_budget Reconciliation

### Test 3.1 — Total Budget Grand Total

**Method:** Same as Test 2.1 but for `[Total Budget]`

**Expected:** Budget by year should be present for all 5 years. 2022 budget should be the lowest; 2026 should be highest (growing organization).

### Test 3.2 — Budget Covers All Cost Centers

**Method:** Matrix with `dim_cost_center[cost_center_name]` rows and `[Total Budget]` values (no year filter)

**Expected:** All 18 cost centers have a budget value. No blanks.

If a cost center shows blank in `[Total Budget]` but has actuals, the relationship between fact_budget and dim_cost_center may be broken, or the cost_center_key values don't match.

---

## Test Group 4: fact_forecast Reconciliation

### Test 4.1 — All Three Forecast Cycles Present

**Method:** Matrix with `fact_forecast[forecast_cycle]` as rows, `[Total Forecast]` as values

**Expected:** Exactly 3 rows: `3+9`, `6+6`, `9+3`

If fewer rows appear, the forecast_cycle column has blanks or extra whitespace — return to Power Query and Trim.

### Test 4.2 — Forecast Cycle Values Are Reasonable

**Expected:** Each forecast cycle should produce a full-year total close to but slightly different from the others.

- 3+9 forecast < 6+6 forecast ≈ true (early forecasts are typically more conservative)
- 9+3 forecast closest to actual year-end results

---

## Test Group 5: YTD Measures

### Test 5.1 — YTD Actuals = Full Year When December Selected

**Method:**
1. Add a Year slicer — select 2023
2. Add a Month slicer — select December
3. Insert Card: `[YTD Actuals]`
4. Insert Card: `[Total Actuals]` (no time filter — override with a different measure)

**Expected:** `[YTD Actuals]` for December 2023 should equal the total of all 12 months of 2023.

**Cross-check:** Create this measure on a blank page:
```DAX
Dec Check = CALCULATE([Total Actuals], dim_date[month_number] <= 12, dim_date[year] = 2023)
```
This should equal `[YTD Actuals]` when December 2023 is selected.

### Test 5.2 — YTD Actuals = Partial Year When Mid-Year Month Selected

**Method:**
1. Year slicer: 2024
2. Month slicer: June
3. Card: `[YTD Actuals]`

**Expected:** Value equals the sum of January through June 2024 — NOT all 12 months.

**Cross-check:**
```DAX
H1 Check = CALCULATE([Total Actuals], dim_date[month_number] <= 6, dim_date[year] = 2024)
```
Must equal `[YTD Actuals]`.

---

## Test Group 6: Variance Measures

### Test 6.1 — YTD Variance = YTD Actuals − YTD Budget

**Method:** On a blank page, add three cards:
- Card A: `[YTD Actuals]`
- Card B: `[YTD Budget]`
- Card C: `[YTD Variance]`

With Year=2025, Month=June selected:

**Expected:** Card C = Card A − Card B (within rounding)

If Card C ≠ A − B, the variance measure has an error. Return to the DAX measure and verify the formula reads:
```DAX
YTD Variance = [YTD Actuals] - [YTD Budget]
```

### Test 6.2 — YTD Variance % = YTD Variance ÷ YTD Budget

**Method:** Same setup. Add Card D: `[YTD Variance %]`

**Expected:** Card D = Card C ÷ Card B

Example: If Variance = $2.6M and Budget = $109.8M → Variance % = 2.37%

### Test 6.3 — Positive Variance = Over Budget Direction

**Expected:**
- Positive `[YTD Variance]` = actual spend EXCEEDS budget = BAD (over budget)
- Negative `[YTD Variance]` = actual spend BELOW budget = GOOD (under budget)

The conditional formatting should show:
- Positive → red
- Negative → green

If the colors are reversed, the conditional formatting rules need to be flipped.

---

## Test Group 7: Relationship Filter Tests

### Test 7.1 — Business Unit Slicer Filters All Pages

**Method:**
1. Select Business Unit = "Infrastructure & Cloud" (BU06)
2. Check cards on Page 1: `[YTD Actuals]`, `[YTD Budget]`, `[YTD Variance]`
3. Navigate to Page 2 — verify same BU filter applies

**Expected:** All synced pages show only BU06 data. The values should be lower than All BUs combined.

### Test 7.2 — Cost Center Slicer Filters Only Current Page

**Method:**
1. Page 2: Select Cost Center = "Cloud Platform Engineering" (104018)
2. Navigate to Page 3

**Expected:** Page 2 is filtered to CC104018. Page 3 is NOT filtered (cost center slicer is local, not synced).

### Test 7.3 — Vendor Filter Flows Through Cloud Spend

**Method:** On Cloud Spend page:
1. Filter to `dim_vendor[vendor_name]` = "Microsoft Azure"
2. Verify `[Azure Spend]` card = `[Cloud Spend]` card (since only Azure is selected)

**Expected:** Both cards show identical values. If not, the relationship between fact_cloud_spend and dim_vendor is broken.

### Test 7.4 — dim_date Mark as Date Table Works

**Method:**
1. Add `[YTD Actuals]` card
2. Add `[YoY Growth %]` card with Year=2023 selected

**Expected:** YoY Growth % shows a meaningful percentage comparing 2023 to 2022. If it shows BLANK or an error, dim_date was not correctly marked as the date table, or the `date` column is not Date type.

### Test 7.5 — Drill-through Passes Correct Context

**Method:**
1. Go to Page 2 (Budget vs Actuals)
2. Select Year = 2025 in slicer
3. Right-click on a cost center row in the variance matrix
4. Select Drill through > Drill-through Detail

**Expected:** Drill-through Detail page shows ONLY transactions matching:
- The selected cost center
- The year 2025

Verify by checking the transaction_date column — all dates should be in 2025. If 2022–2026 data shows up, the drill-through context filter is not working — confirm drill-through fields are set correctly on the detail page.

---

## Test Group 8: Vendor Spend Reconciliation

### Test 8.1 — Vendor Spend ≠ Total Actuals

**Expected:** `[Vendor Spend]` (from fact_vendor_spend) is DIFFERENT from `[Total Actuals]` (from fact_actuals).

These are two separate fact tables. fact_vendor_spend tracks vendor invoices specifically. fact_actuals tracks all GL account-level spend. They should NOT be equal.

If they are exactly equal, a table may have been accidentally loaded twice or confused.

### Test 8.2 — Vendor Spend Covers Known Vendors

**Method:** Matrix with `dim_vendor[vendor_name]` rows and `[Vendor Spend]` values

**Expected:** Microsoft Azure (VEN001) and AWS (VEN002) should appear in the top rows. Capgemini should appear in the top 3 or 4.

If key vendors are missing (show blank), the vendor_key values in fact_vendor_spend may not match dim_vendor exactly — return to Power Query and verify the join key is Text type on both sides.

### Test 8.3 — Cloud Spend ≠ Vendor Spend

**Expected:** `[Cloud Spend]` (from fact_cloud_spend) is different from `[Vendor Spend]` (from fact_vendor_spend).

fact_cloud_spend contains only cloud consumption records. fact_vendor_spend contains all vendor invoices including software, professional services, and hardware. Cloud Spend should be less than total Vendor Spend.

---

## Test Group 9: Headcount Reconciliation

### Test 9.1 — Open Positions = Approved − Filled

**Method:** Matrix with `dim_cost_center[cost_center_name]` rows and three values:
- `[Approved Positions]`
- `[Headcount]`
- `[Open Positions]`

Add a custom column check in Power Query (done during import):
```
open_positions = approved_positions - filled_positions
```

**Expected:** For every row, `[Open Positions]` = `[Approved Positions]` − `[Headcount]`

If any row differs, the source data contains an inconsistency. Flag for review.

### Test 9.2 — Vacancy Rate Calculates Correctly

**Method:** For a specific cost center and month where the raw data is known:

From the CSV: CC104002, 2022-01 → approved=10, filled=9, open=1, vacancy_rate=0.1

**Expected:**
- `[Open Positions]` = 1
- `[Approved Positions]` = 10
- `[Vacancy Rate]` = 10.0%

If `[Vacancy Rate]` shows 0.1 (not 10%), the measure is returning the raw decimal. Format string should be `0.0%`.

### Test 9.3 — Total Headcount by BU Sums to Org Total

**Method:**
1. Card: `[Headcount]` (no filter) = Org Total
2. Sum of `[Headcount]` filtered for each BU one at a time = BU1+BU2+BU3+BU4+BU5+BU6

**Expected:** Sum of all BU headcounts = Org Total headcount

---

## Test Group 10: Full Report Smoke Test

Run this after all 9 pages are built.

### Test 10.1 — No Visual Error Triangles
- Navigate through all 9 pages
- No yellow warning triangles should appear on any visual
- If found: hover over the triangle to read the error message and resolve

### Test 10.2 — All KPI Cards Show Values (Not BLANK)
- On every page, verify all KPI cards display a number, not "BLANK" or "(Blank)"
- BLANK typically means a relationship is broken or a filter context returns no matching rows

### Test 10.3 — Slicers Work on All Pages
1. Year slicer: select 2022 → all synced pages should update
2. Year slicer: select 2026 → values should be higher than 2022 (growth trend)
3. Business Unit slicer: select "Information Security" → verify all visuals show only BU05 data

### Test 10.4 — Drill-through Is Available on Source Pages
Right-click a data point on:
- Page 1 (top variance table)
- Page 2 (cost center matrix)
- Page 3 (risk flag table)
- Page 4 (contract end date table)

**Expected:** "Drill through" option appears with "Drill-through Detail" as a target.

If "Drill through" does not appear, either:
- The dimension field in the visual is not one of the configured drill-through anchor fields
- The Drill-through Detail page has no drill-through fields configured

### Test 10.5 — Back Button Returns to Source Page
1. Drill through from Page 2 to Drill-through Detail
2. Click "← Back"

**Expected:** Returns to Page 2 (Budget vs Actuals), preserving the filter context that triggered the drill-through.

---

## Validation Test Log Template

Use this to document test results before publishing.

| Test ID | Description | Expected | Actual | Status | Notes |
|---|---|---|---|---|---|
| 1.1 | dim_date row count = 60 | 60 | | ☐ | |
| 1.2 | All fact tables loaded | No errors | | ☐ | |
| 2.1 | Total Actuals grand total | Matches CSV | | ☐ | |
| 2.2 | Actuals by GL category | 11 rows | | ☐ | |
| 2.3 | BU subtotals sum to total | Equal | | ☐ | |
| 3.1 | Budget grand total | Matches CSV | | ☐ | |
| 4.1 | 3 forecast cycles present | 3+9, 6+6, 9+3 | | ☐ | |
| 5.1 | YTD Dec = Full Year | Equal | | ☐ | |
| 5.2 | YTD June = H1 only | Equal | | ☐ | |
| 6.1 | Variance = Actuals − Budget | Equal | | ☐ | |
| 6.2 | Variance % = Variance ÷ Budget | Equal | | ☐ | |
| 6.3 | Positive variance = red | Red | | ☐ | |
| 7.1 | BU slicer syncs all pages | Filters all | | ☐ | |
| 7.2 | CC slicer is local only | Page-scoped | | ☐ | |
| 7.3 | Azure filter = Cloud Spend | Equal | | ☐ | |
| 7.4 | YoY measure works | % shown | | ☐ | |
| 7.5 | Drill-through context correct | Filtered rows | | ☐ | |
| 8.1 | Vendor ≠ Total Actuals | Different | | ☐ | |
| 8.2 | Azure visible in vendor table | Top row | | ☐ | |
| 9.1 | Open = Approved − Filled | Matches | | ☐ | |
| 9.2 | Vacancy rate formats as % | 10.0% | | ☐ | |
| 10.1 | No error triangles | None | | ☐ | |
| 10.2 | No BLANK KPI cards | All show values | | ☐ | |
| 10.3 | Slicers work globally | All update | | ☐ | |
| 10.4 | Drill-through available | Menu shown | | ☐ | |
| 10.5 | Back button works | Returns to source | | ☐ | |
