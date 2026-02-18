# End-to-End Azure Data Engineering Project: Adventure Works

## Project Overview
This project demonstrates a complete, real-world data engineering solution built on the **Azure Cloud Platform**. It follows the **Medallion Architecture**, moving data from raw ingestion to a serving layer ready for business intelligence. The solution focuses on **real-time scenarios** frequently encountered in the industry, such as dynamic pipeline orchestration and the implementation of a **Lakehouse** architecture.

## Architecture
The project follows a three-tier data maturation process:
1.  **Bronze (Raw) Layer:** Data is ingested from an external API and stored in its original format.
2.  **Silver (Transformed) Layer:** Data is cleansed and transformed using Big Data processing tools.
3.  **Gold (Serving) Layer:** Transformed data is organized into a data warehouse/lakehouse structure for stakeholder consumption.

## Technologies Used
*   **Azure Data Factory (ADF):** Used for orchestration and building **Dynamic Pipelines** using parameters and for-each loops to handle multiple tables efficiently.
*   **Azure Data Lake Gen2 (ADLS):** Acts as the centralized storage solution for the Bronze, Silver, and Gold zones.
*   **Azure Databricks:** A Spark-based analytics platform used for high-performance data transformations using **PySpark**.
*   **Azure Synapse Analytics:** Utilized for data warehousing and implementing the **Lakehouse concept** through Serverless SQL pools.
*   **Power BI:** Connected to the Gold layer for end-to-end data visualization and reporting.
*   **Azure Entra ID (formerly Active Directory):** Used for managing security through **Service Principals** and **Managed Identities** to allow secure access between resources.

## Dataset: Adventure Works
The project utilizes the **Adventure Works** dataset, which simulates a complex business environment with multiple interlinked tables.
*   **Fact Tables:** Sales data (2015–2017) and Returns data.
*   **Dimension Tables:** Customers, Products, Product Categories, Subcategories, Calendar, and Territories.
*   **Source Format:** CSV files accessed via the **GitHub API** to simulate real-world API ingestion.

## Implementation Details

### 1. Ingestion (ADF)
Instead of static "hard-coded" pipelines, this project implements **dynamic ingestion**. By using a JSON configuration file and ADF parameters, a single pipeline can iterate through a list of tables to fetch data from the GitHub API and land it in the Bronze container.

### 2. Transformation (Databricks)
Using PySpark, the data undergoes several professional-level transformations:
*   **Schema Enforcement:** Using `inferschema` and defining types for accurate processing.
*   **Data Cleansing:** Handling date formats, splitting strings, and concatenating columns (e.g., creating a `Full Name` from prefix, first, and last names).
*   **Storage Optimization:** Writing transformed data to the Silver layer in **Parquet format**, which is optimized for analytical queries.

### 3. Serving & Lakehouse (Synapse)
The project implements a **Logical Data Warehouse** using Synapse Serverless SQL pools. 
*   **Openrowset:** Used to query Parquet files directly from the Data Lake as if they were traditional SQL tables.
*   **Views & External Tables:** Creation of a gold-layer schema containing views and external tables for final reporting, ensuring data is served efficiently without the high cost of traditional physical storage.

### 4. Visualization (Power BI)
A connection is established between Synapse and Power BI using **SQL Endpoints**. This allows for the creation of interactive dashboards that reflect the matured data from the Gold layer.

## Setup Requirements
*   **Azure Subscription:** (Free trial account is sufficient).
*   **Resource Group:** To house all project resources (ADF, ADLS, Databricks, Synapse).
*   **Permissions:** Proper Role-Based Access Control (RBAC) such as **Storage Blob Data Contributor** must be assigned to the user and the Synapse Managed Identity.
