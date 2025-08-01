---
title: File handling
slug: uGaQ-file-handl
createdAt: Thu Nov 16 2023 15:04:27 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Nov 01 2024 09:34:16 GMT+0000 (Coordinated Universal Time)
---

Jigx stores files as local files on the device and returns the file's URI as the default value. When saving these files to a datasource, you must convert files from the local-uri to base64, data-uri, or buffer. The opposite is true when handling the files returned from the datasource; you must convert them from their saved state (base64, data-uri, or buffer) to a local-uri.

Type of files:

- Images
- Documents

Image files can be used in the following functionality:

| **Data**                       | **Conversion configuration**                                   | **Result**                                                                     |
| ------------------------------ | -------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| REST Provider calls with files | Add the conversion to the REST function                        | GET - incoming&#xA;SAVE - outgoing&#xA;CREATE - outgoing&#xA;UPDATE - outgoing |
| SQL Provider calls with files  | Add the conversion to the REST function                        | GET - incoming&#xA;SAVE - outgoing&#xA;CREATE - outgoing&#xA;UPDATE - outgoing |
| Datasource queries with files  | Add the conversion to the datasource when using Dynamic Data.  | Incoming                                                                       |
| Actions with files             | Add the conversion to the action when saving images and files. | outgoing                                                                       |

The `conversions` property allows you to configure the file conversion to the required format.

| **Core structure** |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `conversions:`     | This holds an array of properties that should be converted. The following properties control the conversion:&#xA;- `property:` The name of the property to convert.&#xA;- `from:` Format of the input data. It can be buffer, base64, data-uri, or local-uri.&#xA;- `to:` Format of the converted data. It can be base64, data-uri, buffer, or local-uri.&#xA;- `convertHeicToJpg:` When set to `true`, and the file being converted is HEIC, it is converted to JPG.&#xA;&#xA;Conversions can be set up as a static array of definitions or dynamically as an array returned by an expression. To set up dynamic conversions, use the expression `conversions: =@ctx.datasources.conversions`, applicable to both local and global actions. |

