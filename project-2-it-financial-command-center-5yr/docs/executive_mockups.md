# Executive Dashboard Mockups
## Nexora IT Financial Command Center

All pages are 1280 x 720px (16:9). Measurements shown as approximate pixel positions.
Grid: 1280px wide, 720px tall. Header bar: 60px. Slicer panel: 200px left column.

Legend:
```
[KPI]   = KPI Card visual
[BAR]   = Bar or Column chart
[LINE]  = Line chart
[DONUT] = Donut chart
[TABLE] = Table or Matrix
[TEXT]  = Text box / commentary
[MAP]   = Treemap
[GAUGE] = Gauge visual
[AREA]  = Area chart
```

---

## Page 1 — CIO Executive Summary

```
┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│ NEXORA IT FINANCIAL COMMAND CENTER                              CIO Executive Summary        │
│ ■ Nexora Logo                                          Reporting Period: FY2025 | As of Jun │
├────────────────┬────────────────────────────────────────────────────────────────────────────┤
│                │ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────┐│
│  SLICERS       │ │  [KPI]   │ │  [KPI]   │ │  [KPI]   │ │  [KPI]   │ │  [KPI]   │ │[KPI] ││
│                │ │ YTD      │ │ YTD      │ │ YTD      │ │ Variance │ │ Year-End │ │ Risk ││
│  Year:   [▼]  │ │ Actuals  │ │ Budget   │ │ Variance │ │    %     │ │ Proj.    │ │ Flag ││
│                │ │$112.4M   │ │$109.8M   │ │+$2.6M    │ │ +2.4%    │ │$224.8M   │ │MED   ││
│  Month:  [▼]  │ └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────┘│
│                ├────────────────────────────────────┬───────────────────────────────────────┤
│  Bus Unit:[▼] │                                    │                                       │
│                │         [LINE/COLUMN]              │           [BAR]                       │
│  Forecast:[▼] │   Monthly Actuals vs Budget         │    Spend by Business Unit             │
│                │                                    │                                       │
│                │   $25M ┤                           │  Corp Technology ████████████ $38.2M  │
│                │   $20M ┤   ╭─╮   ╭──╮              │  Infra & Cloud   ███████     $26.1M  │
│                │   $15M ┤ ╭─╯ ╰──╯  ╰─╮            │  Ent Data Svcs   ██████      $21.4M  │
│                │   $10M ┤ ╰──────────╯   ──line     │  Ent Engineering ████        $14.7M  │
│                │    $5M ┤               (Budget)    │  Info Security   ███         $9.2M   │
│                │        Jan Feb Mar Apr May Jun      │  EPMO            ██          $6.2M   │
│                │        ■ Actuals  ─ Budget          │                                       │
│                ├────────────────────────────────────┤    [DONUT]                            │
│                │                                    │  Spend by GL Category                 │
│                │          [TABLE]                   │                                       │
│                │  Top 5 Variance Drivers            │     ╭──────╮                          │
│                │  ─────────────────────────────     │   ╭╯ ██████╰╮                        │
│                │  Cloud Platform Eng  +$1.2M  8.2%  │  ╱  Internal  ╲                      │
│                │  Data Engineering    +$0.9M  6.1%  │  │   Labor 38% │                     │
│                │  Corp Tech - Apps    +$0.4M  3.8%  │  ╲  Cloud  22%╱                      │
│                │  Ext Labor (Data)    +$0.3M  4.1%  │   ╰╮        ╭╯                        │
│                │  Analytics & Rpt     +$0.2M  2.7%  │    ╰──────╯                          │
│                ├────────────────────────────────────┴───────────────────────────────────────┤
│                │  [TEXT] Executive Commentary                                                │
│                │  Cloud Platform Engineering tracking +8.2% over YTD budget, driven by      │
│                │  Azure Storage growth in PRJ007. External labor in Data Engineering         │
│                │  elevated — 3 high-risk contract expirations in Q3 2025. Recommend          │
│                │  immediate review of VEN006 (Capgemini) renewal. Overall forecast           │
│                │  variance at Medium risk — year-end projection $224.8M vs $220.4M budget.  │
└────────────────┴────────────────────────────────────────────────────────────────────────────┘
```

