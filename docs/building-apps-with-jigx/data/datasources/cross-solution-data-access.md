---
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
---

# Cross-Solution Data Access

## Cross-Package Datasources and Action Execution

Jigx solutions are self-contained by default, but there are scenarios where one solution needs to read data from, or trigger actions in, another installed solution. Cross-package support makes this possible without duplicating data or creating custom sync pipelines.

***

### Overview

Cross-package support lets you:

* Query SQLite entities from another installed solution in a single datasource.
* Execute actions defined in another solution from your own jig.
* Mix local and cross-package data in the same SQL query using `JOIN` or `UNION ALL`.

The runtime handles the underlying database attachment automatically when it detects a `package` property in your configuration.

***

### Cross-Package Datasources

#### Declaring cross-package entities

Add a `package` property to any entity definition in your `datasource.sqlite` config to tell Jigx which solution owns that entity. The `package` value is the name of the solution whose data will be accessed. Entities without a `package` property resolve to the current solution as normal.

```yaml
datasources:
  tasks:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/tasks                   # local entity
        - entity: default/task-categories         # local entity
        - entity: default/project-tasks
          package: projects                      # entity from another solution
        - entity: default/project-categories
          package: projects                      # entity from another solution
```

#### Referencing cross-package tables in SQL

In your SQL query, reference a cross-package table using **bracket-dot notation**:

```sql
[package-name].[entity-name]
```

Local tables use the standard bracket notation:

```sql
[default/tasks]
```

#### Full example: UNION ALL across two solutions

```yaml
datasources:
  all-tasks:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/tasks                   # local entity
        - entity: default/task-categories         # local entity
        - entity: default/project-tasks
          package: projects                      # entity from another solution
        - entity: default/project-categories
          package: projects                      # entity from another solution
      rewriteQuery: false
      query: |
        WITH [combined] AS (
          SELECT
            T.id,
            json_extract(T.data, '$.name')        AS name,
            json_extract(T.data, '$.description') AS description,
            json_extract(T.data, '$.status')      AS status,
            json_extract(T.data, '$.assignedTo')  AS assignedTo,
            json_extract(T.data, '$.createdAt')   AS createdAt,
            C.id                                  AS categoryId,
            json_extract(C.data, '$.name')        AS category,
            NULL                                  AS package
          FROM [default/tasks] AS T
          LEFT JOIN [default/task-categories] AS C
            ON json_extract(T.data, '$.categoryId') = C.id
          UNION ALL
          SELECT
            T.id,
            json_extract(T.data, '$.name')        AS name,
            json_extract(T.data, '$.description') AS description,
            json_extract(T.data, '$.status')      AS status,
            json_extract(T.data, '$.assignedTo')  AS assignedTo,
            json_extract(T.data, '$.createdAt')   AS createdAt,
            C.id AS categoryId,
            json_extract(C.data, '$.name') AS category,
            'projects' AS package
          FROM [projects].[default/project-tasks] AS T
          LEFT JOIN [projects].[default/project-categories] AS C
            ON json_extract(T.data, '$.categoryId') = C.id
        )
        SELECT * FROM [combined]
        ORDER BY [name]
      queryParameters:
        assignedTo: =@.user.email
```

***

### The `rewriteQuery` Option

The `rewriteQuery` option controls whether Jigx automatically rewrites the `$.property` shorthand into full `json_extract()` calls.

<table><thead><tr><th width="164.1640625">Value</th><th>Behaviour</th></tr></thead><tbody><tr><td><code>true</code> (default)</td><td><code>$.name</code> is rewritten to <code>json_extract(data, '$.name') AS [name]</code> before execution. The result is cached after the first run.</td></tr><tr><td><code>false</code></td><td>The query is passed to SQLite exactly as written. Use this when your query already contains explicit <code>json_extract()</code> calls.</td></tr></tbody></table>

**Always set `rewriteQuery: false` for cross-package queries.** The rewriter does not understand `[alias].[table]` syntax and may corrupt your cross-package table references. Since cross-package queries already require explicit `json_extract()` calls, there is nothing for the rewriter to do anyway.

#### Performance note

For single-solution queries, the shorthand with `rewriteQuery: true` (default) is the recommended approach. The rewrite cost is paid only on the first run; subsequent executions hit the query cache and the performance is identical to writing explicit `json_extract()` yourself. SQLite query execution time dominates in both cases.

***

### Cross-Package Action Execution

Add a `package` property to `action.execute-action` to run an action defined in another solution.

```yaml
onConfirmed:
  type: action.execute-action
  options:
    package: projects
    action: action-delete-task
    parameters:
      taskId: =@.current.item.id
```

Omitting `package` preserves existing behavior.  The action resolves within the current solution.

#### Error handling

| Scenario                                              | Result                                             |
| ----------------------------------------------------- | -------------------------------------------------- |
| `package` value does not match any installed solution | Runtime error - package not found                  |
| Package exists but the named action does not          | Runtime error - action not found in target package |
| Parameters fail validation in the target action       | Standard parameter validation error                |

***

### Guard Functions and `performOperations`

The `performOperations` property gives you explicit control over whether table write operations run after a guard function executes. By default, operations run only when the guard returns a falsy value (i.e. the guard failed).

```yaml
guard:
  function: my-guard-function
  performOperations: =@ctx.guard.output.shouldWrite
  operations:
    - type: operation.upsert-merge
      table: default/tasks
```

| `performOperations` value | Operations execute when…                                                                                              |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| _(not set — default)_     | Guard returns falsy                                                                                                   |
| `true`                    | Always                                                                                                                |
| `false`                   | Never                                                                                                                 |
| `=expression`             | Expression evaluates to truthy. Has access to `@ctx.guard.output` (the guard's return value) and `@ctx.guard.result`. |

***

### Considerations

* **Package (solution) not on device** - the datasource or action will fail at runtime. Ensure the target solution is accessible before referencing it.
* **Entity exists in config but not in target database** - the query will return no rows for that table, or error depending on the SQL structure.
* **Circular dependencies** - Solution A referencing Solution B, which references Solution A, is not supported and will produce undefined behavior.
* **Offline behavior** - cross-package queries read from the local on-device SQLite databases, so they work offline provided both solutions have synced their data.
* **Schema validation** — `package` values must match the solution name format. Invalid formats are rejected at the schema validation stage before execution.

## Examples and code snippets

For a simple working example see the [Cross Solution Datasource](https://docs.jigx.com/examples/readme/datasource/cross-solution-datasource-access) example.&#x20;
