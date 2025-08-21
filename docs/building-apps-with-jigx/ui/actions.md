# Actions

Actions refer to specific controls or operations that respond to an event or input. They range from simple operations like clicking a submit button or navigating to a previous screen to more complex tasks like data interaction.

* Actions can be configured locally within a jig or globally to be re-used in multiple jigs.
* Actions can be configured at the root level of a jig, inside a component or in the index file.

## Types of actions

Actions allow you to do many things in an app; below are the types of actions that can be configured when creating a solution.

* _Execution_ - actions to interact with data.
  * [execute-entity](https://docs.jigx.com/examples/execute-entity)
  * [execute-entities](https://docs.jigx.com/examples/execute-entities)
  * [submit-form](https://docs.jigx.com/examples/submit-form)
  * [sync-entities](https://docs.jigx.com/examples/sync-entities) for getting data to the device.
* _Navigational_ - actions used to navigate to another jig or Home Hub.
  * [go-to](https://docs.jigx.com/examples/go-to)
  * [go-back](https://docs.jigx.com/examples/go-back)
* Actions to _open_ components.
  * [open-scanner](https://docs.jigx.com/examples/open-scanner)
  * [open-url](https://docs.jigx.com/examples/open-url)
  * [open-media-picker](https://docs.jigx.com/examples/open-media-picker)
  * [open-map](https://docs.jigx.com/examples/open-map)
  * [open-app-setting](https://docs.jigx.com/examples/open-app-settings)
* _State_ - actions used to determine a specific status or value of a property or component.
  * [set-state](https://docs.jigx.com/examples/set-state)
  * [reset-state](https://docs.jigx.com/examples/reset-state)
* _Events_ - actions that execute after a user or device performs a trigger.
  * onRefresh
  * onFocus
  * onPress
  * onLoad (only on index.jigx)
  * onChange
  * onDelete
  * onButtonPress (only on calendar jigs)
  * [onTableChanged](https://docs.jigx.com/examples/ontablechanged)

For the complete list and code examples of available actions, see [actions](https://docs.jigx.com/examples/actions).

## Where to add actions

### In a Jig

You can configure actions in various places in the jig file, depending on what you need. To create an action as a button that appears at the bottom of the screen, place the `actions:` property at the root level in the YAML, and as the last set of properties in the YAML. The `actions:` property has a `title:` property used for the text on the button.

{% code title="action-button" %}
```yaml
# Edit customer button to navigate to the newCustomer jig
actions:
  - children:
      - type: action.go-to
        options:
          title: Edit Customer
          linkTo: updateCustomer
          parameters:
            custId: =@ctx.datasources.mydata.id
```
{% endcode %}

### In a list

A combination of different actions can be configured throughout a list jig, as shown in the example below. Use parameters or expressions such as `=@ctx.current.item.value` to get the context specific detail you need. Actions can also be added to the `swipeable` elements of a list for example, swipe left to delete a list item.

{% code title="actions-list" %}
```yaml
title: List Customers
description: Show a list of all customers in a SQL database.
type: jig.list
icon: contact

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1553413077-190dd305871c?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1035&q=80

# onFocus is triggered whenever the jig is displayed. The sync-entities action calls the Jigx SQL function and populates the local SQLite tables on the device with the data returned from Azure SQL.
onFocus:
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_SQL
    entities:
      - entity: customers
        function: get-customers

datasources:
  mydata:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL

      entities:
        - entity: customers

      query: |
        SELECT
          id,
          '$.first_name',
          '$.last_name',
          '$.email',
          '$.phone_number',
          '$.address_line1',
          '$.address_line2',
          '$.city',
          '$.state',
          '$.zip_code',
          '$.country'
        FROM
          [customers]
        ORDER BY '$.first_name'

data: =@ctx.datasources.mydata
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.first_name & ' ' & @ctx.current.item.last_name
    subtitle: =@ctx.current.item.email
    description: |
      =@ctx.current.item.address_line1 & ' ' & 
        @ctx.current.item.city & ' ' & 
        @ctx.current.item.state  & ' ' & 
        @ctx.current.item.zip_code
    label:
      title: =@ctx.current.item.country
    leftElement:
      element: avatar
      text: =$substring(@ctx.current.item.first_name,0,1) & $substring(@ctx.current.item.last_name,0,1)
    divider: solid
    # A go-to action is triggered when pressing on a list item.
    onPress:
      type: action.go-to
      options:
        # The name of the jig to navigate to when the item is pressed.
        linkTo: viewCustomer
        parameters:
          # The id column of the current item being pressed on is passed as a parameter called customerId to the viewCustomer jig.
          customerId: =@ctx.current.item.id

# Add customer button to navigate to the newCustomer jig
actions:
  - children:
      - type: action.go-to
        options:
          title: Add Customer
          linkTo: newCustomer
          parameters:
            custId: =$uuid_v4()
```
{% endcode %}

### In the index file

For best performance when working with data, is to get the data when the solution loads in the Jigx App. This is achieved by using the `onLoad` action in the index file which will ensure the data is available from the beginning and throughout the rest of the app.

{% code title="index.jigx" %}
```yaml
widgets:
  - size: 1x1
    jigId: home-hub
# Configure the Onload to sync the salesforce data to the device when the app 
# is opened.
onLoad:
  type: action.action-list
  options:
    actions:
      - type: action.sync-entities
        options:
          provider: DATA_PROVIDER_SALESFORCE
          entities:
            - entity: Account
            - entity: Opportunity
            - entity: OpportunityStage
            - entity: User
            - entity: UserRole
            - entity: Territory2
```
{% endcode %}

## Executing multiple actions

To execute a series of actions use the [action-list](https://docs.jigx.com/examples/action-list), this allows you to configure multiple actions as a group. The `isSequential` property on the action-list is important as it determines when the actions are executed.

* `False` executes the actions randomly
* `True` executes the actions from the top down and waits for the action to complete before executing the next action in the list, making it important to list the actions in the correct order.

{% code title="action-list" %}
```yaml
onFocus:
  type: action.action-list
  options:
    # actions set to execute one after the other starting at the first action
    # in the list.
    isSequential: true
    actions:
      # first action to execute.
      - type: action.set-state
        options:
          state: =@ctx.solution.state.focus-key
          value: focused
      # second action execute after the first action completes.
      - type: action.sync-entities
        options:
          provider: DATA_PROVIDER_DYNAMIC
          entities:
            - default/employees
```
{% endcode %}

## Local actions

Local actions are configured inside the jig and only execute on that specific jig, for example creating a button with an action at the bottom of the jig or in a list jig when swiping left or right.

## Global actions

Often, the actions called during `onRefresh`, `onLoad`, and `onFocus` are exactly the same; this means that YAML is duplicated, which leads to bloat and possible issues when making changes. Global actions allow you to define the action once and reuse it multiple times in different jigs.

* You can configure the global action with inputs if an action requires context-specific values.
* These global actions can be called from mutiple areas, not just lifecycle events like `onFocus`.
* By using the `action.execute-action` provides greater control that enables this reuse when the same actions need to be performed in multiple places. For example, `action.sync-entities` might be called during app initialization, again when data changes, or when only a specific subset of data needs to be synced. By using `execute-action`, you can easily reuse the granular actions that handle the actual work, reducing duplication and improving maintainability.

![Global actions](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/9dfS44d8ZVEbfdqaNjlqs_a-global-action.png)

### Configure global actions

Global actions are added under the `actions` folder in Jigx Builder.

1. Create a jigx file under the Action folder.
2. Auto-completion pops up with the list of available actions.
3. Select the required action and configure the properties' values.
4. Using expressions will provide a list of available global options such as actions, expressions, and datasources.

{% code title="action" %}
```yaml
action:
  type: action.execute-entity
  options:
    provider: DATA_PROVIDER_DYNAMIC
    entity: default/contacts
    method: update
    onSuccess:
      description: Contact Updated
      title: Contact Updated
    data:
      id: =@ctx.action.parameters.id
      name: =@ctx.action.parameters.name
      email: =@ctx.action.parameters.email
parameters:
  id:
    type: string
    required: true
  name:
    type: string
    required: true
  email:
    type: string
    required: true
```
{% endcode %}

### Call the global action in a jig or index.jigx

1. Open the jig where you want to call the global action.
2. Use IntelliSense (ctrl+space) to list the available actions and select the **Execute Action** option `action.execute-action`.
3. Configure the action property by selecting the global action file from the list of global action files.
4. The `when:` proprerty can be used to determine when the global action must execute in a jig.

{% code title="jig-call-action" %}
```yaml
actions:
  - children:
      # use the action.execute-action to reference the global action
      - type: action.execute-action
        options:
          title: Update Work details
          action: update-details
          parameters:
            id: =@ctx.components.id.state.value
            name: =@ctx.components.name.state.value
            email: =@ctx.components.email.state.value
```
{% endcode %}

### Configure contextual values

When configuring a global action you cannot use `=@ctx.current.item` in the file as there is no context to the current item or it's value, instead configure parameters in the global actions file that can be referenced in the jig. The following parameter is configurable in global actions `=@ctx.action.parameters.parametername`. In turn configure the parameter value in the jig with `=@ctx.components.name.state.value` or `=@ctx.current.item.name`.

{% tabs %}
{% tab title="global-action.jigx" %}
```yaml
action:
  type: action.execute-entity
  options:
    provider: DATA_PROVIDER_DYNAMIC
    entity: default/contacts
    method: update
    onSuccess:
      description: Contact Updated
      title: Contact Updated
    # set the global jig parameters
    data:
      id: =@ctx.action.parameters.id
      name: =@ctx.action.parameters.name
      email: =@ctx.action.parameters.email
parameters:
  id:
    type: string
    required: true
  name:
    type: string
    required: true
  email:
    type: string
    required: true
```
{% endtab %}

{% tab title="jig.jigx" %}
```yaml
actions:
  - children:
      - type: action.execute-action
        options:
          title: Update Work details
          action: update-details
          # Provide the context values for the global jig parameters in the jig calling the global action.
          parameters:
            id: =@ctx.components.id.state.value
            name: =@ctx.components.name.state.value
            email: =@ctx.components.email.state.value
```
{% endtab %}
{% endtabs %}

### Considerations

1. When creating sub-folders under the actions folder, ensure that the jigx file names in each folder are unique. Files with the same name will result in only the first action file being available in the IntelliSense list.
2. Certain types of actions have been omitted as they rely on context from the jig they are defined in, and the context cannot be supplied using parameters, these are:
   * `action.submit.form` is not available in global actions because the configuration is specific for each form using the `formId`.
   * `action.open-scanner` action is not available in global actions.
3. The `when:` proprerty can be used to determine when the global action executes in a jig.
4. Actions can be combined with components in the UI, for example [summary](https://docs.jigx.com/examples/summary) component.
5. When using the `actions.action-list` as a global action you can call another global action in the global action list.

{% tabs %}
{% tab title="global-action-multiple.jigx" %}
```yaml
action:
  # execute multiple actions seqentially using the action-list
  type: action.action-list
  options:
    isSequential: true
    actions:
      - type: action.go-to
        options:
          linkTo: detail-list
      # reference another global action file by using execute action and 
      # ctrl+space to select available global action files.
      - type: action.execute-action
        options:
          action: sync-data
```
{% endtab %}

{% tab title="sync-data (global action).jigx" %}
```yaml
action:
  type: action.execute-entity
  options:
    provider: DATA_PROVIDER_DYNAMIC
    entity: default/details
    method: update
    data:
      id: =@ctx.action.parameters.id
      name: =@ctx.action.parameters.name
      email: =@ctx.action.parameters.email
parameters:
  id:
    type: string
    required: true
  name:
    type: string
    required: true
  email:
    type: string
    required: true
```
{% endtab %}
{% endtabs %}

## Working with parent & child actions

When configuring actions across parent and child jigs, the following behavior applies:

* If both the parent and child jigs have an `action` configured, the child’s configuration takes precedence and overrides the parent’s.
* If only the parent has an `action`, it automatically applies to the child.
* If only the child has an `action`, it is used in the parent jig as well.

## See Also

* [File handling](../data/file-handling.md)
