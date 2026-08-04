# Call Centre Workforce Analytics Dashboard
Multi-year Power BI dashboard for call centre workforce analytics staffing gaps, SLA trends, AHT, and forecast accuracy
##Table of Contents

- [Project Overview](#project-overview)
- [The Business Story](#the-business-story)
- [Business Objective](#business-objective)
- [Business Questions](#business-questions)
- [Dataset Overview](#dataset-overview)
- [Data Preparation](#data-preparation)
- [Dashboard Features](#dashboard-features)
- [Key Performance Indicators](#key-performance-indicators-kpis)
- [Insights](#dashboard-insights)
- [Recommendations](#recommendations)
- [Skills Demonstrated](#skills-demonstrated)
- [Tools & Technologies](#tools--technologies)
- [Project Deliverables](#project-deliverables)
- [Repository Structure](#repository-structure)
- [Future Enhancements](#future-enhancements)
- [Conclusion](#conclusion)

## Project Overview

This project presents an interactive **Power BI Workforce Analytics Dashboard** built to evaluate operational performance across a multi-region contact center. It helps leadership determine whether service level shortfalls stem from **staffing capacity**, **operational efficiency**, or **demand fluctuations**, by tracking key workforce and customer service metrics from 2021–2026.

Workforce, service quality, forecasting, and operational KPIs are consolidated into a single executive view, enabling decision-makers to pinpoint where staffing adjustments or process improvements are needed.

## The Business Story

**Situation**
Leadership flagged that service level had been missing its 85% target and no one could say with confidence whether the cause was staffing, efficiency or demand.

**Complication**
Each explanation pointed to a different (and expensive) fix. Hiring more agents solves a staffing problem. Retraining and process redesign solves an efficiency problem. Neither helps if the real issue is demand volatility.

**Investigation**
I built a Power BI model spanning six years of workforce and service data (2021-2026), first fixing a date field that was 60% stored as text a defect that would have silently broken every trend calculation. I then layered in calculated measures (FTE Gap, Abandon Rate, SLA Status, Volume Variance) so the three competing hypotheses could be tested against the same data instead of debated in a meeting.

**Insight : the year-over-year pattern was the real finding.**

| Year | SLA% | FTE Gap | AHT (sec) | Utilization |
|---|---|---|---|---|
| 2021 | 82.51% | 52 | 545.19 | 79.90% |
| 2022 | 82.22% | **113** | 535.69 | 79.90% |
| 2023 | 82.67% | 28 | 547.14 | 79.90% |
| 2024 | 82.54% | 23 | 532.68 | 79.90% |
| 2025 | 82.28% | **117** | 537.52 | 79.90% |
| 2026 | 82.86% | 26 | 536.71 | 79.90% |

If staffing were the real driver, SLA should track the FTE gap worse gap, worse SLA. It doesn't. The FTE gap swings nearly 5x year to year (23 → 117) while SLA barely moves, staying locked in an 82–83% band every single year. AHT and utilization are just as flat across the same period. That combination — a metric that won't break out of its band no matter how much the inputs swing is the signature of a **structural ceiling**, not a staffing crisis: something in the process itself (routing logic, queue design, tooling) is capping performance, and staffing shortfalls are a secondary, noisier problem layered on top.

**Recommendation**

Treat this as two separate workstreams, not one. Fix the process ceiling first — it's suppressing SLA in every year regardless of headcount then address staffing gaps tactically in the specific queues and regions where they spike (Support queue, and regions like EMEA/APAC in high-gap years), rather than approving a blanket hiring request.

**Impact** 

This reframes the ask from "SLA is down, hire more people" to "SLA has a structural ceiling around 82–83% that six years of staffing changes haven't moved fix the process constraint, then right-size staffing against it." That's a materially different (and more defensible) recommendation to bring to leadership.

## Business Objective

> **Where are service levels being lost, why is this happening, and is the underlying cause related to staffing capacity or operational efficiency?**

The dashboard moves beyond descriptive reporting to provide data-backed recommendations for workforce planning and operational improvement.

## Business Questions

**1. Staffing & Capacity**
- Where does actual agent count fall short of required FTE?
- Which region has the largest staffing gap?
- Does shrinkage impact service level?
- Is occupancy indicating over or under-utilization?

**2. Service Level & Customer Experience**
- Which queues and channels have the weakest SLA performance?
- How does wait time influence abandoned volume?
- Which business unit records the lowest service level?

**3. Efficiency & Productivity**
- Which regions have the highest Average Handle Time (AHT)?
- Does AHT vary across communication channels?
- Does higher utilization improve service levels?

**4. Volume & Forecasting**
- How accurately does planned volume match offered volume?
- When do peak demand periods occur?
- Are there seasonal trends affecting workload and SLA?

**5. Root Cause Analysis**
- Is poor SLA driven primarily by staffing shortages, process inefficiencies, or demand surges?
- Which staffing investments would provide the greatest operational improvement?

## Dataset Overview

Operational data from a multi-region contact center spanning **2021–2026**.

| Category | Fields |
|---|---|
| **Time** | Date, Weekday, Week Number, Month, Year, Hour |
| **Organizational** | Country, Region, Site, Business Unit |
| **Queue** | Queue Name, Channel, Customer Segment, Queue Category, Support Tier |
| **Operational** | Planned Volume, Offered Volume, Handled Volume, Abandoned Volume, Backlog Volume |
| **Workforce** | Required FTE, Agent Count, Active Agents, Utilization, Occupancy, Shrinkage |
| **Performance** | Service Level %, Average Handle Time, Average Wait Time |

## Data Preparation

**Data quality issue:** The `Date` column contained mixed data types roughly **60% stored as text** and **40% as date values**. This was identified and corrected before any time-based analysis.

**Calculated fields added:**
- FTE Gap
- Volume Variance
- Abandon Rate
- SLA Status

## Dashboard Features

The report is organized into three operational sections, with a **Year slicer (2021–2026)** for period-over-period analysis.

| Section | Focus |
|---|---|
| **Demand Overview** | Offered Volume, Handled Volume, Volume Trend, Abandoned Volume, Volume by Channel |
| **Capacity & Staffing** | Active Agent Count, Required FTE, Staffing Gap by Queue, Staffing Gap by Region |
| **SLA Performance** | SLA Trend, Shrinkage Trend, Occupancy, SLA by Business Unit, Forecast Accuracy |

## Key Performance Indicators (KPIs)

| KPI | Dashboard Value |
|---|---:|
| SLA | 82.51% |
| Offered Volume | 549,869 |
| Handled Volume | 520,253 |
| Average Wait Time | 40.65 |
| Backlog Rate | 7.55% |
| FTE Gap | 52 |
| Utilization | 79.90% |
| Abandonment Rate | 7.55% |
| Average Handle Time | 545.19 sec |
| SLA Breach Count | 2K |

## Dashboard Insights

- SLA never exceeds ~83% in **any** of the six years tracked (2021–2026), despite the FTE gap swinging from 23 to 117 — indicating a structural constraint on performance rather than a single year's staffing shortfall.
- AHT (532–547 sec) and Utilization (flat at 79.90%) are stable across all six years, reinforcing that efficiency, not raw capacity, is the likely ceiling.
- The 2021 snapshot: overall SLA of **82.51%**, an FTE gap of **52**, and **Support Queue** carrying the largest staffing gap among tracked queues.
- Abandonment rate (7.55% in 2021) tracks in lockstep with Backlog Rate every year, suggesting the two are directly linked in this dataset.
- Forecast variance stays in a stable, narrow band year over year forecasting is not the source of the SLA problem.

## Recommendations

- Treat SLA improvement as two separate workstreams: a **process/efficiency fix** for the recurring 82–83% ceiling, and **targeted staffing** for queue- and region-specific gaps not a single blanket hiring initiative.
- Prioritize additional headcount in the Support queue and in regions with the largest recurring staffing gaps.
- Reduce customer abandonment by lowering wait times and improving routing efficiency.
- Continue the existing forecasting strategy forecast variance is stable and is not contributing to the SLA shortfall.

## Skills Demonstrated

- **Data Modeling** structured relationships across time, organizational, queue, and workforce dimensions
- **Power Query** data cleaning, including resolving mixed-type date fields
- **DAX** calculated fields (FTE Gap, Volume Variance, Abandon Rate, SLA Status) and KPI measures
- **KPI Cards & Executive Scorecards** at-a-glance operational summary
- **Time Intelligence** multi-year trend analysis (2021–2026)
- **Interactive Slicers** year-based filtering across all report pages
- **Root Cause / Diagnostic Analysis** connecting staffing gaps and AHT to SLA outcomes

## Tools & Technologies

- Power BI Desktop
- Power Query
- DAX
- Microsoft Excel

## Project Deliverables

- Interactive Power BI Dashboard
- Workforce KPI Monitoring
- Multi-Year Performance Analysis (2021–2026)
- Staffing Gap Analysis
- SLA Performance Tracking
- Forecast Monitoring
- Executive Recommendations

## Future Enhancements

- Deploy to Power BI Service for scheduled refresh and web access
- Implement Row-Level Security (RLS) for region-specific access control
- Integrate real-time or near real-time data feeds
- Add drill-through pages for queue- and agent-level detail

## Conclusion

This project demonstrates how workforce analytics can be used to monitor staffing, operational efficiency, and service performance within a contact centre environment. By combining workforce KPIs, customer experience metrics, and forecasting indicators into an interactive dashboard, the solution enables stakeholders to identify operational gaps, evaluate service performance over time, and support data-driven workforce planning decisions.

