---
layout: default
title:  "Using Azure OpenAI, LangChain, and Azure Databricks to Understand Any Dataset with Natural Language"
date:   2025-04-30 14:10:46 -0700
categories: Azure Databricks PySpark Python
---

Working with unfamiliar datasets can be overwhelming. What does each column mean? What are the major trends? How do you quickly summarize the contents?

To solve this, I built a solution that combines the power of **Azure OpenAI**, **LangChain**, and **Azure Databricks** to help users explore arbitrary datasets from [data.gov](https://data.gov) using simple, natural language prompts. This project demonstrates a fully integrated workflow for analyzing and summarizing tabular data with LLMs—without needing to manually inspect every file.

## 🚀 Project Overview

The idea is simple: automate the analysis of any dataset using large language models, and allow users to interact with it using natural language.

Here's how it works:
- Randomly selected datasets from <a href="https://data.gov" target="_blank">data.gov</a> are ingested into Databricks.
- The data is processed and cataloged using Unity Catalog.
- Rows and metadata are sent to <a href="https://azure.microsoft.com/en-us/products/cognitive-services/openai-service/" target="_blank">Azure OpenAI</a> via the Python SDK.
- <a href="https://www.langchain.com/" target="_blank">LangChain</a> manages the flow of natural language queries and returns understandable insights.

This solution is perfect for quickly profiling and summarizing new data—especially in data cataloging, governance, or research-heavy environments.

## 🧠 Key Technologies

- **Azure OpenAI Service**: Used for GPT-powered summarization and insights.
- **LangChain**: Handles language interactions, memory, and tool orchestration.
- **Azure Databricks + Unity Catalog**: Enables scalable data preparation and secure governance.
- **data.gov Datasets**: Provides a wide variety of publicly available CSVs and JSONs.

## 📓 What’s Inside the Notebook?

The notebook (`DataSet_Analysis_Langchain_Batch.ipynb`) walks through an end-to-end pipeline:

1. **Data Import**: Downloads a random dataset from `data.gov`.
2. **Data Wrangling**: Cleans, casts, and formats the data in PySpark.
3. **Natural Language Summarization**:
   - Extracts table schema and sample rows.
   - Sends this structured information to Azure OpenAI to generate:
     - Column descriptions
     - Key takeaways
     - Potential outliers or trends
4. **Conversational Q&A**:
   - LangChain is used to simulate a chat interface.
   - Users can ask domain-specific questions like “What are the top categories?” or “Are there any missing values?”

## 🏗 Architecture Snapshot

Here’s a simplified flow:

```mermaid
graph TD
  A[Random Dataset from data.gov] --> B[Azure Databricks (Ingestion & Preprocessing)]
  B --> C[Unity Catalog (Governance)]
  C --> D[LangChain + Azure OpenAI]
  D --> E[User Natural Language Queries & Summaries]
```

## 🛠 How to Try It Yourself

1. Set up access to:
   - Azure OpenAI
   - Azure Databricks
2. Install the required Python packages:
   ```bash
   pip install azure-ai langchain pandas requests
   ```
3. Clone the repo and run the notebook:
   ```bash
   git clone https://github.com/<your-username>/natural-language-data-understanding.git
   cd natural-language-data-understanding
   ```
4. Open `DataSet_Analysis_Langchain_Batch.ipynb` in Azure Databricks and run each cell to explore.

## 🧪 Use Cases

- Rapid profiling for data cataloging or metadata tagging
- Domain-specific exploration for research analysts
- Helping non-technical stakeholders understand raw datasets
- LLM-powered data exploration chatbots

## 🙌 Acknowledgements

- <a href="https://azure.microsoft.com/en-us/products/databricks/" target="_blank">Azure Databricks</a> for the robust analytics platform
- <a href="https://data.gov" target="_blank">data.gov</a> for open and diverse datasets
- <a href="https://openai.com/blog/openai-api" target="_blank">Azure OpenAI</a> for enabling intuitive data understanding
- <a href="https://www.langchain.com/" target="_blank">LangChain</a> for building seamless language agent pipelines