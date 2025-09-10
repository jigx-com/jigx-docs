# InputTransform

When integrating with external REST APIs using a function in Jigx, the `inputTransform` property defines how input parameters are mapped to the body of the HTTP request. This is essential when the function’s `format` is set to `json`.

The `inputTransform` is written using [JSONata](https://jsonata.org/), a lightweight query and transformation language for JSON. It allows you to dynamically construct the JSON payload by referencing the parameters defined in the `parameters` section of the function.

Use `inputTransform` to:

* Map parameters into a structured JSON object.
* Build a request body that matches the target API’s requirements.
* Dynamically generate values based on user input or context.

## Simple Parameter Mapping

In this example:

* Two parameters are defined: `orderNumberParameter` and `orderDescriptionParameter`.
* Inside the `inputTransform`, these are referenced directly (without quotes).
* The resulting JSON object maps these values to the expected keys for the API call.

{% code title="inputTransform" %}
```yaml
parameters:
  orderNumberParameter:
    type: string
    location: body
    required: true
  orderDescriptionParameter:
    type: string
    location: body
    required: true

inputTransform: |
  $.{
    "orderNumber": orderNumberParameter,
    "orderDescription": orderDescriptionParameter
  }
```
{% endcode %}

## Multi-line YAML Strings

The `|` character in YAML indicates a multi-line string. This is useful for formatting complex transformations like JSONata expressions over multiple lines for better readability.

{% code title="YAML" %}
```yaml
inputTransform: |
  $.{
    "field1": value1,
    "field2": value2
  }
```
{% endcode %}

## Example and code snippet

Below is a more advanced example showing how to send an email using the SendGrid API. The URL for the service is `https://api.sendgrid.com/v3/mail/send`

The JSON body for this service is:

{% code title="JSON" %}
```json
{
  "personalizations": [
    {
      "to": [
        {
          "email": "anemail@com"
        }
      ]
    }
  ],
  "from": {
    "email": "youremail.com"
  },
  "subject": "Sending with SendGrid is Fun",
  "content": [
    {
      "type": "text/plain",
      "value": "and easy to do anywhere, even with cURL"
    }
  ]
}
```
{% endcode %}

In this configuration:

* `parameters` are defined for values like `emailto`, `name`, `subject`, and `content`.
* The `inputTransform` builds a JSON structure required by the SendGrid API using those parameters.
* The function constructs the request body at runtime, ensuring it dynamically reflects user or system inputs.

{% code title="YAML" %}
```yaml
provider: DATA_PROVIDER_REST
method: POST
url: https://api.sendgrid.com/v3/mail/send

parameters:
  Authorization:
    location: header
    type: string
    value: Bearer xxxxxxxxxxxxxxxxxxxx
    required: true
  emailfrom:
    location: body
    type: string
    required: true
  emailto:
    location: body
    type: string
    required: true
  name:
    location: body
    type: string
    required: true
  subject:
    location: body
    type: string
    required: true
  content:
    location: body
    type: string
    required: true
    
inputTransform: |
  $.{
    "personalizations": [{
      "to": [ { "email": emailto, "name": name }]}],
      "from": {"email": emailfrom, "name": name}, 
      "reply to": {"email": emailfrom, "name": name },
      "subject": subject, 
      "content": [{ "type": "text/html", "value": content}
      ]}    
```
{% endcode %}
