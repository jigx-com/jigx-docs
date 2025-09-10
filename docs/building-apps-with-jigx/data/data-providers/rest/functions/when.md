# When

The when property allows you to control when a function, operation, guard, or error handler should execute. It uses a condition, typically based on the local state of the database. This makes functions more dynamic by ensuring they only run when certain conditions are met, helping to optimize performance, avoid redundant calls, and manage conditional logic efficiently.

* Conditionally skip function execution based on local state or query results.
* Prevent unnecessary API calls by checking if a condition has already been met.
* Dynamically execute operations or error handlers only under certain circumstances.
* Evaluate conditions on continuation unless configured otherwise.

## Where to use the when property

<table><thead><tr><th width="154.95703125">Where</th><th>When</th></tr></thead><tbody><tr><td><code>Main function</code></td><td>Determines whether the function should be executed. The when expression is evaluated after the parameters and queries are evaluated. The <code>when</code> expression is evaluated before token credentials are checked and <code>inputTransforms</code> are evaluated. The <code>when</code> expression is re-evaluated on each <code>continuation</code>.</td></tr><tr><td><code>Operations</code></td><td>Determines whether the operation should execute. Useful for selectively inserting, updating, or transforming data.</td></tr><tr><td><code>Error handler</code></td><td>Determines the conditions under which the error should be executed. Specify one or more error handling definitions. The first rule that matches the <code>when</code> condition will be used. A rule without a <code>when</code> condition will become the default error handler. If no rules are specified, default error handling will be used, i.e., checking for actual errors or using HTTP status codes and messages for REST providers.</td></tr><tr><td><code>Guard function</code></td><td>Evaluates whether the guard function should run, allowing conditional validation or control.</td></tr></tbody></table>

{% code title="when" %}
```yaml
provider: DATA_PROVIDER_REST
method: DELETE
url: https://rest-data-service.net/api/v0.1/collections/books/items/{id}
when: =@ctx.solution.settings.custom.fiction
```
{% endcode %}

## Examples and code snippets

### Conditional Function Execution

{% code title="main-when-function" %}
```yaml
provider: DATA_PROVIDER_REST
url: https://graph.microsoft.com/v1.0/me/drive/root/children
method: GET
# Determine conditions when the main function executes.
when: =@ctx.queries.current-record ? false:true 
useLocalCall: true

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
    
# In the function definition.
queries: 
  current-record: 
    statement: SELECT * FROM [local-countries] WHERE [id] = @id
    parameters:
      id: =@.parameters.countryId
  existing-countries:
    statement: SELECT * FROM [local-countries]
    jsonColumns: =@ctx.entity
```
{% endcode %}

### Custom error handling error

This custom error message is shown only when the response status of 503 is recieved from the server.

{% code title="when-error" %}
```yaml
error: 
  - title: Server is temporarily unavailable
    description: |
      The server is currently unavailable, please try again in a few minutes.
    details: =@ctx.response.body
    icon: on-error-sad
    notification: true
    operations:
      - type: operation.delete-insert
        table: =@ctx.entity & "_error"
    # Condition that determines when a 503 custom error message executes.    
    when: =@ctx.response.status = 503
```
{% endcode %}
