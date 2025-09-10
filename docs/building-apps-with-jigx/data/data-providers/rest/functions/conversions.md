# Conversions

Jigx stores uploaded files as local files on the device and returns their file paths as `local-uri`. However, most REST APIs do not accept files in this format. To send files to a REST endpoint, you must convert the `local-uri` to a compatible format, such as `base64`, `data-uri`, or `buffer`, before including them in the request body.

Likewise, when retrieving files from a REST endpoint, they are often returned in a non-local format (e.g., `base64` or `buffer`). To use or display these files in the app, you must convert them back to `local-uri`.

This is achieved by using `conversions` in functions. See [File handling](../../../file-handling.md) for detailed information on working with files and converting them into the correct format.

## Example and code snippet

### Incoming and outgoing conversions

In the examples below, the file conversions are configured:

1. In the **REST (GET) functions** to convert the incoming files to local-uri.
2. The file conversions are configured in the **REST (SAVE/CREATE/UPDATE) functions** to convert the files that are outgoing to REST.

{% tabs %}
{% tab title="rest-function-incoming" %}
```javascript
provider: DATA_PROVIDER_REST
method: GET
# Pdf indicates a generic binary type
format: pdf 
url: https://graph.microsoft.com/v1.0/me/photo/$value
outputTransform: $.{"data":$.data,"userId":$.inputs.userId.value} 
useLocalCall: true

parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: oauth.microsoft 
  userId:
    type: string
    location: path
    required: true
# Add a conversion to ensure the file can be viewed in the app.    
conversions:
  - property: data
    from: base64
    to: local-uri
```
{% endtab %}

{% tab title="rest-function-outgoing" %}
```yaml
provider: DATA_PROVIDER_REST
method: PATCH
url: https://graph.microsoft.com/v1.0/me/photo/$value
useLocalCall: true
parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: oauth.microsoft 
  Content-Type:
    location: header
    required: true
    type: string
    # Set the content type of the body.
    value: image/jpeg 
  file:
    location: body
    required: true
    type: image
# Convert the file from local-uri to an acceptable format
# to store in the remote database.     
conversions:
  - property: file
    from: local-uri
    to: buffer
```
{% endtab %}
{% endtabs %}

## Convert device specific formats

In this example, the file conversion is configured in the REST function to convert the files that are outgoing via REST. `convertHeicToJpg` is configured to true to convert HEIC images to JPEG which ensures images are visible on iOS and Android devices.

{% code title="YAML" %}
```yaml
provider: DATA_PROVIDER_REST
method: PATCH
url: https://graph.microsoft.com/v1.0/me/photo/$value
useLocalCall: true
parameters:
  accessToken:
    location: header
    required: true
    type: string
    # Use manage.jigx.com to define credentials for your solution
    value: oauth.microsoft 
  Content-Type:
    location: header
    required: true
    type: string
    # set the content type of the body
    value: image/jpeg 
  file:
    location: body
    required: true
    type: image
conversions:
  - property: file
    from: local-uri
    to: buffer
    convertHeicToJpg: true
```
{% endcode %}
