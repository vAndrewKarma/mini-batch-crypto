# 🚀 Crypto Micro Batch Pipeline

A production-grade crypto data pipeline using **Azure Synapse**, **Azure Data Lake Storage Gen2**, and **Power BI**. It ingests micro-batch cryptocurrency data from public APIs, transforms and stores it in a lakehouse architecture, and visualizes trends and predictive insights through Power BI dashboards.

---

## 📌 Objective

Build a secure, scalable, and modular cloud-based data pipeline that:
- Collects cryptocurrency market data in 5-minute intervals
- Stores it in a **medallion architecture** on Azure Data Lake
- Transforms and cleanses it using **Azure Synapse Spark**
- Serves analytical insights via **Power BI**

---

## 🧱 Architecture

         +-------------------+
         |  CoinGecko API    |
         +-------------------+
                  ↓
       (Scheduled Ingestion)
                  ↓
 +----------------------------------+
 | Azure Data Factory (Pipelines)   |
 | - REST API calls                 |
 | - Logging, retry, error handling |
 +----------------------------------+
                  ↓
 +----------------------------------+
 | Azure Data Lake Storage Gen2     |
 | - Raw Zone (/raw/yyyy/mm/dd/)    |
 | - Curated Zone (/curated/)       |
 +----------------------------------+
                  ↓
  (ETL / Cleansing / Forecasting)
                  ↓
 +----------------------------------+
 | Azure Synapse Spark Pools        |
 | - PySpark notebooks              |
 | - Delta Lake format              |
 | - Optional: Time-series models   |
 +----------------------------------+
                  ↓
 +----------------------------------+
 | Azure Synapse Serverless SQL     |
 | - Semantic layer over curated    |
 +----------------------------------+
                  ↓
 +----------------------------------+
 | Power BI                         |
 | - Real-time dashboards           |
 | - Auto-refresh + RLS             |
 +----------------------------------+

---

## 🔗 Data Source

We use the [CoinGecko API](https://www.coingecko.com/en/api) to ingest data.

- ✅ No API key required
- ⏱ Updated every ~25-30 minutes
- 📦 JSON output: current price, volume, market cap

### Example Endpoint
```http
GET https://api.coingecko.com/api/v3/simple/price?ids=bitcoin,ethereum&vs_currencies=usd
```