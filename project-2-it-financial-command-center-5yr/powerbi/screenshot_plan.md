# Screenshot Plan
## Nexora IT Financial Command Center

Screenshots serve two purposes: GitHub repository documentation and LinkedIn portfolio posts.

---

## Folder Location

Save all screenshots to:
```
project-2-it-financial-command-center-5yr/assets/screenshots/
```

Create this folder in your local clone of the repo before capturing.

---

## Screenshot Capture Method

**Best quality method:**
1. Set Power BI to full-screen view: View > Full screen (F11)
2. Use Windows Snipping Tool (Win + Shift + S) → Select Rectangular Snip
3. Capture the full canvas (exclude the Power BI chrome/toolbar)
4. Save as PNG, 1280×720 minimum

**Alternative method:**
- File > Export > Export to PDF (multi-page export)
- Then screenshot individual pages from the PDF

**Resolution target:** 1920×1080 if your monitor supports it. Scale canvas to match.

---

## Screenshot 1: CIO Executive Summary — Full-Year Overview

**File Name:** `screenshot_01_cio_executive_summary.png`

**Slicer Settings:**
- Year: **2025**
- Month: **December** (shows full-year YTD)
- Business Unit: **All (no filter)**
- Forecast Cycle: **9+3**

**Story This Screenshot Tells:**
> "The IT organization finished FY2025 tracking above budget. Cloud and external labor were the primary pressure points, while Cybersecurity came in under budget. The executive summary gives the CIO a single view of spend, variance, and year-end risk status."

**Elements That Must Be Visible:**
- All 6 KPI cards (YTD Actuals, Budget, Variance, Variance %, Year-End Projection, Risk Flag)
- Monthly trend chart showing 12 months of actuals vs budget
- Top 5 variance drivers table with red/green conditional formatting
- Spend by Business Unit bar chart
- GL Category donut chart
- Executive commentary box

**LinkedIn Caption Idea:**
"The Nexora IT Financial Command Center CIO Executive Summary — built in Power BI on a 5-year star schema dataset. One page answers: What did we spend? How did we perform against budget? Where do we need to act?"

---

## Screenshot 2: Budget vs Actuals — Monthly Drill-Down

**File Name:** `screenshot_02_budget_vs_actuals.png`

**Slicer Settings:**
- Year: **2025**
- Month: **June** (mid-year review)
- Business Unit: **All**
- GL Category: **All**

**Story This Screenshot Tells:**
> "Mid-year view showing Cloud Platform Engineering and Data Engineering tracking over budget. The cost center variance matrix highlights where pressure is building. GL Category breakdown shows cloud and external labor as the over-budget drivers."

**Elements That Must Be Visible:**
- KPI card strip (YTD totals)
- Monthly actuals vs budget line/column chart (zoom slider visible)
- Cost center variance matrix with conditional color formatting (red cells clearly visible)
- GL Category variance bar chart with positive/negative bars in distinct colors

**LinkedIn Caption Idea:**
"Budget vs Actuals page — the variance matrix makes it immediately clear which cost centers need attention. Red = over budget. Green = favorable. Built with DAX TOTALYTD and conditional formatting rules."

---

## Screenshot 3: Forecast & Projection — Year-End Risk View

**File Name:** `screenshot_03_forecast_projection.png`

**Slicer Settings:**
- Year: **2026**
- Business Unit: **All**
- Forecast Cycle: **6+6**

**Story This Screenshot Tells:**
> "Heading into the second half of 2026, Infrastructure & Cloud and Enterprise Data Services are tracking at High Risk — forecast exceeds budget by more than 5%. The year-end projection gauge shows we are on pace to finish above plan."

**Elements That Must Be Visible:**
- Full-year budget vs forecast KPI cards
- Forecast Accuracy % card
- Area chart showing actuals (solid) vs remaining forecast (lighter)
- Forecast cycle comparison column chart (3+9 vs 6+6 vs 9+3)
- Risk table with red/yellow/green risk flag column
- Year-end projection gauge

**LinkedIn Caption Idea:**
"Forecast & Projection page — three forecast cycles in one view. The gauge shows whether year-end projection is above or below budget. The risk table surfaces which cost centers need immediate forecast review."

---

## Screenshot 4: External Labor — Contract Risk Dashboard

