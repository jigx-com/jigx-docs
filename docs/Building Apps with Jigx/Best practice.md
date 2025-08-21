---
title: Best practice
slug: ipWT-state
createdAt: Mon Sep 02 2024 12:33:26 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Dec 03 2024 11:46:39 GMT+0000 (Coordinated Universal Time)
---

# Best practice

### When to use solution state (global state)

[State](../building-apps-with-jigx/logic/state.md) manages the state of the app, including the UI's data and the user's interactions, and is best used in scenarios with a _one-to-one relationship_; for example, a field services person selects one job or task to complete, or a pilot selects one mission to fly.

**Design Pattern:** Singletons

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-S\_MP9oBcex53yT9JezU9t-20240911-134725.gif" size="60" position="center" caption}

#### Setup:

1. Set the **ID** to be stored in the solution state, using the `set-state` action. The ID is the least amount of data required to identify each job uniquely. The ID is used throughout the solution to reference the necessary data in each of the solution's jigs.
2. In the datasource queries use the ID to return the required data.
   * In a [global datasource ](https://docs.jigx.com/datasources#gCN9o)query reference the data required. The global datasource is referenced in each jig where the data is required.
   * In the individual jig 's [datasource](https://docs.jigx.com/datasources#2AD3k) query. The query is configured to only return the exact data required for that jig using the ID as the unique identifier.

{% tabs %}
{% tab title="set-solution-state (action)" %}
```yaml
actions:
  - children:
      - type: action.set-state
        options:
          title: Task A
          state: =@ctx.solution.state.id
          value: =@ctx.solution.state.id
```
{% endtab %}

{% tab title="use-solution-state (datasource)" %}
```yaml
datasources:
  contactData:
    type: datasource.sqlite
    options:
      isDocument: true
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/tasks
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
          [default/tasks]
        WHERE
          id = @taskId
      queryParameters:
        taskId: =@ctx.solution.state.id
```
{% endtab %}
{% endtabs %}

State resources and code samples:

* [Solution (Global) State](../building-apps-with-jigx/logic/state.md)
* [Set-state](https://docs.jigx.com/examples/set-state)
* [Reset-state](https://docs.jigx.com/examples/reset-states)
* [Examples of state](../building-apps-with-jigx/logic/state.md)

### When to use inputs

[Inputs](../building-apps-with-jigx/ui/jigs-_screens_/passing-data-using-inputs.md) are used in complex apps to pass multiple variables between jigs using parameters, and is best used in scenarios where there is a _one-to-many relationship_, for example, a manager needs to check on the progress of each field service worker.

**Design Pattern**: Mediator

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-ecGae4Ri9XtX6vah4PaB\_-20240912-074706.gif" size="60" position="center"}

#### Setup:

1. Set up **parameters** in the jig that needs to pass data, then in the jig needing to receive the data set up **inputs**. Multiple parameters and inputs can be configured on a single jig.
2. In the components of the jig use expressions to reference the data passed in, for example, `=@ctx.jig.inputs.parameterName`.

{% tabs %}
{% tab title="set-parameters" %}
```yaml
actions:
  - children:
      - type: action.go-to
        options:
          title: Team Progress
          linkTo: team-progress
          # Define what data the parameters must use
          # The parameters name is used in the receiving jig's input expression
          parameters:
            taskId: =@ctx.components.taskId.state.value
            taskStatus: =@ctx.components.taskStatus.state.value
            taskCost: =@ctx.components.taskCost.state.value
            taskAssignee: =@ctx.components.taskAssignee.state.value
```
{% endtab %}

{% tab title="use-input" %}
```yaml
title: Team Progress
type: jig.default
# Define the input type
inputs:
  taskId:
    type: number
    required: true
  taskAssignee:
    type: string
    required: true
  taskStatus:
    type: string
    required: true
  taskCost:
    type: number
    required: false

children:
  - type: component.expander
    options:
      header:
        centerElement:
          type: component.titles
          options:
            align: left
            # Use the parameter in the input expression
            # to show who is working on the task
            title: =@ctx.jig.inputs.taskAssignee
            icon: professions-man-construction-2
            iconColor: color10

      children:
        - type: component.entity
          options:
            children:
              - type: component.entity-field
                options:
                  label: Task Status
                  # Use the parameter in the input expression to show the status
                  value: =@ctx.jig.inputs.taskStatus
              - type: component.entity-field
                options:
                  label: Task Costs
                  # Use the parameter in the input expression to show the cost
                  value: =@ctx.jig.inputs.taskCost
```
{% endtab %}
{% endtabs %}

Input resources and code samples:

* [Passing data using inputs](../building-apps-with-jigx/ui/jigs-_screens_/passing-data-using-inputs.md)
* [Input examples](../building-apps-with-jigx/ui/jigs-_screens_/passing-data-using-inputs.md)

### When to use outputs

[Outputs](../building-apps-with-jigx/ui/jigs-_screens_/passing-data-using-outputs.md) are used to combine multiple jigs into one jig. Outputs pass variables from each jig into the next jig, and is best used in scenarios where there is a _many-to-one relationship_, for example, a manager needs to report on the progress of the team. Creating a master detail form is another use case for outputs.

**Design Pattern**: Observer

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-J2wSHx9xzGdeEuV5uLHvg-20240912-192654.gif" size="60" position="center"}

#### Setup:

1. In the jig that will pass the data define the **output** property with an expression that will pass the variable, such as an **ID**.
2. In the composite jig, which combines multiple jigs, define the **input** property on the jig that must receive the variable.

{% tabs %}
{% tab title="team-progress (output)" %}
```yaml
title: Team list
type: jig.list
icon: contact
isHorizontal: true
isHorizontalScrollIndicatorHidden: false
isSelectable: true
hasActiveItem: true

datasources:
  team:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC

      entities:
        - default/tasks
      query: |
        SELECT
         id, 
         '$.taskId',
         '$.Profile', 
         '$.taskAssignee',
         '$.team' 
        FROM [default/tasks] 
        WHERE '$.team' IS NOT NULL
# Set the output to use the Id defined in the set state
# The output- key will be passed in the input property,
# in the composite jig
outputs:
  output-key: =@ctx.solution.state.teamId

data: =@ctx.datasources.team
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.taskAssignee
    horizontalItemSize: large
    progress: =@ctx.current.item.id = @ctx.solution.state.teamId ? 1 :0
    color:
      - when: =@ctx.current.item.id = @ctx.solution.state.teamId ? true :false
        color: color2
    isContained: true
    leftElement:
      element: image
      text: ""
      uri: =@ctx.current.item.Profile
    onPress:
      type: action.action-list
      options:
        actions:
          # set the solution state and the value as id of the current selected item
          - type: action.set-state
            options:
              state: =@ctx.solution.state.teamId
              value: =@ctx.current.item.id
```
{% endtab %}

{% tab title="team" %}
```yaml
title: Team progress
type: jig.list
icon: contact

datasources:
  team-update:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC

      entities:
        - default/tasks
      # Define a query parameter to use the output property,
      # when it is passed into the jig.
      query: |
        SELECT
         id,
         '$.taskId',
         '$.taskAssignee',
         '$.taskCost',
         '$.taskStatus',
         '$.taskProfile' 
        FROM [default/tasks] 
        WHERE id = @statId
      queryParameters:
        statId: =@ctx.solution.state.teamId

data: =@ctx.datasources.team-update
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.taskId
    subtitle: =@ctx.current.item.taskCost
    leftElement:
      element: avatar
      text: =@ctx.current.item.taskAssignee
      uri: =@ctx.current.item.taskProfile
    rightElement:
      element: value
      text: =@ctx.current.item.taskStatus
```
{% endtab %}

{% tab title="team-report (input)" %}
```yaml
title: Team Report
type: jig.composite

children:
  - jigId: team-list
    instanceId: team-profile
  - jigId: team-data
    inputs:
      id: =@ctx.jigs.team-profile.outputs.output-key
```
{% endtab %}
{% endtabs %}

Output resources and code samples:

* [Passing data using outputs](../building-apps-with-jigx/ui/jigs-_screens_/passing-data-using-outputs.md)
* [Output examples](../building-apps-with-jigx/ui/jigs-_screens_/passing-data-using-outputs.md)

### Performance optimization

Using an `id` in your datasource enhances performance, particularly when handling large volumes of records.

{% code title="datasource" %}
```yaml
datasources:
  team-update:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/tasks
      query: |
        SELECT
         id,
         '$.taskId',
         '$.taskAssignee',
         '$.taskCost',
         '$.taskStatus',
         '$.taskProfile' 
        FROM [default/tasks] 
        WHERE id = @statId
      queryParameters:
        statId: =@ctx.solution.state.teamId
```
{% endcode %}
