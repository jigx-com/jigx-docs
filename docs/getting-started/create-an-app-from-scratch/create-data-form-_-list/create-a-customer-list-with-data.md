---
title: Create a customer list with data
slug: 0A0X-create-a-customer-list-with-data
createdAt: Wed Apr 12 2023 11:27:47 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Nov 05 2024 13:40:44 GMT+0000 (Coordinated Universal Time)
---

# Create a customer list with data

In this section, you learn how to create a [jig.list](https://docs.jigx.com/examples/jiglist) type that uses the [dynamic data provider](../../../building-apps-with-jigx/data/data-providers/dynamic-data/dynamic-data.md) to return and display a list of records. You specify the fields that must be returned in the list jig and add an [onPress list action](https://docs.jigx.com/examples/list-item) that opens a jig used to view the selected list item record.

## Steps

### Create a list jig

1. Open the Hello-Jigx solution in Jigx Builder in VS Code, **right-click** on the jigs node in Explorer, and select **New file**.
2. Name the file **list-customer**. The file opens and shows the Jigx's auto-complete popup listing the five types of jigs you can select. Click on **List** to open the skeleton YAML created by the Jigx Builder.
3. Give the jig a title called \*List customers \*and provide a description like _List my customers_.
4. Change the icon to `icon: list`.This icon displays on the widget on the Home Hub.
5. Delete the `header` and `onfocus` nodes.

### Add the data source to return data in the list

1. Under the `datasource` node specific the data provider where the customer records are stored. The name of the table that the information is being returned from. All Jigx Dynamic Data-based tables are saved in the "default" database. Use a SQLite `query` to specify the fields to be returned in the list, in this case, we want the customer's first and last name as well as their email address. You can add your own datasource entries or use the code example below.&#x20;

{% code title="YAML" %}
```yaml
datasources:
  customerList:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/customers
      query: SELECT id, '$.firstName', '$.lastName', '$.email' FROM [default/customers]
```
{% endcode %}

### Add controls and actions to the list item

1. All list output controls are placed on the `list-item component`. Use the `swipeable:` action to configure a left or right swipe and the method to call. For example, in this step, we use a left swipe to delete the customer using the delete method. You can add your own controls or use the code example below.

{% code title="YAML" %}
```yaml
data: =@ctx.datasources.customerList
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.firstName & " " & @ctx.current.item.lastName
    subtitle: =@ctx.current.item.email
    swipeable:
      left:
        - label: Delete
          icon: delete
          color: warning
          onPress:
            type: action.execute-entity
            options:
              provider: DATA_PROVIDER_DYNAMIC
              entity: default/customers
              method: delete
```
{% endcode %}

2\. Configure the action to take you back to the list once the list-item has been deleted, by using the code below.

{% code title="YAML" %}
```yaml
data:
  id: =@ctx.current.item.id
onSuccess:
  type: action.go-back
```
{% endcode %}

### Add a navigation action

1. Add a navigation action that is performed when a single item is clicked in the list, and referenced by using the `custId` parameter. In this step clicking on a customer in the list opens the view-customer jig to view the customer's details. Use the `onPress` action with an `action.go-to` type and the `linkTo` option as shown below.

{% code title="YAML" %}
```yaml
onPress:
  type: action.go-to
  options:
    linkTo: view-customer
    parameters:
      custId: =@ctx.current.item.id
```
{% endcode %}

2\. Your list-customer.jigx file should resemble the code below.

{% code title="list-customer.jigx" %}
```yaml
# The system name that uniquely identifies the jig
title: List customers
# Description of the jig. This is not a required field and can be omitted.
description: List of our customers
# The jig type used to list data values and elements
type: jig.list
# icon that displays on the widget on the home hub
icon: list

# The type of datasource used to store the created data in the jig
datasources:
  customerList:
    type: datasource.sqlite
    options:
      # The data provider being used. In this case, the Jigx Dynamic Data provider
      provider: DATA_PROVIDER_DYNAMIC
      # The name of the table that the information is being returned from. All Dynamic Data-based tables are saved in the "default" database.
      entities:
        - entity: default/customers
      # The SQLite query used to specifiy the data to return
      query: SELECT id, '$.firstName', '$.lastName', '$.email' FROM [default/customers]

data: =@ctx.datasources.customerList
item:
  # All list output controls are placed on the list-item component
  type: component.list-item
  options:
    title: =@ctx.current.item.firstName & " " & @ctx.current.item.lastName
    subtitle: =@ctx.current.item.email
    # The list-item action that defines what to do when swiping left or right on the item
    swipeable:
      left:
        - label: Delete
          icon: delete
          color: warning
          onPress:
            type: action.execute-entity
            options:
              provider: DATA_PROVIDER_DYNAMIC
              entity: default/customers
              method: delete
              data:
                id: =@ctx.current.item.id
              onSuccess:
                type: action.go-back
    # The navigation action that is performed when an individual item is tapped in the list, in this instance to view the customer details
    onPress:
      type: action.go-to
      options:
        linkTo: view-customer
        parameters:
          custId: =@ctx.current.item.id
```
{% endcode %}

{% hint style="warning" %}
The list-customer.jigx file will display in red and cannot be saved yet as it references the view-customer.jigx file that you will be creating in the [Create a view of the customer record](create-a-view-of-the-customer-record.md) step.
{% endhint %}
