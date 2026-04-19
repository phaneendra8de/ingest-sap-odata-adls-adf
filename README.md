# SAP OData Ingestion using Azure Data Factory

## **Overview**
This repository provides a scalable framework for ingesting **SAP OData services** into **Azure Data Lake Storage Gen2 (ADLS)** using **Azure Data Factory (ADF)**.

### **Key Features**
- **Full load ingestion** for bulk datasets  
- **Incremental ingestion** using watermark logic  
- **OData pagination handling**  
- **Dynamic partitioning in ADLS**  
- **Reusable and parameterized datasets**

---

## **Architecture**
SAP OData → ADF (REST Connector) → ADLS Gen2 (Raw Layer)

---

## **Storage Structure**
'''
raw/
├── customers/
│ └── full/
│ └── load_date=YYYY-MM-DD/
│ └── customers.json
│
├── orders/
│ └── incremental/
│ └── load_date=YYYY-MM-DD/
│ └── orders_HHMMSS.json
│
└── config/
├── watermark_orders.json
└── dummy.json
'''

---

## **Pipelines**

### **pl_customers_full_load_odata**
- Performs **full data ingestion** of customers  
- Uses OData pagination (`$.d.__next`)  
- No filters applied  
- Writes data to partitioned ADLS path  

---

### **pl_orders_incremental_odata**
- Performs **incremental ingestion** of orders  
- Uses **watermark-based filtering**

---

## **Summary**

This project demonstrates a robust data ingestion framework for integrating **SAP OData services** with **Azure Data Lake Storage Gen2** using **Azure Data Factory**.

- Implemented **full load ingestion** for customers with OData pagination  
- Designed **incremental ingestion pipeline** for orders using watermark logic  
- Enabled efficient data processing using:
  - Dynamic OData filtering (`$filter`)
  - Automatic pagination (`$.d.__next`)
- Maintained **state management** using ADLS-based watermark file  
- Ensured **scalable and reusable design** with parameterized datasets and pipelines  

This approach supports **reliable, incremental data ingestion**, minimizes data duplication, and aligns with **industry best practices for modern data engineering pipelines**.
