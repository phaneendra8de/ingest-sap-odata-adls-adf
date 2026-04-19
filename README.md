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

#### **Pipeline Flow**
