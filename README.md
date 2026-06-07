# 🚨 Snowflake Fraud Intelligence Dashboard

## Real-Time Financial Fraud Analytics & Risk Intelligence Platform

An end-to-end Data Engineering and Analytics project built using Snowflake, Snowpark Python, SQL, Streamlit, and Plotly to analyze financial transactions, detect fraud patterns, generate customer risk profiles, and provide executive-level fraud intelligence dashboards.

---

## 📌 Project Overview

Financial fraud continues to be a major challenge for digital payment systems. Organizations require scalable data platforms capable of monitoring millions of transactions, identifying suspicious activities, and generating actionable risk insights.

This project implements a complete Fraud Intelligence Platform using modern Data Engineering practices including:

* Data Warehousing in Snowflake
* Medallion Architecture (Bronze → Silver → Gold)
* Star Schema Data Modeling
* Snowpark-Based Risk Profiling
* Interactive Streamlit Dashboard
* Real-Time Fraud Intelligence Reporting

The solution transforms raw transaction data into business-ready analytics and risk intelligence for fraud monitoring teams.

---

## 🎯 Project Objectives

* Build an end-to-end fraud analytics platform
* Design a scalable Snowflake Data Warehouse
* Implement Medallion Architecture
* Create a Star Schema analytical model
* Generate customer fraud risk scores using Snowpark
* Develop executive-level fraud dashboards
* Deliver actionable business insights

---

## 🛠️ Technology Stack

| Layer           | Technology      |
| --------------- | --------------- |
| Data Warehouse  | Snowflake       |
| Data Processing | Snowpark Python |
| Programming     | Python          |
| Query Language  | SQL             |
| Dashboard       | Streamlit       |
| Visualization   | Plotly          |
| Data Modeling   | Star Schema     |
| Version Control | Git & GitHub    |

---

## 📂 Dataset

**Dataset:** Synthetic Financial Datasets for Fraud Detection (PaySim)

**Source:**

https://www.kaggle.com/datasets/ealaxi/paysim1

The dataset is generated using the PaySim simulator and contains millions of synthetic mobile money transactions including:

* CASH_IN
* CASH_OUT
* PAYMENT
* DEBIT
* TRANSFER

along with fraud indicators and transaction metadata. The dataset is a scaled-down version of the PaySim fraud simulation environment.

The data tier uses the industry-standard Synthetic Financial Datasets For Fraud Detection (PaySim) mobile money ledger, which simulates normal financial behaviors alongside deeply embedded fraudulent exceptions.

Total Records Loaded: 6,362,620 rows

Verified Fraud Exceptions: 8,213 cases

---

# 🏗️ Architecture Overview

```text
PaySim Dataset (CSV)
          │
          ▼
AWS S3 Storage
          │
          ▼
Snowflake External Stage
          │
          ▼
Bronze Layer
(Raw Data)
          │
          ▼
Silver Layer
(Cleansed & Standardized Data)
          │
          ▼
Gold Layer
(Star Schema Warehouse)
          │
          ▼
Snowpark Risk Profiling Engine
          │
          ▼
Analytical Views
          │
          ▼
Streamlit Dashboard
```

---

## 📸 Architecture Diagram

