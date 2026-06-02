# Executive Insights
## Nexora IT Financial Command Center — 2022–2026

Generated from the 5-year IT finance dataset. All figures derived from the star schema data model.

---

## Five-Year Financial Summary

| Year | IT Budget | IT Actuals | Variance $ | Variance % |
|---|---|---|---|---|
| 2022 | $183.2M | $178.4M | -$4.8M | -2.6% |
| 2023 | $191.0M | $197.3M | +$6.3M | +3.3% |
| 2024 | $204.6M | $209.1M | +$4.5M | +2.2% |
| 2025 | $215.8M | $226.4M | +$10.6M | +4.9% |
| 2026 | $228.4M | $242.1M (forecast) | +$13.7M | +6.0% |

**5-Year Total IT Spend: ~$1.053 billion**

**Trend:** IT spend is growing faster than budget. Budget growth averages 5.6% per year; actual spend growth averages 7.9% per year. The gap is widening — driven primarily by unbudgeted cloud consumption growth and external labor expansion in 2025 and 2026.

---

## Insight 1 — Largest Budget Variances

### Top 5 Over-Budget Cost Centers (2025 YTD)

| Rank | Cost Center | Owner | Actuals | Budget | Variance $ | Variance % |
|---|---|---|---|---|---|---|
| 1 | Cloud Platform Engineering (104018) | Mike Hanley | $28.4M | $26.1M | +$2.3M | **+8.8%** |
| 2 | Data Engineering (104023) | Vimala Rao | $23.1M | $21.8M | +$1.3M | **+6.0%** |
| 3 | Corp Tech – Enterprise Apps (104003) | Alan Smith | $19.4M | $18.9M | +$0.5M | **+2.6%** |
| 4 | Enterprise Project Delivery (109003) | Renee Johnson | $9.8M | $9.4M | +$0.4M | **+4.3%** |
| 5 | Business Applications (104019) | Alan Smith | $17.2M | $16.9M | +$0.3M | **+1.8%** |

**Root Cause Analysis:**
- CC104018 (Cloud Platform Engineering): Azure Storage and Compute exceeded plan due to Data Lakehouse Buildout (PRJ003) and Network Modernization (PRJ008) activity running ahead of schedule
- CC104023 (Data Engineering): Capgemini contractor ramp-up for Data Lakehouse and Claims Analytics programs — external labor is the primary driver
- CC104003 (Corp Tech – Enterprise Apps): ERP Modernization (PRJ001) professional services exceeded planned hours; Oracle licensing uplift not included in original budget

### Top 3 Under-Budget Cost Centers (2025 YTD)

| Rank | Cost Center | Actuals | Budget | Favorable Variance |
|---|---|---|---|---|
| 1 | Cybersecurity Operations (110101) | $9.8M | $10.1M | -$0.3M (-3.0%) |
| 2 | Corp Tech – End User Services (104001) | $15.2M | $15.8M | -$0.6M (-3.8%) |
| 3 | Identity & Access Management (110102) | $5.9M | $6.2M | -$0.3M (-4.8%) |

**Note:** Under-budget in Cybersecurity reflects delayed CrowdStrike rollout (now rescheduled to Q4 2025), not a true savings — expect Q4 variance reversal.

---

## Insight 2 — Largest Vendor Spend Increases

### Strategic Vendor Year-over-Year Comparison

| Vendor | 2024 Spend | 2025 Spend | Increase $ | Increase % | Category |
|---|---|---|---|---|---|
| Microsoft Azure | $16.8M | $20.5M | +$3.7M | **+22.0%** | Cloud |
| AWS | $12.1M | $14.8M | +$2.7M | **+22.3%** | Cloud |
| Capgemini | $9.8M | $12.1M | +$2.3M | **+23.5%** | External Labor |
| Snowflake | $4.8M | $6.2M | +$1.4M | **+29.2%** | Software |
| Databricks | $4.2M | $5.8M | +$1.6M | **+38.1%** | Software |

**Key Observation:** Databricks and Snowflake represent the highest YoY percentage growth among strategic vendors. Combined, the data platform stack (Snowflake + Databricks) grew from $9.0M to $12.0M — a 33.3% increase in a single year. This reflects the Data Lakehouse Buildout program (PRJ003) scaling into production.

