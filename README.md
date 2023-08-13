## Azure AP Morgan Data Platform Project

### Overview

This project focuses on building an end-to-end data platform solution using Azure services, aimed at processing CSV files received from an internal application and ensuring their quality and accuracy before being integrated into the data ecosystem.

### Process

1. CSV files are sent by an internal application to Azure Data Lake Storage.
2. Validation checks are performed on the files:
   - Duplicate rows are identified, and if found, files are moved to a rejection folder.
   - Date formats are verified according to the required format for Azure SQL database. Incorrect formats lead to rejection.
3. Successfully validated files are moved to a staging folder.
4. These files are then transformed into a Delta Table using Azure Databricks.

![Project Architecture](https://user-images.githubusercontent.com/67950889/185568589-fe3e1532-6b66-4ca5-aeaf-7f1cea5c520c.png)

### Tools and Technologies

This project leverages several Azure services and tools:
- Azure Data Factory (ADF)
- Databricks
- Azure Data Lake Storage Gen2 (ADLS)
- Azure SQL Server
- Azure Key Vault

### Databricks Notebook

The Databricks notebook utilizes PySpark to:
- Validate column names and data formats against an Azure SQL database.
- Move validated files to Azure Data Lake Storage Gen2 (passing files to the landing folder and failed files to the rejected folder).
- Create a Databricks mount for linking Azure Data Lake cloud storage to the Databricks workspace.

### Security and Credentials

Azure Key Vault is employed to securely store sensitive credentials and storage SAS token. This ensures a safe and controlled connection between the Azure SQL database and the Databricks cluster.

### Automation

An Azure Data Factory trigger is set up to initiate the pipeline whenever a new .csv file is added to the storage container.

#### Trigger Parameters

- ADF Trigger: Activates the pipeline upon addition of a new .csv file to the storage container.
- Trigger Run Parameters: `FileName = @triggerBody().fileName`
- Azure Databricks Parameters: `FileName @pipeline().parameters.fileName`

By adopting the above approach, the Databricks cluster dynamically reads the FileName from the storage container through the ADF pipeline, ensuring smooth execution.

This project strives to provide a robust and scalable solution for handling data ingestion, validation, and integration within an enterprise-level data platform.
