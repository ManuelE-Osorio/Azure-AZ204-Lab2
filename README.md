# Azure-AZ204-Lab2
Azure AZ 204 Lab 02: Implement task processing logic by using Azure Functions

## Instructions

### 1. Setup Azure Storage

To create the storage account the following commands where used.

```bash
tenant=<tenant-id>
az login --tenant $tenant
resource-group-name=<resource-group-name>
az group create --location <location name> --name $resource-group-name
storage-account-name=<storage-account-name>
az storage account create --name $storage-account-name  --resource-group <resource group name> --sku Standard_LRS
az storage account show-connection-string --name $storage-account-name -g <resource group name>
connection-string=<connection-string>
container-name=<container-name>
az storage container create --name $container-name --connection-string $connection-string --resource-group $resource-group-name
az storage blob upload --connection-string $connection-string --container-name $container-name --file <file path>
```

When the account is created, one can specify the following:

```
[--access-tier {Cold, Cool, Hot, Premium}]
[--kind {BlobStorage, BlockBlobStorage, FileStorage, Storage, StorageV2}]
[--public-network-access {Disabled, Enabled, SecuredByPerimeter}]
```

### 2. Setup Azure Functions

To create the functions using the Azure CLI, the following commands were used:


```bash
planname=<plan-name>
az appservice plan create --name $planname --resource-group $resourcegroup --sku B1 --is-linux
functionname=<function-name>
az functionapp create --name $functionname --resource-group $resourcegroup --storage-account $storageaccount --os-type Linux --runtime dotnet-isolated --runtime-version 8 --plan $planname
az functionapp deployment source config-zip -g $resorucegroup -n $functionname --src <zipFilePathLocation>
```

The deployment can be made within visual studio. The functions are diferent from the lab example, they had to be refactored to async since the flag AllowSynchronousIO is set to false by default.
