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


### Install dependencies
```bash
pip install -r requirements.txt
```

### Configure PostgreSQL
- Create database: **orly_calls_db**  
- Credentials:  
  - **User:** postgres  
  - **Password:** 1054851  
  - **Host:** localhost  
  - **Port:** 5432  
- Update `db_config.py` if different  

### Install Power BI Desktop
👉 [Download here](https://powerbi.microsoft.com/desktop)  

---

## 🚀 Usage

### 1. Generate and Load Data
```bash
python scripts/generate_data.py
```
Creates `orly_call_data.csv` and loads data to PostgreSQL.  

### 2. Perform Analysis
```bash
python scripts/analyze_data.py
```
Generates `daily_calls.csv`, `forecast.csv`, and `crosstab.csv`.  

### 3. Load Summary Tables
```bash
python scripts/load_tables.py
```
Populates `daily_summary`, `forecast_summary`, and `reason_location_crosstab` tables.  

### 4. Build Power BI Dashboard
- Open `Orly_COCD_Dashboard.pbix`  
- Or connect Power BI to `orly_calls_db` (DirectQuery mode)  
- Customize visuals (heatmaps, forecast line, etc.)  

---

## 📂 Project Structure
```
orly-calls-analysis/
│
├── data/                     # Generated CSVs
├── scripts/                  # Python scripts
│   ├── generate_data.py      # Data generation & DB load
│   ├── analyze_data.py       # Aggregations & forecasting
│   └── load_tables.py        # Load summary tables
├── db_config.py               # Database connection settings
├── requirements.txt           # Python dependencies
├── Orly_COCD_Dashboard.pbix   # Power BI file
├── README.md                  # Documentation
└── LICENSE                    # License info
```

---

## 📊 Prediction Model
- **Model:** ARIMA(1,1,1)  
- **Why:** Simple, interpretable for short-term forecasting  
- **Forecast:** 7 days (Sep 14–20, 2025)  
- **Result:** Predicted drop from **379 (Sep 13)** → **345 (Sep 14)**, stabilizing around **334 calls/day**  

---

## 📈 BI Analysis & Findings
- **10,000 calls total**  
- **Top Reason:** Information Request (2,009 calls)  
- **Top Location:** P1 (2,973 calls)  
- **Polluting Calls:** ~40% (4,014 calls)  
- **Hotspots:** P1–P3 (75% of calls)  
- **Peak:** Sep 13 (379 calls)  
- **Weekend Share:** 34%  

### Heatmap Example (Reason × Location)
| Reason              | P1  | P2  | P3  | P4  | P5  |
|---------------------|-----|-----|-----|-----|-----|
| Payment Issue       | 627 | 517 | 390 | 307 | 164 |
| Information Request | 591 | 493 | 408 | 339 | 178 |
| Exit Barrier        | 415 | 369 | 299 | 225 | 133 |
| Entry Problem       | 444 | 382 | 307 | 202 | 153 |
| Lost Ticket         | 313 | 237 | 218 | 153 | 106 |
| Technical Malf.     | 267 | 282 | 201 | 160 | 97  |
| Other               | 316 | 227 | 218 | 158 | 104 |
| **Total**           |2973 |2507 |2041 |1544 | 935 |

---

## 💡 Suggestions
- **Technical:** Upgrade P1/P2 payment systems → target **25% reduction** in polluting calls  
- **Organizational:** Increase staffing on weekends/peak days  
- **Communication:** Add signage & FAQs in P1–P3 → cut info requests by **20%**  
- **Plan:** Pilot fixes in P1, monitor via BI alerts (>350 calls/day)  

---

## ✅ Conclusion
This project delivers a **scalable solution** for COCD call optimization:  
- From **synthetic data → BI dashboards → ARIMA forecasts**  
- Identifies key pain points (**P1 payment & info requests**)  
- Proposes **20–30% reduction** in polluting calls  
- Ready for **real data integration**  


