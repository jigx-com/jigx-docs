# JavaScript in functions

Use custom JavaScript in REST function expressions to define complex logic directly within parameters, headers, errors, and transformations. JavaScript enables advanced data manipulation, conditional logic, and formatting beyond the capabilities of standard expressions, offering greater flexibility and control when integrating with external REST APIs.

## Configuration

1. Create the JavaScript file in Jigx Builder in the _scripts/expressions_ folder.
2. Reference the expression in the function file. Use IntelliSense to select the required JavaScript expression.

## Example and code snippets

The `coalesce` export function in the JavaScript code below returns the first non-null, non-undefined, and non-empty-string value from the list of candidates provided. If none of the candidates are valid (i.e., all are null, undefined, or empty string), it returns undefined.

```javascript
// scripts/expressions/utils.js
export function coalesce(...candidates) {
    console.log('coalesce', JSON.stringify({ candidates }));
    for (let candidate of candidates) {
        if (candidate !== null && candidate !== undefined && candidate !== '') {
            return candidate;
        }
    }
    return undefined;
}
```

The JavaScript file is used as expressions in the function's:

1. Header parameter - Use the configured API key or a default.
2. Input transform - Use the user's name or email or defaults to unknown.
3. Error handling - Extract the most relevant error message for display and condition check.

{% code title="Function" %}
```yaml
provider: DATA_PROVIDER_REST
method: POST
url: https://[your_rest_service]/api/customers  
useLocalCall: true

parameters:
  x-api-key:
    type: string
    location: header
    required: false
    value: =$utils.coalesce(@ctx.solution.settings.custom.restStorageApiKeyx, 'abc123')
  title:
    type: string
    location: body
  description:
    type: string
    location: body
    required: false
  authors:
    type: string
    location: body
    required: false

inputTransform: |
  ={
    "title": @ctx.parameters.title,
    "description": @ctx.parameters.description,
    "authors": @ctx.parameters.authors,
    "createdBy": {
      "id": @ctx.user.id,
      "name": $utils.coalesce(@ctx.user.displayName1, @ctx.user.email2, 'unknown')
    }
  }

outputTransform: |
  {
      "id": $substringAfter($$.headers.location, '/items/')
  }

error:
  - when: =$contains($utils.coalesce(@ctx.error.message, @ctx.error.title, @ctx.error.description), 'no access')
    notification: true
    title: "='Access denied: ' & @ctx.error.message"
    description: "='Access denied: ' & @ctx.error.message"
    table: sync_error
    transform: =@ctx.error
```
{% endcode %}
