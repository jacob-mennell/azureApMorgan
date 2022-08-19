# Azure AP Morgan Data Platform Project

### Process
1) Internal application sends CSV files into Azure Data Lake Storage
2) The file needs to be valdiated to check for duplicate rows - if duplicate rows exist the file needs to be rejected (sent to reject folder). File also needs to be validated to check the date format is correct. This is based on a format stored in Azure SQL -if this format is not correct the file needs to be rejected (sent to reject folder).
3) If the file passes all checks it can be passed to the staging folder.
4) The passed files will be writen as the Delta Table in Azure Databricks.

<img width="394" alt="Project_Archiecture" src="https://user-images.githubusercontent.com/67950889/185568589-fe3e1532-6b66-4ca5-aeaf-7f1cea5c520c.png">

### Project Learning Points: 

The aim to is to architect design and build an nterprise level data platform solution.

A pipeline has been created in Azure Data Factory (ADF) using Databricks, Azure Data lake storage Gen 2 (ADLS), Azure SQL Server. 

The databricks notebook uses PySpark and takes a .csv file from Azure Data Lake Storage Gen2 and validates the Column Name and Column Data Format against entries within an Azure SQL database. After validation, files are sent toA zure Data Lake Storage Gen2 storage, passed files to the landing folder and failed files to the reejcted folder. A Databricks mount has been created to link the Azure Data Lake cloud storage to the Databricks workspace. 

Azure Key Vault has been used to store secret credentials and the storage SAS token. The Key Vault stored credential details that enable connection between the Azure SQL database and Databricksc cluster.

A trigger has been created in ADF to execute the pipeline when a new .csv file is added to the storage container. 

Trigger Parameters
FileName = @triggerBody().fileName

Azure Databricks Parameters (read file from the trigger)
FileName @pipeline().parameters.fileName

# get the file name from the adf (first cell of .ipynb notebook)
fileName = dbutils.widgets.get('fileName')

The above ensures the Databricks cluster reads the FileName from the storage container dynamically through the ADF pipeline. 
