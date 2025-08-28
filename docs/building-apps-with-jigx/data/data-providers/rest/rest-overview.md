# REST Overview

## REST Overview

## Introduction

When a REST call returns data to Jigx, the processed JSON is inserted into a local SQLite database. The Jigx mobile application then queries the database, displaying the data on the device. This architecture supports offline scenarios. Data is stored in a document database format. Jigx provides a shorthand SQL parser to select using logical column names. Alternatively, you can use the native json\_extract() function to manipulate the data from SQLite. When the result of the output transform is an array of JSON objects, Jigx will insert each item in the array in its row. Note that SQL is case-insensitive while JSON is case-sensitive.

Functions definitions are stored in the functions folder in a Jigx project and are files that end in a .jigx file extension. When .jigx files are created in the functions folder, the Jigx Builder IntelliSense code completion is available using ctrl+spacebar. We recommend using this capability, as it provides all available code completion options relevant to Jigx functions.

<figure><img src="../../../../.gitbook/assets/REST-function.png" alt="Jigx&#x27;s functions" width="375"><figcaption><p>Jigx's functions</p></figcaption></figure>

To add a new function, add a new file in the functions folder, the .jigx extension is automatically added for you. Function file names must be lowercase and may not contain special characters.

Once functions are published in a Jigx solution you can preview the function in Jigx Management under the solution's REST functions option. See [REST Functions](../../../../administration/solutions/rest-functions.md) for more information.

## Parameters and Authentication Support

All REST functions support header, path, query, and body parameters. In addition, including calling services with no authentication, Jigx supports OAuth, API Key, and Basic Auth or Secrets for authentication.

The code completion will display the available template options when adding a new function.

<figure><img src="../../../../.gitbook/assets/REST-function-code.png" alt="Functions code completion options"><figcaption><p>Functions code completion options</p></figcaption></figure>

Creating a new function using one of these template options adds the skeleton code to the function definition, making it easier to configure functions for specific providers with their authentication configuration. These options are:

* **REST**: A REST service call with no authentication that returns JSON by default.
* **REST (API Key)**: A REST service call that includes x-API-key in the header for authentication.
* **REST (Basic Auth)**: A REST service call that includes basicAuth in the header populated with the credential's information.
* **REST (OAuth)**: A REST service call that includes accessToken (Authorization) in the header populated with the OAuth Token returned during the OAuth loop.
* **REST (Secret)**: A REST service call that includes a secret that can be added to the header or query string parameters for authentication.
* **Soap**: A template for Soap calls.
* **SQL**: The template for making either query or stored procedure calls to Microsoft SQL Azure.

## REST Call function components

The following describes the options available when configuring a REST function call.

<figure><img src="../../../../.gitbook/assets/REST-function-op.png" alt="REST function options"><figcaption><p>REST function options</p></figcaption></figure>

<table data-header-hidden><thead><tr><th width="110.03125"></th><th></th></tr></thead><tbody><tr><td><strong>Provider</strong></td><td><code>DATA_PROVIDER_REST</code> for making REST service calls.</td></tr><tr><td><strong>Methods</strong></td><td><p>Jigx supports the following methods when making REST calls:</p><ul><li>DELETE</li><li>GET</li><li>HEAD</li><li>PUT</li><li>PATCH</li><li>POST</li></ul></td></tr><tr><td><strong>URL</strong></td><td>The URL of the service that must be called. Jigx supports path and query parameters in the URL. Path parameters are tagged with curly brackets {}. Jigx will replace the path parameters with the values of the parameters defined in the parameter section of the function definition. Query parameters specified in the URL will be removed by Jigx and replaced by parameters defined in the parameters section of the function definition with a location property of type Query.</td></tr></tbody></table>

### Swagger parser

The Swagger parser function allows you to convert Swagger, open API, and Postman collection data to Jigx functions in the Jigx Builder.

Command to start the Swagger parser function is (command + shift + p): `Generate Jigx Functions`

<figure><img src="../../../../.gitbook/assets/REST-swaggerParser.png" alt="Generate Jigx functions"><figcaption><p>Generate Jigx functions</p></figcaption></figure>

Both remote and local files can be used, and only the JSON format is allowed.

<figure><img src="../../../../.gitbook/assets/REST-fileOptions.png" alt="File options"><figcaption><p>File options</p></figcaption></figure>

All files created by the Swagger parser function saves in your functions folder.

#### Variable replacement

You can replace variables in your Postman collection, for example, replacing the _baseUrl_. As you add the value 'google.com' to the variable all functions requiring this variable will be updated.

<figure><img src="../../../../.gitbook/assets/REST-variableReplacement.png" alt=""><figcaption></figcaption></figure>

### Input Transform – Detail and Examples

