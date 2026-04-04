# ingest-sapodata-adls-adf

## Project Overview

This project demonstrates ingestion of SAP OData services using Azure Data Factory into ADLS Gen2 (raw layer).

## Architecture

SAP OData → Azure Data Factory → ADLS Gen2 (Raw JSON)

## Key Features

* OData-based extraction
* Pagination using $top and $skip
* Incremental loading using delta fields
* Parameterized pipelines

## Tech Stack

* Azure Data Factory
* Azure Data Lake Storage Gen2
* Azure Key Vault

## Structure

* adf/ → Pipelines, datasets, linked services
* source_config/ → OData configuration
* config/ → Environment configuration

## Security

Credentials are securely managed using Azure Key Vault.

## Output

Data is stored in ADLS Gen2 in JSON format.
