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

# State

State manages the data within Jigx solutions, jigs, and components and controls the UI dynamically. The state allows solutions and components to change their output in response to user inputs and actions. Often, the state is used as a global variable that can be used throughout the solution or as a local state used only in that specific jig or component.

Examples of using state include:

* Displaying a list of items that change based on user interaction.
* Handling user inputs in forms, such as text inputs or switches. By storing input values in the state, you can easily control the components and validate user input.
* Control the behavior of components, like showing or hiding a component based on a condition, enabling or disabling buttons or fields, and resetting a component's value.
* State is local to the jig or component where it is declared; you can share the state across multiple jigs and their components or use a global state across the entire solution.

State allows you to **read** and **write** the state of various data in your solution at runtime.

{% hint style="warning" %}
Whenever working with data, consider the performance impact on the Jigx App at runtime. The best practice is to write only the required data in the state and consider using state versus [inputs](../ui/jigs-_screens_/passing-data-using-inputs.md) and [outputs](../ui/jigs-_screens_/passing-data-using-outputs.md).
{% endhint %}

Using states in Jigx is divided into categories:

1. **Global state** - known as solution state in Jigx, refers to data that needs to be accessed and updated by multiple components across the app. Effectively managing the global state ensures that all parts of the app that depend on this data are updated consistently. The global/solution state is a variable used throughout the solution.
2. **Local state** - known as component state in Jigx, refers to data that is confined to a single component or jig. This type of state is typically managed within the component itself. The creator can set each component state in the YAML or by user input, such as a text field. The state key options depend on the component.
3. **State navigation** allows you to determine the flow of screens and the state of each one in the flow. See [Navigation](navigation.md) for more information.

## State syntax

States vary based on the context in which they are used. Use IntelliSense in [expressions](expressions.md) to determine where you can make use of states. IntelliSense can assist by directing you to the context tree, showing which states are available for use within the context of the jig.

{% hint style="warning" %}
Avoid using state keywords, such as `component`, as `instanceId` values in expressions. Doing so will cause an "Expression is not valid" error in the app.
{% endhint %}

Avoid using state keywords, such as `component`, as `instanceId` values in expressions. Doing so will cause an "Expression is not valid" error in the app.

### Solution (Global) State

<table><thead><tr><th width="184.20703125">Syntax</th><th width="148.13671875">Key</th><th>Area</th></tr></thead><tbody><tr><td>=@ctx.solution.state.</td><td>activeItem key now</td><td><ul><li>Global variable used throughout a solution.</li><li>Your variable that can be set and read.</li></ul></td></tr></tbody></table>

### Component (local) State

<table><thead><tr><th width="299.9140625">Syntax</th><th width="129.2265625">Key</th><th>Area</th></tr></thead><tbody><tr><td>=@ctx.jig.state.</td><td>activeItem activeItemId amounts filter isHorizontal isRefreshing isSelectable isSelectActive searchText selected value</td><td><ul><li>Applies to a list jig.</li><li>The creator configures the state in the YAML.</li></ul></td></tr><tr><td>=@ctx.jigs.<em>jigInstanceId</em>.components.<em>componentInstanceId</em>.state.</td><td>data isDirty isValid response</td><td><ul><li>Read the state of a component in a specific jig using the instanceId of both the jig and component.</li><li>Referencing components on a composite jig.</li></ul></td></tr><tr><td>=@ctx.component.state.</td><td>amount checked selected value</td><td>State is the variable of or for each component.</td></tr><tr><td>=@ctx.components.componentInstanceId.state.</td><td>data filter isValid<br>isDirty isPending searchText selected response value</td><td><ul><li>State of components, using the component's instanceId.</li><li>Can use interaction from the user to add a value to the component's state, such as email-field, text-field, or number-field.</li></ul></td></tr><tr><td>=@ctx.current.state.</td><td>amount checked</td><td>Applies to a list, list.item, product-item, and stage components. The list's data is an array of records. The <code>=@ctx.current.state</code> is the state of the current object in the array.</td></tr></tbody></table>

### Jig (local) State

<table><thead><tr><th width="189.515625">Syntax</th><th width="238.25390625">Key</th><th>Area</th></tr></thead><tbody><tr><td>=@ctx.jig.instanceId</td><td></td><td>Used to push the jig instance (state) to the navigation stack.</td></tr></tbody></table>

## How to use State

## Solution state (global read and write state)

You can define your solution state to store objects and values temporarily and then read them in multiple places in your solution. These are not stored in any local or remote data store but only in live memory. If you log out your solution state is cleared.

* Configure the initial solution state in the **index.jigx** file by providing a `State Key` with a value.
* You can update the state using the `action.set-solution-state` action.
* To revert back to the initial state, simply use the `action.reset-solution-state` action.
* Multiple states can be added in index.jigx and `initialValues` support nested objects.
* To call nested objects in a state expression use `=@ctx.solution.state.state-key.objectName`

