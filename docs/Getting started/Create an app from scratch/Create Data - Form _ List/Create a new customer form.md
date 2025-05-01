---
title: Create a new customer form
slug: Yy55-create-a-new-customer-form
description: Learn how to create a two-column form with three fields using JigxBuilder in VSCode. Capture customer information and save it to a SQLite database with the action button. Easily navigate back to HomeHub and customize your form with YAML code examples.
createdAt: Wed Apr 12 2023 11:27:48 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Nov 05 2024 13:36:50 GMT+0000 (Coordinated Universal Time)
---

# Overview

In this section, you learn how to create a form with a two-column layout and three fields, and how to configure an action button on the form that will create the record in the [Dynamic data provider](<./../../../Building Apps with Jigx/Data/Data Providers/Dynamic Data.md>).&#x20;

## Steps

### Create the form jig to capture data

1. Open the Hello-Jigx solution in Jigx Builder in VS Code,** right-click** on the jigs node in Explorer, and select **New file**.
2. Name the file **new-customer.** The file opens and shows the Jigx's auto-complete popup listing the five jig types. Click on **Default** to open the skeleton YAML created by the Jigx Builder.&#x20;
3. Give the jig a `title` called *Customers *and provide a description like *New customer form.*&#x20;
4. Add `icon: person` under the description line. This icon displays on the widget on the Home Hub .
5. You can delete this jig's header, onFocus, and datasource lines.
6. The controls displayed on the jig are defined under the `children` node on a default    jig. All the input controls are placed on a `form component`. A control is uniquely identified by its `instanceId`. They are added as children of a `field-row component` to display two controls next to each other. A `text-field component` is used to capture text information on a form, and the `email field component` is used to capture email addresses. Under the `children:` node, add these fields as shown below to capture the customer's first and last name and email address:&#x20;

:::CodeblockTabs
YAML

```yaml
children:
  - type: component.form
    instanceId: customerInfo
    options:
      children:
        - type: component.field-row
          options:
            children:
              - type: component.text-field
                instanceId: firstName
                options:
                  label: First Name
              - type: component.text-field
                instanceId: lastName
                options:
                  label: Last Name
        - type: component.email-field
          instanceId: email
          options:
            label: Email
```
:::

### Add the submit form action (button)

1. The top-level action on a *default *jig places a button at the bottom of the screen. A *submit-form action* saves the data from the text boxes to the SQLite database. The `submit form action` automatically matches the `instanceIds` of the controls on the jig and creates a record in the local SQLite table with each `instanceIds` as a property for the JSON object in the Data column. At the same  root YAML level as `children:` use **ctrl+space** to add the `actions` node. Use the code below to create the `action.submit-form` type, define the data provider to be the Dymamic data provider, and use the `method: create` to save the record.

:::CodeblockTabs
YAML

```yaml
actions:
  - children:
      - type: action.submit-form
        options:
          formId: customerInfo
          provider: DATA_PROVIDER_DYNAMIC
          title: Save Customer
          entity: default/customers
          method: create
```
:::

2\. After the record is created you want to navigate back to the Home Hub, add the
&#x20;`onSuccess:
type: action.go-back` action to the bottom of the actions node.&#x20;
3\. With Dynamic Data you need to add the reference to the table in the database. In the databases node click on the *default.jigx *file. Type `customers: null` under `tables:` as shown below.

:::CodeblockTabs
default.jigx

```yaml
# tables:
tables:
  customers: null
```
:::

4\. Your new-customer.jigx file should resemble the code below.

:::CodeblockTabs
new-customer.jigx

```yaml
# The system name that uniquely identifies the jig
title: New Customer
# Description of the jig. This is not a required field and can be omitted
description: Add a new customer record
# The jig type used to display data
type: jig.default
# icon that displays on the widget on the home hub
icon: person

# The controls that will be displayed on the jig are defined under the children node on a default jig   
children:
  # All input controls are placed on a form component
  - type: component.form
    # A control is uniquely identified by its instance id
    instanceId: customerInfo
    options:
      children:
       # To display two controls next to each other, they are added as children of a field-row component
        - type: component.field-row
          options:
            children:
              # A text-field component is used to capture text information on a form
              - type: component.text-field
                instanceId: firstName
                options:
                  label: First Name
              - type: component.text-field
                instanceId: lastName
                options:
                  label: Last Name
        - type: component.email-field
          instanceId: email
          options:
            label: Email

# The top level action on a default jig places a button at the bottom of the screen
actions:
  - children:
     # A submit-form action is used to save the data from the text boxes to the SQLite database. The submit form action will automatically match the instanceIds of the controls on the jig and create a record in the local SQLite table with each instanceIds as a property for the JSON object in the Data column
      - type: action.submit-form
        options:
          # The name of the form being submitted
          formId: customerInfo
          # The data provider being used. In this case, the Jigx Dynamic Data provider, which is a built-in database using methods to work with the data. 
          provider: DATA_PROVIDER_DYNAMIC
          # The title of the button
          title: Save Customer
          # The name of the table that the information is being save to. All Dynamic Data-based tables are saved in the "default" database 
          entity: default/customers
          # The Jigx Dynamic Data provider method to create the data
          method: create
          # The navigation action that is performed after the form-submit action completes
          onSuccess: 
            type: action.go-back
```
:::

