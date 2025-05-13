---
layout: default
title: "How to Build a Resilient API Data Pipeline in Databricks"
date:   2025-05-12 12:00:00 -0700
categories: Azure Databricks REST API Python PySpark
---


## 📘 Introduction

As a seasoned data engineer, you're often challenged to pull data from unpredictable APIs and transform it into reliable insights. In this guide, we'll walk through a real-world notebook that demonstrates how to **ingest historical newspaper records from the Library of Congress API**, while building in robust error handling and logging—ideal for any modern data pipeline running in **Azure Databricks**.

---

## 📊 Project Overview

We’ve built a notebook that:

* Connects to the **Library of Congress "Chronicling America" API**
* Extracts article metadata related to specific U.S. states and keywords (e.g., `"Tacoma"` and `"Washington"`)
* Handles common API errors with `try-except` blocks
* Logs execution messages for observability and troubleshooting
* Saves the final dataset to a Databricks Delta Lake table for downstream analytics

This approach is ideal for any data engineer looking to **build fault-tolerant ingestion pipelines** from public or third-party APIs.

---

## 🧱 Tech Stack

* **Python**: `requests`, `json`, `logging`
* **Apache Spark (PySpark)**: `Row`, `DataFrame`, `StructType`
* **Databricks**: Unified workspace for development and scheduled workflows

---

## 🛠️ Key Components

### 1. Setup & Configuration

The notebook starts by importing all essential libraries and setting up a custom logging configuration:

```python
import requests
import json
import logging
from pyspark.sql import Row
from pyspark.sql.types import StructType, StructField, StringType

logger = logging.getLogger('databricks_api_logging')
logger.setLevel(logging.DEBUG)
...
```

This setup ensures that any API or Spark error is immediately captured and visible during interactive or scheduled runs.

---

### 2. API Request Parameters

You can configure the notebook to fetch data for a specific `state`, `subject`, and write it to a named cataloged table in your Delta Lake.

```python
state = "Washington"
subject = "Tacoma"
catalog = "generaldata"
schema = "dataanalysis"
table_name = "tacoma_articles"
```

---

### 3. Robust Data Retrieval Loop

The heart of the notebook is a loop that paginates through **up to 50 pages of API results**, dynamically builds a Spark schema from the JSON response, and constructs a PySpark DataFrame:

```python
for p in range(0, numPages):
    response = requests.get(f"...&page={p+1}")
    ...
    for article in article_data["items"]:
        rows.append(Row(**article))
```

This lets you scale retrieval for large datasets, without hardcoding the schema or worrying about brittle transformations.

---

### 4. Error Handling & Logging

The notebook makes excellent use of Python’s `try-except` structure to handle both HTTP-specific and general request failures:

```python
except requests.exceptions.HTTPError as err:
    logger.error(f"HTTP error occurred: {err}")
except requests.exceptions.RequestException as err:
    logger.error(f"Error occurred: {err}")
```

---

### 5. Data Persistence

Finally, the DataFrame is saved directly into the Databricks metastore, enabling immediate access from BI tools like Power BI or downstream notebooks:

```python
df.write.mode("overwrite").saveAsTable(f"{catalog}.{schema}.{subject}")
```

---

## 🎯 Why This Matters

This notebook showcases a **production-ready template** for any API ingestion task:

* It’s **modular** – update the API endpoint or schema with minimal changes.
* It’s **safe** – logging and error handling protect your jobs from silent failures.
* It’s **scalable** – integrates seamlessly into Delta Lake and Databricks pipelines.

Whether you’re pulling from financial APIs, weather feeds, or open government data, this approach ensures your data workflows are **resilient and transparent**.

---

## 📦 Try It Yourself

You can adapt this notebook to work with any REST API by modifying the endpoint and schema logic. To build on this:

* Add automated email/Slack alerts via Azure Functions or Databricks webhooks.
* Parameterize the notebook for batch scheduling with Databricks Jobs.
* Integrate with Unity Catalog for secure, governed data access.

---

## 📚 Resources

* <a href="https://github.com/LibraryOfCongress" target="_blank">Library of Congress API</a>
* <a href="https://docs.databricks.com/" target="_blank">Databricks API Best Practices</a>


---

### 💬 Final Thoughts

In a world full of unreliable APIs, your pipelines need to be bulletproof. With this template, you’re not just collecting data—you’re **engineering reliability into your ETL**.

---



🔗 **Want to see the notebook in action?** 
<a href="https://github.com/dspriggs-ds/databricks_api">GitHub</a>

