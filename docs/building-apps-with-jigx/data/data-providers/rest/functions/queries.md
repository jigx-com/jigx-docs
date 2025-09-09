# Queries

The `queries` property allows you to define Just-In-Time (JIT) queries that are executed when a function runs. These queries retrieve local data from the SQLite database at the moment the function executes, ensuring that decisions and operations are based on the most current information available.

## Purpose and benefits

* Ensures accuracy by querying local tables at runtime.
* Reduces stale data by removing the need to store older data in the Command Queue.
* Supports offline use by relying on local data, not remote API calls.
* Improves flexibility by allowing conditional logic or table operations to be based on current state.

## How queries work

* Queries are **evaluated** at the time the function executes (when it comes off the command queue).
* They are **re-evaluated** on continuation unless `onContinuation: false` is explicitly set.
* Results of the queries are available in expressions using:\
  `=@ctx.queries.{query-name}`

## Result types

The `resultType` property lets you control the format of the returned data:

| Type                | Description                                                      | Returned value                      |
| ------------------- | ---------------------------------------------------------------- | ----------------------------------- |
| `records` (default) | Returns all matching records                                     | Array of objects                    |
| `record`            | Returns the first matching record                                | Single object                       |
| `scalar`            | Returns a single value from the first column of the first record | Single value (string, number, etc.) |

