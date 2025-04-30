---
layout: default
title:  "Washington State Electric Vehicle Analysis"
date:   2025-04-29 14:10:46 -0700
categories: Azure OpenAI Python
---


Here’s a blog post draft showcasing your personal project analyzing Washington State Electric Vehicle (EV) data using Azure Databricks and PySpark:

---

# ⚡ Driving Change: Analyzing Washington State Electric Vehicle Trends with Azure Databricks

As part of my personal interest in sustainability and data engineering, I recently explored a public dataset detailing electric vehicle (EV) registrations in Washington State. My goal was simple: **Is EV adoption truly accelerating, or is it all hype?**

To find out, I built a data pipeline using **Azure Databricks**, leveraging **PySpark**, **Pandas**, and **Matplotlib** to perform exploratory data analysis and visualization on this fast-evolving transportation trend.

---

## 📊 Project Overview

**Project Objective**:  
Analyze trends in EV ownership across Washington State over time using registration data.

**Tools Used**:
- **Azure Databricks** (for scalable distributed processing)
- **PySpark** (data cleaning, transformation, aggregation)
- **Pandas + Seaborn/Matplotlib** (final visualizations)
- **Databricks Utilities** (quick data profiling)

---

## 🚀 Step-by-Step Breakdown

### 1. Load the Data from the Bronze Zone

I began by reading the raw CSV file containing vehicle title and registration data into a Spark DataFrame.

```python
bronze_path = "/Volumes/main/djsprojects/evdata/bronze/Electric_Vehicle_Title_and_Registration_Activity.csv"
ev_df = spark.read.format("csv")\
           .option("header", "true")\
           .option("inferSchema", "true")\
           .load(bronze_path)
```

---

### 2. Clean and Format the Date Columns

Accurate time-based analysis starts with clean date fields. I converted both the **Sale Date** and **Transaction Date** to `date` format for time series aggregation.

```python
ev_df = ev_df.withColumn("Sale Date", to_date(col("Sale Date"), "MMMM dd yyyy"))
ev_df = ev_df.withColumn("Transaction Date", to_date(col("Transaction Date"), "MMMM dd yyyy"))
```

---

### 3. Quick Profiling with Databricks Utilities

To get a fast, visual summary of the data types and value distributions, I used:

```python
dbutils.data.summarize(ev_df, precise=True)
```

This gave me a high-level snapshot of record counts, nulls, and column distributions before diving into analysis.

---

### 4. Visualize the Growth of EV Ownership

The heart of the project was visualizing the rise in EV registrations over time. I grouped the data by `Transaction Date` and plotted the results using Pandas and Matplotlib.

```python
ev_count_df = ev_df\
    .groupby("Transaction Date")\
    .count()\
    .toPandas()

# Convert to datetime
ev_count_df["Transaction Date"] = pd.to_datetime(ev_count_df["Transaction Date"])

# Plotting
plt.figure(figsize=(12,6))
sns.lineplot(data=ev_count_df, x="Transaction Date", y="count")
plt.title("Washington State EV Registrations Over Time")
plt.xlabel("Date")
plt.ylabel("Number of Transactions")
plt.grid(True)
plt.show()
```

---

## 📈 Key Takeaways

- There is a **clear upward trend** in EV registrations, especially post-2020.
- The analysis validates anecdotal impressions with data-backed evidence.
- Azure Databricks is ideal for scaling public dataset analysis and producing quick, reliable insights.

---

## 🔧 What’s Next?

Future extensions could include:
- Geo-analysis by county or ZIP code
- Classification of EV types (battery vs. plug-in hybrid)
- Integration with charging station availability or energy usage data

---

## 💬 Final Thoughts

This project reaffirmed the power of **cloud-native data platforms** and **open data** in answering important societal questions. The results were insightful, the development process was smooth, and Azure Databricks provided the perfect environment to build, iterate, and visualize.

Repo: <a href="https://github.com/dspriggs-ds/electric_vehicle">Electric Vehicle Analysis</a>
