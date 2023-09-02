#Azure AP Morgan Data Platform Project

##Overview

The Azure AP Morgan Data Platform Project is a comprehensive data processing solution designed to manage CSV files originating from an internal application. This project includes validation checks and an organized sorting mechanism to efficiently handle incoming data.

##Process
- Data Ingestion: CSV files are transmitted by an internal application and are stored within Azure Data Lake Storage.
- Validation and Sorting: The project employs a Databricks Python notebook to perform filename-based filtering and validation of date formats within the selected files. The validation process ensures data integrity and accuracy.
- Folder Management: Depending on the validation outcome, the files are systematically sorted into distinct folders:
- Files that pass validation are moved to the staging folder for further processing.
- Files that fail validation are redirected to the rejection folder for manual review and resolution.

##Tools and Technologies

The project capitalizes on the capabilities of various Azure services and tools:
- Azure Data Factory (ADF)
- Databricks
- Azure Data Lake Storage Gen2 (ADLS)
- Azure SQL
- Azure Key Vault

![Project Architecture](https://user-images.githubusercontent.com/67950889/185568589-fe3e1532-6b66-4ca5-aeaf-7f1cea5c520c.png)

##Implementation

The provided Python script carries out essential tasks:
- Filters files based on predefined filename criteria.
- Executes date format validation within the selected files.
- Manages the transfer of files to relevant directories based on validation outcomes.

It’s important to note that this code snippet does not directly interact with Delta tables.

##Security and Automation

The secure storage of sensitive credentials is ensured through Azure Key Vault, establishing a trusted connection between the Azure SQL database and the Databricks cluster. Automation is achieved via an Azure Data Factory trigger, which automates the pipeline execution upon the addition of new .csv files to the storage container.

##Databricks Notebook Reference

For additional insight and reference, the incoming_data_check Databricks notebook should be consulted. This notebook includes data validation and sorting actions.

##Conclusion

The Azure AP Morgan Data Platform Project showcases a robust solution for handling incoming CSV files with a focus on validation and efficient data sorting. 
