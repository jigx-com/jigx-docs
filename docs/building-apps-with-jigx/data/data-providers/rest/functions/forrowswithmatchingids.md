# forRowsWithMatchingids

By default, the JSON payload returned from the REST call replaces all existing data in the SQLite database. However, when `forRowsWithMatchingIds` is specified, Jigx performs an **upsert** operation, updating or inserting records based on a matching id.

The `outputTransform` must include a field named id, which Jigx uses to match against the id column in the target table.

* If a record with the specified id already exists in the table, it will be **updated**.
* If no matching id is found, a **new row** will be **inserted**.
* **No rows are deleted** when using `forRowsWithMatchingIds`.

This approach is useful for incrementally syncing data without affecting unrelated records, making it ideal for scenarios where partial updates or record-level inserts are required.
