# Queries

The `queries` property allows you to define Just-In-Time (JIT) queries that are executed when a function runs. These queries retrieve local data from the SQLite database at the moment the function executes, ensuring that decisions and operations are based on the most current information available.

## Purpose and benefits

* Ensures accuracy by querying local tables at runtime.
* Reduces stale data by removing the need to store older data in the Command Queue.
* Supports offline use by relying on local data, not remote API calls.
* Improves flexibility by allowing conditional logic or table operations to be based on the current state.

## How queries work

* Queries are **evaluated** at the time the function executes (when it comes off the command queue).
* They are **re-evaluated** on continuation unless `onContinuation: false` is explicitly set.
* Results of the queries are available in expressions using:\
  `=@ctx.queries.{query-name}`

## Result types

The `resultType` property lets you control the format of the returned data:

<table><thead><tr><th width="182.44921875">Type</th><th>Description</th><th>Returned value</th></tr></thead><tbody><tr><td><code>records</code> (default)</td><td>Returns all matching records</td><td>Array of objects</td></tr><tr><td><code>record</code></td><td>Returns the first matching record</td><td>Single object</td></tr><tr><td><code>scalar</code></td><td>Returns a single value from the first column of the first record</td><td>Single value (string, number, etc.)</td></tr></tbody></table>

If no records match the query:

* records returns an empty array \[]
* record and scalar return null

In this example:

* current-record uses a parameter to fetch a specific country from the local table.
* existing-countries fetches all records from the local/countries table.

{% code title="Queries" %}
```yaml
# In the function definition.
queries:
  current-record:
    statement: SELECT * FROM [local/countries] WHERE [id] = @id
    parameters:
      id: =@.parameters.countryId
  existing-countries:
    statement: SELECT * FROM [local/countries]
```
{% endcode %}

You can access the results in other parts of the function like this:

{% code title="YAML" %}
```yaml
records: =@ctx.queries.existing-countries
```
{% endcode %}

## Queries properties

<table><thead><tr><th width="162.85546875">Properties</th><th>Description</th></tr></thead><tbody><tr><td><code>dependencies</code></td><td>The queries that this query depends on. They will be executed before this query. Dependencies allow you to stop recursive queries, because queries can be inputs to each other.</td></tr><tr><td><code>jsonColumns</code></td><td>The columns that are automatically parsed as JSON string.<br>Defaults to no JSON columns to parse.</td></tr><tr><td><code>onContinuation</code></td><td>Set to false re-runs the query on each continuation of the function. Defaults to true, so the query only runs initially by default and not again on each continuation.</td></tr><tr><td><code>parameters</code></td><td>Named parameters used in the query statement. They are referenced using the @ prefix (e.g., @id). If not prefixed manually, the @ is automatically added. Defaults to no parameters.</td></tr><tr><td><code>resultType</code></td><td>Defines the expected result format. Can be one of: records (default), record, or scalar.</td></tr><tr><td><code>statement</code></td><td>The SQL query statement to execute.</td></tr><tr><td><code>tables</code></td><td>The tables to use in the query. Defaults to none. These tables are validated to exist before the query is executed.</td></tr></tbody></table>

