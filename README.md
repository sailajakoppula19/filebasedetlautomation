# Azure Data Factory - File-Based ETL Automation

## Project Overview
This project automates the ingestion and processing of multiple CSV files using Azure Data Factory (ADF), Azure Data Lake Storage Gen2, and Azure SQL Database.

The pipeline dynamically identifies files, loads data into staging tables, performs insert and update operations using SQL stored procedures, logs processing details, and archives successfully processed files.

## Technologies Used
- Azure Data Factory (ADF)
- Azure Data Lake Storage Gen2
- Azure SQL Database
- Stored Procedures
- Schedule Triggers

## Architecture
The ETL pipeline follows this workflow:

**Azure Storage → Get Metadata → ForEach → Copy Data → SQL Staging Tables → Stored Procedure → Target Tables → Audit Log → Archive Files → Delete Source Files**

## Source Files
The `source` container contains these sample CSV files:

- `customers.csv`
- `products.csv`
- `sales.csv`
- `employees.csv`

## Pipeline Activities

1. **Get Metadata:** Retrieves the list of files from the source container.
2. **ForEach:** Processes each file dynamically.
3. **Copy Data:** Loads CSV data into the corresponding SQL staging table.
4. **Stored Procedure:** Uses SQL `MERGE` logic to insert new records and update existing records.
5. **Audit Logging:** Stores the filename, target table, status, and rows copied in `ETL_Audit_Log`.
6. **Archive File:** Copies successfully processed files to the `processed` container.
7. **Delete Source File:** Deletes the original file after successful archival.

## Database Tables

### Target Tables
- `Customers`
- `Products`
- `Sales`
- `Employees`

### Staging Tables
- `Stg_Customers`
- `Stg_Products`
- `Stg_Sales`
- `Stg_Employees`

### Audit Table
- `ETL_Audit_Log`

## Key Features
- Metadata-driven file processing
- Parameterized datasets and dynamic expressions
- Automated CSV ingestion
- SQL staging and upsert processing
- ETL audit logging
- File archival and source cleanup
- Scheduled pipeline execution

## How to Set Up
1. Create an Azure Storage account and the `source` and `processed` containers.
2. Upload the sample CSV files into the `source` container.
3. Create an Azure SQL Database and the required target, staging, and audit tables.
4. Create the required SQL stored procedures.
5. Configure linked services and parameterized datasets in Azure Data Factory.
6. Build the pipeline using the activities described above.
7. Publish and test the pipeline.
8. Configure a schedule trigger for automated execution.

## Expected Outcome
The pipeline processes available CSV files, loads their records into the appropriate SQL target tables, records successful executions in the audit table, and archives processed files.

## Learning Outcomes
- Designing end-to-end ETL pipelines
- Working with Azure Data Factory activities and expressions
- Integrating Azure Storage with Azure SQL Database
- Implementing SQL upsert logic
- Automating data ingestion and file management

## Author
Azure Data Engineering Project
