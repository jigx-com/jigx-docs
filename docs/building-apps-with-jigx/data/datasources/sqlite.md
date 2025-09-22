# SQLite

## SQLite Query **Structure**

When using SQLite as a datasource in Jigx, queries are written in an idiomatic SQL pattern, selecting the `id` and `data` columns from Jigx tables (e.g., `[default/customers]`), applying joins with related tables (e.g., `[default/orders]`), filtering with `json_extract` expressions on the `data` JSON payload, supporting parameters like `@search` or `@status`, and finishing with standard clauses such as `ORDER BY` and `LIMIT` for predictable, efficient results.

{% code title="SQLite datasource" %}
```sql
SELECT
  id,
  data
FROM [default/customers] AS cus
INNER JOIN [default/orders] AS ord
  ON ord.customer_id = cus.id
WHERE (
    @search IS NULL OR @search = '' 
    OR json_extract(cus.data, '$.name') LIKE '%' || @search || '%'
    OR json_extract(cus.data, '$.email') LIKE '%' || @search || '%'
  )
  AND json_extract(cus.data, '$.active') = 1
  AND json_extract(ord.data, '$.status') = @status
ORDER BY
  json_extract(cus.data, '$.lastName'),
  json_extract(cus.data, '$.firstName')
LIMIT 100
```
{% endcode %}

## **Key Elements**:

<table><thead><tr><th width="282.85546875">Element</th><th>Description</th></tr></thead><tbody><tr><td><code>[default/table]</code> </td><td>FQN bracket notation (fully qualified name)</td></tr><tr><td><code>AS cus</code> </td><td>Table aliases (3-letter preferred)</td></tr><tr><td><code>json_extract(data, '$.prop')</code> </td><td>JSON property access</td></tr><tr><td><code>@search</code>, <code>@status</code> </td><td>Query parameters for filtering</td></tr><tr><td><code>LIKE '%' || @param || '%'</code> </td><td>Parameter concatenation for search</td></tr><tr><td><code>@param IS NULL OR @param = ''</code></td><td>Null/empty parameter handling</td></tr><tr><td><code>SELECT id, data</code></td><td>Standard column pattern</td></tr><tr><td><code>UPPERCASE</code></td><td>SQL keywords always uppercase</td></tr></tbody></table>

## Common Variations

### Basic List

```sql
SELECT id, data FROM [default/customers] AS cus
-- Expressions: =@ctx.datasources.customers[0].data
```

### Singleton

```sql
SELECT id, data FROM [default/customers] AS cus
WHERE id = @customerId
-- Use .isDocument(true) in datasource
-- Expressions: =@ctx.datasources.customers.data.name, =@ctx.current.item.data.name
```

### Aggregation

Use `.isDocument(true)` to avoid `@ctx.datasources.stats[0]`

```sql
SELECT
  COUNT(1) AS total,
  SUM(json_extract(ord.data, '$.amount')) AS revenue
FROM [default/orders] AS ord
WHERE json_extract(ord.data, '$.date') >= @startDate
-- Use .isDocument(true) in datasource
-- Expressions: =@ctx.datasources.stats.total, =@ctx.datasources.stats.revenue
```

## JSON Property Access

### Standard Pattern (Recommended)

```sql
SELECT id, data FROM [default/customers]
-- Use .jsonProperties('data') in datasource
-- Use data as a single JSON object, path into, pass to parameters
-- Expressions: =@ctx.current.item.data.name
```

### Shred (Special cases only)

This works fine but becomes hard to maintain with many properties eg passing 10 fields to a form.

```sql
SELECT
  id,
  json_extract(data, '$.name') AS customer_name
FROM [default/customers]  
-- Expressions: =@ctx.datasources.customers[0].customer_name, =@ctx.current.item.customer_name
```

## CTEs

Compose complexity via CTEs for clarity/maintainability.

```sql
-- Layer complexity inside CTEs
WITH base AS (
  SELECT * FROM [default/table] -- Complex query (joins, filters, windows)
),
filtered AS (
  SELECT * FROM base -- Apply filters, parameters
),
projected AS (
  SELECT * FROM filtered -- Reshape, extract fields
)
-- Keep outer SELECT small
SELECT id, name, email FROM projected -- Final projection, filtering
```

## SDK Integration

```typescript
// Dynamic datasource
screen.addDatasource.sqlite('filtered-customers', 'dynamic')
  .entity('default/customers')
  .query(`
    SELECT id, data FROM [default/customers] AS cus
    WHERE @search IS NULL OR @search = ''
       OR json_extract(cus.data, '$.name') LIKE '%' || @search || '%'
  `)
  .queryParameter('search', '=@ctx.components.searchBox.state.value')
  .jsonProperties('data')
  .isDocument(false)  // Array of results (default)

// Single record datasource  
screen.addDatasource.sqlite('customer-detail', 'dynamic')
  .entity('default/customers')
  .query('SELECT id, data FROM [default/customers] WHERE id = @customerId')
  .queryParameter('customerId', '=@ctx.jig.inputs.customerId')
  .jsonProperties('data')
  .isDocument(true)   // Single document result
```

## Quick Patterns

```sql
-- Multi-field search
json_extract(data, '$.name') LIKE '%' || @search || '%'
OR json_extract(data, '$.email') LIKE '%' || @search || '%'

-- Null-safe parameter
@param IS NULL OR @param = '' OR condition

-- Nested property
json_extract(data, '$.address.city') = 'Seattle'

-- Date comparison
json_extract(data, '$.createdAt') >= @startDate

-- Boolean filter
-- Note: JSON booleans compare as 1/0 in SQLite
json_extract(data, '$.isActive') = 1
```

## Considerations

* &#x20;Use the following in SQLite queries:
  * Always use FQN bracket notation: `[default/table]`
  * All keywords UPPERCASE: `SELECT`, `FROM`, `WHERE`
  * &#x20;`json_extract()`
  * Use table aliases for clarity: `AS cus`, `AS ord`
  * Use `@params` for filters
  * Parameters start with `@`: `@search`, `@customerId`
  * Standard pattern: `SELECT id, data` with `.jsonProperties('data')`
  * Single records use `.isDocument(true)`
* Avoid using the following in SQLite queries:&#x20;
  * Lowercase keywords
  * Field extraction
  * Unqualified tables
  * direct column access