When the format of the function is specified as JSON, the body of the call is generated by the input transform. The input transform is a JSONata statement ([https://jsonata.org](https://jsonata.org/)) that can contain parameters defined in the parameter section of the function definition. In this example, we are applying the following mapping:

```none
Jigx parameter: orderNumberParameter
Jigx parameter: orderDescriptionParameter
```

The values of these parameters are replaced in the input transform to build the JSON payload which will be submitted to the order REST service.

Parameters in the input transform are specified using their name without quotes. An example is:

```yaml
inputTransform: |
  $.{
    “orderNumber”: orderNumberParameter, 
    “orderDescription”: orderDescriptionParameter
  }
```

The | character in YAML allows you to format the content of the YAML node over multiple lines.

### Output Transform - Detail and Examples

The output transform is a JSONata expression that transforms the JSON received by the REST call into the JSON that will be inserted in the local SQLite tables. When the result of the output transform is an array of JSON objects, Jigx will insert each item in the array in its own row. Then, the values in the JSON object are selected as data columns in an SQLite statement using the json\_extract() function SQLite function. Below is an example of JSON returned by a REST call and then transformed into an array of JSON objects:

```json
{
  "customerId": "1432",
  "customerName": "Johson Shipping",
  "shippingAddress1": "7645 1st Street",
  "shippingCity": "Nashville",
  "shippingState": "TN",
  "shippingZip": "78654",
  "orders": [
    {
      "orderNumber": "1234",
      "orderDescription": "Printer Refil",
      "orderTotal": 345.67,
      "customerId": "1432",
      "orderDate": "1-29-2022"
    },
    {
      "orderNumber": "654",
      "orderDescription": "Printer Paper",
      "orderTotal": 185.27,
      "customerId": "1432",
      "orderDate": "1-29-2022"
    },
    {
      "orderNumber": "8934",
      "orderDescription": "Envelopes",
      "orderTotal": 25.88,
      "customerId": "1432",
      "orderDate": "1-29-2022"
    }
  ]
}
```

Output transform to get an array of orders: $.orders. $ is the root of the document and orders the array with the collection of orders. The result of the transform is:

```json
[
  {
    "orderNumber": "1234",
    "orderDescription": "Printer Refil",
    "orderTotal": 345.67,
    "customerId": "1432",
    "orderDate": "1-29-2022"
  },
  {
    "orderNumber": "654",
    "orderDescription": "Printer Paper",
    "orderTotal": 185.27,
    "customerId": "1432",
    "orderDate": "1-29-2022"
  },
  {
    "orderNumber": "8934",
    "orderDescription": "Envelopes",
    "orderTotal": 25.88,
    "customerId": "1432",
    "orderDate": "1-29-2022"
  }
]
```

As mentioned above, all order objects in the array will be inserted as individual rows into a SQLite table specified in the datasource section in the jig definition.

### Function parameters

Function parameters are used to pass data into the function definition from the jig that uses the function. See the [Datasources](../../datasources.md) section of the documentation. Parameters are defined by naming them and describing the properties of that parameter. Parameter names are used when the parameters are referred to in the REST query path or input transforms. (See an example above for an inputTransform).

### Function parameter properties

#### Location

The location determines where the parameter will be applied in the REST call as follows:

* **path:** When path is specified as the location, the parameter is available as a token in the URL's path.
* **query:** When query is specified as the location, a query string parameter with a name set to the name of the function parameter will be added to the URL. The value of the query string parameter is set to the value of the function parameter.
* **header:** When header is specified as the location, a header entry with a name set to the name of the function parameter will be added to the request. The value of the header entry is set to the value of the function parameter.
* **body:** when body is specified as the location, the function parameter is available in the inputTransform defined for the function. Tokens matching the parameter's name will be replaced with the value of the function parameter.

#### Type

Type is specific to the REST call being made. Most types are defined as strings when they are used in path, query, or body locations. The available types are string, number, array, object.

When types are declared in authentication header parameters, they are specific to the authentication type being configured. See authentication parameters below.

#### Required

The required value is either `true` or `false`. This determines whether the parameter needs to be set when the function is used in a jig's datasource. Parameters used in paths must be set to `required: true` or they will generate an error. This determines if the REST call \*\*requires \*\*this parameter. If so, set this property to `true`, alternatively if the parameter is optional, you can set it to `false`.

### Additional properties&#x20;

#### Continuation

Many REST services limit the number of items that can be retrieved from the service in a single call. To retrieve all items associated with a query, additional calls must be made to the service using a URL or additional data passed to the caller. The caller then makes repeated calls to the service using these continuation parameters to retrieve all records.

Jigx REST functions can be configured to automatically repeat calls to `continuation` functions by specifying a continuation block in the function YAML.

{% hint style="warning" %}
The continuation URL and parameters overwrite the parameters in the original function call therefore all parameters, including OAuth tokens and API keys, must be replicated in the continuation function.

Since the continuation URL or parameters are outside of the data returned by the function (at a higher level), the **outputTransform** of the function will need to be changed to return the records in their own property and the **records** property specified in the function YAML to locate the output records.&#x20;
{% endhint %}

**Example**

Microsoft Graph API uses continuation URLs to request the next page of items from their services. If there are more items in the response than can be handled in a single call, or the caller has limited the number of items per page, the service will return the `@odata.nextLink` parameter specifying the URL to call to fetch the next page of results.

```json
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('bb13f9b6-d289-485f-9ae6-76be00f5bab3')/drive/root/children",
    "@odata.nextLink": "https://graph.microsoft.com/v1.0/me/drive/root/children?$top=2&$skiptoken=UGFnZWQ9VFJVRSZwX1NvcnRCZWhhdmlvcj0xJnBfRmlsZUxlYWZSZWY9TWljcm9zb2Z0K1RlYW1zK0NoYXQrRmlsZXMmcF9JRD0yMA",
    "value": [
        {
	   ...
	}
    ]
}
```

All data has been returned when the `@odata.nextLink` parameter is no longer present in the results.

Note in this case that the `nextUrl` expression is used to both check for continuation data as well as the URL to fetch the next page of data.

```yaml
method: GET
provider: DATA_PROVIDER_REST
parameters:
  $top:
    location: query
    type: number
    required: false
  accessToken:
    location: header
    type: microsoft
    value: jigx.microsoft.oauth
    required: true
url: "https://graph.microsoft.com/v1.0/me/drive/root/children"
outputTransform: >-
  $.{"nextLink":`@odata.nextLink`,"items":value.{"id":id,"name":name,"size":size,"lastModifiedDateTime":lastModifiedDateTime,"type":$exists(folder) ? "Folder" : "File"}}
records: =$.items
continuation:
  when: =$.nextLink
  url: =$.nextLink
  parameters:
    accessToken:
      location: header
      type: microsoft
      value: jigx.microsoft.oauth
      required: true
```

#### Error

Jigx allows you to customize REST endpoint error messages to improve user experience, communicate more effectively, and ensure users understand that errors are not their fault. By configuring custom `error` properties, you can, suppress or customize default error messages, log error details for more effective debugging, and create more robust and user-friendly error solutions. See [REST error handling](rest-error-handling.md) and [REST errors](rest-overview.md) for more information.

#### forRowsWithValues

By default the return JSON payload from the REST call replaces previous data in the SQLite database. The `forRowsWithValues` property allows you to update specific values in the SQLite database instead of replacing all rows, providing a better user experience. The `forRowsWithValues` property specifies a key-value pair where the key is a json\_extract() column in the SQLite table that will be matched by the value. Only rows that match these criteria will be updated. The object will be added as a new row to the collection if a match isn't found. You can have multiple key-value pairs specified under `forRowsWithValues`. Think of this as a WHERE clause that Jigx uses when it adds the result of the REST call's `outputTransform` to the SQLite table.

{% hint style="info" %}
The property should be passed as a parameter and be referenced in the `outputTransform` as shown in the example below.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/REST-forRowsValue.png" alt="forRowsWithValues"><figcaption><p>forRowsWithValues</p></figcaption></figure>

#### forRowsInRange

Similar to `forRowsWithValue` but instead of matching rows by value the `forRowsInRange` specifies a key-value pair where the key is a json\_extract() column in the table that a value range will match. Only rows that match these criteria will be updated. The object will be added as a new row to the collection if a match isn't found. You can have multiple key-value pairs specified under `forRowsInRange`. Think of this as a WHERE clause with a BETWEEN that Jigx uses when it adds the result of the REST call's  `outputTransform` to the table.

{% hint style="info" %}
Pass the values you want to test as input parameters. In this example, minmag and maxmag. The property to test is **mag**. This property (**mag**) must appear in the `outputTransform`. Then set the range you are testing for in the input parameter (**minmag**) and (**maxmag**).
{% endhint %}

<figure><img src="../../../../.gitbook/assets/REST-forRowsRange.png" alt="forRowsInRange"><figcaption><p>forRowsInRange</p></figcaption></figure>

{% hint style="info" %}
* You can combine `forRowswithValues` and `forRowsInRange` as per the example below.
* You cannot combine `forRowsWithMatchingIds` with any other range or value check.&#x20;
{% endhint %}

<figure><img src="../../../../.gitbook/assets/REST-ForRowsCombined.png" alt="Combined properties" width="375"><figcaption><p>Combined properties</p></figcaption></figure>

#### forRowsWithMatchingIds

Similar to `forRowsWithValue`, when `forRowsWithMatchingIds` is specified, Jigx will perform an upsert on a specific id. The `outputTransform` MUST contain a field called id. This id will be used to match the id column in the database; if a record with this id exists, it will be updated. If no match is found, the record will be inserted. No deletion is performed when `forRowsWithMatchingIds` is used.

<figure><img src="../../../../.gitbook/assets/REST-forRowsMatchId.png" alt="forRowsWithMatchingIds" width="375"><figcaption><p>forRowsWithMatchingIds</p></figcaption></figure>

#### Summary

Jigx will delete all rows from the table matching the `forRowsWithValues` or `forRowsInRange` key-value pairs before it inserts new results. The user interface is only updated once the data action has been completed on the table to avoid flickering of user interfaces. The user interface is only updated as the last step.

### See Also

* [REST examples](https://docs.jigx.com/examples/rest)
* [Offline remote data handling](../../offline-remote-data-handling.md)
