---
layout: default
title: "Analyzing IMDb & Box Office Data: A Personal Data Engineering Project"
date:   2025-05-20 12:00:00 -0700
categories: Azure Databricks, Python, PySpark, Power BI
---


# 🎬 Analyzing IMDb & Box Office Data: A Personal Data Engineering Project

As a data engineer passionate about both storytelling and statistics, I recently embarked on a project that brought together two rich data ecosystems: the IMDb dataset and box office revenue data. The goal was simple but insightful — to explore the intersection of **audience ratings** and **financial performance** across thousands of movies.

---

## 📁 Project Overview

This project is driven by two powerful data sources:

1. **IMDb Datasets** from <a href="https://datasets.imdbws.com/" target="_blank">datasets.imdbws.com</a>
   These include structured `.tsv.gz` files containing metadata like title basics, ratings, crew, and principal cast.

2. **Box Office Mojo Data via `boxoffice_api`**
   A Python package that retrieves real-time and historical box office statistics like domestic gross, international earnings, and opening weekend performance.

With these tools in hand, I created a fully analyzable dataset and built visual insights using **Azure Databricks and Delta Lake**, **PySpark in a Jupyter notebook** and **Power BI for dashboarding**.

---

## 🛠️ Technical Workflow

The end-to-end pipeline was developed in the attached <a href="https://github.com/dspriggs-ds/imdb-analysis/blob/main/imdb_analysis.ipynb" target="_blank">Azure Databricks notebook</a>, which outlines the following steps:

1. **Ingest & Parse IMDb Files**: Using PySpark, I loaded key files like `title.basics.tsv.gz`, `title.ratings.tsv.gz`, and `title.crew.tsv.gz`, transforming them into structured DataFrames.
2. **Data Cleaning**: Filtering the dataset to focus only on full-length films with valid release years and ratings.
3. **Enrichment with Box Office Data**: Using `boxoffice_api`, I enhanced the dataset with financial figures, including gross earnings, budget, and studio metadata.
4. **Schema Design**: All data was modeled into a clean, normalized structure ready for downstream analytics in Power BI.
5. **Data Export**: Final tables were exported to Parquet format and imported into Power BI for visualization.

---

## 📊 Visualizing with Power BI

I imported the processed dataset into <a href="https://powerbi.microsoft.com/" target="_blank">Power BI</a>, where I built a report (attached as <code>IMDbAnalysis.pbix</code>) to answer questions such as:
</p>, where I built a report (attached as `IMDbAnalysis.pbix`) to answer questions such as:

* How do IMDb ratings correlate with box office performance?
* Which genres consistently deliver high revenue?
* How has the market shifted over the past two decades?

Some highlights from the dashboard:

* 🎯 A scatter plot of IMDb rating vs gross revenue
* 📈 Time series showing box office revenue and IMDb rating trends

---

## 🔍 Key Insights

* **Higher ratings don’t always translate to higher revenue**, but critically acclaimed movies tend to have longer revenue tails.
* **Action and Adventure genres** dominate the top revenue brackets, while Drama and Documentaries lead in ratings.

---

## 🔐 Challenges & Learnings

* **Data harmonization** between IMDb titles and box office entries was non-trivial — title matching and fuzzy logic were used to reconcile naming conventions.
* Working with large `.tsv.gz` files required **memory-efficient loading**, which made Spark an essential tool.
* Incorporating `boxoffice_api` calls in batch without exceeding rate limits required thoughtful retry logic and parallelization.

---

## 🚀 What's Next?

This project serves as a foundation for more advanced analytical questions, such as:

* Can we predict a movie’s success based on cast, genre, and rating?
* How do streaming-first releases compare in performance?

I’m also considering migrating the full pipeline to **Azure Databricks and Delta Lake** for greater scalability and automation.

---

## 📂 Files & Resources


<ul>
  <li>🔍 <a href="https://github.com/dspriggs-ds/imdb-analysis/blob/main/imdb_analysis.ipynb" target="_blank">Notebook: imdb_analysis.ipynb</a></li>
  <li>📊 <a href="https://github.com/dspriggs-ds/imdb-analysis/blob/main/IMDbAnalysis.pbix" target="_blank">Power BI Report: IMDbAnalysis.pbix</a></li>
  <li>📦 <a href="https://datasets.imdbws.com/" target="_blank">IMDb Datasets</a></li>
  <li>🧪 <a href="https://pypi.org/project/boxoffice-api/" target="_blank">boxoffice_api on PyPI</a></li>
</ul>

---

## 👋 Final Thoughts

This project blends **data engineering, enrichment, and visualization** to produce real-world insights from publicly available entertainment data. Whether you're a film buff, a data scientist, or both, there’s something fascinating about making the numbers behind our favorite stories come to life.

Feel free to explore the code and Power BI dashboard in my  <a href="https://github.com/dspriggs-ds/imdb-analysis" target="_blank">GitHub repo</a> — and let me know what trends you uncover!