**File Name:** `screenshot_04_external_labor_risk.png`

**Slicer Settings:**
- Year: **2025**
- Business Unit: **All**
- Risk Level: **High** (filter to show only high-risk contracts)

**Story This Screenshot Tells:**
> "23 contractor contracts are at high risk of expiration in the next 90 days. All are tied to active strategic programs — ERP Modernization, Data Lakehouse, and Cloud Optimization. Immediate renewal review is required to avoid program schedule risk."

**Elements That Must Be Visible:**
- KPI cards: External Labor Spend, Contractor Count, Avg Hourly Rate, High Risk Contracts (red card)
- External labor spend trend line chart
- Contract end date risk table sorted by soonest expiry — red rows clearly visible
- Days to Expiry column highlighted in red/yellow

**LinkedIn Caption Idea:**
"External Labor page — contract expiry risk management built into the dashboard. Sorted by soonest contract end date, with risk levels color-coded. Built using DAX calculated column for days_until_expiry."

---

## Screenshot 5: Vendor Spend — Strategic Vendor Concentration

**File Name:** `screenshot_05_vendor_spend_concentration.png`

**Slicer Settings:**
- Year: **2025**
- Business Unit: **All**
- Vendor Category: **All**
- Vendor Tier: **Strategic** (show only strategic vendors)

**Story This Screenshot Tells:**
> "Microsoft Azure, AWS, and Capgemini dominate IT vendor spend. The treemap makes concentration immediately visible — three vendors represent over 65% of total strategic spend. YoY growth shows Databricks (+38%) and Snowflake (+29%) as the fastest-growing platforms."

**Elements That Must Be Visible:**
- Top 10 vendors bar chart sorted descending
- Vendor YoY comparison bar chart (current vs prior year)
- Treemap with proportional tile sizes
- Spend by category donut

**LinkedIn Caption Idea:**
"Vendor Spend page — a treemap makes concentration risk impossible to ignore. Azure and AWS tiles dominate the view. YoY comparison shows which vendors grew fastest. Built on fact_vendor_spend with dim_vendor star schema joins."

---

## Screenshot 6: Cloud Spend — Azure vs AWS 5-Year Trend

**File Name:** `screenshot_06_cloud_spend_trend.png`

**Slicer Settings:**
- Year: **All** (unfilter to show full 2022–2026 trend)
- Business Unit: **All**
- Provider: **All**

**Story This Screenshot Tells:**
> "Cloud spend more than doubled between 2022 and 2026 — growing 121% in 5 years. Azure leads AWS consistently. Infrastructure & Cloud and Data Engineering are the largest cloud consumers. Analytics workloads are the fastest-growing service category."

**Elements That Must Be Visible:**
- Azure vs AWS trend line chart showing clear growth trajectory from 2022 to 2026
- Azure (blue) and AWS (orange) lines clearly differentiated
- Cloud by service category stacked bar chart (multi-year view)
- Cloud by cost center matrix (high-spend cells clearly highlighted)

**LinkedIn Caption Idea:**
"Cloud Spend page — the trend chart tells the story in one glance. Azure outpaces AWS but both are growing. Infrastructure & Cloud Engineering drives the highest consumption. Built on 5 years of monthly cloud consumption data."

---

## Screenshot 7: Headcount — Vacancy Rate Analysis

**File Name:** `screenshot_07_headcount_vacancy.png`

**Slicer Settings:**
- Year: **2025**
- Business Unit: **All**
- Month: **December**

**Story This Screenshot Tells:**
> "EPMO and the Transformation Portfolio carry the highest vacancy rates — 20% and 25% respectively. These open positions are being backfilled with external contractors, creating a cost compounding effect. Org-wide vacancy rate increased from 7.3% in 2024 to 10.3% in 2025."

**Elements That Must Be Visible:**
- KPI cards: Approved, Filled, Open Positions, Vacancy Rate (amber or red), Labor Cost, Cost per FTE
- Headcount trend chart showing approved vs filled over time
- Vacancy rate by business unit bar chart with color coding
- Headcount detail table with highest vacancy rows visible

**LinkedIn Caption Idea:**
"Headcount page — not just a count of people. Vacancy rate by BU surfaces where open positions are compounding into contractor cost. Power BI makes this cross-factor analysis easy to see at a glance."

---

## Screenshot 8: Project Spend — Capital vs Operating Split

