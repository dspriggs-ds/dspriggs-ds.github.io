---
layout: default
title:  "Analyzing Washington State Driver’s License Transfers with Azure Databricks"
date:   2025-04-29 14:10:46 -0700
categories: Azure Databricks PySpark Python
---

Breaking into data engineering means exploring real-world datasets and solving meaningful problems. In this blog post, I’ll walk you through a personal project where I leveraged **Azure Databricks** to explore demographic data on driver licenses and ID cards transferred to Washington State. This project showcases the practical application of cloud-based analytics and the power of interactive dashboards for storytelling with data.

## 📊 Project Overview

The goal was to analyze migration trends into Washington State using public data from the [Washington State Open Data Portal](https://data.wa.gov/demographics/Driver-Licenses-and-ID-Cards-Transferred-to-Washin/769e-73q6/about_data). The dataset includes detailed demographic information—state of origin, age, and time of transfer—for individuals moving into Washington and applying for a driver’s license or ID card.

Using **Azure Databricks**, I:

- Cleaned and processed the raw dataset
- Aggregated and grouped data by state and year
- Created visualizations to understand trends over time
- Deployed an interactive dashboard to explore patterns geographically and demographically

## 🛠️ Tech Stack

- **Azure Databricks** for scalable processing and visualization
- **Python (PySpark)** for distributed data manipulation
- **Matplotlib & Databricks Visualizations** for insights
- **Washington Open Data** as the source

## 🔍 Key Insights

- **Top Source States**: California, Oregon, and Texas consistently top the list of inbound states.
- **Migration Trends Over Time**: The number of people transferring to Washington fluctuates seasonally but has shown consistent growth over the past decade.
- **Demographics**: Young adults (20–35) represent a significant share of new residents, indicating educational and job-related moves.

## 📈 Interactive Dashboard

One of the highlights of the project is the Databricks Dashboard, which allows users to explore:

- Yearly migration trends
- Top states of origin
- Age distribution of incoming residents

These insights can help policymakers, urban planners, and businesses better understand population shifts and resource needs.

## 🔗 Try It Yourself

You can check out the <a href="(https://github.com/dspriggs-ds/wa-state-license-transfer">GitHub repository</a> to access the code, data links, and dashboard setup instructions. All you need is an Azure Databricks account to get started.

## 🙏 Acknowledgements

- Thanks to <a href="https://azure.microsoft.com/en-us/services/databricks/">Azure Databricks</a> for making large-scale analytics accessible.
- Shoutout to <a href="https://data.wa.gov">Washington State Open Data</a> for sharing rich and insightful public datasets.
