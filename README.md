# Spark E-Commerce Data Processing Project

## Overview
This project implements a data lakehouse architecture for processing e-commerce data using Apache Spark and the medallion architecture (Bronze, Silver, Gold layers). It handles both historical full loads and incremental data updates for various e-commerce entities including customers, products, orders, shipments, and returns.

![Project Architecture](resources/project_architecture.png)

## Project Structure

### 0_data/
Contains raw e-commerce data organized by entity type:
- **ecomm-raw-data/historical-full-load/**: Initial full dataset for brands, categories, customers, dates, order items, products, etc.
- **ecomm-raw-data/incremental-load/**: Incoming incremental data for order items, returns, and shipments.

### 1_setup/
Setup notebooks for initializing the Databricks environment:
- `setup_catalog.ipynb`: Configures the catalog and database structure
- `setup_raw_external_volume.ipynb`: Sets up external volumes for raw data access

### 2_medallion_processing_dim/
Dimension table processing notebooks following the medallion architecture:
- `1_dim_bronze.ipynb`: Raw data ingestion and initial cleansing
- `2_dim_silver.ipynb`: Data standardization and enrichment
- `3_dim_gold.ipynb`: Final dimension tables with business logic

### 3_medallion_processing_fact/
Fact table processing notebooks:
- `1_fact_bronze.ipynb`: Raw fact data ingestion
- `2_fact_silver.ipynb`: Fact data cleansing and validation
- `3_fact_gold.ipynb`: Final fact tables with aggregations
- `4_daily_summary.ipynb`: Daily summary reports and metrics

### 4_dashboarding/
Reserved for dashboard development and visualization notebooks.

### 5_exercise/
Additional exercises and examples.

### resources/
Supporting files and documentation.

## Prerequisites
- Databricks workspace with Spark runtime
- Access to cloud storage (e.g., Azure Data Lake Storage, AWS S3, or Google Cloud Storage)
- Appropriate cluster configuration for data processing workloads

## Setup Instructions

1. **Environment Setup**:
   - Run `1_setup/setup_catalog.ipynb` to create the necessary catalogs and databases
   - Run `1_setup/setup_raw_external_volume.ipynb` to configure external volume access

2. **Data Ingestion**:
   - Ensure raw data is available in the `0_data/` directory structure
   - Configure external volumes to point to your data storage location

3. **Processing Pipeline**:
   - Execute dimension processing notebooks in order (2_medallion_processing_dim/)
   - Execute fact processing notebooks in order (3_medallion_processing_fact/)

## Data Flow
1. **Bronze Layer**: Raw data ingestion with minimal transformation
2. **Silver Layer**: Data cleansing, deduplication, and standardization
3. **Gold Layer**: Business-ready tables with aggregations and metrics

## Key Features
- Incremental data processing for real-time updates
- Medallion architecture for data quality and performance
- Support for multiple e-commerce entities
- Daily summary reporting
- Scalable Spark-based processing

## Usage
Execute the notebooks in the following order:
1. Setup notebooks (1_setup/)
2. Dimension processing (2_medallion_processing_dim/)
3. Fact processing (3_medallion_processing_fact/)

Final Dashboard

![Dashboard](resources/ecommerce_analytics_report.jpg)

Monitor job runs and data quality through Databricks job scheduler.