# Quickstart Experience to Setup your first Index
In this quickstart, you use the Import and vectorize data wizard in the Azure portal to get started with integrated vectorization. The wizard chunks your content and calls an embedding model to vectorize content during indexing and for queries.

## Setup
- The initial setup has already been completed
- Start to follow the instrctions from "Start the wizard" onwards ([Vector Search wizard](https://learn.microsoft.com/en-us/azure/search/search-get-started-portal-import-vectors?tabs=sample-data-adlsgen2%2Cmodel-aoai%2Cconnect-data-adlsgen2))

- Go to your Azure AI Search service and select **Import and vectorize data** on the overview page

![Import and vectorize](./../images/journey0-import-and-vectorize.png)

- Choose the storage account and the container that provide the data

![Select Azure Data Lake Storage Gen2](./../images/journey0-import-adls-gen2.png)

- Configure the storage account connection, especially specify that managed identity authentication shall be used

![Configure Storage connection](./../images/journey0-configure-storage-connection.png)