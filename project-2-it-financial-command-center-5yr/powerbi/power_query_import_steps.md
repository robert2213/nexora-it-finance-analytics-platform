# Power Query Import Steps
## Nexora IT Financial Command Center

Follow these steps in order. All tables are imported via **Home > Get Data > Text/CSV**.
Apply every transformation before clicking **Close & Apply**.

---

## General Rules (Apply to Every Table)

1. After import, immediately open the **Advanced Editor** and rename the query to match the table name exactly.
2. Remove the auto-generated "Changed Type" step — you will re-apply types manually to avoid locale issues.
3. Verify the first row is used as headers (Power BI does this by default for CSVs with headers).
4. Never modify the source CSV files — all transformations happen inside Power Query.

---

## Table 1: dim_date

**File:** `dim_date.csv`
**Query Name:** `dim_date`
**Role:** Central date table. This table drives all time intelligence.

### Columns to Keep and Types

| Column Name | Data Type | Notes |
|---|---|---|
| date_key | Whole Number | Primary key — format YYYYMMDD |
| date | Date | Used as the date table column |
| year | Whole Number | e.g. 2022 |
| quarter_number | Whole Number | 1–4 |
| quarter_name | Text | e.g. Q1, Q2 |
| month_number | Whole Number | 1–12 |
| month_name | Text | e.g. January |
| month_abbr | Text | e.g. Jan (create if missing) |
| year_month | Text | e.g. 2022-01 |
| day_of_week | Whole Number | If present |
| is_weekday | Logical (True/False) | If present |

### Transformations

1. **Set date_key → Whole Number**
   - Select column > Transform > Data Type > Whole Number

2. **Set date → Date**
   - Select column > Transform > Data Type > Date
   - If date format is YYYY-MM-DD, Power BI parses automatically

3. **Set year, quarter_number, month_number → Whole Number**

4. **Set quarter_name, month_name, year_month → Text**

5. **Add month_abbr calculated column (if not in source):**
   - Add Column > Custom Column
   - Name: `month_abbr`
   - Formula: `Text.Start([month_name], 3)`

6. **Sort by date ascending**
   - Select `date` column > Home > Sort Ascending

7. **Verify no blank rows:** Filter `date_key` — no nulls should exist.

### Relationship Key
- `date_key` (Whole Number) — joins to `date_key` in all fact tables

### Mark as Date Table
After loading, in Report view: right-click `dim_date` > **Mark as date table** > select `date` column.

---

## Table 2: dim_business_unit

**File:** `dim_business_unit.csv`
**Query Name:** `dim_business_unit`
**Role:** Business unit dimension — 6 rows (BU01–BU06)

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| business_unit_key | Text | e.g. BU01 |
| business_unit_name | Text | e.g. Corporate Technology |
| business_unit_owner | Text | e.g. Alan Smith |
| owner_title | Text | e.g. VP, Corporate Technology |

### Transformations

1. Set all columns → **Text**
2. **Trim whitespace** on all columns: Select All > Transform > Format > Trim
3. **Add sort column** for business unit display order:
   - Add Column > Custom Column
   - Name: `bu_sort_order`
   - Formula:
   ```
   if [business_unit_key] = "BU01" then 1
   else if [business_unit_key] = "BU02" then 2
   else if [business_unit_key] = "BU03" then 3
   else if [business_unit_key] = "BU04" then 4
   else if [business_unit_key] = "BU05" then 5
   else 6
   ```
   - Set type → Whole Number
   - In Model view, sort `business_unit_name` by `bu_sort_order`

### Relationship Key
- `business_unit_key` (Text) — joins to `business_unit_key` in all fact tables

---

## Table 3: dim_cost_center

**File:** `dim_cost_center.csv`
**Query Name:** `dim_cost_center`
**Role:** Cost center dimension — 18 rows

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| cost_center_key | Text | e.g. 104001 |
| business_unit_key | Text | Foreign key to dim_business_unit |
| cost_center_name | Text | e.g. Corp Tech - End User Services |
| cost_center_owner | Text | e.g. Alan Smith |

### Transformations

1. Set all columns → **Text**
2. **Trim whitespace** on all columns
3. **Add display name** for clean slicer labels:
   - Add Column > Custom Column
   - Name: `cost_center_display`
   - Formula: `[cost_center_key] & " – " & [cost_center_name]`
   - Set type → Text
   - Use this column in slicers (shows CC number + name together)

### Relationship Key
- `cost_center_key` (Text) — joins to `cost_center_key` in all fact tables

---

## Table 4: dim_gl_account

