# FMCG Data Lakehouse Pipeline

### End-to-End Data Engineering Project Using AWS S3, Databricks, PySpark, and Delta Lake

## 📌 Project Overview

This project focuses on building a data engineering pipeline to process FMCG data and consolidate data from Sports Bar with the existing Atlon data.

The pipeline uses Amazon S3 for cloud storage and Databricks with Apache Spark and PySpark for data processing. It follows the Medallion Architecture (Bronze, Silver, and Gold) to organize raw, transformed, and business-ready data.

The project also covers dimension and fact data processing, incremental loading of daily order files, and data consolidation using merge and upsert concepts.

## 🎯 Business Problem

Atlon acquired Sports Bar and needed to integrate its data with the existing Atlon data platform.

The main challenges were:

- Managing data received in multiple CSV files.
- Processing customer, product, pricing, and order data.
- Cleaning and transforming raw data.
- Handling daily order files and incremental data loads.
- Consolidating Sports Bar data with existing Atlon Gold data.
- Preparing structured data for business analytics and reporting.

## 🎯 Project Objectives

- Store source CSV files in Amazon S3.
- Process datasets using Databricks and PySpark.
- Implement the Bronze, Silver, and Gold data layers.
- Process dimension and fact data.
- Support incremental processing of daily order files.
- Understand merge and upsert operations for data integration.
- Prepare consolidated data for downstream analytics.

## 🏗️ Architecture

The pipeline follows this high-level data flow:

**Sports Bar CSV Files → Amazon S3 → Databricks → Bronze Layer → Silver Layer → Gold Layer → Data Consolidation with Atlon → Analytics and Reporting**

The architecture consists of the following components:

1. **Amazon S3:** Stores the source CSV files.
2. **Databricks:** Provides the environment for data engineering and processing.
3. **Bronze Layer:** Stores raw ingested data.
4. **Silver Layer:** Contains cleaned and transformed data.
5. **Gold Layer:** Contains business-ready datasets.
6. **Data Consolidation:** Combines processed Sports Bar data with existing Atlon data.
7. **Analytics:** Enables downstream reporting and analysis using consolidated data.

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Amazon S3 | Cloud storage for source CSV files |
| Databricks | Data engineering and processing platform |
| Apache Spark | Distributed data processing |
| PySpark | Data transformation using Python |
| Spark SQL | SQL-based data processing and querying |
| Delta Lake | Table storage and merge operations, where configured |
| Databricks Jobs | Workflow orchestration, where configured |
| GitHub | Source code management and documentation |

## 📂 Data Sources

The project uses FMCG-related datasets containing customer, product, pricing, and order information.

| Dataset | Description |
|---|---|
| `customers.csv` | Customer information |
| `products.csv` | Product details |
| `gross_price.csv` | Product pricing information |
| `orders_*.csv` | Order records, potentially separated into daily files |

Example source file organization:

```text
sportsbar-data/
├── customers/
│   └── customers.csv
├── products/
│   └── products.csv
├── gross_price/
│   └── gross_price.csv
└── orders/
    ├── orders_2025_07_01.csv
    ├── orders_2025_07_02.csv
    └── orders_2025_07_03.csv
```

The structure above is an example. Actual folder names and file paths depend on the S3 bucket configuration.

## 🥉 Medallion Architecture

The project follows the Medallion Architecture concept to organize data processing into three layers.

### 1. Bronze Layer — Raw Data

The Bronze layer is the initial stage of the data pipeline.

- Ingests source data.
- Maintains raw data for downstream processing.
- Provides a starting point for data transformations.

### 2. Silver Layer — Cleaned and Transformed Data

The Silver layer improves data quality and consistency.

- Cleans and transforms source data.
- Standardizes data formats where required.
- Prepares datasets for further processing.

### 3. Gold Layer — Business-Ready Data

The Gold layer contains processed data prepared for business use.

- Organizes data for downstream consumption.
- Supports dimension and fact table structures.
- Provides a target layer for data consolidation and analytics.

## ⚙️ Project Workflow

### Step 1: Source Data Preparation

Prepare the customer, product, gross price, and order CSV files.

### Step 2: Upload Data to Amazon S3

Upload the source files to the appropriate S3 bucket and organize them into suitable folders.

### Step 3: Configure Databricks Access

Configure the required permissions and connectivity so Databricks can access the source data.

### Step 4: Dimension Data Processing

Process dimension datasets such as customers, products, and gross prices using the transformations defined in the notebooks.

### Step 5: Fact Data Processing

Process order data and apply the required transformations to prepare fact data.

### Step 6: Gold Layer Preparation

Create business-ready datasets from the processed data according to the pipeline logic.

### Step 7: Data Consolidation

Combine Sports Bar Gold data with existing Atlon Gold data using the configured consolidation logic.

### Step 8: Incremental Data Processing

Process newly arriving order files according to the incremental-loading implementation.

### Step 9: Pipeline Orchestration

Use Databricks Jobs for scheduling and orchestration if configured in the environment.

## 🔄 Incremental Data Loading

Order data may arrive in separate daily files instead of a single consolidated file.

For example:

```text
orders_2025_07_01.csv
orders_2025_07_02.csv
orders_2025_07_03.csv
```

Incremental loading processes new data as it arrives rather than requiring the entire historical dataset to be processed on every run.

A typical incremental workflow includes:

1. Identify newly available order files.
2. Read the new data.
3. Apply required transformations.
4. Write the processed records to the target table.
5. Track processed data to avoid unintended duplicate processing, where implemented.

The exact incremental strategy depends on the pipeline implementation.

## 🔗 Data Consolidation and Upsert

The business objective is to integrate Sports Bar data with existing Atlon data.

An **upsert** combines two operations:

- **Update:** Update an existing record when its matching key is found.
- **Insert:** Insert a new record when its matching key does not exist.

Delta Lake supports `MERGE` operations for implementing upsert logic when the source and target tables are configured appropriately.

The matching keys and update conditions depend on the relevant datasets and business requirements.

## 📁 Repository Structure

A suggested repository structure is:

```text
FMCG-Data-Lakehouse-Pipeline/
│
├── README.md
├── .gitignore
│
└── notebooks/
    ├── setup/
    ├── dimension_data_processing/
    ├── fact_data_processing/
    └── incremental_load/
```

Keep only the folders and files that actually exist in your repository.

## ▶️ How to Run

This project requires an AWS and Databricks environment.

1. Set up an AWS S3 bucket.
2. Upload the required source CSV files.
3. Configure secure access from Databricks to S3.
4. Import the project notebooks into Databricks.
5. Configure source paths and target table settings.
6. Execute the notebooks in the correct dependency order.
7. Validate the processed data in the target tables.
8. Run the consolidation and incremental-loading workflows where implemented.
9. Configure Databricks Jobs if workflow orchestration is part of your setup.

### Prerequisites

- An AWS account with appropriate S3 permissions.
- A Databricks workspace with suitable compute access.
- Access to the required source datasets.
- Permissions to read source data and write target tables.

## 📚 Key Learning Outcomes

This project provides practical exposure to:

- Cloud data storage using Amazon S3.
- Distributed processing using Apache Spark.
- Data transformation using PySpark and Spark SQL.
- Medallion Architecture.
- Dimension and fact data processing.
- Incremental data loading concepts.
- Data consolidation and upsert concepts.
- Delta Lake and Databricks workflows.
- GitHub documentation and source code management.

## 👩‍💻 Author

**Rupali Srivastava**

MCA Student | Aspiring Data Engineer