**Concentration Risk:** Microsoft Azure, AWS, and Capgemini together represent $47.4M of 2025 vendor spend — 65.5% of total vendor spend is concentrated in three vendors. A disruption, rate increase, or contract dispute with any of these three vendors would materially impact IT operations.

---

## Insight 3 — Cloud Spend Growth Trend

### Cloud Spend by Provider (Annual)

| Year | Azure | AWS | Total Cloud | YoY Growth |
|---|---|---|---|---|
| 2022 | $9.6M | $7.1M | $16.7M | — |
| 2023 | $11.8M | $8.9M | $20.7M | +24.0% |
| 2024 | $14.2M | $11.4M | $25.6M | +23.7% |
| 2025 | $17.1M | $13.8M | $30.9M | +20.7% |
| 2026 (Forecast) | $20.5M | $16.4M | $36.9M | +19.4% |

**2022–2026 Cloud Growth: +121%** (more than doubled in 5 years)

### Cloud by Service Category (2025)

| Category | Spend | % of Cloud Total |
|---|---|---|
| Compute | $10.8M | 35.0% |
| Storage | $8.4M | 27.2% |
| Analytics | $6.2M | 20.1% |
| Network | $3.7M | 12.0% |
| Database | $1.8M | 5.8% |

**Largest Cloud Consumers by Cost Center (2025):**
1. Cloud Platform Engineering (104018): $5.9M — Infrastructure foundation
2. Analytics & Reporting (104027): $4.3M — Data platform workloads
3. Data Engineering (104023): $4.7M — Lake and pipeline processing
4. Service Desk Operations (104022): $2.9M — Azure-hosted ITSM tooling

**Optimization Opportunity:**
Analytics workloads in CC104023 and CC104027 grew 34% in 2025 without a corresponding reserved capacity purchase. Switching from on-demand to reserved instances for consistent workloads is estimated to reduce cloud spend by 20–30% for those cost centers — a potential $1.8M–$2.7M annual savings opportunity.

---

## Insight 4 — Headcount Growth Trend

### Headcount Snapshot (End of Year)

| Year | Approved | Filled | Open | Vacancy Rate | Avg Monthly Labor Cost |
|---|---|---|---|---|---|
| 2022 | 162 | 148 | 14 | 8.6% | $11.2M |
| 2023 | 171 | 158 | 13 | 7.6% | $12.1M |
| 2024 | 178 | 165 | 13 | 7.3% | $13.0M |
| 2025 | 185 | 166 | 19 | 10.3% | $13.8M |
| 2026 (Plan) | 192 | — | — | — | $14.8M (est.) |

**2025 Vacancy Rate Increase Alert:** Open positions grew from 13 to 19 in 2025, pushing vacancy rate from 7.3% to 10.3%. The highest concentrations are in:
- Enterprise Project Delivery (BU04/EPMO): 4 open positions, 20% vacancy rate
- Transformation Portfolio (BU04): 2 open positions, 25% vacancy rate
- Data Governance (BU02): 3 open positions, 13.6% vacancy rate

**Observation:** The EPMO and BU04 vacancy rate is particularly notable because open internal positions are being backfilled with external contractors — this is adding external labor cost pressure at the same time internal labor is under budget. This cross-factor dynamic should be surfaced at the CIO level.

**Cost per FTE Trend:**

| Year | Cost per Internal FTE (Annual) | Change |
|---|---|---|
| 2022 | $90,800 | — |
| 2023 | $91,800 | +1.1% |
| 2024 | $94,200 | +2.6% |
| 2025 | $99,800 | +5.9% |

The 5.9% cost per FTE increase in 2025 exceeds both budget assumptions and prior year trends — driven by mid-year salary adjustments and benefit cost increases. This should feed into the 2026 budget model.

---

## Insight 5 — External Labor Risk

### External Labor Spend Trend

| Year | External Labor Spend | Contractors | Avg Hourly Rate | YoY Growth |
|---|---|---|---|---|
| 2022 | $22.1M | 78 | $104/hr | — |
| 2023 | $26.8M | 92 | $109/hr | +21.3% |
| 2024 | $31.4M | 118 | $113/hr | +17.2% |
| 2025 | $38.4M | 142 | $118/hr | +22.3% |
| 2026 (Forecast) | $44.2M | 160 | $124/hr | +15.1% |

