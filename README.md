# Sales Case Study Data Pipeline (Python + DuckDB + Power BI)

**Author:** Rey Li  
**Last Updated:** 2025-10-21  

---

## Project Overview
This repository demonstrates a lightweight, end-to-end **data-pipeline simulation** using ***Python** and **DuckDB** inside **Google Colab**, structured around  data-engineering principles (Bronze → Silver → Gold).  
The goal is to model a realistic retail dataset from raw CSVs to analytics-ready tables and Power BI dashboards.

---

## Notebook Structure

| Notebook | Layer | Description |
|-----------|--------|-------------|
| **`01_clean_data_bronze.ipynb`** |  Bronze | Ingests and lightly cleans raw CSVs. This stage mimics the *Bronze* layer — the raw data lake. Includes type alignment, date parsing, and minimal cleaning to preserve raw fidelity. |
| **`02_transform_silver_gold.ipynb`** |  Silver /  Gold | Transforms cleaned CSVs into structured **Silver** tables in **DuckDB** (`silver_products`, `silver_customers`, `silver_sales`, etc.).<br>Creates **Gold** analytical views (`v_sales_product_weighted`, `v_promotion_impact`) to flatten bridges and prepare facts for BI consumption. |
| **Power BI Dashboard** |  BI Layer | Connects to the extracted Gold views / fact table and Dim tables and visualizes: - Overall sales performance  - Regional & seasonal trends  - Promotion impact and discount analysis  - Product and category performance |

---

##  Data Model Highlights

- **Fact Table:** `fact_sales` (flattened bundle ↔ product ↔ promotion relationships)  
- **Dimensions:** Products, Categories, Stores, Customers, Promotions, Promotion Status
- **Gold Views:**
  - `v_sales_product_weighted` — Allocates bundled sales proportionally to products based on price weights.  
  - `v_promotion_impact` — Joins sales with promotions to calculate **gross**, **discount**, and **net** product-level sales. Depends on `v_sales_product_weighted`

---



## ⚠️ Limitations

Because this project runs entirely inside **Google Colab**:

- Session storage is **temporary** – all data and DuckDB files reset when the runtime disconnects.  
- **No persistent scheduling** – you can’t automate refreshes natively.  
- Limited local resources – suitable for demo-scale data only.  
- Hence, only **two notebooks** were used to keep the pipeline efficient within Colab constraints.

---

## Future Improvements

- Integrate with **dbt** for modular SQL, lineage tracking, and automated tests.  
- SCD Design for Dim Promotion would be high valuable for most of the business use. The current promotion table does not need this.
- Migrate DuckDB database  to **BigQuery** / **Databricks** for scalability.  
- Expand BI layer: add dashboards for **customer segmentation**

---