Referencing files in a jig - You can access the file using the `state` of the components and properties in a jig, such as [media-field](https://docs.jigx.com/examples/media-field) or [avatar-field](https://docs.jigx.com/examples/avatar). When referencing files in jigs use the `.state.value` configuration.
For example:

- `file: =@ctx.components.profilePicture.state.value`
- `image: =@ctx.components.image.state.value`

## Considerations

- Conversions should be configured within the SQL and REST functions. When the conversion is configured in the function, it stores the data as the 'from' type in the datasource.
- When conversions are done at the datasource level, they are still stored in the datasource as their original value. They are only converted after the fact when requested; however, the datasource value does not change.&#x20;
- Do not load data back from buffer using the Dynamic Data provider; the file will not show.&#x20;
- When saving images to Dynamic Data consider the file size. You can reduce the file size in the [media-field](https://docs.jigx.com/examples/media-field) by configuring the `imageQuality` property.
- Use `convertHeicToJpg` to ensure images are visible on iOS and Android devices. The property is available for REST and SQL functions, Dynamic Data and actions.

:::hint{type="warning"}
Jigx does not recommend storing images in Dynamic Data (via any conversion), as the max file size per record is 350K.
:::

## Examples and code snippets

## Convert incoming data

::::ExpandableHeading

### REST & SQL function

In the examples below, the file conversions are configured in the** REST and SQL (GET) functions **to convert the incoming files.

:::CodeblockTabs
rest-function-in

```yaml
provider: DATA_PROVIDER_REST
method: GET
format: pdf #pdf indicates a generic binary type
url: https://graph.microsoft.com/v1.0/me/photo/$value
outputTransform: $.{"data":$.data,"userId":$.inputs.userId.value} #add the email input to the output to identify image later in select
useLocalCall: true
parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: oauth.microsoft #Use manage.jigx.com to define credentials for your solution
  userId:
    type: string
    location: path
    required: true
conversions:
  - property: data
    from: base64
    to: local-uri
```

sql-function-in

```yaml
provider: DATA_PROVIDER_SQL
method: query
connection: test-db
query: SELECT TOP(@top) Id, FirstName, LastName, AvatarBase64, AvatarDataUri, AvatarBuffer FROM Employee
parameters:
  top:
    location: input
    required: false
    type: number
    value: 10
conversions:
  - property: AvatarBuffer
    from: buffer
    to: local-uri
  - property: AvatarBase64
    from: base64
    to: local-uri
  - property: AvatarDataUri
    from: data-uri
    to: local-uri
```

:::
::::

## Convert outgoing data

::::ExpandableHeading

### REST & SQL function

In the examples below, the file conversions are configured in the **REST and** **SQL \*\***(SAVE/CREATE/UPDATE) \***\*functions** to convert the files that are outgoing to REST and SQL.

:::CodeblockTabs
rest-function-out

```yaml
provider: DATA_PROVIDER_REST
method: PATCH
url: https://graph.microsoft.com/v1.0/me/photo/$value
useLocalCall: true
parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: oauth.microsoft # Use manage.jigx.com to define credentials for your solution
  Content-Type:
    location: header
    required: true
    type: string
    value: image/jpeg # set the content type of the body
  file:
    location: body
    required: true
    type: image
conversions:
  - property: file
    from: local-uri
    to: buffer
```

sql-function-out

```yaml
provider: DATA_PROVIDER_SQL
method: execute
connection: test-db
procedure: AddWidget
parameters:
  firstname:
    location: input
    required: true
    type: string
  lastname:
    location: input
    required: true
    type: string
  avatarbase64:
    location: input
    required: true
    type: string
  avatardatauri:
    location: input
    required: true
    type: string
  avatarbuffer:
    location: input
    required: true
    type: file
    encoding: binary
conversions:
  - property: avatarbuffer
    from: local-uri
    to: buffer
  - property: avatarbase64
    from: local-uri
    to: base64
  - property: avatardatauri
    from: local-uri
    to: data-uri
```

:::
::::

## Datasource conversion

In this example, the Dynamic Data image file conversion is configured in the datasource to convert the files to be used in the solution.

:::CodeblockTabs
datasource-conversion

```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_DYNAMIC
  entities:
    - default/category
  query: |
    SELECT id, '$.name', '$.description', '$.image'
    FROM [default/category]
    ORDER BY [name]
  conversions:
    - property: image
      from: base64
      to: local-uri
```

:::

## Action image conversion

File conversions in actions can be configured with Dynamic Data, SQL, and REST providers. They can be set up as a static array of definitions or dynamically as an array returned by an expression. To set up dynamic conversions, use the expression `conversions: =@ctx.datasources.conversions`, applicable to both local and global actions.

:::CodeblockTabs
execute-entity-action (static)

```yaml
- type: action.execute-entity
    options:
      title: Save
      provider: DATA_PROVIDER_DYNAMIC
      entity: default/category
      method: save
      data:
        id: =@ctx.jig.inputs.categoryId
        name: =@ctx.components.name.state.value
        description: =@ctx.components.description.state.value
        # reference the image using an expression
        image: =@ctx.components.image.state.value
 # Static conversion configuration
      conversions:
        - property: image
          from: local-uri
          to: base64
```

execute-entity-action (dynamic)

```yaml
- type: action.execute-entity
    options:
      title: Save
      provider: DATA_PROVIDER_DYNAMIC
      entity: default/category
      method: save
      data:
        id: =@ctx.jig.inputs.categoryId
        name: =@ctx.components.name.state.value
        description: =@ctx.components.description.state.value
        # reference the image using an expression
        image: =@ctx.components.image.state.value
# Dynamic conversion configuration
      conversions: =@ctx.datasources.conversions
```

datasource

```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_DYNAMIC
  entities:
    - default/category
  query: |
    SELECT id, '$.name', '$.description', '$.image'
    FROM [default/category]
    ORDER BY [name]
  conversions:
    - property: image
      from: base64
      to: local-uri
```

:::

## Add multiple files with SQL data provider

This example uses the `text-field` with `mediaType: image` and `isMultiple: true` to add multiple images to SQL. The `conversion` of the files is done in the SQL function.

:::CodeblockTabs
sql-add-widget-multiple-function.jigx

```yaml
# Add under function folder
provider: DATA_PROVIDER_SQL
method: execute
connection: SportConnect
procedure: AddMultipleAvatar
parameters:
  avatarbuffer:
    encoding: binary
    location: input
    required: true
    type: file
  description:
    location: input
    required: true
    type: string

conversions:
  - from: local-uri
    property: avatar
    to: buffer
```

sql-get-widget-multiple-jigx

```yaml
# Add under function folder
provider: DATA_PROVIDER_SQL
method: query
connection: SportConnect

query: |
  SELECT  
    Id, 
    description,
    Avatar
  FROM avatarMultiConversion

conversions:
  - property: Avatar
    from: buffer
    to: local-uri
```

add-widget-mutiple-sql.jigx

```yaml
# Add under jig folder
title: Add Widget Multiple
type: jig.default

onFocus:
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_SQL
    entities:
      - entity: avatarMultiConversion
        function: sql-get-widget-multiple

datasources:
  allImages:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: avatarMultiConversion
      query: |
        SELECT
          '$.Id',
          '$.type',
          '$.Avatar'
        FROM [avatarMultiConversion]

children:
  - type: component.form
    instanceId: add-widget-multiple
    options:
      children:
        - instanceId: description
          options:
            label: Description
          type: component.text-field
        - instanceId: avatarbuffer
          options:
            # set for multiple files to be added
            isMultiple: true
            label: Avatar
            mediaType: image
          type: component.media-field
      isDiscardChangesAlertEnabled: false

  - type: component.list
    options:
      data: =@ctx.datasources.allImages
      maximumItemsToRender: 8
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.type
          leftElement:
            element: image
            text: ""
            uri: =@ctx.current.item.Avatar

actions:
  - children:
      # use execute entites for multiple files to be added
      - type: action.execute-entities
        # Options in error are expected as there are no functionParameters
        options:
          title: Add Widget Multiple
          provider: DATA_PROVIDER_SQL
          entity: avatarMultiConversion
          data: |
            =@ctx.components.avatarbuffer.state.value.{
              "description" : @ctx.components.description.state.value 
            , "avatarbuffer" : $ }
          function: sql-add-widget-multiple
          goBack: stay
          method: functionCall
          onSuccess:
            title: Success
```

:::

## Convert HEIC to JPEG

In this example, the file conversion is configured in the REST function to convert the files that are outgoing via REST. `convertHeicToJpg` is configured to `true` to convert HEIC images to JPEG which ensures images are visible on iOS and Android devices. The property is available REST and SQL functions, Dynamic Data and actions.

```yaml
provider: DATA_PROVIDER_REST
method: PATCH
url: https://graph.microsoft.com/v1.0/me/photo/$value
useLocalCall: true
parameters:
  accessToken:
    location: header
    required: true
    type: string
    value: oauth.microsoft # Use manage.jigx.com to define credentials for your solution
  Content-Type:
    location: header
    required: true
    type: string
    value: image/jpeg # set the content type of the body
  file:
    location: body
    required: true
    type: image
conversions:
  - property: file
    from: local-uri
    to: buffer
    convertHeicToJpg: true
```

### See Also

- [Example converting local-uri to buffer in SQL function](https://docs.jigx.com/examples/media-field#haYKX)
