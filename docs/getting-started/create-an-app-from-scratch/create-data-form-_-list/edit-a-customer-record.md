---
title: Edit a customer record
slug: R20--edit-a-customer-record
createdAt: Wed Apr 12 2023 11:27:43 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Nov 05 2024 13:41:12 GMT+0000 (Coordinated Universal Time)
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
---

# Edit a customer record

In this section, you learn how to create a form using the `component.form` to display the fields returned from the dynamic data provider. Add an `action.submit-form` with a `method: update` that saves the changes to the record in the dynamic data provider.

## Steps

### Create a jig to edit data

1. Open the Hello-Jigx solution in Jigx Builder in VS Code, **right-click** on the jigs node in Explorer, and select **New file**.
2. Name the file **edit-customer**. Click on **Default** to open the skeleton YAML created by the Jigx Builder.
3. Give the jig a title called _Edit customers_ and provide a description like _Edit customer details_.
4. Delete the `header` and `onfocus` nodes.

### Add a datasource and form

1. You are going to use the same datasource, query, form, and form fields that you used in the view-customer.jigx file. Use the code below.

{% code title="YAML" %}
```yaml
datasources:
  customerInfo:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/customers
      query: SELECT id, '$.firstName', '$.lastName', '$.email'  FROM [default/customers] WHERE id = @custId
      queryParameters:
        custId: =@ctx.jig.inputs.custId
      isDocument: true 
children:
  - type: component.form
    instanceId: editCustomer
    options:
      children:
        - type: component.field-row
          options:
            children:
              - type: component.text-field
                instanceId: firstName
                options:
                  label: First Name
                  initialValue: =@ctx.datasources.customerInfo.firstName
              - type: component.text-field
                instanceId: lastName
                options:
                  label: Last Name
                  initialValue: =@ctx.datasources.customerInfo.lastName
              - type: component.text-field    
                instanceId: email
                options:
                  label: Email
                  initialValue: =@ctx.datasources.customerInfo.email    
```
{% endcode %}

### Add the submit-form action to save the data

1. A `submit-form` action is used to save the data from the text boxes to the SQLite database. The `submit form` action will automatically match the `instanceIds` of the controls on the jig and use the `update method` to save the changes to the record in the local SQLite table with each `instanceIds` as a property for the JSON object in the Data column. Use the submit.form action code below:

{% code title="YAML" %}
```yaml
actions:
  - children:
      - type: action.submit-form
        options:
          formId: editCustomer
          provider: DATA_PROVIDER_DYNAMIC
          title: Save Customers
          entity: default/customers             
          method: update
          recordId: =@ctx.jig.inputs.custId
          onSuccess: 
            type: action.go-back  
```
{% endcode %}

2\. Your edit-customer.jigx file should resemble the code below.

{% code title="edit-customer.jigx" %}
```yaml
# The system name that uniquely identifies the jig
title: Edit Customer
# The jig type used to display data
type: jig.default

# The type of datasource used to store the edited data in the jig
datasources:
  customerInfo:
    type: datasource.sqlite
    options:
     # The data provider being used. In this case, the Jigx Dynamic Data provider, which is a built-in database using methods to work with the data. 
      provider: DATA_PROVIDER_DYNAMIC
      # The name of the table that the information is being returned from. All Dynamic Data-based tables are saved in the "default" database.
      entities:
        - default/customers
      # The SQLite query used to specifiy the data to return  
      query: SELECT id, '$.firstName', '$.lastName', '$.email'  FROM [default/customers] WHERE id = @custId
      queryParameters:
        custId: =@ctx.jig.inputs.custId
      isDocument: true
# The controls that will be displayed on the jig are defined under the children node on a default jig      
children:
  # All input controls are placed on a form component
  - type: component.form
    # A control is uniquely identified by its instance id
    instanceId: editCustomer
    options:
      children:
        # To display two controls next to each other, they are added as children of a field-row component
        - type: component.field-row
          options:
            children:
              # A text-field component is used to capture or update text information on a form. In this case the value is returned from the database
              - type: component.text-field
                instanceId: firstName
                options:
                  label: First Name
                  initialValue: =@ctx.datasources.customerInfo.firstName
              - type: component.text-field
                instanceId: lastName
                options:
                  label: Last Name
                  initialValue: =@ctx.datasources.customerInfo.lastName
              - type: component.text-field    
                instanceId: email
                options:
                  label: Email
                  initialValue: =@ctx.datasources.customerInfo.email    

# The top level action on a default jig places a button at the bottom of the screen                  
actions:
  - children:
     # A submit-form action is used to save the data from the text boxes to the SQLite database. The submit form action will automatically match the instanceIds of the controls on the jig and update the record in the local SQLite table with each instanceIds as a property for the JSON object in the Data column
      - type: action.submit-form
        options:
          # The name of the form being submitted
          formId: editCustomer
          provider: DATA_PROVIDER_DYNAMIC
          title: Save Customers
          entity: default/customers
          # The Jigx Dynamic Data provider method to update the data                  
          method: update
          recordId: =@ctx.jig.inputs.custId
          onSuccess: 
            type: action.go-back  
```
{% endcode %}