**File:** `dim_gl_account.csv`
**Query Name:** `dim_gl_account`
**Role:** GL account dimension — 11 rows

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| gl_account_key | Whole Number | e.g. 611000 |
| gl_category | Text | e.g. Internal Labor |
| gl_description | Text | e.g. Salaries and wages |

### Transformations

1. Set `gl_account_key` → **Whole Number**
2. Set `gl_category`, `gl_description` → **Text**
3. **Trim whitespace** on text columns
4. **Add gl_category_sort** for display order:
   - Add Column > Custom Column
   - Name: `gl_sort_order`
   - Formula:
   ```
   if [gl_category] = "Internal Labor" then 1
   else if [gl_category] = "Benefits" then 2
   else if [gl_category] = "External Labor" then 3
   else if [gl_category] = "Managed Services" then 4
   else if [gl_category] = "Software" then 5
   else if [gl_category] = "Cloud" then 6
   else if [gl_category] = "Hardware" then 7
   else if [gl_category] = "Professional Services" then 8
   else if [gl_category] = "Telecom" then 9
   else if [gl_category] = "Training" then 10
   else 11
   ```
   - Set type → Whole Number
   - In Model view, sort `gl_category` by `gl_sort_order`

### Relationship Key
- `gl_account_key` (Whole Number) — joins to `gl_account_key` in fact_actuals, fact_budget, fact_vendor_spend, fact_project_spend

---

## Table 5: dim_vendor

**File:** `dim_vendor.csv`
**Query Name:** `dim_vendor`
**Role:** Vendor dimension — 18 rows

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| vendor_key | Text | e.g. VEN001 |
| vendor_name | Text | e.g. Microsoft Azure |
| vendor_category | Text | e.g. Cloud, Software, External Labor |
| vendor_tier | Text | Strategic, Preferred, Transactional |
| vendor_description | Text | Long text — keep for tooltips |

### Transformations

1. Set all columns → **Text**
2. **Trim whitespace** on all columns
3. **Add tier_sort_order:**
   - Add Column > Custom Column
   - Name: `tier_sort_order`
   - Formula:
   ```
   if [vendor_tier] = "Strategic" then 1
   else if [vendor_tier] = "Preferred" then 2
   else 3
   ```
   - Set type → Whole Number
4. **Add is_cloud_vendor calculated column:**
   - Add Column > Custom Column
   - Name: `is_cloud_vendor`
   - Formula: `if [vendor_category] = "Cloud" then "Yes" else "No"`
   - Set type → Text
   - Use this as a filter in Cloud Spend page slicer

### Relationship Key
- `vendor_key` (Text) — joins to `vendor_key` in fact_external_labor, fact_vendor_spend, fact_cloud_spend

---

## Table 6: dim_project

**File:** `dim_project.csv`
**Query Name:** `dim_project`
**Role:** Project dimension — 10 rows (PRJ001–PRJ010)

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| project_key | Text | e.g. PRJ001 |
| project_name | Text | e.g. ERP Modernization |
| project_category | Text | e.g. Transformation, Cloud, Data |
| project_status | Text | Active or Planned |
| project_owner | Text | e.g. Alan Smith |

### Transformations

1. Set all columns → **Text**
2. **Trim whitespace** on all columns
3. **Add project_status_sort:**
   - Add Column > Custom Column
   - Name: `status_sort`
   - Formula: `if [project_status] = "Active" then 1 else 2`
   - Set type → Whole Number

### Relationship Key
- `project_key` (Text) — joins to `project_key` in fact_external_labor, fact_cloud_spend, fact_project_spend

---

## Table 7: dim_employee

**File:** `dim_employee.csv`
**Query Name:** `dim_employee`
**Role:** Employee dimension — supports headcount analysis

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| employee_key | Text | Primary key |
| employee_name | Text | |
| cost_center_key | Text | FK to dim_cost_center |
| business_unit_key | Text | FK to dim_business_unit |
| job_title | Text | |
| hire_date | Date | |
| employee_status | Text | Active / Inactive |

### Transformations

1. Set key columns → **Text**
2. Set `hire_date` → **Date**
3. Set all other text columns → **Text**
4. **Trim whitespace** on text columns

### Relationship Key
- `employee_key` (Text) — joins to employee references in fact tables if present

---

## Table 8: fact_actuals

