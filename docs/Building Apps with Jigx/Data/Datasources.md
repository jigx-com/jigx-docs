# Datasources

Datasources are sets of data used in Jigx solutions and are used to reference data from the various [Data Providers](<./Data Providers.md>).

## Types

There are three types of datasources available in Jigx Builder.

1. **SQLite** - Using the SQLite datasource provides the ability to write SQL queries to get data from Dynamic Data and local data providers. For code examples and snippets, see [sqlite](https://docs.jigx.com/examples/sqlite).
2. **Static** - Static lists are typically used when data needs to be accessed but hardly ever changed. Static Data is helpful because it can be created quickly inside the jig, and there is no need to specify any database connections or set up tables. The amount of records that can be created in Static data is unlimited. Static data is commonly used to bind data to the UI components. For code examples and snippets, see [Static](https://docs.jigx.com/examples/static).
3. **System** - The system datasource is used to get a list of icons for jig components. For code examples and snippets, see [system](https://docs.jigx.com/examples/system).

## Configuration options

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="158,371">
  <tr>
    <td selected="false" align="left">
      <p><strong>Property</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Description</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Code Examples</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isDocument</code></p>
    </td>
    <td selected="false" align="left">
      <p>When the <code>isDocument</code> property is set to <code>true</code> on a datasource, the datasource will return as a single record (object) to be displayed on a component instead of an array. The first matching row becomes the datasource without wrapping the array. If there is no match it is NULL. If you want to set the <code>initialValues</code> for a <a href="https://docs.jigx.com/examples/form">form</a>, set it on the form level and in the datasource <code>isDocument: true</code>, this way you don't have to set it up in the individual components. It is set up in one place and form will match the components to the column names of the datasource.</p>
    </td>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/form#zUejA">new-contact.jigx</a></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>jsonProperties</code></p>
    </td>
    <td selected="false" align="left">
      <p>Working with complex objects can be tricky, as they include arrays, nested objects, and other complex data structures. When integrating and manipulating these JSON structures you can use <code>jsonProperties</code> to specify the exact property in the array or nested object that you require. See <a href="./Data%20Providers/REST/REST%20best%20practice.md">Working with complex REST structures</a>.</p>
    </td>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/list-and-view-customers-get#nQfCR">view-customer-details.jigx</a></p>
    </td>
  </tr>
</table>

### isDocument example

:::CodeblockTabs
datasource

```yaml
datasources:
  contactData:
    type: datasource.sqlite
    options:
      # The isDocument property for the datasource is set to true.
      # As a result, the datasource will return as a single record to be displayed,
      # instead of an array of records.
      isDocument: true
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/contacts
      query: |
        SELECT 
          id,
          '$.firstName',
          '$.lastName',
          '$.jobTitle',
          '$.companyName',
          '$.phone',
          '$.email' 
        FROM 
          [default/contacts]
        WHERE
          id = @contactId
      queryParameters:
        contactId: =@ctx.jig.inputs.contact.id
```

JSON

```json
{
  "contacts": [
    {
      "id": 1,
      "firstName": "Merilyn",
      "lastName": "Bayless",
      "companyName": "20 20 Printing Inc",
      "phone": "408-758-5015",
      "email": "merilyn_bayless@cox.net",
      "web": "http://www.printinginc.com",
      "jobTitle": "Project Manager"
    }
  ]
}
```

form.jigx

```yaml
title: Add new contact A
type: jig.default
icon: book-address

inputs:
  id:
    type: string
    required: true

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80

datasources:
  contactData:
    type: datasource.sqlite
    options:
      # The isDocument property for the datasource is set to true.
      # As a result, the datasource will return as a single record to be displayed,
      # instead of an array of records.
      isDocument: true
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/contacts
      query: |
        SELECT 
          id,
          '$.firstName',
          '$.lastName',
          '$.jobTitle',
          '$.companyName',
          '$.phone',
          '$.email' 
        FROM 
          [default/contacts]
         WHERE
          id = @contactId
      queryParameters:
        contactId: =@ctx.jig.inputs.id

children:
  - type: component.form
    instanceId: new-contact
    options:
      initialValues: =@ctx.datasources.contactData
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.avatar-field
          instanceId: employee-photo
          options:
            label: Photo
        - type: component.section
          options:
            title: Personal information
            children:
              - type: component.text-field
                instanceId: firstName
                options:
                  label: First name
              - type: component.text-field
                instanceId: lastName
                options:
                  label: Last name
              - type: component.email-field
                instanceId: email
                options:
                  label: Email
                  icon: email
              - type: component.number-field
                instanceId: phone
                options:
                  label: Phone number
                  icon: phone
        - type: component.section
          options:
            title: Business information
            children:
              - type: component.text-field
                instanceId: jobTitle
                options:
                  label: Position
              - type: component.text-field
                instanceId: companyName
                options:
                  label: Company Name

actions:
  - children:
      - type: action.execute-entity
        options:
          title: Create Record
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/contacts
          method: create
          data:
            firstName: =@ctx.components.firstName.state.value
            lastName: =@ctx.components.lastName.state.value
            email: =@ctx.components.email.state.value
            phone: =@ctx.components.phone.state.value
            jobTitle: =@ctx.components.jobTitle.state.value
            companyName: =@ctx.components.companyName.state.value
```
:::

### jsonProperties example

:::CodeblockTabs
```yaml
datasources:
  customers:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL

      entities:
        - entity: customers

      query: |
        SELECT 
          cus.id AS id, 
          json_extract(cus.data, '$.firstName') AS firstName, 
          json_extract(cus.data, '$.lastName') AS lastName,
          json_extract(cus.data, '$.companyName') AS companyName,
          json_extract(cus.data, '$.addresses') AS addresses,
          json_extract(cus.data, '$.phones') AS phones,
          json_extract(cus.data, '$.email') AS email,
          json_extract(cus.data, '$.web') AS web,
          json_extract(cus.data, '$.customerType') AS customerType,
          json_extract(cus.data, '$.jobTitle') AS jobTitle
        FROM 
          [customers] AS cus
        ORDER BY 
          json_extract(cus.data, '$.companyName')
      # Specify the exact property in the array or nested object that you require.
      jsonProperties:
        - addresses
        - phones

data: =@ctx.datasources.customers
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.companyName
    subtitle: =@ctx.current.item.firstName & ' ' & @ctx.current.item.lastName
    description: =@ctx.current.item.addresses[0].city
    leftElement:
      element: avatar
      text: =@ctx.current.item.addresses[0].state

    label:
      title: =$uppercase((@ctx.current.item.customerType = 'Silver' ? @ctx.current.item.customerType:@ctx.current.item.customerType = 'Gold' ? @ctx.current.item.customerType:''))
      color:
        - when: =@ctx.current.item.customerType = 'Gold'
          color: color3
        - when: =@ctx.current.item.customerType = 'Silver'
          color: color14
    onPress:
      type: action.go-to
      options:
        linkTo: view-customer
        parameters:
          customer: =@ctx.current.item
```

```json
"customers": [
        {
            "custId": 1,
            "firstName": "Merilyn",
            "lastName": "Bayless",
            "companyName": "20 20 Printing Inc",
            "addresses": [
                {
                    "address": "195 13n N",
                    "city": "Santa Clara",
                    "county": null,
                    "state": "CA",
                    "zip": "95054"
                }
            ],
            "phones": [
                {
                    "mobile": "408-758-5015",
                    "office": "408-758-5015"
                }
            ],
            "email": "merilyn_bayless@cox.net",
            "web": "http://www.printinginc.com",
            "region": "US West",
            "customerType": "Silver",
            "jobTitle": "Project Manager",
            "logo": null
        },
```
:::

## Where and how to use datasources

### In a Global file

Datasources are defined once and are available throughout your solution to be reused in multiple jigs. Adding a global datasource improves performance as the data is retrieved once rather than multiple times.

![Global datasource](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/RKfB1NkVqQCckqcWoR-cR_ds-global.gif "Global datasource")

1. Open your solution in Jigx Builder and navigate to the **datasources** folder of your solution.
2. Create a new file called *\<your\_datasource\_name>.jigx.*
3. Invoke IntelliSense (ctrl+space) for the list of available datasources.
4. Select the datasource you want to use and configure the properties with values. When choosing Dynamic Dataor SQL data, you can write SQL queries to return the data you want to use in the solution.
5. Next, open the jigs where you want to use the data, use expressions with the datasource option to reference the global datasource file, for example, `=@ctx.datasources.employee`.

### Local within a jig

The data sets are defined in the datasources inside the individual jig generally under the `datasources:` property. Use datasources locally if you only need the data in that specific jig.

![Local datasource](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/fnvUAIdPdJV8GV1y_MOg-_ds-local.gif "Local datasource")

1. Open your solution in Jigx Builder and navigate to the jig.
2. Under the `datasources:` property, replaces the `mydata:` property with a unique name for the data set.
3. Invoke IntelliSense (ctrl+space) next to the `mydata:` property for the list of available datasources.
4. Select the datasource you want to use and configure the properties with values. When choosing Dynamic Dataor SQL data, you can write SQL queries to return the data you want to use in the jig. *Tip*: only return the specific data you need in the datasource.
5. The data is now available to use in that jig by using expressions with the datasource option to reference the local datasource using the unique name you gave it, for example, `=@ctx.datasources.contact`.

### See Also

- [static](https://docs.jigx.com/examples/static) datasource examples
- [sqlite](https://docs.jigx.com/examples/sqlite) datasource examples
- [system](https://docs.jigx.com/examples/system)
- [File handling](<./File handling.md>)