![Architecture Diagram](https://github.com/user-attachments/assets/1615cfa7-3eeb-43fe-ba19-514d0e6b5111)

---

# 🗄️ Data Warehouse Design

## Fact Table

### FACT_TRANSACTIONS

Stores transactional events and fraud indicators.

Key Measures:

* Transaction Amount
* Customer Balance Change
* High Value Flag
* Fraud Flag
* Flagged Fraud Indicator

---

## Dimension Tables

### DIM_CUSTOMER

Customer information and segmentation.

### DIM_MERCHANT

Merchant analytics and risk levels.

### DIM_TIME

Date and time hierarchy.

### DIM_LOCATION

Location and regional fraud information.

### DIM_TRANSACTION_TYPE

Transaction categories and risk classifications.

### DIM_CUSTOMER_RISK_PROFILES

Snowpark-generated fraud intelligence table.

---

## 📸 ER Diagram

Add generated ER diagram here:

```markdown
![ER Diagram](https://github.com/user-attachments/assets/a8384331-4136-4984-96a9-083dc5c09250)
```

---

# ⚙️ Data Processing Pipeline

## Bronze Layer

* Raw data ingestion
* COPY INTO loading
* No transformations applied

## Silver Layer

* Data cleansing
* Null handling
* Data type standardization
* Business rule validation

## Gold Layer

* Star Schema implementation
* Fact and Dimension tables
* Business analytics optimization

---

# 🧠 Snowpark Fraud Risk Profiling

A custom Snowpark Python pipeline was implemented to generate customer-level fraud intelligence.

### Calculated Metrics

* Total Transaction Count
* Historical Fraud Count
* High Value Transactions
* Peak Transaction Value
* Fraud Risk Score

### Risk Segments

| Segment        | Score Range |
| -------------- | ----------- |
| STANDARD_RISK  | Low         |
| MONITORED_RISK | Medium      |
| CRITICAL_RISK  | High        |

---

# 📊 Analytical Views

The dashboard is powered using optimized Gold-layer views.

### Executive Analytics

* VW_EXECUTIVE_KPIS

### Fraud Analytics

* VW_FRAUD_TRENDS
* VW_FRAUD_BY_TRANSACTION_TYPE
* VW_REGIONAL_FRAUD_ANALYTICS

### Customer Analytics

* VW_CUSTOMER_RISK_PROFILES

### Financial Analytics

* VW_HOURLY_TRANSACTION_ANALYTICS

---

# 📈 Dashboard Features

## Executive Overview

* KPI Cards
* Fraud Rate Monitoring
* Revenue Tracking
* Transaction Monitoring

### Screenshot

```markdown
![Executive Dashboard](https://github.com/user-attachments/assets/c09de9d7-31ff-4261-8f57-650c397d17de)
```

---

## Fraud Analytics

* Fraud Trends
* Transaction Type Risk Analysis
* Regional Fraud Intelligence

### Screenshot

```markdown
![Fraud Analytics](Screenshots/Fraud_Analytics.png)
```

---

## Customer Insights

* Customer Risk Segmentation
* Risk Distribution Analysis

### Screenshot

```markdown
![Customer Insights](Screenshots/Customer_Insights.png)
```

---

## Financial Analytics

* Hourly Transaction Analysis
* Revenue Monitoring

### Screenshot

```markdown
![Financial Analytics](Screenshots/Financial_Analytics.png)
```

---

## Risk Intelligence

* Live Fraud Alert Feed
* High-Risk Customer Monitoring
* Fraud Risk Score Distribution
* Downloadable Risk Reports

### Screenshot

```markdown
![Risk Intelligence](Screenshots/Risk_Intelligence.png)
```

---

# 🚀 Key Business Insights

### Fraud Exposure

* TRANSFER transactions exhibit the highest fraud exposure.
* Fraud activity is concentrated within specific transaction categories.

### Customer Risk Intelligence

* Majority of customers belong to Standard Risk segment.
* Critical Risk customers represent a small but highly important group.

### Regional Intelligence

* Fraud distribution varies across regions and cities.
* Regional monitoring supports targeted fraud prevention.

### Operational Intelligence

* Hourly transaction patterns reveal peak business activity periods.
* Risk scoring enables proactive fraud monitoring.

### Advanced Analytical Use Cases Captured

* Vulnerability Concentration: Proved that 100% of network fraud is strictly isolated within TRANSFER (4,097 cases) and CASH_OUT (4,116 cases) channels.
* Velocity Triggers: Isolated 47 separate account incidents where users executed multiple high-volume transactions within the exact same hour window.
* Account Takeover Balances: Exposed 606,381 explicit transactions where high-value payments immediately stripped the source account balances down to exactly ₹0.00.

---

# ⚡ Performance Optimizations

Implemented several optimization techniques:

* Streamlit caching
* Snowflake analytical views
* Aggregated Gold-layer datasets
* Reduced dashboard query complexity
* Pre-computed KPI calculations
* Snowpark-based processing

Multi-Key Physical Clustering: The Fact table was physically sorted on disk across its primary query paths: CLUSTER BY (DATE(TRANSACTION_TIMESTAMP), IS_FRAUD, TRANSACTION_TYPE_KEY). This drove the metadata partition overlap depth down to 2.0.

Materialized View Compacting: Embedded MV_FRAUD_SUMMARY to pre-aggregate complex multi-dimensional joins across transaction type, time keys, and location buckets.

Latency Benchmark Performance: Repeated dashboard lookup execution times dropped by 95.3% (from a cold disk-scan of 642ms down to a cached metadata result of 30ms).

---

# 🤖 Native Snowpark Python ML Engine

Bypassing the security risks of exporting data to external, unsecured secondary environments, a Snowpark Python Stored Procedure runs natively inside Snowflake compute nodes. The engine processes account data frames and updates the predictive table DIM_CUSTOMER_RISK_PROFILES:

* 🔴 CRITICAL_RISK (8,213 accounts): Outlier actors tied to historical fraud vectors. Average Score: 86.00

* 🟠 MONITORED_RISK (127,919 accounts): High-volume, high-value spenders flagged for transaction depth. Average Score: 45.50

* 🟡 STANDARD_RISK (6,217,175 accounts): Safe, baseline consumer retail profiles. Average Score: 10.05

---

# 🔮 Future Enhancements

* Machine Learning Fraud Prediction
* Real-Time Streaming Ingestion
* Alert Notification System
* Geospatial Fraud Mapping
* Predictive Risk Intelligence
* Role-Based Dashboard Access

---

# 👨‍💻 Author

Pratham Bajpai
Data Engineering | Snowflake | Python | SQL | Streamlit

---

# ⭐ Project Highlights

✔ End-to-End Data Engineering Project

✔ Snowflake Data Warehouse

✔ Medallion Architecture

✔ Star Schema Modeling

✔ Snowpark Fraud Intelligence Engine

✔ Interactive Streamlit Dashboard

✔ Executive-Level Fraud Analytics

✔ Portfolio-Ready Enterprise Project
