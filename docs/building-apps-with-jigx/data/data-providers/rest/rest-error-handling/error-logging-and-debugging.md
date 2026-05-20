# Error logging and debugging

Logging errors is a crucial part of the error handling mechanism. Errors are logged into a dedicated error `table` defined by you, capturing key information for debugging and analysis. Take the information that you currently have in the context of the function and log it using the `operations` properties to the table by defining the data to be logged in the `records` property.&#x20;

* The full error coming back from the backend system should be logged.
* Expose error tables in Jigx Builder to help with troubleshooting.
* Define a datasource against the error tables.

## **Error logging configuration**

When configuring REST errors, several system expressions and variables can be used. These variables allow you to dynamically log and handle errors based on the context of the function call. The following context is available to write to the error table, using `=@ctx.variable.value`:

<table><thead><tr><th width="141.3203125">Variables</th><th>Value</th></tr></thead><tbody><tr><td>commandId</td><td>Unique id logged for the item on the commandQueue. The id matches the id in the entity table.</td></tr><tr><td>correlationId</td><td>The unique identifier that appears in the app. It is used in <a href="../../../../../administration/solutions/troubleshooting-_solution_.md">troubleshooting</a> to help identify specific entries in the logs and to follow the user's journey while using the solution in the app. By filtering logs using this ID, you can troubleshoot issues more effectively.</td></tr><tr><td>entity</td><td>The specified table where the error context is logged</td></tr><tr><td>error</td><td><ul><li>message: string</li><li>title: string</li><li>description: string</li><li>details: string</li><li>icon: string</li><li>table: string</li><li>notification: boolean</li></ul></td></tr><tr><td>parameters</td><td>Specify any of the parameters in the function to be logged to the error table.</td></tr><tr><td>request</td><td><ul><li>method: string</li><li>url: string</li><li>headers: Record&#x3C;string, string></li><li>body:string</li><li>Buffer</li></ul></td></tr><tr><td>response</td><td><ul><li>ok: boolean</li><li>status: number</li><li>statusText: string</li><li>headers: Record&#x3C;string, string></li><li>body: any</li></ul></td></tr><tr><td>solution</td><td><ul><li>id: SolutionId</li><li>name: SolutionName</li><li>organizationId: OrganizationId</li><li><p>settings:</p><ul><li>custom: Record&#x3C;string, unknown></li></ul></li></ul></td></tr><tr><td>user</td><td><ul><li>id: string</li><li>email: string</li><li>displayName: string</li><li>avatarUrl: string</li><li>phone: string</li><li>isVerified: boolean</li><li>settings: Record&#x3C;string, unknown></li></ul></td></tr></tbody></table>

{% tabs %}
{% tab title="function-error-table" %}
```yaml
error:
  # Configure details for each erro status code.
  - when: =@ctx.response.status = 403   
    # Configure the error table and the data to log to the table,
    # in the error section of the function. 
    operations:
      - type: operation.upsert-merge
        table: =@ctx.entity & "_error"
        records: 
          '={ "id": @ctx.commandId, "type": "System Offline", "response": @ctx.response,
          "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution,
          "entity": @ctx.entity, "correlationId": @ctx.correlationId}'  
        timestamp: remoteSystemTimestamp          
```
{% endtab %}

{% tab title="error-datasource" %}
```yaml
# Call the error details from the dedicated error table in a datasource.
# Use the datasource to configure jigs to action the error, e.g. retry.
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_LOCAL
  entities:
    - entity: datasync-error
  query: SELECT
    id,
    json_extract(err.data, '$.response.ok') as ok,
    json_extract(err.data, '$.response.status') as status,
    json_extract(err.data, '$.response.statusText') as statusText,
    json_extract(err.data, '$.response.headers') as headers,
    json_extract(err.data, '$.response.body') as body,
    json_extract(err.data, '$.screen') as screen,
    json_extract(err.data, '$.type') as type
    FROM
    [datasync-error] AS err
```
{% endtab %}
{% endtabs %}
