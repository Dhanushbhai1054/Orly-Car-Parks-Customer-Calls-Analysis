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

### Setup
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/orly-calls-analysis.git
   cd orly-calls-analysis
Install Dependencies:
bashpip install -r requirements.txt

Configure PostgreSQL:

Create database orly_calls_db.
Set user: postgres, password: 1054851, host: localhost, port: 5432.
Update db_config.py with your credentials if different.


Install Power BI Desktop:

Download from powerbi.microsoft.com/desktop.



Usage
Running the Project

Generate and Load Data:

Run generate_data.py to create orly_call_data.csv and load to PostgreSQL.

bashpython generate_data.py

Perform Analysis:

Execute analyze_data.py for aggregations, crosstabs, and forecasts (saves daily_calls.csv, forecast.csv, crosstab.csv).

bashpython analyze_data.py

Load Summary Tables:

Run load_tables.py to populate daily_summary, forecast_summary, and reason_location_crosstab tables.

bashpython load_tables.py

Build Power BI Dashboard:

Open Orly_COCD_Dashboard.pbix or connect Power BI to orly_calls_db (DirectQuery mode).
Customize visuals (e.g., heatmap, forecast line) as per instructions.



Project Structure
textorly-calls-analysis/
│
├── data/                # Generated CSVs (e.g., orly_call_data.csv)
├── scripts/             # Python scripts
│   ├── generate_data.py # Data generation and initial load
│   ├── analyze_data.py  # Analysis and forecasting
│   └── load_tables.py   # Load summary tables to DB
├── db_config.py         # Database connection settings
├── requirements.txt     # Python dependencies
├── Orly_COCD_Dashboard.pbix # Power BI file
├── README.md            # This file
└── LICENSE              # License info
Codes and Steps
1. Data Generation & Structuring

Script: generate_data.py
Generates 10,000 calls with biased reasons/locations, loads to calls table.

pythonimport pandas as pd
import numpy as np
from datetime import datetime, timedelta
from sqlalchemy import create_engine

np.random.seed(42)
car_parks = ['P1', 'P2', 'P3', 'P4', 'P5']
reasons = ['Payment Issue', 'Entry Problem', 'Exit Barrier', 'Lost Ticket', 'Information Request', 'Technical Malfunction', 'Other']
start_date = datetime(2025, 8, 15)
dates = [start_date + timedelta(days=i) for i in range(30)]
data = []
for _ in range(10000):
    date = np.random.choice(dates)
    hour = np.random.randint(0, 24)
    timestamp = date + timedelta(hours=hour)
    duration = np.random.randint(1, 10)
    reason = np.random.choice(reasons, p=[0.2, 0.15, 0.15, 0.1, 0.2, 0.1, 0.1])
    location = np.random.choice(car_parks, p=[0.3, 0.25, 0.2, 0.15, 0.1])
    data.append([timestamp, duration, reason, location])
df = pd.DataFrame(data, columns=['Timestamp', 'Duration', 'Reason', 'Location'])
df.to_sql('calls', engine, if_exists='replace', index=False)
2. Exploratory Analysis

Script: analyze_data.py
Aggregates data, creates crosstabs, forecasts with ARIMA.

pythonfrom statsmodels.tsa.arima.model import ARIMA
daily_calls = df.groupby('Date').size().reset_index(name='Calls')
model = ARIMA(daily_calls.set_index('Date')['Calls'], order=(1,1,1))
model_fit = model.fit()
forecast = model_fit.forecast(steps=7).round(0)
forecast_df = pd.DataFrame({'Date': [daily_calls['Date'].max() + timedelta(days=i+1) for i in range(7)], 'Forecasted Calls': forecast})
forecast_df.to_csv('forecast.csv', index=False)
3. Saving Tables

Script: load_tables.py
Loads summaries to PostgreSQL.

pythondaily_calls.to_sql('daily_summary', engine, if_exists='replace', index=False)
forecast_df.to_sql('forecast_summary', engine, if_exists='replace', index=False)
pd.crosstab(df['Reason'], df['Location']).to_sql('reason_location_crosstab', engine, if_exists='replace', index=False)
Prediction Model

Model: ARIMA(1,1,1)
Why: Simple, interpretable time-series model for short-term forecasting of daily calls, capturing trends and seasonality without complex ML.
Approach: Aggregate daily calls, fit on 30 days, forecast 7 days (Sep 14-20, 2025).
Results: Predicts a drop from 379 (Sep 13) to 345 (Sep 14), stabilizing at ~334, aiding staffing decisions.

BI Analysis and Findings

Dashboard: 3 pages in Orly_COCD_Dashboard.pbix:

Overview: 10,000 calls, Info Requests (2,009) top reason, P1 (2,973) dominant.
Trends: Daily line (peaks Sep 13: 379) + forecast (345 next day).
Analysis: Heatmap (P1 Payment 627 red hotspot), polluting % (~40%).


Findings: 40% polluting calls (4,014), P1-P3 hotspots (75%), weekend peaks (34%), forecast stable post-peak.

Suggestions

Technical: Upgrade P1/P2 payment systems (25% reduction target).
Organizational: Increase staffing on weekends/peaks (use forecast).
Communicational: Add signage/FAQs in P1-P3 (20% Info Request cut).
Plan: Pilot P1 fixes, monitor via BI alerts (>350 calls).

Conclusion
This project delivers a scalable solution for COCD call optimization, from synthetic data to BI dashboards and ARIMA forecasts. It identifies key issues (e.g., P1 hotspots) and proposes a 20-30% reduction, enhancing Orly efficiency. Ready for real data integration.
Contributing
Feel free to fork this repository, submit issues, or pull requests. Contact [your.email@example.com] for collaboration.
