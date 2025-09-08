---
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

# Forms and Composite Jigs

In this section, we will have a look at how you can create and update forms using composite jigs. For more information see the [jig.composite](https://docs.jigx.com/examples/jigcomposite) topic.

1.  First we need to create a new jig with type composite. :::CodeblockTabs composite-form.jigx

    ```yaml
    title: Composite
    type: jig.composite

    children:
      - jigId: myjig1
      - jigId: myjig2
    ```
2. Now we create two new jigs with a form as we did on the top of this section where we created our first form. For the first, we put just tow text-fields one for the Firstname and the second for the Lastname. Let's call this jig name-form.jigx

{% code title="name-form.jigx" %}
```yaml
title: Employees name
type: jig.default

children:
  - type: component.form
    instanceId: form-name
    options:
      children:
        - type: component.field-row
          options:
            children:
              - type: component.text-field
                instanceId: first-name
                options:
                  label: First name
              - type: component.text-field
                instanceId: last-name
                options:
                  label: Last name
```
{% endcode %}

After that, we create a second jig where we can put some additional information like phone number and email.

{% code title="personal-info-form.jigx" %}
```yaml
title: Personal info
type: jig.default

children:
  - type: component.form
    instanceId: form-personal-info
    options:
      children:
        - type: component.field-row
          options:
            children:
              - type: component.text-field
                instanceId: email
                options:
                  label: Email
                  keyboardType: email-address
              - type: component.text-field
                instanceId: phone
                options:
                  label: Phone number
                  keyboardType: name-phone-pad
```
{% endcode %}

1.  Now we have two jigs where we have two forms. Let's back to the composite jig that we create at the start on the top of this section. Change the myjig1 and 2 to the name-form and personal-info-form and add the instanceId: thanks to instanceId we can refer to the children in the specific jig.&#x20;

    {% code title="composite-form.jigx" %}
    ```yaml
    title: Composite
    type: jig.composite

    children:
      - jigId: name-form
        instanceId: names
      - jigId: personal-info-form
        instanceId: infos
    ```
    {% endcode %}
2. For saving our data from we need to create action with action.execute-entity but now our section data will look a little different. The syntax for first-name will be as follows - _**firstname: =@ctx.jigs.names.components.first-name.state.value**_ _**=@ctx.jigs.names**_ - will refer to the specific jig _**components.first-name.state.value**_ - will refer to the specific component inside the jig that we refer before.

{% code title="composite-form.jigx" %}
```yaml
title: Composite
type: jig.composite

actions:
  - children:
      - type: action.execute-entity
        options:
          title: Save form
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/form
          method: save
          data:
            firstname: =@ctx.jigs.names.components.first-name.state.value
            lastname: =@ctx.jigs.names.components.last-name.state.value
            email: =@ctx.jigs.infos.components.email.state.value
            phone: =@ctx.jigs.infos.components.phone.state.value

children:
  - jigId: name-form
    instanceId: names
  - jigId: personal-info-form
    instanceId: infos
```
{% endcode %}

The full example of the composite form is available on [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/jigs/components/form/composite-form).
