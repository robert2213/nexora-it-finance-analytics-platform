# Nexora IT Finance Analytics Platform

AI-assisted IT Finance analytics project using Claude Code.

## Project Overview

This project transforms a 5-year transactional IT finance dataset into an executive reporting package.

## Deliverables

- Excel financial dashboard
- Executive PowerPoint deck
- Portfolio case study
- LinkedIn article graphic

## Tools Used

Claude Code, Excel, Python, Pandas, OpenPyXL, Python-PPTX, Python-DOCX

## Skills Demonstrated

IT Finance, FP&A, Dashboard Design, Executive Reporting, KPI Development, Financial Storytelling, AI-Assisted Analytics

---

## Project 2: Nexora IT Financial Command Center

The Nexora IT Financial Command Center expands the original Nexora IT Finance Analytics Platform into an enterprise-grade Power BI reporting solution.

This project includes a 5-year IT finance dataset covering 2022–2026 and is designed to support executive decision-making across budgeting, forecasting, headcount planning, vendor management, cloud optimization, external labor management, and project portfolio governance.

### Business Objectives

- Improve visibility into IT spend
- Track budget vs actual performance
- Monitor forecast accuracy
- Analyze vendor concentration risk
- Optimize cloud spend
- Manage contractor and external labor costs
- Support CIO and executive leadership reporting

### Key Deliverables

- 5-year IT finance dataset, 2022–2026
- Power BI-ready star schema data model
- Executive dashboard requirements
- DAX measure library
- Executive insight documentation
- Dashboard wireframes
- Architecture documentation
- Power BI build guide

### Skills Demonstrated

- Financial Planning & Analysis
- Power BI Development
- Data Modeling
- Budgeting & Forecasting
- Executive Reporting
- Vendor Spend Analytics
- Cloud Cost Management
- Workforce Planning
- Data Architecture
- AI-Assisted Development

### Folder Structure

```text
project-2-it-financial-command-center-5yr/
├── data/
├── docs/
├── assets/
└── powerbi/
```

---

### Power BI Dashboard Build

The `powerbi/` folder contains the complete step-by-step implementation guide for building the dashboard in Power BI Desktop.

#### Build Documents

| Document | Description |
|---|---|
| [Power Query Import Steps](project-2-it-financial-command-center-5yr/powerbi/power_query_import_steps.md) | Detailed import instructions for all 15 CSV files — column types, calculated columns, relationship keys, and Power Query transformations |
| [DAX Measure Script](project-2-it-financial-command-center-5yr/powerbi/dax_measure_script.md) | Copy/paste-ready DAX measures organized into 12 sections — base, budget, forecast, variance, time intelligence, headcount, external labor, vendor, cloud, project, and risk |
| [Page Build Instructions](project-2-it-financial-command-center-5yr/powerbi/page_build_instructions.md) | Step-by-step construction guide for all 9 dashboard pages — exact field assignments, visual settings, conditional formatting, slicers, tooltips, and drill-through configuration |
| [Validation Tests](project-2-it-financial-command-center-5yr/powerbi/validation_tests.md) | 25-point validation checklist covering row counts, financial reconciliation, YTD logic, relationship filters, and drill-through behavior |
| [Screenshot Plan](project-2-it-financial-command-center-5yr/powerbi/screenshot_plan.md) | 10-screenshot capture plan with exact slicer settings, file names, story descriptions, and LinkedIn post templates for each screenshot |

#### Dashboard Pages

| Page | Primary Focus |
|---|---|
| CIO Executive Summary | Full financial picture — KPIs, monthly trend, top variance drivers, executive commentary |
| Budget vs Actuals | Month-by-month budget execution — cost center variance matrix, GL category breakdown |
| Forecast & Projection | 3+9 / 6+6 / 9+3 forecast comparison, year-end projection gauge, risk flag table |
| External Labor | Contractor spend, avg hourly rate, contract end date risk table |
| Vendor Spend | Top 10 vendors, YoY growth, concentration treemap, category analysis |
| Cloud Spend | Azure vs AWS trend 2022–2026, service category breakdown, cost center allocation |
| Headcount | Approved vs filled positions, vacancy rate by BU, labor cost trend |
| Project Spend | Capex vs Opex split, project budget vs actuals vs forecast, portfolio detail |
| Drill-through Detail | Transaction-level audit — every KPI drills through to underlying records |