**File Name:** `screenshot_08_project_spend_capex.png`

**Slicer Settings:**
- Year: **2025**
- Business Unit: **All**
- Project Status: **Active**

**Story This Screenshot Tells:**
> "IT project portfolio is 61% Capex, 39% Opex. ERP Modernization is the largest project and tracking over budget. The AI Finance Reporting Pilot is significantly under spend — likely delayed into 2026. 8 active projects are in flight simultaneously."

**Elements That Must Be Visible:**
- KPI cards including Capex Spend, Opex Spend, and Capex %
- Project budget vs actuals vs forecast clustered column chart
- Capex vs Opex donut chart
- Project detail table with status badges (Active green, Planned amber) and variance % data bars

**LinkedIn Caption Idea:**
"Project Spend page — a full portfolio view with budget, actuals, and forecast for every project. Capex vs Opex split is tracked in real time. Conditional formatting on project status and variance makes prioritization immediate."

---

## Screenshot 9: Drill-through Detail — Transaction Transparency

**File Name:** `screenshot_09_drillthrough_detail.png`

**How to Get Here:**
1. Go to Page 2 (Budget vs Actuals)
2. Year = 2025
3. Right-click on Cloud Platform Engineering in the cost center matrix
4. Drill through → Drill-through Detail

**Story This Screenshot Tells:**
> "Every KPI in the dashboard is backed by transaction-level data. From the executive summary, a CIO can drill through to see exactly which invoices, by vendor, by GL account, by date, drove the variance. Full audit trail to the lowest level of detail."

**Elements That Must Be Visible:**
- "← Back" button visible
- Header showing which cost center and time period was drilled through
- Context KPI cards (Transaction Count, Total Amount, Avg per Transaction)
- Transaction table with: Date, Month, Year, BU, Cost Center, GL Category, Vendor, Project, Amount, Notes
- Amount column formatted as currency, sorted by date descending

**LinkedIn Caption Idea:**
"Drill-through Detail page — every headline number links to every transaction behind it. Right-click any data point. One click to full transparency. Power BI drill-through at enterprise scale."

---

## Bonus Screenshot 10: Mobile Layout (Optional)

**File Name:** `screenshot_10_mobile_view.png`

**How to Capture:**
1. View > Mobile Layout
2. Arrange KPI cards and key visuals for mobile view
3. Screenshot the mobile canvas

**Story:**
> "The executive dashboard is mobile-ready. KPI cards visible without scrolling. Built for CIO review on any device."

---

## LinkedIn Post Strategy

### Post 1 — Announcement Post (use Screenshot 1)
> "I built the Nexora IT Financial Command Center — a 5-year enterprise IT finance dashboard in Power BI.
>
> Covers: $1B+ in IT spend | 18 cost centers | 18 vendors | 10 projects | 2022–2026
>
> One page. Everything the CIO needs to know. [Screenshot 1]
>
> Full project on GitHub: [link]"

### Post 2 — Technical Deep Dive (use Screenshots 2 + 3)
> "How I modeled 5 years of IT finance data in a star schema:
> • 7 dimension tables
> • 8 fact tables
> • 30+ DAX measures
> • TOTALYTD, SAMEPERIODLASTYEAR, DATEADD, DIVIDE — all in production
>
> [Screenshot 2] [Screenshot 3]"

### Post 3 — Insight Story (use Screenshot 4 or 5)
> "External labor risk is invisible until it's a problem.
> I built a contract expiry tracker that surfaces high-risk contractor renewals 90 days in advance.
> 23 high-risk contracts. $9.8M at risk. Color-coded by urgency.
> [Screenshot 4]"

### Post 4 — Cloud Analytics (use Screenshot 6)
> "Cloud spend grew 121% in 5 years in this dataset.
> Azure outpaced AWS every year.
> Analytics workloads are the fastest-growing service category.
> One trend chart tells the whole story. [Screenshot 6]"

---

## GitHub README Embed

After uploading screenshots to `assets/screenshots/`, embed the hero screenshot in the README:

```markdown
### Dashboard Preview

![CIO Executive Summary](project-2-it-financial-command-center-5yr/assets/screenshots/screenshot_01_cio_executive_summary.png)
```

Add all screenshots with captions in a "Screenshots" section of the README for portfolio viewers.