**5-Year External Labor Growth: +100%** — external labor has doubled in spend while internal headcount grew only 14.2%.

### Contract Expiry Risk (2025–2026)

| Risk Level | Contract Count | % of Engagements | Total Spend at Risk |
|---|---|---|---|
| High | 23 | 16.2% | $9.8M |
| Medium | 41 | 28.9% | $14.6M |
| Low | 78 | 54.9% | $14.0M |

**High-Risk Expirations (Next 6 Months):**
- 8 Cloud Engineer roles (CC104018, CC104023) — critical to Data Lakehouse and Cloud Optimization programs
- 6 Architect roles across ERP Modernization (PRJ001)
- 5 QA Analyst roles for Claims Analytics Automation (PRJ007)
- 4 Developer roles for ServiceNow Workflow Expansion (PRJ005)

**Action Required:** All 23 High-risk contracts should be reviewed within 30 days. Contracts supporting active programs (PRJ001, PRJ003, PRJ007) must be renewed or transitioned before expiry to avoid program schedule risk.

---

## Insight 6 — Forecast Risk

### 2026 Full-Year Forecast vs Budget

| Business Unit | Budget | Forecast | Variance | Risk |
|---|---|---|---|---|
| Infrastructure & Cloud (BU06) | $42.1M | $46.8M | +$4.7M (+11.2%) | HIGH |
| Enterprise Data Services (BU02) | $38.4M | $42.1M | +$3.7M (+9.6%) | HIGH |
| Corporate Technology (BU03) | $74.2M | $76.8M | +$2.6M (+3.5%) | MEDIUM |
| EPMO (BU04) | $16.1M | $16.9M | +$0.8M (+5.0%) | MEDIUM |
| Information Security (BU05) | $18.8M | $18.4M | -$0.4M (-2.1%) | LOW |
| Enterprise Engineering (BU01) | $39.0M | $41.1M | +$2.1M (+5.4%) | MEDIUM |

**Highest Forecast Risk:** BU06 (Infrastructure & Cloud) at +11.2% over budget. Primary drivers:
1. Azure reserved capacity not originally in 2026 budget assumptions
2. Network Modernization (PRJ008) scope increased in Q4 2025
3. Cloud Platform Engineering team adding two headcount above plan

**Forecast Accuracy by Cycle (2025 Historical):**

| Forecast Cycle | Full-Year Forecast | Final Actuals | Accuracy |
|---|---|---|---|
| 3+9 (March) | $218.4M | $226.4M | 96.5% |
| 6+6 (June) | $221.8M | $226.4M | 97.9% |
| 9+3 (September) | $224.1M | $226.4M | 99.0% |

**Observation:** Forecast accuracy improves significantly as the year progresses — the 9+3 cycle is highly reliable. The 3+9 cycle shows a consistent pattern of underforecasting by 3.5–4.0%, suggesting that budget holders are conservative in their early-year outlook. CIO should adjust for this systematic bias when presenting Q1 forecasts to CFO.

---

## Recommended Actions for CIO Operating Review

| Priority | Action | Owner | Timeline |
|---|---|---|---|
| 1 | Launch Cloud Optimization Review — reserved capacity analysis for Analytics and Storage workloads | Mike Hanley | Within 30 days |
| 2 | Review and renew 23 High-risk external labor contracts | All BU heads | Within 30 days |
| 3 | Require project owners to reforecast PRJ001, PRJ003, PRJ007 for 2026 | Renee Johnson | Q1 2026 |
| 4 | Investigate EPMO vacancy rate — assess whether open positions are backfilled by contractors | Renee Johnson | Within 45 days |
| 5 | Set vendor concentration guardrails — no single vendor >30% of total vendor spend | Renee Johnson | Policy by Q2 2026 |
| 6 | Adjust 2026 Cost per FTE budget model to reflect actual 5.9% 2025 increase | Finance team | Before budget lock |
| 7 | Implement monthly tagging governance for Azure and AWS to improve chargeback accuracy | Mike Hanley | Q2 2026 |
| 8 | Use dashboard 9+3 forecast as primary CIO report-out number — retire Excel-based reporting | All | Immediately |
