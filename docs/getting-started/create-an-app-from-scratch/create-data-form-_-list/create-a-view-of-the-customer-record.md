---
title: Create a view of the customer record
slug: _3wu-create-a-view-of-the-customer-record
createdAt: Wed Apr 12 2023 11:27:44 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Oct 31 2023 13:36:45 GMT+0000 (Coordinated Universal Time)
---

# Create a view of the customer record

In this section, you learn how to create a view using the [entity-field](https://docs.jigx.com/examples/entity-field) component to display the data returned from the [Dynamic data provider](../../../building-apps-with-jigx/data/data-providers/dynamic-data/dynamic-data.md). Add an action to go to a form that allows you to edit and [update a record](../../../building-apps-with-jigx/ui/jigs-_screens_/forms/updating-a-record.md).

## Steps

### Create a jig to view data

1. Open the Hello-Jigx solution in Jigx Builder in VS Code, **right-click** on the jigs node in Explorer, and select **New file**.
2. Name the file **view-customer**. The file opens and shows the Jigx's auto-complete popup listing the five types of jigs you can select. Click on **Default** to open the skeleton YAML created by the Jigx Builder.
3. Give your jig a `title` and `description`.
4. Delete the `header` and `onfocus` nodes.
5. Specify the SQLite Dynamic data provider, the table, and the SQLite query needed to return the customer's details. Below is an example of the code you can use.

{% code title="YAML" %}
```yaml
datasources:
  customerInfo:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/customers
      query: SELECT id, '$.firstName', '$.lastName', '$.email' FROM [default/customers] WHERE id = @custId
      queryParameters:
        custId: =@ctx.jig.inputs.custId
      isDocument: true
```
{% endcode %}

### Create the view form

1. Now that you have the data you want to view, specify how you want to view the data. For this step, we want to view the data in a form similar to the new customer form. The code below shows using the `form component`, `field-row`, and `entity- fields` to display the customer's first and last name, and email address.

{% code title="YAML" %}
```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: First Name
                  value: =@ctx.datasources.customerInfo.firstName
              - type: component.entity-field
                options:
                  label: Last Name
                  value: =@ctx.datasources.customerInfo.lastName
        - type: component.entity-field
          options:
            label: Email
            value: =@ctx.datasources.customerInfo.email
```
{% endcode %}

### Add an edit action (button)

1. Once you can view the returned customer record, you want to be able to edit the record and save the changes to the SQLite Dynamic Data provider. Add the `action.go-to` that directs you to the edit form using the `custId` to reference the individual customer record. Use the code below to create the action button.

{% code title="YAML" %}
```yaml
actions:
  - children:
      - type: action.go-to
        options:
          title: Edit Customer
          linkTo: edit-customer
          parameters:
            custId: =@ctx.jig.inputs.custId
```
{% endcode %}

2\. Your view-customer.jigx file should resemble the code below.

{% code title="view-customer.jigx" %}
```yaml
# The system name that uniquely identifies the jig
title: View Customer
# The jig type used to display data
type: jig.default

# The type of datasource used to return data in the jig
datasources:
  customerInfo:
    type: datasource.sqlite
    options:
      # The data provider being used. In this case, the Jigx Dynamic Data provider, which is a built-in database that can be queried to get data from
      provider: DATA_PROVIDER_DYNAMIC
      # The name of the table that the information is being returned from. All Dynamic Data-based tables are saved in the "default" database
      entities:
        - default/customers
      # The SQLite query used to specifiy the data to return
      query: SELECT id, '$.firstName', '$.lastName', '$.email' FROM [default/customers] WHERE id = @custId
      queryParameters:
        custId: =@ctx.jig.inputs.custId
      isDocument: true
# The controls that will be displayed on the jig are defined under the children node on a default jig
children:
  # All input controls are placed on a form component
  - type: component.entity
    options:
      children:
        # To display two controls next to each other, they are added as children of a field-row component
        - type: component.field-row
          options:
            children:
              # A text-field component is used to display text information on a form
              - type: component.entity-field
                options:
                  label: First Name
                  value: =@ctx.datasources.customerInfo.firstName
              - type: component.entity-field
                options:
                  label: Last Name
                  value: =@ctx.datasources.customerInfo.lastName
        - type: component.entity-field
          options:
            label: Email
            value: =@ctx.datasources.customerInfo.email

# The top level action on a default jig places a button at the bottom of the screen
actions:
  - children:
      # The navigation action that is performed when the go-to action completes
      - type: action.go-to
        options:
          title: Edit Customer
          linkTo: edit-customer
          parameters:
            custId: =@ctx.jig.inputs.custId
```
{% endcode %}

{% hint style="warning" %}
The view-customer file will display in red and cannot be saved yet as it references the edit-customer file that you will be creating in the [Edit a customer record](edit-a-customer-record.md) step.
{% endhint %}
