# Data Model

## Recommended Star Schema
Use `dim_date`, `dim_cost_center`, `dim_business_unit`, `dim_vendor`, `dim_gl_account`, `dim_project`, and `dim_employee` as dimension tables.

## Fact Tables
- `fact_actuals`
- `fact_budget`
- `fact_forecast`
- `fact_headcount`
- `fact_external_labor`
- `fact_vendor_spend`
- `fact_cloud_spend`
- `fact_project_spend`

## Relationships
Create one-to-many relationships from each dimension to the relevant fact table. Keep filter direction single from dimension to fact. Mark `dim_date` as the date table in Power BI using the `date` column.

## Keys
- `date_key` joins all monthly fact tables to `dim_date`
- `cost_center_key` joins facts to `dim_cost_center`
- `business_unit_key` joins facts to `dim_business_unit`
- `vendor_key` joins vendor-related facts to `dim_vendor`
- `gl_account_key` joins finance facts to `dim_gl_account`
- `project_key` joins project-related facts to `dim_project`

## Why This Scales
This model separates descriptive attributes from measurable business events. It supports consistent filtering, better DAX, easier refresh, and cleaner dashboard development.
