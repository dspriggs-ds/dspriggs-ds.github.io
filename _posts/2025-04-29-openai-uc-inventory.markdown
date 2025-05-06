---
layout: default
title:  "OpenAI and Unity Catalog the unlikely pair"
date:   2025-04-29 14:10:46 -0700
categories: Azure Databricks Azure OpenAI Unity Catalog
---

Managing data assets efficiently in a data lake is critical for organizations aiming to maximize the value of their data. Recently, I worked on a project that uses **Databricks**, **OpenAI's APIs**, and **PySpark** to automatically **inventory** a **Data Lake** environment, and I’m excited to walk you through the process!

In this post, I'll explain how the notebook, **“OpenAI Data Lake Inventory”**, systematically inventories data assets, enriches them using AI, and stores the results for downstream analytics.


## 📋 What This Notebook Does

This notebook **automates the following tasks**:
- **Scan** available catalogs, schemas, and tables in a Databricks workspace
- **Extract** metadata about each table
- **Enrich** descriptions using **OpenAI’s GPT models** for better documentation
- **Store** the final enriched inventory back into a managed table for future querying and reporting


## 🛠️ Step-by-Step Breakdown

### 1. Setup Environment
The notebook begins by:
- Installing the latest versions of `langchain` and `langchain-openai` libraries
- Restarting the Databricks cluster session to make the new packages available.

```python
%pip install -qU langchain
%pip install -qU langchain-openai
dbutils.library.restartPython()
```

### 2. Import Libraries
It loads essential libraries:
- `pandas`, `pyspark.sql.functions`, and `json` for data manipulation
- `logging` for tracking progress
- `time` for managing API request pacing

```python
import pandas as pd
import pyspark.sql.functions as F
import json, logging, time
```

### 3. Connect to OpenAI and Azure
Secrets (e.g., API keys and endpoints) are securely retrieved using **Databricks Secrets** for interacting with the OpenAI API.

```python
api_key = dbutils.secrets.get(scope="<yourscope>", key="<yourkey>")
azure_endpoint  = dbutils.secrets.get(scope="<yourscope>", key="<youruri>")
```

### 4. Gather Catalogs
The script pulls a list of all available **catalogs** in the Databricks environment but **excludes system catalogs** (like `hive_metastore`, `system`, etc.) to focus only on user-created assets.

```python
catalogs_df = spark.sql("SHOW CATALOGS")
```

### 5. Inventory Tables
For every remaining catalog:
- Retrieve the **schemas**
- Retrieve all **tables** within each schema
- Collect and organize this metadata into a structured **DataFrame**.

This step creates a full inventory of the Data Lake's organizational structure.



## ✨ (Optional) Enrichment with OpenAI

While the notebook you uploaded didn't show enrichment in the first few cells, typically, notebooks like this would:
- Send table and column metadata to OpenAI’s GPT models
- Get back **automated, human-readable descriptions** of tables and fields
- Add the enriched metadata to your inventory table

If your notebook has this later (past the cells I reviewed), it would make the dataset more *self-documenting*.


### 6. Save Inventory Back to Databricks
Finally, the script writes the **enriched inventory** back into Databricks, using `overwriteSchema` mode to ensure that schema changes don't cause future issues.

```python
spark_df.write\
    .mode("overwrite")\
    .option("overwriteSchema", "true")\
    .saveAsTable("<your_inventory_table>")
```


## 📊 Why This Matters

Having a **self-updating**, **AI-enhanced** inventory:
- Makes it easier for new team members to understand data assets
- Improves governance by providing better documentation
- Saves time compared to manual cataloging
- Lays the groundwork for advanced features like data quality monitoring and lineage tracking

## 🚀 Final Thoughts

This notebook is a **powerful example** of combining **AI + Data Engineering** to tackle a very practical need: managing and understanding data at scale.

If you want to future-proof your data lake and make your assets easier to navigate, **building an inventory like this is a great first step** — and OpenAI can take it to the next level.

## Process Visual

```mermaid
flowchart LR
    A[Databricks Data Lake] --> B[Scan Catalogs and Schemas]
    B --> C[Extract Table Metadata]
    C --> D[Enrich Descriptions via OpenAI]
    D --> E[Store Enriched Inventory Table]

    subgraph "OpenAI"
        D
    end

    style A fill:#f9f,stroke:#333,stroke-width:2px
    style E fill:#bbf,stroke:#333,stroke-width:2px
```

## 🔗 Try It Yourself

You can check out the <a href="https://github.com/dspriggs-ds/djs_open_ai_dd">GitHub repository</a> to access the code, data links, and dashboard setup instructions. All you need is an Azure Databricks account to get started.

