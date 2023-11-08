[Virtual Network Service Endpoints](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-service-endpoints-overview)

Virtual Network (VNet) service endpoint provides secure and direct connectivity to Azure services over an optimized route over the Azure backbone network. Endpoints allow you to secure your critical Azure service resources to only your virtual networks. Service Endpoints enables private IP addresses in the VNet to reach the endpoint of an Azure service without needing a public IP address on the VNet.

Service endpoints are available for the following Azure services and regions. The _Microsoft.*_ resource is in parenthesis. Enable this resource from the subnet side while configuring service endpoints for your service:

**Generally available**

- **[Azure Storage](https://learn.microsoft.com/en-us/azure/storage/common/storage-network-security?toc=/azure/virtual-network/toc.json#grant-access-from-a-virtual-network)** (_Microsoft.Storage_): Generally available in all Azure regions.
- **[Azure Storage cross-region service endpoints](https://learn.microsoft.com/en-us/azure/storage/common/storage-network-security?toc=/azure/virtual-network/toc.json#azure-storage-cross-region-service-endpoints)** (_Microsoft.Storage.Global_): Generally available in all Azure regions.
- **[Azure SQL Database](https://learn.microsoft.com/en-us/azure/azure-sql/database/vnet-service-endpoint-rule-overview?toc=%2fazure%2fvirtual-network%2ftoc.json)** (_Microsoft.Sql_): Generally available in all Azure regions.
- **[Azure Synapse Analytics](https://learn.microsoft.com/en-us/azure/azure-sql/database/vnet-service-endpoint-rule-overview?toc=%2fazure%2fvirtual-network%2ftoc.json)** (_Microsoft.Sql_): Generally available in all Azure regions for dedicated SQL pools (formerly SQL DW).
- **[Azure Database for PostgreSQL server](https://learn.microsoft.com/en-us/azure/postgresql/howto-manage-vnet-using-portal?toc=/azure/virtual-network/toc.json)** (_Microsoft.Sql_): Generally available in Azure regions where database service is available.
- **[Azure Database for MySQL server](https://learn.microsoft.com/en-us/azure/mysql/howto-manage-vnet-using-portal?toc=/azure/virtual-network/toc.json)** (_Microsoft.Sql_): Generally available in Azure regions where database service is available.
- **[Azure Database for MariaDB](https://learn.microsoft.com/en-us/azure/mariadb/concepts-data-access-security-vnet)** (_Microsoft.Sql_): Generally available in Azure regions where database service is available.
- **[Azure Cosmos DB](https://learn.microsoft.com/en-us/azure/cosmos-db/how-to-configure-vnet-service-endpoint?toc=/azure/virtual-network/toc.json)** (_Microsoft.AzureCosmosDB_): Generally available in all Azure regions.
- **[Azure Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/general/overview-vnet-service-endpoints)** (_Microsoft.KeyVault_): Generally available in all Azure regions.
- **[Azure Service Bus](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-service-endpoints?toc=/azure/virtual-network/toc.json)** (_Microsoft.ServiceBus_): Generally available in all Azure regions.
- **[Azure Event Hubs](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-service-endpoints?toc=/azure/virtual-network/toc.json)** (_Microsoft.EventHub_): Generally available in all Azure regions.
- **[Azure Data Lake Store Gen 1](https://learn.microsoft.com/en-us/azure/data-lake-store/data-lake-store-network-security?toc=/azure/virtual-network/toc.json)** (_Microsoft.AzureActiveDirectory_): Generally available in all Azure regions where ADLS Gen1 is available.
- **[Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/app-service-ip-restrictions)** (_Microsoft.Web_): Generally available in all Azure regions where App service is available.
- **[Azure Cognitive Services](https://learn.microsoft.com/en-us/azure/ai-services/cognitive-services-virtual-networks?tabs=portal)** (_Microsoft.CognitiveServices_): Generally available in all Azure regions where Azure AI services are available.

**Public Preview**

- **[Azure Container Registry](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-vnet)** (_Microsoft.ContainerRegistry_): Preview available in limited Azure regions where Azure Container Registry is available.