**Design Notes:**
- Header bar: Dark navy `#0D1B2A`, white text
- KPI cards: Dark card background `#1C2B3A`, colored metric text
- YTD Variance card: Red text if positive (over budget), green if negative
- Risk Flag card: Medium = amber background `#F0AD4E`
- Bottom commentary box: Same dark background as header, smaller font
- Left slicer panel: Slightly lighter `#1A2A3C`

---

## Page 2 — Budget vs Actuals

```
┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│ NEXORA IT FINANCIAL COMMAND CENTER                                  Budget vs Actuals        │
├────────────────┬────────────────────────────────────────────────────────────────────────────┤
│                │ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────────────────┐│
│  SLICERS       │ │  [KPI]   │ │  [KPI]   │ │  [KPI]   │ │  [KPI]   │ │      [KPI]         ││
│  Year:   [▼]  │ │ YTD Act  │ │ YTD Bud  │ │ YTD Var  │ │ Var %    │ │  Budget Status     ││
│  Month:  [▼]  │ │$112.4M   │ │$109.8M   │ │ +$2.6M   │ │ +2.4%    │ │  ▲ Over Budget     ││
│  Bus Unit:[▼] │ └──────────┘ └──────────┘ └──────────┘ └──────────┘ └────────────────────┘│
│  Cost Ctr:[▼] ├────────────────────────────────────────────────────────────────────────────┤
│  GL Cat: [▼]  │                                                                             │
│                │                    [LINE/COLUMN]                                            │
│                │              Monthly Actuals vs Budget — FY2025                            │
│                │                                                                             │
│                │  $22M ┤                   ╭───╮                                            │
│                │  $20M ┤ ╭─╮   ╭─╮   ╭───╯   ╰──╮   ╭─╮                                  │
│                │  $18M ┤ │ │ ╭─╯ ╰───╯           ╰───╯ ╰──                                │
│                │  $16M ┤ ╰─╯─────────────────────────── Budget Line                       │
│                │       Jan  Feb  Mar  Apr  May  Jun  Jul  Aug  Sep  Oct  Nov  Dec           │
│                │       ■ Actuals (columns)    ─── Budget (line)   [Zoom slider]            │
│                │                                                                             │
│                ├─────────────────────────────────┬──────────────────────────────────────────┤
│                │         [MATRIX]                │          [BAR]                           │
│                │  Variance by Cost Center         │  Variance by GL Category                │
│                │                                  │                                         │
│                │         Jan   Feb   Mar  Total   │  ◄──────── 0 ──────────►               │
│                │  CC104018  +12  +18  +22  +52K   │  Cloud         ████████► +$1.4M         │
│                │  CC104023  +8   +11  +9   +28K   │  Ext Labor     █████►   +$0.8M          │
│                │  CC104026  +3   +5   +4   +12K   │  Pro Svcs      ██►      +$0.3M          │
│                │  CC104001  -4   -2   -3   -9K    │  Hardware      ◄        -$0.1M          │
│                │  CC110101  -6   -8   -5   -19K   │  Training      ◄        -$0.2M          │
│                │  (Red=over, Green=under)          │  (Red=over budget, Green=under)        │
└────────────────┴─────────────────────────────────┴──────────────────────────────────────────┘
```

**Design Notes:**
- Variance matrix uses conditional background color: red gradient for positive, green gradient for negative
- Zero reference line clearly visible in the GL Category bar chart
- Zoom slider below the monthly trend enables narrower month-range views
- All visuals cross-filter when a cost center row is clicked in the matrix

---

## Page 3 — Forecast & Projection

