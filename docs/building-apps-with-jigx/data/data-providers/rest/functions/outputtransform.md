# OutputTransform

The `outputTransform` property defines how the response from a REST API is transformed into a format suitable for insertion into a local SQLite table. The transform is written using [JSONata](https://jsonata.org/) and allows for both structural mapping and logic-based processing.

Use `outputTransform` to:

* Extract and reformat data from an API response.
* Return a single object or an array of objects.
* Map data into a structure that can be inserted into local tables.

## How Output Transform Works

* When the result of the `outputTransform` is an **array of objects**, each item in the array is inserted as a separate row in the local SQLite table.
* Each key-value pair in the resulting object becomes a column-value pair in the SQLite row.
* The insertion is performed using SQLite’s `json_extract()` function to map JSON fields to database columns.

### Extracting Orders from a Customer Record

This transform extracts the `orders` array from the response. Each order object is inserted into the SQLite table as a separate row.

{% code title="API Response (JSON)" %}
```json
{
  "customerId": "1432",
  "customerName": "Johson Shipping",
  "shippingAddress1": "7645 1st Street",
  "shippingCity": "Nashville",
  "shippingState": "TN",
  "shippingZip": "78654",
  "orders":[
    {
      "orderNumber": "1234",
      "orderDescription": "Printer Refil",
      "orderTotal": 345.67,
      "customerId": "1432",
      "orderDate": "1-29-2022"
    },
    {
      "orderNumber": "654",
      "orderDescription": "Printer Paper",
      "orderTotal": 185.27,
      "customerId": "1432",
      "orderDate": "1-29-2022"
    },
    {
      "orderNumber": "8934",
      "orderDescription": "Envelopes",
      "orderTotal": 25.88,
      "customerId": "1432",
      "orderDate": "1-29-2022"
    }
  ]
}
```
{% endcode %}

Output transform to get an array of orders: `$.orders`. `$` is the root of the document and orders the array with the collection of orders.

{% code title="outputTransform" %}
```yaml
outputTransform: |
  $.orders
```
{% endcode %}

The result of the transform is:

{% code title="outputTransform (JSON result)" %}
```json
[
  {
    "orderNumber": "1234",
    "orderDescription": "Printer Refil",
    "orderTotal": 345.67,
    "customerId": "1432",
    "orderDate": "1-29-2022"
  },
  {
    "orderNumber": "654",
    "orderDescription": "Printer Paper",
    "orderTotal": 185.27,
    "customerId": "1432",
    "orderDate": "1-29-2022"
  },
  {
    "orderNumber": "8934",
    "orderDescription": "Envelopes",
    "orderTotal": 25.88,
    "customerId": "1432",
    "orderDate": "1-29-2022"
  }
]
```
{% endcode %}

## JSONata in Output Transforms

You can enhance output transforms using built-in JSONata functions such as `$trim()`, `$substring()`, `$map()`, and `$exists()`.

#### Example: YouTube Playlist Items

This example shows how to transform complex nested data. It uses logic and helper functions to clean up fields and format dates.

This example shows how to transform complex nested data. It uses logic and helper functions to clean up fields and format dates.

{% code title="YAML" %}
```yaml
provider: DATA_PROVIDER_REST
method: GET
url: https://www.googleapis.com/youtube/v3/playlistItems

outputTransform: |
  $.items[].{
    "id": id,
    "videoid": snippet.resourceId.videoId,
    "publishedat": $toMillis(snippet.publishedAt),
    "title": $contains(snippet.title, "]") ?
      $trim($substringAfter(snippet.title, "]")) :
      $trim(snippet.title),
    "description": snippet.description,
    "thumbnail": $exists(snippet.thumbnails.maxres) ?
      snippet.thumbnails.maxres.url :
      snippet.thumbnails.high.url
  }

parameters:
  key:
    location: query
    type: string
    value: xyBaQF3E1qxxxxQGl99q5Kkpa--xxx
    required: true
  playlistId:
    location: query
    type: string
    value: PL_500m6Wb0wjTjKDoM_G7MkIqLWtvCm0o
    required: true
  part:
    location: query
    type: string
    value: snippet
    required: true
  maxResults:
    location: query
    type: string
    value: "500"
    required: true
```
{% endcode %}

## Mapping Nested Arrays

You can also use `$map()` to transform nested arrays into structured fields within a single object. This example returns a single row with structured ingredients and instructions arrays. Use this pattern when you want to store related subitems within a single SQLite row, e.g., for display in a list jig using `$.eval()`.

{% tabs %}
{% tab title="YAML" %}
```yaml
outputTransform: >-
  {
    "id": $.recipes.id,
    "name": $.recipes.title,
    "image": $.recipes.image,
    "desc": $.recipes.summary,
    "ingredients": $map($.recipes.extendedIngredients, function($ingredient, $idx, $arr) {
      {
        "name": $ingredient.name
      }
    }),
    "instructions": $map($.recipes.analyzedInstructions.steps, function($instruction, $idx, $arr) {
      {
        "step": $instruction.step
      }
    })
  }
```
{% endtab %}

{% tab title="list-jig.jigx" %}
```yaml
 - type: component.section
    options:
      title: Ingredients
      children:
        - type: component.list
          options:
            data: =$eval(@ctx.datasources.randomRecipeData.ingredients)
            item: 
              type: component.list-item
              options:
                title: =@ctx.current.item.name
#         {"name": $ingredient.name}
#       })
```
{% endtab %}
{% endtabs %}