**File:** `fact_actuals.csv`
**Query Name:** `fact_actuals`
**Role:** Core financial fact table — every actual transaction 2022–2026

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| transaction_id | Text | Unique row identifier — keep for audit |
| date_key | Whole Number | FK to dim_date |
| transaction_date | Date | The actual transaction date |
| cost_center_key | Text | FK to dim_cost_center |
| business_unit_key | Text | FK to dim_business_unit |
| gl_account_key | Whole Number | FK to dim_gl_account |
| vendor_key | Text | Nullable — not all transactions have a vendor |
| project_key | Text | Nullable — not all transactions tied to a project |
| scenario | Text | Should always be "Actual" |
| amount | Fixed Decimal Number | Dollar amount — positive = spend |
| notes | Text | Keep for drill-through detail |

### Transformations

1. Set `transaction_id` → **Text**
2. Set `date_key` → **Whole Number**
3. Set `transaction_date` → **Date**
4. Set `cost_center_key`, `business_unit_key`, `vendor_key`, `project_key`, `scenario`, `notes` → **Text**
5. Set `gl_account_key` → **Whole Number**
6. Set `amount` → **Fixed Decimal Number** (currency)
7. **Handle nullable keys:** `vendor_key` and `project_key` may be blank — this is expected. Do not fill or remove blank rows.
8. **Trim `notes` column** to prevent long strings affecting rendering
9. **Verify row count** by running: Transform > Statistics > Count Rows. Record this number for validation.

### Calculated Column (optional — for drill-through display)

Add Column > Custom Column:
- Name: `year_month_display`
- Formula: `Text.From([date_key])` — or join from dim_date after load

### Relationship Keys
- `date_key` → dim_date[date_key]
- `cost_center_key` → dim_cost_center[cost_center_key]
- `business_unit_key` → dim_business_unit[business_unit_key]
- `gl_account_key` → dim_gl_account[gl_account_key]

---

## Table 9: fact_budget

**File:** `fact_budget.csv`
**Query Name:** `fact_budget`
**Role:** Monthly budget plan for each cost center and GL account

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| date_key | Whole Number | FK to dim_date |
| cost_center_key | Text | FK to dim_cost_center |
| business_unit_key | Text | FK to dim_business_unit |
| gl_account_key | Whole Number | FK to dim_gl_account |
| scenario | Text | Should always be "Budget" |
| amount | Fixed Decimal Number | Budgeted amount |
| notes | Text | If present |

### Transformations

Apply same type assignments as fact_actuals. Set `amount` → **Fixed Decimal Number**.

### Relationship Keys
Same structure as fact_actuals — same FK columns join to same dimensions.

---

## Table 10: fact_forecast

**File:** `fact_forecast.csv`
**Query Name:** `fact_forecast`
**Role:** Multiple forecast cycles per year (3+9, 6+6, 9+3)

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| date_key | Whole Number | FK to dim_date |
| cost_center_key | Text | FK |
| business_unit_key | Text | FK |
| gl_account_key | Whole Number | FK |
| forecast_cycle | Text | "3+9", "6+6", "9+3" |
| scenario | Text | "Forecast" |
| amount | Fixed Decimal Number | |

### Transformations

1. Apply standard type assignments
2. **Trim `forecast_cycle`** — ensure no trailing spaces
3. **Verify 3 distinct values** in forecast_cycle: Transform > Column Statistics

### Key Column
- `forecast_cycle` — this powers the Forecast Cycle slicer on the Forecast page

---

## Table 11: fact_headcount

**File:** `fact_headcount.csv`
**Query Name:** `fact_headcount`
**Role:** Monthly workforce snapshot per cost center

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| date_key | Whole Number | FK to dim_date |
| cost_center_key | Text | FK |
| business_unit_key | Text | FK |
| approved_positions | Whole Number | Authorized headcount |
| filled_positions | Whole Number | Actual headcount in seat |
| open_positions | Whole Number | approved minus filled |
| vacancy_rate | Decimal Number | Between 0 and 1 (e.g. 0.1429 = 14.29%) |
| monthly_labor_cost | Fixed Decimal Number | Dollar amount |
| notes | Text | |

### Transformations

1. Set `approved_positions`, `filled_positions`, `open_positions` → **Whole Number**
2. Set `vacancy_rate` → **Decimal Number** (do NOT use Percentage type — format in visuals instead)
3. Set `monthly_labor_cost` → **Fixed Decimal Number**
4. **Validate:** Filter for any rows where open_positions ≠ approved_positions - filled_positions. Flag if found.

---

## Table 12: fact_external_labor

**File:** `fact_external_labor.csv`
**Query Name:** `fact_external_labor`
**Role:** Individual contractor record per month — rate, hours, spend, risk

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| date_key | Whole Number | FK |
| cost_center_key | Text | FK |
| business_unit_key | Text | FK |
| vendor_key | Text | FK to dim_vendor |
| resource_name | Text | e.g. Contractor 385 |
| role | Text | e.g. Architect, Developer |
| hourly_rate | Fixed Decimal Number | e.g. 85.00 |
| hours | Whole Number | Monthly hours billed |
| amount | Fixed Decimal Number | hourly_rate × hours |
| project_key | Text | FK to dim_project |
| contract_end_date | Date | Critical for risk analysis |
| risk_level | Text | High, Medium, Low |

