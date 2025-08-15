# Microsoft Azure SQL

:::hint{type="warning"} Best practice for production apps is to use REST as the data layer to access data and not directly integrate to SQL using the SQL data provider. The SQL data provider will be squiggled in blue to indicate it is not recommended, together with a message to use [REST](microsoft-azure-sql.md) instead. See [REST endpoints from Azure SQL](microsoft-azure-sql.md) for more information. :::

::embed\[]{url="https://vimeo.com/833354418?share=copy"}

Jigx integrates with Microsoft Azure SQL through the SQL data provider, allowing you to select or insert data from an Azure SQL database. This includes Microsoft Azure SQL and Microsoft SQL Server on-premise.

## Use the SQL data provider

To use the SQL data provider in Jigx , follow these high-level steps:

1. **Choose your Azure SQL database**
   * Identify the SQL table you will use as your data source. Ensure you understand its structure and data.
2. **Configure the SQL connection**
   * [Configure a new Azure SQL connection ](configuring-the-sql-connection.md)for the solution in Jigx Management before adding the Jigx cloud IP addresses to the allowlist IP addresses in Azure SQL.
3. \*\*Define the SQL query or stored procedure in a **Jigx** function in **Jigx Builder**
   * Navigate to the [functions](../rest/rest.md) folder in Jigx Builder.
   * Use [IntelliSense](../../../jigx-builder-_code-editor_/editor.md) to configure the SQL data provider.
   * Enter the name of the connection set up in Jigx Management.
4. **Define data methods in the function**:
   * Configure a method to use to interact with the data. There are two options:
     * EXECUTE - used with stored procedures
     * QUERY - used to write SQL queries
   * For each method, create a new function file.
5. \*\*Reference the Jigx functions in \*\*jigs\*\*:
   * Reference the function in your jigs. This step is crucial for integrating the SQL data seamlessly into your Jigx solution.
6. **Publish your solution**:
   * [Publish your solution](../../../jigx-builder-_code-editor_/publishing-a-solution.md) and use the app to interact with the SQL data provider.
7. **Test the Data Provider**:
   * Use Jigx Builder [developer tools](../../../jigx-builder-_code-editor_/debugging.md) to test the data provider configurations. Check if the data provider can connect to SQL successfully and perform operations like SELECT, INSERT, UPDATE or DELETE data.

Following these steps, you can effectively integrate external Azure SQL data into your Jigx solutions, allowing you to enhance your apps with data and functionalities from diverse external sources.

## Connections

For security, all SQL calls from a Jigx App are routed through the Jigx cloud to the Microsoft Azure SQL instance. No data is stored in the Jigx cloud and is only used as a routing proxy for IP allowlisting in Microsoft Azure SQL. The [Configuring the SQL Connection](configuring-the-sql-connection.md) section explains the steps to configure a connection for the Azure SQL database in Jigx cloud, as well as configuring the IP allowlisting in Azure SQL for Jigx cloud.

## Jigx functions

Data from remote data sources such as Azure SQL or REST web services are stored in a local SQLite database on the device from where it is used in the Jigx application.

To fetch data onto the device and into the local SQLite table, Jigx executes a function that sends an SQL command to Azure SQL. This command can include an SQL statement that will be executed or a stored procedure.

The function's result is returned to the Jigx app on the device as a JSON array. Each record in the array is stored as a row in the local SQLite database.

The Jigx solution uses SQL as a query language to access and manipulate data in the local SQLite database.

Once functions are published in a Jigx solution, you can preview the function in Jigx Management under the solution's SQL functions option. See [Viewing and testing SQL data using the Jigx Management](../../../../administration/solutions/sql-functions.md) for more information.

## SQL function components

| **Provider**   | `DATA_PROVIDER_SQL` for making calls to Microsoft Azure SQL.                                                                                                                                                        |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Connection** | Provide the name of the connection configured in for the Azure SQL database.                                                                                                                                        |
| **Methods**    | <p>Jigx supports the following methods in the provider:</p><ul><li>EXECUTE - used to execute a stored procedure</li><li>QUERY - used to write a SQL statement such as SELECT, INSERT, DELETE, and UPDATE.</li></ul> |

The following describes the options available when configuring a SQL function call.

:::CodeblockTabs sql- function-query

```yaml
# Jigx SQL function executing a query to select all customers from a table.
provider: DATA_PROVIDER_SQL
# Use manage.jigx.com to configure a SQL connection.
connection: customer.azure
# Use SQL statements to interact with the data in SQL. 
method: query 
query: |
  SELECT
    id,
    first_name,
    last_name,
    email,
    phone_number,
    address_line1,
    address_line2,
    city,
    state,
    zip_code,
    country
  FROM
    customers
```

sql-function-execute

```yaml
# Jigx SQL function executing a stored procedure to select all customers 
# from a table.
provider: DATA_PROVIDER_SQL
# Use manage.jigx.com to configure a SQL connection.
connection: customer.azure
# Provide the SQL stored procedure to execute.
method: execute 
procedure: sp_GetAllCustomers
```

:::

## Parameters

Function parameters are used to pass data into the function definition from the jig that uses the function. See the [Datasources](../../datasources.md) section of the documentation. Parameters are defined by naming them and describing the properties of that parameter. Parameter names are used when the parameters are referred to in the SQL query.

### Function parameter properties

### Location

The location determines how the parameter will be applied in the SQL call:

* **input:** the parameter is used as an input, for example when creating a record.
* **output:** the parameter is used as an output.
* **both:** the parameter is used as an input and output.

### Type

Type is specific to the SQL call being made. Most types are defined as strings.

