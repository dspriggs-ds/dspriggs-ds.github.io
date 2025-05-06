---
layout: default
title:  "Analyzing Zillow Housing Sales Data with Databricks and Unity Catalog"
date:   2025-05-06 12:00:00 -0700
categories: Azure Databricks Azure OpenAI Unity Catalog Power BI

Housing market trends are a hot topic, especially in today’s rapidly shifting economic landscape. Using publicly available data from [Zillow](https://www.zillow.com/research/data/), we explored housing sales counts across U.S. regions, applied data transformations for analytical flexibility, cleaned inconsistencies, and saved our results into Unity Catalog—all within a Databricks notebook.

This post walks through the key steps of the notebook and the rationale behind each one.

---

### 📊 Step 1: Importing Zillow Housing Sales Data

We begin by loading the Zillow “Housing Sales Count” dataset. This dataset contains region-level data, with sales counts represented as monthly columns—a format that’s convenient for viewing but suboptimal for analysis.

---

### 🔄 Step 2: Data Transformation — Unpivoting Monthly Columns

To make time series analysis and querying easier, the notebook **converts monthly date columns into rows**. This "unpivoting" step is crucial for efficient downstream processing and visualization in BI tools like Power BI or Tableau.

This transformation results in a long-format table with three key fields:

* `RegionName`
* `Date` (month)
* `SalesCount`

---

### 🧹 Step 3: Cleaning — Filling Missing State Values

The dataset contains records with missing `StateName` values, especially when the `RegionType` is `country`. To ensure schema completeness and downstream integrity, we:

* Identify records where `StateName` is `NULL`
* Populate them with `"United States"` to reflect the proper aggregation level

This small but important fix ensures cleaner joins and visual consistency.

---

### 🧪 Bonus: Filtering Invalid or Sparse Regions

In addition to the above, rows with missing sales data or ambiguous regional hierarchies can be excluded or flagged, depending on analytical needs.

---

### 💾 Step 4: Storing to Unity Catalog

To facilitate governed data access across teams, the processed dataset is stored in **Unity Catalog**, Databricks’ centralized governance layer. By saving the table here, we:

* Enforce data lineage and access policies
* Make it reusable across projects and teams
* Enable future updates and pipeline integrations

---

### 📈 Next Steps

With a clean, well-structured dataset stored in Unity Catalog, analysts and data scientists can now:

* Visualize trends over time by region
* Forecast future housing sales
* Compare regional performance and volatility

This notebook is a great starting point for exploring real estate trends using open data and modern data lakehouse tools.

---

🔗 **Want to see the notebook in action?** \[GitHub](https://github.com/dspriggs-ds/housing_sales)]

