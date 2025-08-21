# REST error handling

REST errors returned by the endpoints in an app are often too technical for end-users to comprehend. Jigx allows you to customize these error messages to improve user experience, communicate more effectively, and ensure users understand that errors are not their fault. By configuring custom error handling, you can:

* Suppress or customize default error messages.
* Log error details for more effective debugging.
* Create more robust and user-friendly error solutions.

## Key features

* **Custom error messages**: Control the message shown to users when a REST error occurs.
* **User-friendly retry options**: Allow users to retry an action when an error occurs.
* By default, Jigx automatically catches any **429 error responses** and retries the request up to three times, with a five-second delay between each attempt.
* **Error logging**: Automatically log error details for debugging.
* **Dynamic responses**: Build logic to respond to specific errors flexibly.

::::VerticalSplit{layout="middle"} :::VerticalSplitItem ![Standard REST error](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-cNRtuj2lt8h8Yjn8w_IUy-20241009-124900.png) :::

:::VerticalSplitItem ![Customized REST error](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-jZvT-KAFznVb7Hh5wdIuc-20241009-124927.png) ::: ::::

## How does it work

In Jigx, REST error handling is configured through an `error` section in the REST function. This allows the system to catch various error responses and act accordingly:

* Multiple error responses can be defined and are evaluated in sequence.
* Error responses can trigger notifications, log errors, or provide retry options for users.
* The app supports customized messaging for each error type.
* Expressions are supported in functions.

**High level steps:**

1. Configure the `error` section in the REST **function** to customize the error message and configure an error table.
2. Create a **datasource** for the error table.
3. Create a **UI** (jig) to process the error in the queue using the commandQueue actions.

{% hint style="info" %}
By default, Jigx automatically handles `429` (Too Many Requests) error responses for CRUD and sync methods by retrying the request up to three times, with a five-second delay between each attempt. If the request still fails after the third retry, the error is raised in the app. You can customize this behavior by configuring the handling of the 429 status in the `error` property.
{% endhint %}

## REST Function

In the Jigx function, configure the `error` section to cater for:

* Customizing the error message.
* Determining if a toast notification is required or not.
* Writing the context of the error to a table for debugging and configuring actions to fix the error.

Multiple error handlers can be added in the function, which are executed from the top to bottom until one matches. The error section needs to be configured in each of the individual REST function files.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-ShlmyhYcPqv\_WUEow9Khg-20241009-125734.png" size="94" position="center" caption="Function properties" alt="Function properties" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-ShlmyhYcPqv\_WUEow9Khg-20241009-125734.png" width="800" height="460" darkWidth="800" darkHeight="460"}

## Configuration properties

The following properties are available for configuration when handling REST errors:

<table><thead><tr><th width="157.109375">Property</th><th>Description</th></tr></thead><tbody><tr><td><code>description</code></td><td>Provide a user-friendly message of the error, for example, "<em>It looks like our system is unavailable</em>." Defaults to the provider's description if absent. For example, the REST provider uses the HTTP status code and message. The description property supports.</td></tr><tr><td><code>details</code></td><td>Add additional information that will display under the description. Defaults to the provider's details if absent.</td></tr><tr><td><code>icon</code></td><td>Select an to show on the error notification screen.</td></tr><tr><td><code>notification</code></td><td>Determines whether the notification should be shown on the device. (true/false)</td></tr><tr><td><code>retry</code></td><td>Provides the ability to configure an automatic retry, set a <code>delay</code> time before the retry is executed and specify the <code>maximum</code> number of retries allowed. By default, Jigx automatically handles <strong>429</strong> (Too Many Requests) error responses for CRUD and sync methods by retrying the request up to three times, with a five-second delay between each attempt. If the request still fails after the third retry, the error is raised in the app. You can customize this behavior by configuring the handling of the 429 status in the <code>error</code> property.</td></tr><tr><td><code>table</code></td><td>Define a table where the error information specified in the <code>transform</code> property will be logged to, for example: <code>table: =@ctx.entity &#x26; "_error"</code></td></tr><tr><td><code>title</code></td><td>Title that displays on the toast notification. Defaults to the provider's title if not provided. The title property supports .</td></tr><tr><td><code>transform</code></td><td><p>Specifies the details to log in the table for the error, such as the request, response, and user context, for example: <code>'={ "id": @ctx.commandId, "type": "System Offline",</code></p><p><code>"screen": "system-offline", "response": @ctx.response, "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution, "entity": @ctx.entity, "correlationId": @ctx.correlationId}'</code></p></td></tr><tr><td><code>when</code></td><td>Checks if the result of the function is an error, the first one that resolves to true is used. - The REST provider uses a combination of actual errors encountered and the HTTP status code and message. Configure different types of actions depending on the error received, by using multiple <code>when</code> statements. If the property is not configured it defaults to the REST provider's default error check.</td></tr></tbody></table>

**Example configuration:**

{% code title="rest-function" %}
```yaml
# Configure an error section in each function file for REST endpoint,
# where errors can occur.
error:
  - when: =@ctx.response.status = 403
    title: System Offline
    description: It looks like our system is temporarily unavailable.
      We're working hard to fix this and get things back on
      track. Please try again in a little while. Thank you
      for your patience!
    # Set an automatic retry, specify the delay before the retry is actioned,
    # Set the number of retries allowed.
    retry:
      delay: "=(@.response.headers.'retry-after' ? $number(@.response.headers.'retry-after') : 5)*1000"
      maxRetries: 3
    details: =@ctx.response.body
    icon: server-error-403-hand-forbidden
    notification: false
    table: datasync-error
    transform: '={ "id": @ctx.parameters.syncId, "type": "System Offline",
      "screen": "system-offline",  "response": @ctx.response,
      "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution,
      "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
```
{% endcode %}

