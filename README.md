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
