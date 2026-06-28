# Shoprenter to BigQuery ETL Sync Pipeline

A production-grade **n8n ETL automation pipeline** that synchronizes **80,000+ Shoprenter products** with **Google BigQuery** using scalable batch processing, staging tables, MERGE/UPSERT operations, soft delete reconciliation, and metadata enrichment.

Designed for reliability, scalability, and production environments, this workflow enables continuous synchronization of large e-commerce product catalogs while maintaining data integrity and preventing duplicates.

---

## ✨ Features

- 🚀 Production-ready ETL pipeline
- 📦 Synchronizes 80K+ Shoprenter products
- 🔄 Full catalog synchronization
- ⚡ Batch processing for high performance
- 🗂️ Staging table architecture
- 🔁 MERGE / UPSERT data synchronization
- 🛡️ Duplicate prevention
- 🗑️ Soft delete reconciliation
- 📈 Scalable workflow architecture
- 🔍 Metadata enrichment workflow
- 📊 Sync observability and execution tracking
- ❌ Failed record handling
- 🔐 Secure API authentication
- ☁️ Google BigQuery integration
- 🔄 Modular n8n workflows

---

# Architecture

```
                 Shoprenter API
                        │
                        ▼
             Parent n8n Workflow
                        │
          Pagination & Orchestration
                        │
                        ▼
          Product Metadata Workflow
                        │
                        ▼
         Transformation Pipeline
                        │
                        ▼
             products_staging
                        │
        Validation & Reconciliation
                        │
                        ▼
              Soft Delete Logic
                        │
                        ▼
             BigQuery MERGE
                        │
                        ▼
               products_v2
```

---

# Tech Stack

- n8n
- Google BigQuery
- Shoprenter API
- JavaScript
- SQL
- REST APIs
- HTTP Request Nodes
- Workflow Automation

---

# Workflow Components

## Parent Workflow

Responsible for:

- Full catalog import
- Pagination
- Retry logic
- Execution metadata
- Workflow orchestration
- Soft delete reconciliation
- MERGE execution

---

## Product Metadata Workflow

Responsible for:

- Product descriptions
- Manufacturer lookup
- Metadata enrichment
- Name mapping
- Description mapping

---

## Transformation Workflow

Responsible for:

- Data normalization
- Type conversion
- Stock aggregation
- Timestamp normalization
- Validation
- BigQuery staging insertion

---

# Synchronization Strategy

The pipeline follows a production-safe ETL architecture.

```
Shoprenter API

        ↓

Fetch Products

        ↓

Transform Products

        ↓

Insert Into Staging

        ↓

Validate Staging

        ↓

Soft Delete Reconciliation

        ↓

MERGE / UPSERT

        ↓

Production Table

        ↓

Cleanup Staging
```

---

# BigQuery Architecture

## Production Table

```
products_v2
```

Stores the latest version of every product.

---

## Staging Table

```
products_staging
```

Used for:

- Batch inserts
- Validation
- Reconciliation
- MERGE operations

---

## Additional Tables

- failed_products
- sync_logs

---

# Production Features

## Duplicate Prevention

Products are uniquely identified using:

```
sr_product_id
```

ensuring one row per Shoprenter product.

---

## Soft Delete Support

Products removed from Shoprenter are not deleted.

Instead they are marked as:

- is_active = FALSE
- sync_status = soft_deleted

This preserves historical data while maintaining synchronization accuracy.

---

## Metadata Enrichment

The workflow enriches products with:

- Product Name
- Short Description
- Long Description
- Manufacturer
- Measurement Unit

without affecting operational synchronization.

---

## Performance Optimizations

- Batch processing
- Staging table architecture
- MERGE instead of UPDATE
- Separate metadata workflow
- Continue-On-Fail handling
- Retry support
- Pagination
- Modular workflow design

---

# Repository Structure

```
.
├── Shoprenter → BigQuery Product Sync.json
├── transform_pipeline.json
├── set_product_name.json
├── Documentation.pdf
└── README.md
```

---

# Future Improvements

- Incremental synchronization using `dateUpdated`
- Manufacturer caching
- Retry queues
- Monitoring dashboards
- Sync analytics
- Service Account authentication
- Parallel metadata enrichment
- Automated alerting

---

# Use Cases

- Ecommerce Data Warehousing
- Business Intelligence
- Product Analytics
- Inventory Synchronization
- Enterprise ETL Pipelines
- Workflow Automation
- BigQuery Data Engineering
- Large-scale Catalog Synchronization

---

# Why This Project?

Large e-commerce catalogs can contain tens of thousands of products, making reliable synchronization challenging.

This project demonstrates how to build a scalable ETL pipeline that safely imports, transforms, validates, reconciles, and synchronizes large product datasets into Google BigQuery while maintaining production-grade reliability and data integrity.

---

## Author

**Muhammad Moiz**

Software Engineer | AI & Automation Engineer

GitHub: https://github.com/Moiz005