## Error logging

Logging errors is a crucial part of the error handling mechanism. Errors are logged into a dedicated error `table` defined by you, capturing key information for debugging and analysis. Take the information that you currently have in the context of the function and log it to the table by defining the data to be logged in the `transform` property.

* The full error coming back from the backend system should be logged.
* Expose error tables in Jigx Builder to help with troubleshooting.
* Define a datasource against the error tables.

**Error logging configuration:**

When configuring REST errors, several system expressions and variables can be used. These variables allow you to dynamically log and handle errors based on the context of the function call.The following context is available to write to the error table, using `=@ctx.variable.value`:

<table><thead><tr><th width="141.3203125">Variables</th><th>Value</th></tr></thead><tbody><tr><td>commandId</td><td>Unique id logged for the item on the commandQueue. The id matches the id in the entity table.</td></tr><tr><td>correlationId</td><td>The unique identifier that appears in the app. It is used in to help identify specific entries in the logs and to follow the user's journey while using the solution in the app. By filtering logs using this ID, you can troubleshoot issues more effectively.</td></tr><tr><td>entity</td><td>The specified table where the error context is logged</td></tr><tr><td>error</td><td><ul><li>message: string</li><li>title: string</li><li>description: string</li><li>details: string</li><li>icon: string</li><li>table: string</li><li>notification: boolean</li></ul></td></tr><tr><td>parameters</td><td>Specify any of the parameters in the function to be logged to the error table.</td></tr><tr><td>request</td><td><ul><li>method: string</li><li>url: string</li><li>headers: Record&#x3C;string, string></li><li>body:string</li><li>Buffer</li></ul></td></tr><tr><td>response</td><td><ul><li>ok: boolean</li><li>status: number</li><li>statusText: string</li><li>headers: Record&#x3C;string, string></li><li>body: any</li></ul></td></tr><tr><td>solution</td><td><ul><li>id: SolutionId</li><li>name: SolutionName</li><li>organizationId: OrganizationId</li><li><p>settings:</p><ul><li>custom: Record&#x3C;string, unknown></li></ul></li></ul></td></tr><tr><td>user</td><td><ul><li>id: string</li><li>email: string</li><li>displayName: string</li><li>avatarUrl: string</li><li>phone: string</li><li>isVerified: boolean</li><li>settings: Record&#x3C;string, unknown></li></ul></td></tr></tbody></table>

{% tabs %}
{% tab title="function-error-table" %}
```yaml
# Configure the error table and the data to log to the table,
# in the error section of the function.
table: =@ctx.entity & "_error"
transform: '={ "id": @ctx.commandId, "type": "System Offline",
  "screen": "system-offline",  "response": @ctx.response,
  "request": @ctx.request, "user": @ctx.user, "solution": @ctx.solution,
  "entity": @ctx.entity, "correlationId": @ctx.correlationId}'
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

## commandQueue table & actions

The commandQueue is a system table, when a device is offline items are queued on the table. When the device comes online the items in the queue are processed. However, if items on the queue go into error, they are not processed and remain on the queue. Errors from REST methods, except for `action.sync-entity/entities` are queued in the commandQueue table. The commandQueue is exposed in Jigx Dev tools, allowing you to [debug](../../../jigx-builder-_code-editor_/debugging.md) . You can expose the commandQueue table in a jig and then use the commandQueue actions to interact with the queued items that are in error state by either performing a retry or delete. Take note that when syncing an item or when the device is offline the `commandId` is not available.

![commandQueue](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-0iZcYVQhGLEkow2WFIWNg-20241010-080218.png)

### Actions

There are two actions related specifically to the commandQueue namely:

* `action.retry-queue-command` - executes a retry of the REST function called.
* `action.delete-queue-command` - Only deletes the item from the commandQueue. The record will still be saved locally on the device. You need to provide separately for the deleting of the local data, which can be achieved through an `action.sync-entity/entities` or executing a delete method on the local data provider.

**Action configuration:**

```yaml
swipeable:
  left:
    - icon: close
      label: Delete
      onPress:
        type: action.delete-queue-command
        options:
          id: =@ctx.current.item.id
    - icon: button-refresh-arrow
      label: Retry
      onPress:
        type: action.retry-queue-command
        options:
          id: =@ctx.current.item.id
```

### Considerations

* The `commandId` matches the `id` in the error table, this is important when you want to build a jig/UI to deal with the error.
* When using the commandQueue actions the commandQueue id (`commandId`) is required.
* Use the error table to build a jig/UI as there is more data logged to the table than the commandQueue.

![commandId & error id](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-6n7sjDXlMY1HZXwOuN78T-20241022-104927.png)

* Use the \_commandQueue table as a datasource in your solution. It behaves like a normal entity table with change events and updates.
* When `useLocalCall: true` is set, functions that rely on secrets or other authentication mechanisms not available locally will not execute.

## Examples and code snippets

See [REST error example](https://docs.jigx.com/examples/rest-errors) to understand how to configure error responses in a REST function, create a error table and use the commandQueue with actions to process the error.