```
┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│ NEXORA IT FINANCIAL COMMAND CENTER                            Forecast & Projection          │
├────────────────┬────────────────────────────────────────────────────────────────────────────┤
│                │ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────────────┐│
│  SLICERS       │ │ [KPI]  │ │ [KPI]  │ │ [KPI]  │ │ [KPI]  │ │ [KPI]  │ │     [KPI]      ││
│  Year:   [▼]  │ │Full-Yr │ │Full-Yr │ │Forecast│ │Forecast│ │Fcst    │ │  Remaining     ││
│  Bus Unit:[▼] │ │Budget  │ │Forecast│ │Variance│ │Var %   │ │Accuracy│ │  Forecast      ││
│  Forecast:[▼] │ │$220.4M │ │$224.8M │ │+$4.4M  │ │ +2.0%  │ │ 96.1%  │ │  $112.4M       ││
│  Cost Ctr:[▼] │ └────────┘ └────────┘ └────────┘ └────────┘ └────────┘ └────────────────┘│
│                ├──────────────────────────────────────────┬─────────────────────────────────┤
│                │            [AREA]                        │          [COLUMN]               │
│                │   Actuals + Forecast Full-Year View       │   Forecast Cycle Comparison     │
│                │                                          │                                 │
│                │  $25M ┤╭─────────╮ Actual                │  $226M ┤   ████  ████  ████    │
│                │  $20M ┤│─────────│░░░░░░░░░ Forecast     │  $224M ┤   ████  ████  ████    │
│                │  $15M ┤│░░░░░░░░░│░░░░░░░░░              │  $222M ┤   ████  ████  ████    │
│                │  $10M ┤│░░░░░░░░░│░░░░░░░░░              │  $220M ┤ ──────────────────── Budget│
│                │        Jan──────Jun──────Dec              │         3+9    6+6    9+3      │
│                │   ─── Budget  ■ Actual  ░ Forecast        │   ▲Budget line shows at $220.4M│
│                ├──────────────────────────────────────────┴─────────────────────────────────┤
│                │                   [TABLE]                                    [GAUGE]        │
│                │   Risk & Opportunity Flags by Cost Center                                  │
│                │   ─────────────────────────────────────────           Year-End             │
│                │   Cost Center     Forecast   Budget  Var%  Risk       Projection           │
│                │   Cloud Plat Eng  $28.4M  $26.1M  +8.8% 🔴HIGH                            │
│                │   Data Eng        $23.1M  $21.8M  +6.0% 🔴HIGH      ╭─────╮               │
│                │   Corp Tech Apps  $19.4M  $18.9M  +2.6% 🟡MED      ╱ $224M╲              │
│                │   Corp Tech EU    $15.2M  $15.8M  -3.8% 🟢LOW      │ Proj  │              │
│                │   Cybersecurity   $9.8M   $10.1M  -3.0% 🟢LOW      ╲ vs   ╱              │
│                │   EPMO            $6.5M   $6.3M   +3.2% 🟡MED       ╰─────╯              │
│                │                                                   Budget: $220.4M          │
└────────────────┴────────────────────────────────────────────────────────────────────────────┘
```

---

## Page 4 — External Labor

```
┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│ NEXORA IT FINANCIAL COMMAND CENTER                                   External Labor          │
├────────────────┬────────────────────────────────────────────────────────────────────────────┤
│                │ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────────┐  │
│  SLICERS       │ │  [KPI]   │ │  [KPI]   │ │  [KPI]   │ │  [KPI]   │ │     [KPI]        │  │
│  Year:   [▼]  │ │Ext Labor │ │Contractor│ │ Avg Rate │ │High Risk │ │   YoY Growth     │  │
│  Bus Unit:[▼] │ │ Spend    │ │  Count   │ │          │ │Contracts │ │                  │  │
│  Risk:   [▼]  │ │ $38.4M   │ │    142   │ │  $118/hr │ │    23    │ │    +14.2%        │  │
│  Vendor: [▼]  │ └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────────────┘  │
│  Project:[▼]  ├──────────────────────────────────┬─────────────────────────────────────────┤
│                │           [LINE]                 │          [BAR]                          │
│                │   Ext Labor Spend Trend          │   Spend by Vendor                       │
│                │   (Spend + Headcount overlay)    │                                         │
│                │                                  │  Capgemini    ████████████ $14.2M       │
│                │  $4M ┤     ╭───╮   ╭───╮  150   │  Accenture    ████████     $9.8M        │
│                │  $3M ┤ ─╮╭─╯   ╰──╯   ╰ ─ 120   │  Deloitte     █████        $6.1M        │
│                │  $2M ┤  ││               ─  90   │  Infosys      ████         $5.4M        │
│                │       Jan Mar May Jul Sep Nov      │  AHEAD LLC    ██           $2.9M       │
│                │   ─ Spend  ─ ─ Count (right axis) │                                        │
│                ├──────────────────────────────────┴─────────────────────────────────────────┤
│                │                     [TABLE] Contract End Date Risk                          │
│                │  ────────────────────────────────────────────────────────────────────────  │
│                │  Resource          Role            Vendor     Cost Ctr  Project    End Date  Risk  │
│                │  Contractor 145    Cloud Engineer  Accenture  104018    PRJ010     Jul-25   🔴HIGH │
│                │  Contractor 213    QA Analyst      Deloitte   104002    PRJ008     Aug-25   🔴HIGH │
│                │  Contractor 562    Cloud Engineer  Capgemini  104018    PRJ008     Sep-25   🔴HIGH │
│                │  Contractor 385    Architect       Accenture  104002    PRJ008     Oct-25   🟡MED  │
│                │  Contractor 224    Architect       Accenture  104019    PRJ005     Nov-25   🟡MED  │
│                │  Contractor 301    Developer       Capgemini  104017    PRJ009     Dec-25   🟢LOW  │
│                │  [Sorted by contract_end_date ascending — showing soonest expirations first] │
└────────────────┴────────────────────────────────────────────────────────────────────────────┘
```