### Write solution state

Define your state key in the solution, either in a jig or in the index.jigx file. The value can be any value or object, and you can access it anywhere within your solution. The set-solution-state and [set-state](https://docs.jigx.com/examples/readme/actions/set-state) action are easy ways to define the solution state.

### Read solution state

To access your custom solution state, use the expression path below and replace \[key] with your custom solution state key.

1. `=@ctx.solution.state.[key]`.
2. For nested objects use `=@ctx.solution.state.state-key.objectName`.

{% tabs %}
{% tab title=" index.jigx" %}
```yaml
name: Projects
title: Global Projects
category: business
# Solution state's initial key values.
state:
  project:
    initialValue:
      # Nested objects
      status: "Active"
      team: "Planning team"
  Billing:
    initialValue: "Monthly"
```
{% endtab %}

{% tab title="action.set-solution-state (Write)" %}
```yaml
# Set the solution state keys to the initial values.
actions:
  - children:
      - type: action.set-solution-state
        options:
          title: Update state
          changes:
            status: "InActive"
```
{% endtab %}

{% tab title="action.reset-solution-state (Write)" %}
```yaml
# Reset the solution state key to the initial value.
actions:
  - children:
      - type: action.reset-jig-state
        options:
          title: Rest state
          changes:
            - status
```
{% endtab %}

{% tab title="Untitled" %}
```yaml
children:
  - type: component.entity
    instanceId: change
    options:
      children:
        - type: component.entity-field
          instanceId: state-change
          options:
            label: state
            # Read the solution state using an expression.
            value: =@ctx.solution.state.status
```
{% endtab %}
{% endtabs %}

## Jig state (read and write state)

Defines the state \[key] for jig that can be read from within the current jig.

* Configure the initial jig state in the desired jig file.
* In any jig, you can update the state using the `action.set-jig-state` action.
* To revert back to the initial state, simply use the `action.reset-jig-state` action.
* Multiple states can be added and `initialValues` support nested objects.
* To call nested objects in a state expression use `=@ctx.jig.state.state-key.objectName`

### Within the jig

Reads the value in the jig's context (the jig where the expression is used), for example: `@ctx.jig.state.[key]`

Define your state key in the jig file. The value can be any value or object, and you can access it anywhere within the jig. The 'set-jig-state' action is an easy way to define the jig state and 'r'eset-jig-state' action sets the state back to the initial key values.

{% tabs %}
{% tab title="jig-initial-state.jigx" %}
```yaml
title: Global Inc
description: Welcome to Gobal Inc
type: jig.default
# Configure the initial jig state key values.
state:
  predefinedtext:
    initialValue: "Committed to excellence and innovation"
  address:
    initialValue:
      street: 145 Morrissey Blvd
      city: Boston
      zip code: O2125
```
{% endtab %}

{% tab title="action.set-jig-state (write)" %}
```yaml
# Set the jig state keys to new values.
actions:
  - children:
      - type: action.set-jig-state
        options:
          title: Update state
          changes:
            predefinedtext: "Innovation. Always."
            address:
              street: 8 Columbia Road
              city: Boston
              zip code: O2125
```
{% endtab %}

{% tab title="action.reset-jig-state (write)" %}
```yaml
# Reset the jig state keys to their initial values.
- type: action.reset-jig-state
        options:
          title: Reset state
          changes:
            - predefinedtext
            - address
```
{% endtab %}

{% tab title="jig-a.jigx (read)" %}
```yaml
title: Global Inc
# Read the jig state key value.
description: =@ctx.jig.state.predefinedtext
type: jig.default
```
{% endtab %}
{% endtabs %}

## Component state (read state)

Define your state \[key] for a single component or all components in a jig. Navigating away from the jig clears your component's state as the data is stored in the live memory.

### Within the current component

Reads the value of \[key] in the current component (the component where the expression is used), for example: `@ctx.component.state.[key]`

### Within all components in the current jig

Reads the value of \[key] in the current jig and components with `instanceId`, for example:`@ctx.components.[instanceId].state.[key]`

### Within all jigs and components in the solution

Reads the value of \[key] from the available jigs with `jigId` and components with `instanceId`. For example: `@ctx.jigs.[jigId].components.[instanceId].state.[key]`

## Action state (write state)

You can use actions to set or reset a state either in a solution, jig, or component. These actions can be configured under the `actions` node or under an event node, such as `onPress`.

The following **set-state** actions are available:

* [action.set-state](https://docs.jigx.com/examples/readme/actions/set-state)
* `action.set-solution-state`
* `action.set-jig-state`
* `action.set-custom-component-state`

The following **reset-state** actions are available:

* [action.reset-state](https://docs.jigx.com/examples/reset-state)
* `action.reset-solution-state`
* `action.reset-jig-state`
* `action.reset-custom-component-state`

The only difference between these states are the scope where they are used. See the table below.

<table data-full-width="true"><thead><tr><th width="319.76953125">Action</th><th width="102.91796875">Solution</th><th width="67.47265625">Jig</th><th width="124.7421875">Component</th><th>custom component (alpha)</th></tr></thead><tbody><tr><td><code>action.set-state</code></td><td>✅</td><td></td><td>✅</td><td></td></tr><tr><td><code>action.reset-state</code></td><td>✅</td><td></td><td>✅</td><td></td></tr><tr><td><code>action.set-solution-state</code></td><td>✅</td><td>✅</td><td></td><td>✅</td></tr><tr><td><code>action.reset-solution-state</code></td><td>✅</td><td>✅</td><td></td><td>✅</td></tr><tr><td><code>action.set-jig-state</code></td><td></td><td>✅</td><td></td><td>✅</td></tr><tr><td><code>action.reset-jig-state</code></td><td></td><td>✅</td><td></td><td>✅</td></tr><tr><td><code>action.set-custom-component-state</code></td><td></td><td></td><td></td><td>✅</td></tr><tr><td><code>action.reset-custom-component-state</code></td><td></td><td></td><td></td><td>✅</td></tr></tbody></table>

### Setting a state using an action (set-states)

The basic `set-state` actions code structures are shown below:

{% tabs %}
{% tab title="set-solution-state-action" %}
```yaml
# Set the solution state keys to new values.
actions:
  - children:
      - type: action.set-solution-state
        options:
          title: Update state
          changes:
            # state key.
            status: "InActive"
```
{% endtab %}

{% tab title="set-jig-state-action" %}
```yaml
# Set the jig state keys to new values.
actions:
  - children:
      - type: action.set-jig-state
        options:
          title: Update state
          changes:
            # Multiple state keys.
            predefinedtext: "Innovation. Always."
            address:
              street: 8 Columbia Road
              city: Boston
              zip code: O2125
```
{% endtab %}

{% tab title="set-state-action" %}
```yaml
- type: action.set-state
        options:
          title: Set state
          state: =@ctx.solution.state.global-key
          value: '12345'
```
{% endtab %}
{% endtabs %}

### Reset a state using an action (reset-states)

The basic `reset-state` actions code structures are shown below:

{% tabs %}
{% tab title="reset-solution-state-action" %}
```yaml
# Reset the solution state keys to the initial values.
actions:
  - children:
      - type: action.set-solution-state
        options:
          title: Update state
          changes:
            status: "InActive"
```
{% endtab %}

{% tab title="reset-jig-state-action" %}
```yaml
# Reset the jig state keys to their initial values.
- type: action.reset-jig-state
        options:
          title: Reset state
          changes:
            - predefinedtext
            - address
```
{% endtab %}

{% tab title="reset-state-action" %}
```yaml
- type: action.reset-state
        options:
          title: Reset solution state
          state: =@ctx.solution.state.global-key
```
{% endtab %}
{% endtabs %}

### Setting a state on an event using an action

You can use the `set-states` or `reset-states` actions with the following events:

* onFocus
* onLoad
* onPress
* onRefresh
* onChange

{% code title="onFocus-set-solution-state" %}
```yaml
onFocus:
  type: action.set-solution-state
  options:
    changes:
      status: =@ctx.datasources.company[0].mottos
```
{% endcode %}

## Examples of state

The table below provides links to various examples of configuring state in the [jigx-samples](https://docs.jigx.com/examples/readme/setting-up-your-solution).

<table><thead><tr><th width="267">Scenario</th><th width="165.6328125">Key</th><th>GitHub jigx-samples examples</th></tr></thead><tbody><tr><td>Set an item to active with onPress</td><td>ActiveItemId</td><td>List with active items</td></tr><tr><td>searchText (component level)</td><td>searchText</td><td>Dropdown with search</td></tr><tr><td>filter and searchText (jig level)</td><td>filter, searchText</td><td>List with filter and search</td></tr><tr><td>Saving data to a provider</td><td>value</td><td>Update service form</td></tr><tr><td>Evaluating an amount</td><td>amount</td><td>Product item maximum tag</td></tr><tr><td>Evaluating if an item is selected</td><td>checked</td><td>Highlight selected list of cleaning services</td></tr><tr><td>Evaluating selected items</td><td>selected</td><td>Evaluate progress to show helper and error text</td></tr><tr><td>Reset a form</td><td>reset-state (action)</td><td>Reset a form</td></tr><tr><td>Set state on an active item in a list when the onPress event executes</td><td>set-state (action)</td><td>Color a chosen item when pressing on an item in a list</td></tr></tbody></table>

## See Also

* [set-state](https://docs.jigx.com/examples/readme/actions/set-state)
* [reset-state](https://docs.jigx.com/examples/reset-state)
