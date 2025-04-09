# Getting started with this repository
For the project to run, you need to deploy a few resources on Azure, and configure access between the resources. 

# Azure Resource Setup
Pre-requisites for this repository are the following resources:

## Deploy Azure Resources
1. Deploy an Azure OpenAI service
2. Deploy an Azure Storage Account (ADLS Gen2) with hierarchical namespace enabled
3. Deploy and Azure AI Search Service (if no networking requirements exist, you can choose "Free" or "Basic" tier, else "Standard" Tier S1)

## Roll out permissions
- Search Service Contributor

## Configure Resources
### Azure AI Search
- Set the API access control to "Both" -->x more infor here on [Enable roles](https://learn.microsoft.com/en-us/azure/search/search-security-enable-roles?tabs=config-svc-portal%2Cdisable-keys-portal)
![Search Security Roles](./../images/journey0-search-security.png)
- Configure the search service to use a [managed identity](https://learn.microsoft.com/en-us/azure/search/search-howto-managed-identities-data-sources?tabs=portal-sys%2Cportal-user#create-a-system-managed-identity)
![Search Service Managed Identity](./../images/journey0-search-service-managed-identity.png)

!Note: A free search service supports role-based connections to Azure AI Search, but it doesn't support managed identities on outbound connections to Azure Storage or Azure AI Vision. This level of support means you must use key-based authentication on connections between a free search service and other Azure services.

### Azure Storage Account
- Go to your Azure Storage Account and create a new container (e.g. healthplan)
- Upload the [Health Plan PDF documents](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/health-plan) to this container
![Uploaded documents](./../images/journey0-document-upload-healthplan.png)
- Go to **Access Control** and assign the **Storage Blob Data Reader** role to the search service identity
![Search role assignment](./../images/journey0-search-role-assignment.png)

### Azure OpenAI
- Go to **Access Control** and assign the **Cognitive Services OpenAI User** role to the search service identity
- Launch Azure AI Foundry portal
- Go to the Deployments tab
- Deploy an Azure OpenAI chat completion model (e.g. gpt-4o)
- Deploy an Azure OpenAI embedding model (e.g. text-embedding-ada-002)

