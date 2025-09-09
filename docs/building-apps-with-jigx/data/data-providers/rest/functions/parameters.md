# Parameters

Function parameters pass data into the function from the jig that calls it. They make the function dynamic and reusable by allowing context-specific values, like user input, selected records, or settings, to be used during execution.

Parameters are defined by a name and a set of properties (such as type, location, and whether they are required). These names are then referenced throughout the function, for example, in REST paths, query strings, and input transforms.

## Configuration options

<table><thead><tr><th width="139.3515625"></th><th></th></tr></thead><tbody><tr><td><code>location</code></td><td><p>The location determines where the parameter will be applied in the REST call as follows:</p><ul><li><code>path</code> - The parameter is available as a token in the URL's path.</li><li><code>query</code> - A query string parameter will be added to the URL, using the function parameter's name as the key and its value as the query parameter value.</li><li><code>header</code> - A header will be added to the request using the function parameter’s name as the key and its value as the header value.</li><li><code>body</code> - When body is specified as the location, the function parameter is available in the function’s <code>inputTransform</code>. Any token matching the parameter’s name will be replaced with its value during execution.</li><li><code>credential</code> - Specifies the type of authentication required for REST API calls. It ensures secure communication between the app and the external API by attaching the appropriate authentication tokens or headers, as configured in <a href="../../../../../administration/solutions/credentials.md">Jigx Management</a>.</li><li><code>secret</code> - Securely references the client secret. Instead of hardcoding credentials directly into the function, you reference secret values that are stored securely in the solution's credentials in <a href="../../../../../administration/solutions/credentials.md#adding-credentials">Jigx Management</a>.</li></ul></td></tr><tr><td><code>type</code></td><td><p>Type is specific to the REST call being made. Most types are defined as strings when they are used in path, query, or body locations. The available types are <code>string</code>, <code>number</code>, <code>array</code>, and <code>object</code>.</p><p>When types are declared in authentication header parameters, they are specific to the authentication type being configured.</p></td></tr><tr><td><code>required</code></td><td>The <code>required</code> value can be either <code>true</code> or <code>false</code>, indicating whether the parameter must be provided when the function is used in a jig’s datasource. Parameters used in URL paths must be set to <code>required: true</code>; otherwise, the function will generate an error. Set this property to <code>true</code> if the REST call requires the parameter, or <code>false</code> if the parameter is optional.</td></tr><tr><td><code>value</code></td><td>Provide a value for the parameter based on its defined <code>location</code> (e.g., query, header, path, or body) and <code>type</code> (e.g., string, number, boolean).</td></tr></tbody></table>

### Example and code snippets

{% tabs %}
{% tab title="function-parameters (header, body)" %}
```yaml
provider: DATA_PROVIDER_REST
# Updates data in the REST Service 
# PATCH modifies only the specified fields or properties of the resource.
method: PATCH 
# Use your REST service URL
url: https://[your_rest_service]/api/customers  
format: text
# Use local execution between the device and the REST service.
useLocalCall: true 
# Define parameters with header and body location.
parameters:
  accessToken:
    location: header
    required: true
    type: string
    # Use manage.jigx.com to define credentials for your solution
    value: service.oauth 
  id:
    type: int
    location: body
    required: true
  firstName:
    type: string
    location: body
    required: true
  lastName:
    type: string
    location: body
    required: true
  companyName:
    type: string
    location: body
    required: true
  address:
    type: string
    location: body
    required: false
  city:
    type: string
    location: body
    required: false
  state:
    type: string
    location: body
    required: false
  zip:
    type: string
    location: body
    required: false
  phone:
    type: string
    location: body
    required: false
 
```
{% endtab %}

{% tab title="function-parameters (query, path)" %}
```yaml
provider: DATA_PROVIDER_REST
method: GET
url: https://{RESTURL}
useLocalCall: true
# Define parameters with query and path location.
parameters:
  $expand:
    location: query
    required: false
    type: string
    value: Details,Logs,Settings,Staff
  $filter:
    location: query
    required: true
    type: string
  $select:
    location: query
    required: false
    type: string
    value: Staff/StaffMember,Staff/StaffType,Staff/StaffMemberName,Details
  accessToken:
    location: header
    required: true
    type: authname
    value: authname
  RESTURL:
    location: path
    required: true
    type: string
```
{% endtab %}
{% endtabs %}
