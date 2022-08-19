# azure_ap_morgan

## Process
1) Internal application sends CSV files into Azure Data Lake Storage
2) The file needs to be valdiated to check for duplicate rows - if duplicate rows exist the file needs to be rejected (sent to reject folder). File also needs to be validated to check the date format is correct. This is based on a format stored in Azure SQL -if this format is not correct the file needs to be rejected (sent to reject folder).
3) If the file passes all checks it can be passed to the staging folder.
4) The passed files will be writen as the Delta Table in Azure Databricks.

<img width="394" alt="Project_Archiecture" src="https://user-images.githubusercontent.com/67950889/185568589-fe3e1532-6b66-4ca5-aeaf-7f1cea5c520c.png">

## Project Learning Points: 
- architect, Design and build a real-world enterprise level data platform solution including multiple services.
- design solution using ADF, Databricks, pyspark, Azure Data lake storage Gen 2 (ADLS), Azure SQL Server
- build a real-world data pipeline in Azure Data Factory (ADF). 
- transform data using Databricks Notebook Activity in Azure Data Factory (ADF) and load into Azure Data Lake Storage Gen2
- production ready pipelines and good practices and naming standards
- integrate Databricks with ADF and send the response back from Databricks to ADF
- create Azure Key vault and use it to store secret credentials and SAS token
- connect the Azure SQL Database and Databricks cluster using the Key Vault
- mount he Azure Storage Account in the Databricks to access the files and preform transformation on it.
- transform the data in the Azure Databricks using the pyspark.
