# forRowsWithMatchingids

By default, the JSON payload returned from the REST call replaces all existing data in the SQLite database. However, when `forRowsWithMatchingIds` is specified, Jigx performs an **upsert** operation, updating or inserting records based on a matching id.

The `outputTransform` must include a field named id, which Jigx uses to match against the id column in the target table.

* If a record with the specified id already exists in the table, it will be **updated**.
* If no matching id is found, a **new row** will be **inserted**.
* **No rows are deleted** when using `forRowsWithMatchingIds`.

This approach is useful for incrementally syncing data without affecting unrelated records, making it ideal for scenarios where partial updates or record-level inserts are required.

## Example code

```yaml

# REST Data Provider with forRowsInRange function example
# This example fetches earthquake data and updates only rows within a magnitude range
provider: DATA_PROVIDER_REST
method: GET
url: https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_day.geojson
useLocalCall: true  
# Update existing records or inserts new ones based on ID matching.
forRowsWithMatchingIds: true
# Input parameters for the range values
parameters:
  mag:
    type: number
    location: query
    required: false
    value: 2.0
  dmin:  
    type: number
    location: query
    required: false
    value: 5.0

# Transform the earthquake data
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
operations:
  - type: operation.delete-insert
    table: earthquake_data
    records: |
      =$.earthquakes.{
      "id": id,
      "place": place,
      "mag": mag,
      "time": time,
      "longitude": coordinates[0],
      "latitude": coordinates[1],
      "depth": depth
      }
```