---

## Page 5 — Vendor Spend

```
┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│ NEXORA IT FINANCIAL COMMAND CENTER                                    Vendor Spend           │
├────────────────┬────────────────────────────────────────────────────────────────────────────┤
│                │ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌───────────────────────────────┐  │
│  SLICERS       │ │  [KPI]   │ │  [KPI]   │ │  [KPI]   │ │           [KPI]               │  │
│  Year:   [▼]  │ │  Total   │ │ Active   │ │  YoY     │ │   Top Vendor Concentration     │  │
│  Bus Unit:[▼] │ │  Vendor  │ │ Vendors  │ │  Growth  │ │   (Azure % of total spend)     │  │
│  Category:[▼] │ │  Spend   │ │          │ │          │ │                                │  │
│  Tier:   [▼]  │ │  $72.4M  │ │    18    │ │  +11.3%  │ │          28.4%                 │  │
│                │ └──────────┘ └──────────┘ └──────────┘ └───────────────────────────────┘  │
│                ├────────────────────────────────────────────────────────────────────────────┤
│                │          [BAR]                    │        [BAR — dual series]             │
│                │   Top 10 Vendors by Spend         │   Vendor YoY Comparison                │
│                │                                   │                                        │
│                │  MS Azure   ████████████  $20.5M  │  MS Azure  ████████████ $20.5M CY      │
│                │  AWS        ████████      $14.8M  │            ██████████   $17.2M PY      │
│                │  Capgemini  ███████       $12.1M  │  AWS       ████████     $14.8M CY      │
│                │  ServiceNow █████         $8.4M   │            ███████      $12.9M PY      │
│                │  Snowflake  ████          $6.2M   │  Capgemini ███████      $12.1M CY      │
│                │  Databricks ████          $5.8M   │            █████        $9.8M  PY      │
│                │  Oracle     ████          $5.1M   │                                        │
│                │  Workday    ███           $3.9M   │  ■ Current Year  □ Prior Year          │
│                │  Accenture  ███           $3.4M   │                                        │
│                │  Palo Alto  ██            $2.8M   │                                        │
│                ├─────────────────────────────────────────────────────────────────────────── │
│                │      [MAP] Vendor Concentration (Treemap)    │ [DONUT] By Category          │
│                │                                              │                              │
│                │  ┌──────────────────┬──────────┬──────────┐ │     ╭────╮                   │
│                │  │                  │          │  Snflk   │ │  ╭─╯Cloud╰─╮                 │
│                │  │  MS Azure        │  AWS     │  Datab   │ │ ╱  28%  SW╲                 │
│                │  │   $20.5M         │  $14.8M  │          │ │╱   38%     ╲                │
│                │  │                  ├──────────┤          │ │╲  EL 17%   ╱                │
│                │  ├────────┬─────────┤ ServiceN │          │ │ ╲  PS 10% ╱                 │
│                │  │Capgem  │ Oracle  │          │          │ │  ╰────────╯                  │
│                │  │$12.1M  │ $5.1M  │          │  Others  │ │                               │
│                │  └────────┴─────────┴──────────┴──────────┘ │                              │
└────────────────┴──────────────────────────────────────────────┴──────────────────────────────┘
```

---

## Page 6 — Cloud Spend