### Transformations

1. Set `hourly_rate`, `amount` → **Fixed Decimal Number**
2. Set `hours` → **Whole Number**
3. Set `contract_end_date` → **Date**
4. Set `risk_level` → **Text**
5. **Add risk_sort calculated column:**
   - Add Column > Custom Column
   - Name: `risk_sort`
   - Formula: `if [risk_level] = "High" then 1 else if [risk_level] = "Medium" then 2 else 3`
   - Set type → Whole Number
6. **Add days_until_expiry column:**
   - Add Column > Custom Column
   - Name: `days_until_expiry`
   - Formula: `Duration.Days([contract_end_date] - DateTime.Date(DateTime.LocalNow()))`
   - Set type → Whole Number
   - Negative values = already expired

### Relationship Keys
- `vendor_key` → dim_vendor[vendor_key]
- `project_key` → dim_project[project_key]

---

## Table 13: fact_vendor_spend

**File:** `fact_vendor_spend.csv`
**Query Name:** `fact_vendor_spend`
**Role:** Vendor invoice/spend records

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| date_key | Whole Number | FK |
| cost_center_key | Text | FK |
| business_unit_key | Text | FK |
| vendor_key | Text | FK to dim_vendor |
| gl_account_key | Whole Number | FK |
| amount | Fixed Decimal Number | |
| notes | Text | If present |

### Transformations

Apply standard type assignments. Set `amount` → **Fixed Decimal Number**.

---

## Table 14: fact_cloud_spend

**File:** `fact_cloud_spend.csv`
**Query Name:** `fact_cloud_spend`
**Role:** Cloud consumption by provider, service category, and cost center

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| date_key | Whole Number | FK |
| cost_center_key | Text | FK |
| business_unit_key | Text | FK |
| vendor_key | Text | FK — VEN001 (Azure) or VEN002 (AWS) |
| service_category | Text | Compute, Storage, Network, Analytics, Database |
| amount | Fixed Decimal Number | |
| project_key | Text | FK to dim_project |
| notes | Text | |

### Transformations

1. Apply standard type assignments
2. **Trim `service_category`** — ensure consistent values
3. **Add provider_name calculated column** (for display):
   - Add Column > Custom Column
   - Name: `provider_name`
   - Formula: `if [vendor_key] = "VEN001" then "Microsoft Azure" else if [vendor_key] = "VEN002" then "AWS" else "Other"`
   - Set type → Text

### Key Columns
- `vendor_key` — used to split Azure vs AWS in all cloud visuals
- `service_category` — used in stacked bar / donut on cloud page

---

## Table 15: fact_project_spend

**File:** `fact_project_spend.csv`
**Query Name:** `fact_project_spend`
**Role:** Project-level spend with Capex/Opex classification

### Columns and Types

| Column Name | Data Type | Notes |
|---|---|---|
| date_key | Whole Number | FK |
| cost_center_key | Text | FK |
| business_unit_key | Text | FK |
| project_key | Text | FK to dim_project |
| gl_account_key | Whole Number | FK |
| spend_type | Text | "Capex" or "Opex" |
| amount | Fixed Decimal Number | |
| notes | Text | |

### Transformations

1. Apply standard type assignments
2. **Trim `spend_type`** and verify only "Capex" and "Opex" exist
3. **Add spend_type_sort:**
   - Add Column > Custom Column
   - Name: `spend_type_sort`
   - Formula: `if [spend_type] = "Capex" then 1 else 2`
   - Set type → Whole Number

---

## Final Power Query Checklist

After completing all tables:

- [ ] All 15 queries are named correctly (no spaces, matches table names exactly)
- [ ] No auto-generated "Changed Type" steps remain from initial import
- [ ] All `amount` columns are Fixed Decimal Number (not Decimal)
- [ ] All `date_key` columns are Whole Number (not text)
- [ ] All `_key` text columns are Text type (not auto-detected integers)
- [ ] `contract_end_date` in fact_external_labor is Date type
- [ ] `vacancy_rate` in fact_headcount is Decimal Number
- [ ] `dim_date[date]` is Date type
- [ ] Row counts recorded for each fact table (for validation later)
- [ ] Click **Close & Apply** — wait for all tables to load
- [ ] Open Model view — verify no relationship errors shown in red
