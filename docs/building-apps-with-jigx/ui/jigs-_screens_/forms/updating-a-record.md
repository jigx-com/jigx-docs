---
title: Updating a Record
slug: Tybh-updating-a-record
createdAt: Mon Aug 01 2022 17:32:46 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu May 04 2023 18:33:11 GMT+0000 (Coordinated Universal Time)
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

# Updating a Record

Learn how to update an existing record using a form.

### Populating a form with initial values

Before updating the record, we have to bind the existing record to the form. For that purpose, the form component has an option called `initialValues` which can be used to set all form fields to the current values at once.

In this example, we will use an input parameter `recordId` (see [Inputs & Outputs](https://docs.jigx.com/passing-data-using-inputs)) to query a data record from the Dynamic Data table and then bind that record to the `initialValues` of our form.

{% hint style="info" %}
&#x20;Please note: The optional `isDocument` option of our datasource will ensure that only the first record will be returned by our query as a JSON object.&#x20;
{% endhint %}

{% code title="update-form.jigx" %}
```yaml
title: Update Form
description: My first update form by Jigx
type: jig.default

datasources:
  employee-detail:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC

      entities:
        - entity: default/form

      query: SELECT id, '$.firstname', '$.lastname', '$.email', '$.phone' FROM [default/form] WHERE id = @recordId
      queryParameters:
        recordId: =@ctx.jig.inputs.recordId
      isDocument: true

children:
  - type: component.form
    instanceId: simple-form
    options:
      initialValues: =@ctx.datasources.record
      children:
        - type: component.text-field
          instanceId: firstname
          options:
            label: First name
        - type: component.text-field
          instanceId: lastname
          options:
            label: Last name
        - type: component.email-field
          instanceId: email
          options:
            label: Email
            keyboardType: email-address
        - type: component.number-field
          instanceId: phone
          options:
            label: Phone number
            keyboardType: number-pad
```
{% endcode %}

### Updating the record

In this section, we will gonna have deep look at how you can update your records in the database or delete them with jig form.

#### Update with submit-form action

Another way to update data is by the submit-form action. We put the id of the record which we want to update.

#### Update form - execute-entity action

For the update form, we will use the previous from that we just created and modify it.

We change the method in our action.execute-entity from save to update, under data: we add a new row with **id: =@ctx.components.id.state.value**, also we need to create a new entity-field for id, and for every component what we have we must add new rows with initialValue:

Your update-form.jigx file should resemble the code below:

{% code title="update-form.jigx" %}
```yaml
title: Update Form with execute-entity action
description: My first update form by Jigx
type: jig.default

actions:
  - children:
      - type: action.execute-entity
        options:
          title: Update form
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/form
          method: update
          data:
            id: =ctx.jig.inputs.recordId
            firstname: =@ctx.components.firstname.state.value
            lastname: =@ctx.components.lastname.state.value
            email: =@ctx.components.email.state.value
            phone: =@ctx.components.phone.state.value

children:
  - type: component.form
    instanceId: simple-form
    options:
      children:
        - type: component.text-field
          instanceId: firstname
          options:
            label: First name
            initialValue: =@ctx.datasources.employee-detail.firstname
        - type: component.text-field
          instanceId: lastname
          options:
            label: Last name
            initialValue: =@ctx.datasources.employee-detail.lastname
        - type: component.email-field
          instanceId: email
          options:
            label: Email
            keyboardType: email-address
            initialValue: =@ctx.datasources.employee-detail.email
        - type: component.number-field
          instanceId: phone
          options:
            label: Phone number
            keyboardType: number-pad
            initialValue: =@ctx.datasources.employee-detail.phone
```
{% endcode %}