```
┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│ NEXORA IT FINANCIAL COMMAND CENTER                                    Cloud Spend            │
├────────────────┬────────────────────────────────────────────────────────────────────────────┤
│                │ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────────────────────────┐│
│  SLICERS       │ │ [KPI]  │ │ [KPI]  │ │ [KPI]  │ │ [KPI]  │ │         [KPI]              ││
│  Year:   [▼]  │ │ Total  │ │  YTD   │ │  YoY   │ │ Azure  │ │    AWS Spend               ││
│  Bus Unit:[▼] │ │ Cloud  │ │ Cloud  │ │ Growth │ │ Spend  │ │                            ││
│  Provider:[▼] │ │$35.3M  │ │$18.2M  │ │+18.4%  │ │$20.5M  │ │   $14.8M                   ││
│  Service: [▼] │ └────────┘ └────────┘ └────────┘ └────────┘ └────────────────────────────┘│
│  Project:[▼]  ├──────────────────────────────────────────────────────────────────────────── │
│                │                       [LINE]                                               │
│                │              Azure vs AWS Monthly Trend — 2022 to 2026                     │
│                │                                                                             │
│                │  $3.0M ┤                                           ╭───────────            │
│                │  $2.0M ┤ ──────────────────────────────────────────╯    Azure              │
│                │  $1.5M ┤ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─  AWS               │
│                │  $1.0M ┤                                                                   │
│                │  $0.5M ┤                                                                   │
│                │         2022    2023    2024    2025    2026                                │
│                │   ── Azure (blue)   ─ ─ AWS (orange)                                      │
│                ├──────────────────────────────┬─────────────────────────────────────────────┤
│                │       [STACKED BAR]          │            [MATRIX]                         │
│                │   Cloud by Service Category   │   Cloud Spend by Cost Center (Azure | AWS)  │
│                │   (stacked by year)           │                                             │
│                │                               │           Azure    AWS    Total             │
│                │  2026 ████▓▒░░░░              │  CC104018 $4.1M  $1.8M  $5.9M  ████████  │
│                │  2025 ████▓▒░░                │  CC104027 $3.2M  $1.1M  $4.3M  ██████    │
│                │  2024 ████▓▒░                 │  CC104023 $2.8M  $1.9M  $4.7M  ███████   │
│                │  2023 ████▓▒                  │  CC104022 $2.1M  $0.8M  $2.9M  ████      │
│                │  2022 ████▓                   │  CC104003 $1.8M  $1.3M  $3.1M  █████     │
│                │  ■Comp ▓Net ▒Stor ░Anlyt      │  (Color intensity = spend amount)          │
└────────────────┴──────────────────────────────┴─────────────────────────────────────────────┘
```

---

## Page 7 — Headcount

```
┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│ NEXORA IT FINANCIAL COMMAND CENTER                                      Headcount            │
├────────────────┬────────────────────────────────────────────────────────────────────────────┤
│                │ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌─────────────┐   │
│  SLICERS       │ │ [KPI]  │ │ [KPI]  │ │ [KPI]  │ │ [KPI]  │ │ [KPI]  │ │   [KPI]     │   │
│  Year:   [▼]  │ │Approved│ │ Filled │ │  Open  │ │Vacancy │ │ Labor  │ │ Cost/FTE    │   │
│  Bus Unit:[▼] │ │  Posns │ │        │ │ Roles  │ │  Rate  │ │  Cost  │ │             │   │
│  Cost Ctr:[▼] │ │  185   │ │  166   │ │   19   │ │ 10.3%  │ │$14.8M  │ │  $89,200    │   │
│                │ └────────┘ └────────┘ └────────┘ └────────┘ └────────┘ └─────────────┘   │
│                ├──────────────────────────────────────────┬─────────────────────────────────┤
│                │             [LINE/COLUMN]                │          [BAR]                  │
│                │    Headcount Trend + Vacancy Rate        │   Vacancy Rate by Business Unit  │
│                │                                          │                                 │
│                │  200 ┤ ██ ██ ██ ██ ██ ██  Approved      │  ◄──0──5%──10%──15%──20%──►    │
│                │  180 ┤ ■■ ■■ ■■ ■■ ■■ ■■  Filled        │  EPMO              ████  18.0%  │
│                │  160 ┤                                   │  Corp Technology   ██   10.4%   │
│                │  15% ┤           ╭─╮  Vacancy %          │  Infra & Cloud     ██   9.8%    │
│                │  10% ┤ ─────────╯ ╰────────── (right)   │  Info Security     █    7.2%    │
│                │       Jan Mar May Jul Sep Nov Dec         │  Ent Data Svcs     █    6.1%    │
│                │   ■ Approved □ Filled ─ Vacancy %        │  Ent Engineering   █    5.4%    │
│                ├──────────────────────────────────────────┴─────────────────────────────────┤
│                │                   [TABLE] Headcount by Cost Center                          │
│                │  ──────────────────────────────────────────────────────────────────────── │
│                │  Cost Center              BU    Approved  Filled  Open  Vacancy%  Labor Cost│
│                │  Corp Tech - End User     BU03   14        14      0     0.0%     $190K     │
│                │  Corp Tech - Collab       BU03   10         9      1    10.0%     $ 82K     │
│                │  Data Governance          BU02   22        19      3    13.6%     $217K     │
│                │  Cloud Platform Eng       BU06    7         6      1    14.3%     $ 53K     │
│                │  Enterprise Proj Delivery BU04   10         8      2    20.0%     $107K     │
│                │  Transformation Portfolio BU04    8         6      2    25.0%     $ 84K     │
│                │                    [AREA] Labor Cost Trend (bottom right)                   │
│                │                  Jan─────────────────────────────────Dec                   │
│                │   $14M  ┤ ╭────────────────────────────────────────────────                │
│                │   $12M  ┤╱ (shaded area — monthly labor cost trend line)                   │
└────────────────┴────────────────────────────────────────────────────────────────────────────┘
```

