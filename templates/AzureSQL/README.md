# Azure SQL platform service

The service consits an SQL server and SQL databases. The SQL server does not determine the performance od the databases running in it. The SQL server is just a logical unit that dictates the admin user credentials for all of the databases and the login IP and hostname and the networking rules. The performance of the databases can be set individually. The performance of the databases is defined in Database Transfer Units (DTU).

[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FCloudDirect%2FARMLab%2Fmaster%2Ftemplates%2FAzureSQL%2Fazuredeploy.json)

## Azure CLI deployment

The `az sql server` command is used with parameters to create an SQL server.

### SQL server creation:

```
az sql server create --name <serverName> --resource-group <resourceGroupName> \
--location <location> --admin-user <adminUser> --admin-password <adminPassword>
```

### Create a database in an SQL server:

```
az sql db create --resource-group <resourceGroupName> --server <serverName> \
--name <dbName> --service-objective <serviceObjective>
```

The service level objective parameter determines the performance of the database. The available capacity list is different per location. To get a of possible settings use:

```
az sql db list-editions --location <location> --query [].supportedServiceLevelObjectives[].name
```

## Tamplate deployment

The proviced JSON template deploys an SQL server and a database in the server and opens up an IP range on the firewall of the SQL server. The name of the SQL server and database, the IP range, the admin credentials and the size of the database are configurable.