### Required

The required value is either `true` or `false`. This determines whether the parameter needs to be set when the function is used in a jig's datasource. This determines if the SQL call \*\*requires \*\*this parameter. If so, set this property to `true`, alternatively if the parameter is optional, you can set it to `false`.

### forRowsWithValues

By default the return SQL call replaces previous data in the SQLite database. The `forRowsWithValues` property allows you to update specific values in the SQLite database instead of replacing all rows, providing a better user experience. The `forRowsWithValues` property specifies a key-value pair where the key is a json\_extract() column in the SQLite table that will be matched by the value. Only rows that match these criteria will be updated. The object will be added as a new row to the collection if a match isn't found. You can have multiple key-value pairs specified under `forRowsWithValues`. Think of this as a WHERE clause that Jigx uses when it adds the result of the SQL call to the SQLite table.

### forRowsInRange

Similar to `forRowsWithValue` but instead of matching rows by value the `forRowsInRange` specifies a key-value pair where the key is a json\_extract() column in the table that a value range will match. Only rows that match these criteria will be updated. The object will be added as a new row to the collection if a match isn't found. You can have multiple key-value pairs specified under `forRowsInRange`. Think of this as a WHERE clause with a BETWEEN that Jigx uses when it adds the result of the SQL call to the table.

### forRowsWithMatchingIds

Similar to `forRowsWithValue`, when `forRowsWithMatchingIds` is specified, Jigx will perform an upsert on a specific id. The `outputTransform` MUST contain a field called id. This id will be used to match the id column in the database; if a record with this id exists, it will be updated. If no match is found, the record will be inserted. No deletion is performed when `forRowsWithMatchingIds` is used.

### Conversions

Jigx stores files as local files on the device and only saves the file URI to the file in the datastore/state. When a component needs the binary data, it can read the local file from the file URI. To enable the handling of files, you can convert files from base64, data-uri, or buffer to local-uri. See [File handling](../../file-handling.md) for more information.

```yaml
provider: DATA_PROVIDER_SQL
method: query
connection: customer.azure
query: SELECT TOP(@top) Id, FirstName, LastName, AvatarBase64, AvatarDataUri, AvatarBuffer FROM Employee
parameters:
  top:
    location: input
    required: false
    type: number
    value: 10
conversions:
  - property: AvatarBuffer
    from: buffer
    to: local-uri
  - property: AvatarBase64
    from: base64
    to: local-uri
  - property: AvatarDataUri
    from: data-uri
    to: local-uri
```

## Referencing a Jigx function

Here is an example of a Jigx solution screen that calls the function in the `OnFocus` event with a `sync-entities` action to sync the data from SQL to the local SQLite database, which returns the customers' details.

:::CodeblockTabs list-customers.jigx

```yaml
# A sample list that uses a SQL function to return & display a list of customers from Azure SQL
title: List Customers
description: Show a list of all customers in a SQL database.
type: jig.list
icon: contact
# Header section displaying an image at the top of the screen
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1553413077-190dd305871c?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1035&q=80

# onFocus is triggered whenever the jig is displayed. The sync-entities action
# calls the Jigx SQL function and populates the local SQLite tables on the
# device with the data returned from Azure SQL.
onFocus:
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_SQL
    entities:
      - entity: customers
        function: get-customers

# The mydata data source selects the data from the local SQLite database.
datasources:
  mydata:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL

      entities:
        - entity: customers

      query: |
        SELECT
          id,
          '$.first_name',
          '$.last_name',
          '$.email',
          '$.phone_number',
          '$.address_line1',
          '$.address_line2',
          '$.city',
          '$.state',
          '$.zip_code',
          '$.country'
        FROM
          [customers]

# The list and its list items are configured below. This is a list jig; 
# therefore, its properties, such as data and item, are top-level properties.
# The data property binds the list to a specific data source.
data: =@ctx.datasources.mydata
# The item property specifies the list item type and its attributes.
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.first_name & ' ' & @ctx.current.item.last_name
    subtitle: =@ctx.current.item.email
    description: |
      =@ctx.current.item.address_line1 & ' ' & 
        @ctx.current.item.city & ' ' & 
        @ctx.current.item.state  & ' ' & 
        @ctx.current.item.zip_code
    label:
      title: =@ctx.current.item.country
    leftElement:
      element: avatar
      # The text property is specified using a JSONata expression 
      # that builds a two-letter string by concatenating the first letters 
      # of the customer's first and last names.
      text: =$substring(@ctx.current.item.first_name,0,1) & $substring(@ctx.current.item.last_name,0,1)
    divider: solid
```

:::

We recommend navigating to the Management Console to test your function at this point. This allows you to ensure that the function is configured correctly, connected to SQL Server, and returns results. You can find out more about capabilities for viewing and testing SQL functions from the Management Console at this location. :Link\[Viewing and testing SQL data]{href="https://docs.jigx.com/sql-functions" newTab="true" hasDisabledNofollow="false"} using the Jigx Management Console

## Examples and code snippets

The following examples with code snippets are provided:

1. A [SQL database script](microsoft-azure-sql.md) to create the tables and stored procedures used in the example. These scripts should be executed against an existing database in your Azure SQL environment.
2. [List customers (SELECT)](microsoft-azure-sql.md)
3. [List a single customer (SELECT)](microsoft-azure-sql.md)
4. [Create a customer (INSERT)](microsoft-azure-sql.md)
5. [Update a customer (UPDATE)](microsoft-azure-sql.md)

## See Also

* [File handling](../../file-handling.md)
* [Offline remote data handling](../../offline-remote-data-handling.md)