---

## Page 8 — Project Spend

```
┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│ NEXORA IT FINANCIAL COMMAND CENTER                                   Project Spend           │
├────────────────┬────────────────────────────────────────────────────────────────────────────┤
│                │ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────────┐  │
│  SLICERS       │ │  [KPI]   │ │  [KPI]   │ │  [KPI]   │ │  [KPI]   │ │     [KPI]        │  │
│  Year:   [▼]  │ │  Total   │ │  Capex   │ │  Opex    │ │  Capex%  │ │ Active Projects  │  │
│  Bus Unit:[▼] │ │ Project  │ │  Spend   │ │  Spend   │ │ of Total │ │                  │  │
│  Status: [▼]  │ │  Spend   │ │          │ │          │ │          │ │        8         │  │
│  Category:[▼] │ │  $48.2M  │ │  $29.4M  │ │  $18.8M  │ │  61.0%   │ │                  │  │
│  Capex/Op:[▼] │ └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────────────┘  │
│                ├──────────────────────────────────────┬───────────────────────────────────── │
│                │          [COLUMN — 3 series]         │         [DONUT]                     │
│                │   Project Budget / Actuals / Forecast │     Capex vs Opex Split             │
│                │                                       │                                     │
│                │  $12M ┤                               │        ╭──────╮                    │
│                │  $10M ┤ ██ ██  ██ ██ ██ ██ ██ ██ ██  │     ╭──╯ Capex ╰──╮               │
│                │   $8M ┤ ██ ██  ██ ██ ██ ██ ██ ██ ██  │    ╱    61%        ╲              │
│                │   $6M ┤ ██ ██  ██ ██ ██ ██ ██ ██ ██  │   │  Opex 39%       │             │
│                │   $4M ┤ ░░ ░░  ░░ ░░ ░░ ░░ ░░ ░░ ░░  │    ╲               ╱             │
│                │       ERP Cld Data Cyb SvN DWP Clm Net Vnd  │  ╰──────────────╯           │
│                │   ■Budget ■Actuals ░Forecast               │                              │
│                ├──────────────────────────────────────┴───────────────────────────────────── │
│                │                  [TABLE] Project Detail                                     │
│                │  ──────────────────────────────────────────────────────────────────────   │
│                │  Project              Category     Status   Owner        Spend    Budget  Var%│
│                │  ERP Modernization    Transform.   Active   Alan Smith   $12.8M  $11.4M  +12% │
│                │  Cloud Opt Program    Cloud        Active   Mike Hanley  $ 9.4M  $ 9.1M  +3%  │
│                │  Data Lakehouse       Data         Active   Vimala Rao   $ 8.2M  $ 8.0M  +3%  │
│                │  Cyber Resilience     Security     Active   Maya Chen    $ 6.1M  $ 6.4M  -5%  │
│                │  ServiceNow Expansion Corp Tech    Active   Alan Smith   $ 4.8M  $ 4.9M  -2%  │
│                │  AI Finance Reporting Analytics    Planned  Renee Johnson$ 2.1M  $ 3.2M  -34% │
└────────────────┴────────────────────────────────────────────────────────────────────────────┘
```

---

