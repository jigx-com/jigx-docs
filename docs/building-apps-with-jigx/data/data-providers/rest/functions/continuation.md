# Continuation

Many REST services limit the number of items that can be retrieved from the service in a single call. To retrieve all items associated with a query, additional calls must be made to the service using a URL or additional data passed to the caller. The caller then makes repeated calls to the service using these continuation parameters to retrieve all records.

Jigx REST functions can be configured to automatically repeat calls to `continuation` functions by specifying a continuation block in the function YAML.

{% hint style="warning" %}
The continuation URL and parameters overwrite the parameters in the original function call; therefore, all parameters, including OAuth tokens and API keys, must be replicated in the continuation function.

Since the continuation URL or parameters are outside of the data returned by the function (at a higher level), the **outputTransform** of the function will need to be changed to return the **records** in their own property, and the records property specified in the function YAML to locate the output records.
{% endhint %}

## Configuration options

<table><thead><tr><th width="149.296875">Options</th><th>Description</th></tr></thead><tbody><tr><td><code>when</code></td><td>This condition determines when pagination continuation should occur. The continuation will execute only when the value exists in the API response.</td></tr><tr><td><code>url</code></td><td>This specifies the complete URL for the next page of results. Certain APIs, such as  Microsoft Graph, provide the full continuation URL in the <code>@odata.nextLink</code> response field, which includes the base endpoint plus any necessary query parameters (like skip tokens or cursors) to retrieve the subsequent batch of data. This eliminates the need to manually construct pagination URLs. Other APIs require the full <code>url</code> to be specified.</td></tr><tr><td><code>parameters</code></td><td>These are the parameters required for continuation requests. Unlike the initial request, which included the optional <code>$top</code> query parameter, continuation requests only need the authentication token. </td></tr></tbody></table>

## Example and code snippets

### Continuation using @odata.nextlink

Microsoft Graph API uses continuation URLs to request the next page of items from their services. If there are more items in the response than can be handled in a single call, or the caller has limited the number of items per page, the service will return the `@odata.nextLink` parameter specifying the URL to call to fetch the next page of results.

```json
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('bb13f9b6-d289-485f-9ae6-76be00f5bab3')/drive/root/children",
    "@odata.nextLink": "https://graph.microsoft.com/v1.0/me/drive/root/children?$top=2&$skiptoken=UGFnZWQ9VFJVRSZwX1NvcnRCZWhhdmlvcj0xJnBfRmlsZUxlYWZSZWY9TWljcm9zb2Z0K1RlYW1zK0NoYXQrRmlsZXMmc",
    "value": [
        {
	   ...
	}
    ]
}
```

All data has been returned when the `@odata.nextLink` parameter is no longer present in the results. Note, in this case, that the `nextUrl` expression is used to both check for continuation data as well as the URL to fetch the next page of data.

```yaml
provider: DATA_PROVIDER_REST
url: https://graph.microsoft.com/v1.0/me/drive/root/children
method: GET

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

operations:
  - type: operation.upsert-merge
    records: =$.items
    
outputTransform: >-
  $.{"nextLink":`@odata.nextLink`,"items":value.{"id":id,"name":name,"size":size,"lastModifiedDateTime":lastModifiedDateTime,"type":$exists(folder) ? "Folder" : "File"}}

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

### Continuation using URL

This code defines a REST API configuration for fetching tasks from ClickUp with automatic pagination handling. The `when`  property checks if the current response contains exactly 100 tasks (ClickUp's page limit). If true, it assumes there are more pages to fetch. Then the same URL and parameters as the original request is used, and the `page` number is incremented.

* **First call:** Fetches page 0 with up to 100 tasks
* **If 100 tasks returned:** Automatically makes another call for page 1
* **Continues:** Until a response has fewer than 100 tasks (indicating the last page)
* **Result:** All pages are automatically fetched and combined into a single dataset

{% code title="REST function" %}
```yaml
provider: DATA_PROVIDER_REST
method: GET
url: https://api.clickup.com/api/v2/list/{listId}/task
parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: cuapi
  listId:
    location: path
    required: true
    type: number
  page:
    location: query
    required: false
    type: number
    value: 0
outputTransform: |
  $.tasks.{
    "id": id,
    "name": name,
    "status": status.status,
    "statusColor": status.color,
    "statusType": status.type,
    "orderIndex": orderindex,
    "priority": priority.priority,
    "priorityColor": priority.color,
    "assignees": assignees,
    "dueDate": due_date,
    "startDate": start_date,
    "dateCreated": date_created,
    "dateUpdated": date_updated,
    "url": url,
    "creator": creator,
    "parent": parent,
    "tags": tags,
    "list": list,
    "project": project,
    "space": space
  }
# Configure the Continution using the full URL and when it should continue  
continuation:
  url: https://api.clickup.com/api/v2/list/{listId}/task
  when: =$count($.tasks) = 100
  parameters:
    accessToken:
      location: header
      required: true
      type: string
      value: cuapi
    listId:
      location: path
      required: true
      type: number
    page:
      location: query
      required: false
      type: number
      value: =$number(@ctx.parameters.page) + 1

```
{% endcode %}
