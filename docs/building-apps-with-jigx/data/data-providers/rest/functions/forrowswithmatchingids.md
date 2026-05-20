# forRowsWithMatchingids

By default, the JSON payload returned from the REST call replaces all existing data in the SQLite database. However, the `forRowsWithMatchingIds` property controls how data from REST API responses is synchronized with the local SQLite database.&#x20;

This approach is useful for incrementally syncing data without affecting unrelated records, making it ideal for scenarios where partial updates or record-level inserts are required.

### Understanding data sync behavior

The behavior of data synchronization depends on whether `forRowsWithMatchingIds` and explicit `operations` are specified. When using explicit `operations`, you lose the automatic upsert-merge behavior provided with the `forRowsWithMatchingIds` and must define all desired operations yourself. The `id` field in your `outputTransform` is critical for matching records. \
There are three scenarios:

<table><thead><tr><th width="123.12109375">Scenario</th><th width="401.5">Combinations</th><th>Results</th></tr></thead><tbody><tr><td>Scenario 1 <br>(Default)</td><td>No <code>forRowsWithMatchingIds</code> + no <code>operations</code></td><td>Wipe and sync</td></tr><tr><td>Scenario 2 (Automatic)</td><td><code>forRowsWithMatchingIds: true</code> + no <code>operations</code> </td><td> Automatic upsert-merge</td></tr><tr><td>Scenario 3 (Manual)</td><td><code>forRowsWithMatchingIds</code> + explicit <code>operations</code> </td><td>You control the behavior</td></tr></tbody></table>

<details>

<summary><strong>Scenario 1</strong>: No <code>forRowsWithMatchingIds</code>, no <code>operations</code> (Default behavior)</summary>

**Use case:** When you want to completely refresh the table contents.

When neither `forRowsWithMatchingIds` nor explicit `operations` are specified, Jigx performs a **wipe and sync**:

* **Deletes** all existing records in the table
* **Inserts** all new records from the API response

This is the standard default operation that completely replaces the table contents.

```yaml
provider: DATA_PROVIDER_REST
method: GET
url: https://api.example.com/data
useLocalCall: true
outputTransform: |
  {
    "data": $.items
  }
# No forRowsWithMatchingIds specified
# No operations specified
# Result: Complete table replacement (wipe and sync)
```

</details>

<details>

<summary><strong>Scenario 2</strong>: <code>forRowsWithMatchingIds</code> specified, no <code>operations</code></summary>

**Use case**: Use for simple incremental syncing without deletions.

When `forRowsWithMatchingIds: true` is specified **without** any explicit `operations`, Jigx automatically performs an **upsert-merge** operation:

* **Updates** existing records where the `id` matches
* **Inserts** new records where no matching `id` exists
* **Preserves** existing records that are not in the API response (no deletion)

The `outputTransform` must include a field named `id`, which Jigx uses to match against the `id` column in the target table.

```yaml
provider: DATA_PROVIDER_REST
method: GET
url: https://{api.example.com}/data
useLocalCall: true
# Automatically performs upsert-merge when no operations are specified
forRowsWithMatchingIds: true

outputTransform: |
  {
    "earthquakes": features[].{
      "id": id,
      "place": properties.place,
      "mag": properties.mag,
      "time": properties.time,
      "coordinates": geometry.coordinates,
      "depth": geometry.coordinates[2]
    }
  }
# No operations specified - automatic upsert-merge behavior applies.
```

</details>

<details>

<summary><strong>Scenario 3:</strong> <code>forRowsWithMatchingIds</code> with explicit <code>operations</code></summary>

**Use case**: When you need custom logic, such as handling server-side deletions or complex synchronization.

<mark style="color:red;">**IMPORTANT:**</mark> When you specify explicit `operations`, `forRowsWithMatchingIds` loses its automatic upsert-merge behavior. You must explicitly define the `operations` you want to perform.

This scenario is useful when you need custom synchronization logic, such as:

* Deleting records that no longer exist on the server
* Combining upsert with cleanup operations

```yaml
provider: DATA_PROVIDER_REST
method: GET
useLocalCall: true
url: https://{api.example.com}/ExpenseReceipt
records: =$.data
# forRowsWithMatchingIds is used with explicit operations.
forRowsWithMatchingIds: true

outputTransform: >-
  ={
    "top": @ctx.parameters."$top",
    "skip": @ctx.parameters."$skip",
    "data": @ctx.response.body ? $map(@ctx.response.body, function($item){
      $merge([$item, { "Remote": true }])
    }) : []
  }

operations:
  # First operation: 
  # Delete local records that no longer exist on the server.
  - type: operation.execute-sql
    statements:
      - statement: |
          ="DELETE FROM [expense-receipts] WHERE [id] NOT IN (" & 
          $join($map(@ctx.response.body.id, function($v) { "'" & $v & "'" }), ", ") & 
          ")"
    tables:
      - expense-receipts
  
  # Second operation: 
  # Explicitly define upsert-merge for matching records.
  - type: operation.upsert-merge
    table: expense-receipts
    records: |
      =@ctx.response.body ? $map(@ctx.response.body, function($item){
        $merge([$item, { "Remote": true }])
      }) : []
```

</details>

### Considerations

* Always ensure your `outputTransform` includes an `id` field when using `forRowsWithMatchingIds`.
* When using explicit `operations` ([Scenario 3](forrowswithmatchingids.md#scenario-3-forrowswithmatchingids-with-explicit-operations)), carefully plan your operation sequence.
* Test your synchronization logic thoroughly, especially when handling deletions.