## Page 9 — Drill-through Detail

```
┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│ ← Back    NEXORA IT FINANCIAL COMMAND CENTER              Transaction Detail                │
│           Drill-through from: Budget vs Actuals | Filter: Cloud Platform Eng (CC104018)    │
├─────────────────────────────────────────────────────────────────────────────────────────────┤
│ ┌──────────────────────┐ ┌──────────────────────┐ ┌──────────────────────┐ ┌──────────────┐│
│ │       [KPI]          │ │       [KPI]          │ │       [KPI]          │ │    [KPI]     ││
│ │ Transaction Count    │ │ Total Amount         │ │ Avg per Transaction  │ │ Date Range   ││
│ │        847           │ │      $5.9M           │ │       $6,972         │ │ Jan–Jun 2025 ││
│ └──────────────────────┘ └──────────────────────┘ └──────────────────────┘ └──────────────┘│
├─────────────────────────────────────────────────────────────────────────────────────────────┤
│                     [TABLE] Transaction Detail — Cloud Platform Engineering (CC104018)      │
│  ─────────────────────────────────────────────────────────────────────────────────────────  │
│  Date        Month   Year  Business Unit      Cost Center       GL Category  GL Desc         │
│  2025-01-01  Jan     2025  Infra & Cloud      Cloud Plat Eng    Cloud        Cloud hosting   │
│                                                                                               │
│  Vendor          Project               Scenario  Amount      Notes                           │
│  Microsoft Azure  Cloud Opt Program    Actual    $104,029.68  Cloud consumption allocation   │
│  ─────────────────────────────────────────────────────────────────────────────────────────  │
│  2025-01-01  Jan     2025  Infra & Cloud      Cloud Plat Eng    Cloud        Cloud hosting   │
│  AWS              Cloud Opt Program    Actual    $ 40,936.84  Cloud consumption allocation   │
│  ─────────────────────────────────────────────────────────────────────────────────────────  │
│  2025-02-01  Feb     2025  Infra & Cloud      Cloud Plat Eng    Cloud        Cloud hosting   │
│  Microsoft Azure  Cloud Opt Program    Actual    $108,431.12  Cloud consumption allocation   │
│  ─────────────────────────────────────────────────────────────────────────────────────────  │
│  [Table continues — scrollable — sorted by date descending]                                  │
│  Showing 847 transactions | Total: $5,918,204.32 | Export ▼                                  │
│  ─────────────────────────────────────────────────────────────────────────────────────────  │
│                                                                                               │
│  [Full-width table spanning ~95% of canvas width — columns resize to content]                │
└─────────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Navigation Design

Each page includes a navigation bar in the top-right corner with buttons for every page:

```
[Exec Summary] [Budget/Act] [Forecast] [Ext Labor] [Vendors] [Cloud] [Headcount] [Projects]
```

Implementation:
- Insert > Buttons > Blank
- Add page name as button text
- Set Action Type: Page Navigation
- Set Destination: target page
- Style: Filled button, active page highlighted in `#1E88E5`, inactive in `#2D4A6A`

---

## Theme Color Palette

| Element | Color | Hex |
|---|---|---|
| Page background | Dark navy | `#0D1B2A` |
| Card background | Dark blue-grey | `#1C2B3A` |
| Slicer panel | Slightly lighter navy | `#1A2A3C` |
| Primary data color | Corporate blue | `#1E88E5` |
| Secondary data color | Light blue | `#90CAF9` |
| Positive variance (over budget) | Alert red | `#D9534F` |
| Negative variance (under budget) | Success green | `#5CB85C` |
| Warning / medium risk | Amber | `#F0AD4E` |
| Azure brand color | Azure blue | `#00B0F0` |
| AWS brand color | AWS orange | `#FF9900` |
| White text | White | `#FFFFFF` |
| Muted label text | Light grey | `#B0BEC5` |
| Border / divider | Dark line | `#2D4A6A` |

**Font:** Segoe UI throughout
- Page title: 18pt Bold
- Section title: 14pt SemiBold
- Body / data labels: 11pt Regular
- KPI card value: 24–28pt Bold
- KPI card label: 10pt Regular, `#B0BEC5`

**KPI Card Style:**
- No border
- Dark background `#1C2B3A`
- Value: 26pt, white or conditional color
- Label: 10pt, muted grey
- Trend indicator: small up/down arrow with percentage delta
