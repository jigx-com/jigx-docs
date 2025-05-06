---
title: REST endpoints from Azure SQL
slug: eOUi-call
createdAt: Wed May 22 2024 07:19:44 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed May 22 2024 07:26:14 GMT+0000 (Coordinated Universal Time)
---

Best practice for production apps is to use REST as the data layer to access data and not directly integrate to SQL using the SQL data provider. The SQL data provider will be squiggled in blue to indicate it is not recommended, together with a message to use [REST](./../REST.md) instead. 

1. Configure your Azure SQL database to call external REST endpoints.
   To learn how to call external REST endpoints from Azure SQL databases, read:
   - Microsoft Learn: <a href="https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-invoke-external-rest-endpoint-transact-sql?view=azuresqldb-current&tabs=request-headers" target="_blank">sp\_invoke\_external\_rest\_endpoint (Transact-SQL)</a>
   - GitHub sample: <a href="https://github.com/Azure-Samples/azure-sql-db-invoke-external-rest-endpoints" target="_blank">azure-sql-db-invoke-external-rest-endpoints</a>
2. Now use the [REST data provider ](./../REST.md) to configure your Jigx solution to integrate with your Azure SQL data.

