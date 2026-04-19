SAP OData Ingestion using Azure Data Factory
Overview
This repository contains a production-ready framework for ingesting SAP OData services into Azure Data Lake Storage Gen2 (ADLS) using Azure Data Factory (ADF).

It supports two key pipelines:

pl_customers_full_load_odata → full dataset ingestion of customers

pl_orders_incremental_odata → incremental ingestion of orders using watermark-based logic

Architecture
SAP OData → ADF (REST Connector) → ADLS Gen2 (Raw Layer)

This design ensures scalability, auditability, and separation of responsibilities between full and incremental loads.

Storage Layout
Code
raw/
├── customers/
│   ├── full/
│   │   └── load_date=YYYY-MM-DD/
│   │       └── customers.json
│
├── orders/
│   ├── incremental/
│   │   └── load_date=YYYY-MM-DD/
│   │       └── orders_HHMMSS.json
│
└── config/
    ├── watermark_orders.json
    └── dummy.json
Pipelines
pl_customers_full_load_odata
Loads the complete customer dataset

Uses OData pagination ($.d.__next)

No filters applied

pl_orders_incremental_odata
Fetches only new or updated orders

Flow:

Lookup watermark

Copy incremental orders ($filter=OrderDate gt last_watermark)

Capture current timestamp

Update watermark file

Incremental Logic
$filter=OrderDate gt last_watermark

Ensures only records newer than the last processed timestamp are ingested

Pagination handled automatically via $.d.__next

Watermark Management
Location: raw/config/watermark_orders.json

Initial setup:  
{ "last_watermark": "1997-01-01T00:00:00" }

Update process:

Uses dummy source file

Adds dynamic column (last_watermark)

