# REST endpoints from Azure SQL

Best practice for production apps is to use REST as the data layer to access data and not directly integrate to SQL using the SQL data provider. The SQL data provider will be squiggled in blue to indicate it is not recommended, together with a message to use [REST](./../REST.md) instead.

1. Configure your Azure SQL database to call external REST endpoints.
   To learn how to call external REST endpoints from Azure SQL databases, read:
   - Microsoft Learn: :Link[sp\_invoke\_external\_rest\_endpoint (Transact-SQL)]{href="https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-invoke-external-rest-endpoint-transact-sql?view=azuresqldb-current&tabs=request-headers" newTab="true" hasDisabledNofollow="false"}
   - GitHub sample: :Link[azure-sql-db-invoke-external-rest-endpoints]{href="https://github.com/Azure-Samples/azure-sql-db-invoke-external-rest-endpoints" newTab="true" hasDisabledNofollow="false"}
2. Now use the [REST data provider ](./../REST.md) to configure your Jigx solution to integrate with your Azure SQL data.

