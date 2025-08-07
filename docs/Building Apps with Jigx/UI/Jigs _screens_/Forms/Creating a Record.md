# Creating a Record

We will now create a Jig with a form that creates a record with multiple columns in our Dynamic Data table, which we defined in the previous [Forms](./../Forms.md) part.

## Creating a Jig

First, we create an empty Jig and call it *form.jigx*. Delete the `datasources` section, as we don't need it now.

:::CodeblockTabs
form.jigx

```yaml
title: Form
description: My first from by Jigx
type: jig.default

children:
  -
```
:::

## Adding a form to the Jig

We need to add a *form* component to our Jig, as it will be the container for the form input components.

1. Go ahead and use IntelliSense (**Ctrl+Space**) to add a [form](https://docs.jigx.com/examples/form) component to the `children` option of your Jig.
2. Note the empty `instanceId` option. This is the unique identifier of your form. Set it to *simple-form* as we need it later to submit the form.

:::CodeblockTabs
form.jigx

```yaml
title: Form
description: My first form by Jigx
type: jig.default

children:
  - type: component.form
    instanceId: simple-form
    options:
      children:
        -
```
:::

## Adding form input components to the form

You can now go ahead and add the first input field to your form. Use **Ctrl+Space** to add a [text-field](https://docs.jigx.com/examples/text-field) to the `children` option of your form component.

Two options are important for every form field:

- `instanceId` - This is the unique identifier of each form input component and it will be used later to retrieve the field values using [State](./../../../Logic/State.md). Set it to *firstname*.
- `label` - The label will be displayed on the actual component UI and is important for user interaction. Keep it simple and descriptive. Set it to *First name*.

:::CodeblockTabs
form.jigx

```yaml
title: Form
description: My first form by Jigx
type: jig.default

children:
  - type: component.form
    instanceId: simple-form
    options:
      children:
        - type: component.text-field
          instanceId: firstname
          options:
            label: First name
```
:::

:::hint{type="warning"}
Please note: It's best practice for mobile forms to be as short and simple as possible! No one wants to fill out dozens of fields on a mobile device. Because of this, all Jigx input components are marked as required (option `isRequired`) by default. If you want to make a field optional set `isRequired` to *false,* but ask yourself if you then really need that field on your form.
:::

Next, add some more fields to your form. Note that for the email and phone fields we specified an additional option, called `keyboardType`. This will present the devices onscreen keyboard in the right mode. You can use **Ctrl+Space** to see all available types.

Go ahead and create a form with this YAML:

:::CodeblockTabs
form.jigx

```yaml
title: Form
description: My first form by Jigx
type: jig.default

children:
  - type: component.form
    instanceId: simple-form
    options:
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
:::

## Submitting the form data

Good job! Now that we have the basic structure of our form in place we can start thinking about how to store its data.

In general, there are two main ways of sending a form's data back to your data store:

- **Submit-Form Action** - This is the standard approach for submitting data to your data store. Choose this one if your form just needs to create or update data in a single table.
- **Execute-Entity Action** - If you need more control about how and where to send your form data, select this action type. Keep in mind that it requires you to understand [State](./../../../Logic/State.md) to access the field values.

::::ExpandableHeading
### Submit form

Now we will add a submit-form action to our Jig. The action will automatically display an action button at the bottom of the Jig and take care of sending the data to a Dynamic Data table.

1. Go to the root indent level of the Jig and use **Ctrl+Space** to bring up IntelliSense. Pick actions
2. Now, use **Ctrl+Space** again to add a *Submit Form (Create)* action

Now we need to set our *submit-form* action to the form component:

1. `formId` - Remember that we set the identifier of our form component (`instanceId`) to *simple-form* earlier. We will use this identifier to connect our action to the form. Set `formId` to *simple-form*, you can use** **Ctrl+Space for this as well.
2. `provider` - As we want to store our form data in a Dynamic Data table, we can leave this value as is.
3. `title` - The title will be displayed on the action button at the bottom of our Jig. Set it to *Submit form*.
4. `entity` - This is the entity table that will be used to store the data. Use Ctrl + Space to select the *default/form* table we defined at the beginning of the guide.
5. `method` - We want to create a new record, therefore we leave this value set to create.
6. `go-back` - After the record is created, we want to navigate back to the previous screen. Note that there are more options available.

Our YAML looks like this now :

:::CodeblockTabs
form.jigx

```yaml
title: Form
description: My first from by Jigx
type: jig.default

actions:
  - children:
      - type: action.submit-form
        options:
          formId: simple-form
          provider: DATA_PROVIDER_DYNAMIC
          title: Submit form
          entity: default/form
          method: create
          onSuccess:
            type: action.go-back
children:
  - type: component.form
    instanceId: simple-form
    options:
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
:::
::::

::::ExpandableHeading
### Execute-entity

The execute-entity action allows for more control over how your data is stored. For instance, you could transform the *lastname* value to uppercase, or combine firstname and lastname into one column before saving it. Also you could add multiple forms to one Jig and store data from both or access forms of [jig.composite](https://docs.jigx.com/examples/jigcomposite) children from the composite Jig action.

As you can see in below example, the action exposes a `data` option that allows you to specify each column that will be used in the payload. Each column value can be bound to an expression and state of your components. In this example we are accessing state for each field (remember, **Ctrl+Space **is your best friend). It's very helpful to learn more about [State](./../../../Logic/State.md) in general when using this type of action.

:::hint{type="info"}
You could also use JSONata [expression](./../../../Logic/Expressions.md) to transform the state values before binding them to the columns. An example for this would be:

*lastname: =$uppercase(@ctx.components.lastname.state.value)*
:::

:::CodeblockTabs
form.jigx

```yaml
title: Form
description: My first form by Jigx
type: jig.default

actions:
  - children:
      - type: action.execute-entity
        options:
          title: Submit form
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/form
          method: create
          data:
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
:::
::::

## Adding a widget to home hub

Now let's head over to the *index.jigx* fiel of our solution to add a widget for the Home Hub that takes the user to our form:

:::CodeblockTabs
index.jigx

```yaml
title: First form
category: personal

tabs:
  home:
    jigId: form
    icon: home-apps-logo
```
:::

Publish your solution now, so that you can try it out on your mobile device 🎉 Remember, that you always check out the contents of your Dynamic Data form table in the :Link[Jigx Management]{href="https://manage.jigx.com" newTab="true" hasDisabledNofollow="false"}. Navigate to the Solutions area in the left sidebar, select your solution and check out the Data section in the sidebar.

Next see how to [update a record](<./Updating a Record.md>). For more examples on formatting your form see :Link[GitHub]{href="https://github.com/jigx-com/jigx-samples/blob/main/samples/jigx-samples/jigs/components/form/simple-form-submit.jigx" newTab="true" hasDisabledNofollow="false"}.
