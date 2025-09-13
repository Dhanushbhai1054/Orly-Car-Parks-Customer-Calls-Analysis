# Orly Car Parks Customer Calls Analysis

## Overview
This project analyzes customer call data for Orly car parks managed by the Remote Commercial Operations Center (COCD) using synthetic data simulating 10,000 calls over 30 days (August 15 - September 13, 2025). The goal is to identify "polluting" calls (unnecessary and avoidable ones), detect patterns, forecast future volumes, and propose actionable improvements to enhance operational fluidity. The solution integrates Python for data generation and modeling, PostgreSQL for storage, and Power BI for interactive visualization.

- **Created:** September 13, 2025, 09:16 PM CEST
- **Status:** Completed (ready for internship demo)

## Problem Statement
The COCD handles a high volume of calls, many of which are recurring issues (e.g., payment problems, information requests) that disrupt efficiency. This project aims to:
- Analyze call patterns, hotspots, and peaks.
- Predict future call volumes for proactive planning.
- Reduce polluting calls by 20-30% through targeted actions.

## Methodology and Tools
### Approach
1. **Data Generation & Structuring:** Create synthetic call data in Python, store in PostgreSQL.
2. **Exploratory Analysis:** Use SQL and Python to aggregate data (reasons, locations, peaks).
3. **Predictive Modeling:** Apply ARIMA for time-series forecasting.
4. **Visualization:** Build interactive dashboards in Power BI.
5. **Recommendations:** Derive insights and suggest improvements.

### Tools
- **Python (pandas, numpy, statsmodels):** Data generation, analysis, ARIMA forecasting.
- **PostgreSQL & pgAdmin:** Database management and SQL querying.
- **Power BI Desktop:** Dashboards with conditional formatting and DAX.

## Installation
### Prerequisites
- Python 3.9+
- PostgreSQL (with pgAdmin)
- Power BI Desktop
- Required Python packages: `pandas`, `numpy`, `statsmodels`, `sqlalchemy`

orly-calls-analysis/
│
├── data/                     # Generated CSVs (e.g., orly_call_data.csv)
├── scripts/                  # Python scripts
│   ├── generate_data.py      # Data generation and initial load
│   ├── analyze_data.py       # Analysis and forecasting
│   └── load_tables.py        # Load summary tables to DB
├── db_config.py              # Database connection settings
├── requirements.txt          # Python dependencies
├── Orly_COCD_Dashboard.pbix  # Power BI file
├── README.md                 # This file
└── LICENSE                   # License info
