# Ingest From Dataverse

This repository provides a solution to extract data from **Microsoft Dataverse** using **Azure Data Factory (ADF)** and **Python**.

The workflow:
- **ADF pipeline** orchestrates the process and triggers the notebooks.
- **Python notebooks** handle authentication (using Azure Key Vault secrets) and perform the Dataverse API queries.
- Data extraction is fully customizable via a `.csv` configuration file.

Since the notebooks are supposed to be used in **Azure Databricks**, you will see the use of different widgets, widly explaneted in each notebook. The serve as dynamical parameters, and they are also defined in ADF, which is the main orchestrator.

---

## 📂 Repository Structure

- **`dataverse_lookup.ipynb`** – Connects to Dataverse, reads secrets from Azure Key Vault, and retrieves the requested data.
- **`landing_to_raw_dataverse.ipynb`** – Take the parquet file created in ADF after the lookup and create the raw tables.
- **AzureDataFactory** a folder with all ADF related content, in particular:
  - **`pl-dataverse-ingestion.json`** – ADF pipeline definition to orchestrate the process and download the tables from dataverse into the landing zone of Azure.
  - **`dataverse-ingestion.png`** - A png for showing how the pipeline should look like. 
- **`config.csv`** – Specifies which tables and columns to download.

---

## ⚙️ Requirements

- **Python 3.8+**
- **Azure Subscription** with:
  - Azure Data Factory
  - Azure Key Vault with all secrets related to Dataverse (tenant-id, app-id, app-secret)
  - Access to Dataverse
  - Environment in the key vault (I have stored the letter of the environment in the key vault in order to dynamically recreate my default catalog in Azure)
