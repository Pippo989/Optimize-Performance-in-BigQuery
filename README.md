# Optimize Performance in BigQuery

This repository contains a technical deep dive designed to move data practitioners from reactive troubleshooting to proactive architectural optimization. The included notebook provides a hands-on workflow for mastering BigQuery internals, data modeling, and performance diagnostics.

---

## Overview
The goal of this playbook is to provide hands-on experience in **data modeling, monitoring, and query optimization**. By the end of this notebook, you will not just know *that* a query is slow; you will know how to model your data and read the **Execution Graph** to identify specific bottlenecks and implement architectural optimizations.



---

## Notebook Flow

### 1. Physical Data Modeling
Move beyond default settings to build a storage layer designed for scale:
* **The Baseline:** Implement **Partitioning** and **Clustering** to drastically reduce bytes scanned and minimize costs.
* **Advanced Features:** Deploy **Materialized Views** for auto-refreshed aggregations and configure **BI Engine** for sub-second, in-memory analytical latency.
* **Advanced Storage:** Utilize **Search Indexes** for unstructured text, **Primary/Foreign Key constraints** to enable join elimination, and **Nested/Repeated fields** for efficient denormalization.

### 2. Analyze BigQuery Performance (The "MRI")
Learn to diagnose performance issues using advanced telemetry:
* **Simulate Chaos:** The notebook generates a **"Chaos Table"** featuring intentional partition skew, heavy payloads, and CPU-intensive strings to create a realistic troubleshooting environment.
* **The Diagnosis:** Use the Execution Graph to "read the MRI" of a Query Plan. You will learn to identify:
    * **Partition Skew:** When work is unevenly distributed across slots.
    * **Shuffle Quota Exhaustion:** Identifying data repartitioning limits.
    * **Slot Contention:** Understanding compute-bound workloads.
    * **High Cardinality Joins:** Spotting "Join Explosions" before they crash.



### 3. Query Optimization Patterns
Quantify the impact of SQL best practices through side-by-side **"Bad vs. Good"** benchmarks:
* **Performance Benchmarking:** Compare SQL patterns to measure the delta in **Slot Time** and **Total Duration**.
* **Key Patterns Explored:**
    * Avoiding `SELECT *` and optimizing `COUNT(DISTINCT)`.
    * Efficient `ORDER BY` and `WHERE` clause ordering.
    * **Data Types:** Benchmarking `INT64` vs. `STRING` joins.
    * **Complex Logic:** Optimizing JSON parsing, RegExp vs. `LIKE`, and implementing pre-aggregation strategies.

---

## Prerequisites
To run this notebook, you will need:
* A **Google Cloud Platform (GCP)** project with an active billing account.
* The **BigQuery API** enabled.
* **Appropriate IAM permissions:** `BigQuery Admin` (required for managing reservations, BI Engine, and dataset creation).
* *Note: Some advanced sections (Slots/Reservations) require a billing account that supports BigQuery Editions.*

---

## Setup & Safety
1.  **Open the Notebook:** Load `Optimize_Performance_in_BigQuery.ipynb` into Google Colab or Vertex AI Workbench.
2.  **Authentication:** Run the initialization cell to authenticate your GCP credentials.
3.  **Project Configuration:** Set your `PROJECT_ID` and `REGION` in the configuration cell.
4.  **Cost Management:** The notebook includes cost-calculation scripts. **Always check the estimated "Bytes Processed" before running the Chaos Lab at scale.**

---

## Cleanup
A comprehensive cleanup section is included at the end of the notebook to prevent unnecessary charges. It will automatically:
* Reset **BI Engine** capacity to 0GB.
* Delete diagnostic datasets, "Chaos Tables," and all temporary reservations/slots.

---

## 📧 Contact
**Philip Chopovsky** Customer Engineer, Data Analytics @ Google Cloud  
[LinkedIn]([https://www.linkedin.com/in/pchop/]) | [Email](mailto:philipchop@google.com)
