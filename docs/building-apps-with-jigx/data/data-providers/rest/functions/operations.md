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

<table><thead><tr><th width="193.921875"></th><th></th></tr></thead><tbody><tr><td><code>conversions</code></td><td><p>Converting files runs per operation. This holds an array of properties that should be converted. The following properties control the conversion:</p><ul><li><code>property</code>: The name of the property to convert.</li><li><code>from</code>: Format of the input data. It can be buffer, base64, data-uri, or local-uri.</li><li><code>to</code>: Format of the converted data. It can be base64, data-uri, buffer, or local-uri.</li><li><code>convertHeicToJpg</code>: When set to true, and the file being converted is HEIC, it is converted to JPG. </li></ul><p>Conversions can be set up as a static array of definitions or dynamically as an array returned by an expression. To set up dynamic conversions, use the expression:<br> <code>conversions: =@ctx.datasources.conversions</code>, applicable to both local and global actions. See <a href="../../../file-handling.md">File handling</a> for details on using conversions in REST functions.</p></td></tr><tr><td><code>forRowsWithValues</code></td><td>Only applies to <code>operation.delete-insert</code></td></tr><tr><td><code>forRowsInRange</code></td><td>Only applies to <code>operation.delete-insert</code></td></tr><tr><td><code>parameters</code></td><td>Only applies to <code>operation.execute_sql</code>. The parameters used in the above statement.</td></tr><tr><td><code>primaryKey</code></td><td>Specify the remote data column that must be used as the primary key in the local data, such as Customer ID. This allows you to specify an expression (<code>=@ctx.record.CustomerID</code>) to define the primary key, including the ability to reference the whole record. This enables the building of dynamic keys, for example, by concatenating multiple fields from the record to construct an ID, timestamp, or GUID.</td></tr><tr><td><code>records</code></td><td>What records to use for the table operation, can manipulate data. Evaluates the expression against the function inputs and result to construct the records for the specified table. The constructed data will be stored in the table.</td></tr><tr><td><code>statements</code></td><td>Only applies to <code>operation.execute_sql</code>. List of statements to execute in sequence. Multiple statements can be configured to execute in sequence.<br><code>statement</code> - the SQL statement to execute against the solution database.</td></tr><tr><td><code>tables</code></td><td>Only applies to <code>operation.execute_sql</code>. The tables affected by the <code>statements</code>. Before executing the statements, a check ensures that the tables exist. After execution any datasources that use these entities will be notified that the database was changed.</td></tr><tr><td><code>timeStamp</code></td><td>Use a timestamp such as last <em>modified</em> from the remote data that must be used as the timestamp in the local table.</td></tr><tr><td><code>type</code></td><td>See the table operations types in the table below.</td></tr><tr><td><code>when</code></td><td>Specify the condition under which the function should execute (default) and when it should be skipped.</td></tr></tbody></table>

## Table Operation Types

Applies to the operations that are performed on the local data from the remote data.

<table><thead><tr><th width="185.54296875">Type</th><th width="230.5703125">Property</th><th>Description</th></tr></thead><tbody><tr><td>DELETE_INSERT<br>(used to sync data)</td><td><code>operation.delete_insert</code></td><td>Deletes old records that match a specified range and rows with matching values and inserts new records.<br>Deletion runs at the beginning of the function.<br>The table is only cleared on non-continuation operations on the first call.<br>Uses this to overwrite the local data with the remote data.</td></tr><tr><td>UPSERT_REPLACE</td><td><code>operation.upsert_replace</code></td><td>Appends new records and replaces matching existing records. (Continuous update).<br>The data of any existing record is replaced with the data from the matched new record.<br>Records are matched by id (primary key).<br>Use this type to append records to the local data and replace any existing records with the same id,<br>leaving unmatched records unchanged and undeleted.</td></tr><tr><td>UPSERT_MERGE<br>(used on CRUD methods and output transform)</td><td><code>operation.upsert_merge</code></td><td>Appends new records and merges matching existing records.<br>The data of any existing record is merged with the data from the matched new record.<br>Only top-level properties are copied, overwriting any existing top-level properties.<br>Records are matched by id (primary key).<br>Use this to append records to the local data and merge any existing records with the same id,<br>leaving unmatched records unchanged and undeleted.</td></tr><tr><td>EXECUTE_SQL</td><td><code>operation.execute_sql</code></td><td>Executes a custom SQL operation specified with the SQL statement and parameters. This is the same functionality as the <a href="https://docs.jigx.com/examples/readme/actions/execute-sql">execute-sql</a> action, which runs when a button is tapped; here, it runs when the function finishes or on continuation.</td></tr></tbody></table>

## Expressions

<table><thead><tr><th width="115.1015625"></th><th></th><th></th></tr></thead><tbody><tr><td>records</td><td><code>=@ctx.record.{primaryKey}</code></td><td>Defines the primary key, including the ability to reference the full record.</td></tr></tbody></table>
