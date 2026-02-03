# E-commerce Cohort Analysis (2024–2025)

This project implements an end-to-end cohort analysis pipeline using Databricks and Delta Lake, simulating a real-world e-commerce analytics scenario with incremental data ingestion.

The main objective is to analyze customer retention, repeat purchase behavior, and acquisition trends, and to evaluate how insights evolve when new data (2025) is added to an existing pipeline built on 2024 data.

---

## Business Context

Cohort analysis is a core technique in e-commerce analytics used to understand customer behavior over time.  
This project focuses on answering questions such as:

- How quickly customers return for a second purchase
- How deep repeat purchasing goes over time
- Whether customer acquisition and retention improve or deteriorate
- How incremental data impacts previously reported metrics

---

## Data Architecture

The pipeline follows a Medallion Architecture pattern.

### Bronze Layer
- Raw order-level data
- Separate datasets for:
  - 2024 (initial load)
  - 2025 (incremental load)

### Silver Layer
- Cleaned and validated orders
- One row per order
- Invalid records removed
- Deduplication applied

### Gold Layer
- Customer-level cohort tables
- One row per customer
- Derived attributes such as:
  - First purchase date
  - Second purchase date
  - Cohort month
  - Days to second purchase

---

## Metrics and Dashboards

Three cohort-based indicators are produced and visualized using Databricks dashboards.

### Retention to Second Purchase (1–3 months)

This metric measures the percentage of customers who make a second purchase within 1, 2, or 3 months after their first purchase.

Observation:  
Later cohorts initially appear to have lower retention due to limited observation time. When incremental data is added, retention metrics for these cohorts increase and stabilize.

---

### Repeat Purchase Depth (2+, 3+, 4+)

This metric evaluates how many customers reach deeper levels of repeat purchasing:
- At least 2 orders
- At least 3 orders
- At least 4 orders

Observation:  
Deeper repeat behavior becomes visible only after sufficient time has passed, highlighting the importance of cohort maturity when interpreting results.

---

### Cohort Size (New Customers)

This metric tracks the number of new customers acquired each month.

Observation:  
Cohort size is fixed at the time of acquisition and is not affected by incremental data, making it a stable reference metric.

---

## Incremental Update Analysis (2024 to 2025)

A key focus of this project is the comparison of two analytical states.

### Initial State (2024 data only)
- Late 2024 cohorts show artificially low retention
- Results for recent cohorts are inconclusive due to insufficient observation time

### Updated State (2024 plus 2025 data)
- Retention and repeat purchase depth metrics for late 2024 cohorts increase
- Earlier conclusions are revised as cohorts mature
- Demonstrates the analytical impact of incremental data ingestion

---

## Assumptions and Limitations

- Cohorts require sufficient time to mature before conclusions can be drawn
- Recent cohorts naturally show lower retention
- Retention metrics depend on the observation window
- No marketing channel, pricing, or promotion data is included

---

## Potential Improvements

- Enrich the dataset with customer demographics or acquisition channels
- Add revenue-based cohort metrics such as lifetime value
- Track time to third and fourth purchase
- Introduce rolling or comparative cohort analysis
- Automate incremental ingestion using scheduled jobs

---

## Technology Stack

- Databricks SQL
- Delta Lake
- Databricks Dashboards
- GitHub for version control

---

## Repository Structure

