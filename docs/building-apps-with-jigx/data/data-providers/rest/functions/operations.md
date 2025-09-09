# Operations

Operations in a Jigx function allow you to manipulate data after a REST call completes. They are used to process the response and store it across one or more local SQLite tables. Operations run automatically after the REST function executes and can be defined for both success and error scenarios.

## When and where to use operations

`operations` can be defined in the following places:

* Under the `operations` property in the main function.
* Within `guard` functions.
* Inside the `error` block for error-specific handling.

`operations` are particularly useful when:

* The REST response must be split and inserted into multiple tables.
* You need to control how data is stored in the local SQLite tables, e.g., merge, replace, or delete-insert.
* You want to run custom SQL after a function executes.

## Multi-table operations

Specify multiple output tables and operations for both success and error scenarios.

* Use the operations property to specify an array of operations (executed in sequence) at the top level of the function or under an error handler.
* Each operation specifies an operation `type`, target `table`, and the `records` to use for the operation on the table.
* If the type is `execute_sql` you can specify an array of `statements`, similar to the [action.execute-sql](https://docs.jigx.com/examples/readme/actions/execute-sql) in a jig.
* If you've prepared data using `outputTransform`, you must reference the output in your `operations` or adjust your records to account for the transformed structure. In this case, `operations` will use `ctx.output`, the result of `outputTransform` becomes `ctx.output`.
* Each `operation` targets a `table` and specifies what `records` to insert or update. The `records` property can use JSONata expressions to transform the response data.

{% code title="Operations" %}
```yaml
operations:
  - table: =@.entity
    type: operation.upsert-merge
    records: |
      =$each($.response.body, function($v, $k) {
        $merge([{ "id": $k}, $v])
      })
  - table: local-flags
    type: operation.delete-insert
    records: |
      =$each(response.body, function($v, $k) {
          {
              "id": $k,
              "name": $v.name,
              "flag": $v.emoji
          }
      })
  - table: local-counts
    type: operation.upsert-replace
    records: |
      ={
        'id': 'local-countries',
        'count': $count(@ctx.queries.existing-countries)
      }
```
{% endcode %}

## Operation Property

|   |   |
| - | - |
|   |   |
|   |   |
|   |   |

## Table Operation Types

Applies to the operations that are performed on the local data from the remote data.

| Type                                                               | Property                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------------------------------------ | -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>DELETE_INSERT<br>(used to sync data)</p>                        | `operation.delete_insert`  | <p>Deletes old records that match a specified range and rows with matching values and inserts new records.<br>Deletion runs at the beginning of the function.<br>The table is only cleared on non-continuation operations on the first call.<br>Uses this to overwrite the local data with the remote data.</p>                                                                                                                                     |
| UPSERT\_REPLACE                                                    | `operation.upsert_replace` | <p>Appends new records and replaces matching existing records. (Continuous update).<br>The data of any existing record is replaced with the data from the matched new record.<br>Records are matched by id (primary key).<br>Use this type to append records to the local data and replace any existing records with the same id,<br>leaving unmatched records unchanged and undeleted.</p>                                                         |
| <p>UPSERT_MERGE<br>(used on CRUD methods and output transform)</p> | `operation.upsert_merge`   | <p>Appends new records and merges matching existing records.<br>The data of any existing record is merged with the data from the matched new record.<br>Only top-level properties are copied, overwriting any existing top-level properties.<br>Records are matched by id (primary key).<br>Use this to append records to the local data and merge any existing records with the same id,<br>leaving unmatched records unchanged and undeleted.</p> |
| EXECUTE\_SQL                                                       | `operation.execute_sql`    | Executes a custom SQL operation specified with the SQL statement and parameters. This is the same functionality as the [execute-sql](https://docs.jigx.com/examples/readme/actions/execute-sql) action, which runs when a button is tapped; here, it runs when the function finishes or on continuation.                                                                                                                                            |

## Expressions

<table><thead><tr><th width="115.1015625"></th><th></th><th></th></tr></thead><tbody><tr><td>records</td><td><code>=@ctx.record.{primaryKey}</code></td><td>Defines the primary key, including the ability to reference the full record.</td></tr></tbody></table>
