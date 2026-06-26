# IT Incident Trend Analysis

## Overview
An end-to-end data analytics project analyzing IT incident management patterns using a real-world ITSM dataset. Built to demonstrate data cleaning, exploratory analysis, visualization, and business intelligence skills.

**Tools Used:** Python, pandas, matplotlib, seaborn, Jupyter Notebook, Power BI  
**Dataset:** UCI Incident Management Process Enriched Event Log  
**Domain:** IT Operations / Infrastructure

---

## Dataset
- **Source:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/498/incident+management+process+enriched+event+log)
- **Raw size:** 141,712 rows × 36 columns
- **Note:** Raw dataset not hosted here due to file size (435MB). Download directly from the UCI link above.

---

## Methodology

### 1. Data Cleaning
- Filtered dataset to Resolved and Closed incidents only
- Identified and resolved duplicate rows — each incident was recorded multiple times as its state changed (New → Active → Resolved → Closed)
- Deduplicated to final state per incident: 141,712 rows → 24,918 unique incidents
- Converted date columns from text to datetime
- Calculated resolution time in hours (resolved_at - opened_at)
- Handled missing values (3,119 incidents had no resolved_at timestamp)

### 2. Analysis & Visualizations (Python)
- Incident count by category
- Priority distribution
- Median resolution time by priority
- SLA compliance rate overall and by priority
- Incident volume trend over time

### 3. Dashboard (Power BI)
- Interactive dashboard with priority slicer
- Cross-validated all findings against Python analysis
- Created DAX measure for median resolution time calculation

---

## Key Findings

### Finding 1 — Category Concentration
Incident volume is heavily concentrated in a small number of categories. Category 42, 26, and 53 account for a disproportionate share of all tickets, suggesting recurring systemic issues in specific areas.

### Finding 2 — Priority Distribution
94% of all incidents are Priority 3 (Moderate). Only ~3% are P1/P2 combined, indicating a relatively stable environment with infrequent critical incidents.

### Finding 3 — Resolution Time Anomaly (Key Finding)
**P1-Critical incidents take the longest to resolve (~80 hrs median), while P4-Low resolves fastest (~6 hrs).** This is the opposite of expected behavior.

|   Priority   | Median Resolution Time |
|--------------|------------------------|
| 1 - Critical | 80 hours               |
| 2 - High     | 38 hours               |
| 3 - Moderate | 22 hours               |
| 4 - Low      |  6 hours               |

### Finding 4 — SLA Compliance Crisis (Key Finding)
When measured at final ticket closure (the true end state), SLA compliance for high-priority incidents is critically low:

|   Priority   | SLA Compliance |
|--------------|----------------|
| 2 - High     | ~0.5%          |
| 1 - Critical | ~1.9%          |
| 3 - Moderate | ~64.5%         |
| 4 - Low      | ~84.1%         |

This reveals a significant misalignment — P1-Critical and P2-High are the most business-critical incidents (major outages, severe failures), yet they have the lowest SLA compliance rates. Only 1.9% of P1-Critical and 0.5% of P2-High incidents meet their SLA targets at closure, meaning 98%+ of the most critical incidents are breaching SLA. Meanwhile, routine P3/P4 tickets are meeting SLA at much higher rates, suggesting resources may be prioritizing easy tickets over critical ones.

### Finding 5 — Volume Trend
Reliable data covers Feb–May 2016, showing a mild declining trend from ~9,000 incidents in March to ~7,500 in May (~17% reduction).

---

## Data Quality Notes
- Categories and assignees are anonymized in the public dataset
- Some fields contain "?" as placeholder for missing values
- The dataset is heavily concentrated in Feb–May 2016 (~99% of all unique incidents). Investigation confirmed that only 274 genuine incidents exist beyond June 2016, spread across Jun 2016–Feb 2017. This appears to be a minimal second phase of data collection rather than a system artifact. Trend analysis is therefore most meaningful within the Feb–May 2016 window.
- SLA status (made_sla) was found to change between Resolved and Closed states for ~36% of incidents — final Closed state used as the definitive measure
- Deduplication was essential: without it, incidents were double/triple counted, inflating all metrics

---

## File Structure
├── IT Incident Trend Analysis.ipynb  # Python analysis and visualizations

├── IT Incident Trend Analysis.pbix   # Power BI interactive dashboard

├── incidents_cleaned_v2.csv          # Cleaned, deduplicated dataset

└── README.md                         # Project documentation

---

## Key Skills Demonstrated
- Data cleaning and deduplication
- Exploratory data analysis (EDA)
- Data quality investigation and correction
- Python (pandas, matplotlib, seaborn)
- Power BI (DAX measures, interactive slicers)
- Cross-validation of findings across multiple tools
- IT domain expertise (ITSM, SLA management, incident prioritization)
