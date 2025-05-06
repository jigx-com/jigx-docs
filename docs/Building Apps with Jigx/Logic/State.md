---
title: State
slug: 0JS3-state
description: Learn about the concept of state in a solution and discover its applications in solution state, jig state, component state, keg state, and action state. Explore examples and techniques to access and modify state values in each context. Access additional e
createdAt: Tue Jun 07 2022 12:14:05 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Apr 23 2025 07:46:39 GMT+0000 (Coordinated Universal Time)
---

State manages the data within Jigx solutions, jigs, and components and controls the UI dynamically. The state allows solutions and components to change their output in response to user inputs and actions. Often, the state is used as a global variable that can be used throughout the solution or as a local state used only in that specific jig or component.

Examples of using state include:

- Displaying a list of items that change based on user interaction.
- Handling user inputs in forms, such as text inputs or switches. By storing input values in the state, you can easily control the components and validate user input.
- Control the behavior of components, like showing or hiding a component based on a condition, enabling or disabling buttons or fields, and resetting a component's value.
- State is local to the jig or component where it is declared; you can share the state across multiple jigs and their components or use a global state across the entire solution.

State allows you to **read** and **write** the state of various data in your solution at runtime.

:::hint{type="warning"}
Whenever working with data, consider the performance impact on the Jigx App at runtime. The best practice is to write only the required data in the state and consider using state versus [inputs](<./../UI/Jigs _screens_/Passing data using inputs.md>) and [outputs](<./../UI/Jigs _screens_/Passing data using outputs.md>).
:::

Using states in Jigx is divided into categories:

1. **Global state** - known as solution state in Jigx, refers to data that needs to be accessed and updated by multiple components across the app. Effectively managing the global state ensures that all parts of the app that depend on this data are updated consistently. The global/solution state is a variable used throughout the solution. 
2. **Local state** - known as component state in Jigx, refers to data that is confined to a single component or jig. This type of state is typically managed within the component itself. The creator can set each component state in the YAML or by user input, such as a text field. The state key options depend on the component.
3. **State navigation** allows you to determine the flow of screens and the state of each one in the flow. See [Navigation](./Navigation.md) for more information.

## State syntax

States vary based on the context in which they are used. Use IntelliSense in [expressions](./Expressions.md) to determine where you can make use of states.  IntelliSense can assist by directing you to the context tree, showing which states are available for use within the context of the jig.

:::hint{type="warning"}
Avoid using state keywords, such as `component`, as `instanceId` values in expressions. Doing so will cause an "Expression is not valid" error in the app.
:::

Avoid using state keywords, such as `component`, as `instanceId` values in expressions. Doing so will cause an "Expression is not valid" error in the app.

### Solution (Global) State

| **Syntax**             | **Key**                    | **Area**                                                                                      |
| ---------------------- | -------------------------- | --------------------------------------------------------------------------------------------- |
| =@ctx.solution.state.  | activeItem&#xA;key&#xA;now | - Global variable used throughout a solution.
- Your variable that can be set and read. |

### Component (local) State

| **Syntax**                                                         | **Key**                                                                                                                                                         | **Area**                                                                                                                                                                                      |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| =@ctx.jig.state.                                                   | activeItem&#xA;activeItemId&#xA;amounts&#xA;filter&#xA;isHorizontal&#xA;isRefreshing&#xA;isSelectable&#xA;isSelectActive&#xA;searchText&#xA;selected&#xA;value  | - Applies to a list jig.
- The creator configures the state in the YAML.&#x20;                                                                                                                |
| =@ctx.jigs.*jigInstanceId*.components.*componentInstanceId*.state. | data&#xA;isDirty&#xA;isValid&#xA;response                                                                                                                       | * Read the state of a component in a specific jig using the instanceId of both the jig and component.
* Referencing components on a composite jig.                                            |
| =@ctx.component.state.                                             | amount&#xA;checked&#xA;selected&#xA;value                                                                                                                       | - State is the variable of or for each component.                                                                                                                                             |
| =@ctx.components.*componentInstanceId.*state.                      | data&#xA;filter&#xA;isValid&#xA;isDirty&#xA;isPending&#xA;searchText&#xA;selected&#xA;response&#xA;value                                                        | * State of components, using the component's instanceId.
* Can use interaction from the user to add a value to the component's state, such as email-field, text-field, or number-field.       |
| =@ctx.current.state.                                               | amount&#xA;checked                                                                                                                                              | - Applies to a list, list.item, product-item, and stage components. The list's data is an array of records. The `=@ctx.current.state` is the state of the current object in the array. |

### Jig (local) State

| **Syntax**           | **Key** | **Area**                                                        |
| -------------------- | ------- | --------------------------------------------------------------- |
| =@ctx.jig.instanceId |         | Used to push the jig instance (state) to the navigation stack.  |

## How to use State

::::ExpandableHeading
## Solution state (global read and write state)

You can define your solution state to store objects and values temporarily and then read them in multiple places in your solution. These are not stored in any local or remote data store but only in live memory. If you log out your solution state is cleared.

- &#x20;Configure the initial solution state in the **index.jigx **file by providing a `State Key` with a value.
- You can update the state using the `action.set-solution-state` action.
- To revert back to the initial state, simply use the `action.reset-solution-state` action.
- Multiple states can be added in index.jigx and `initialValues` support nested objects.
- To call nested objects in a state expression use `=@ctx.solution.state.state-key.objectName`

### Write solution state

Define your state key in the solution, either in a jig or in the index.jigx file. The value can be any value or object, and you can access it anywhere within your solution. The [set-solution-state]()  and [set-state]() action are easy ways to define the solution state.

### Read solution state

To access your custom solution state, use the expression path below and replace \[key] with your custom solution state key.

1. `=@ctx.solution.state.[key]`.
2. For nested objects use `=@ctx.solution.state.state-key.objectName`.

:::CodeblockTabs
index.jigx

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

action.set-solution-state (Write)

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

action.reset-solution-state (Write)

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

jig-a.jigx

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
:::
::::

::::ExpandableHeading
## Jig state (read and write state)

Defines the state \[key] for jig that can be read from within the current jig.

- Configure the initial jig state in the desired jig** **file.
- In any jig, you can update the state using the `action.set-jig-state` action.
- To revert back to the initial state, simply use the `action.reset-jig-state` action.
- Multiple states can be added and `initialValues` support nested objects.
- To call nested objects in a state expression use `=@ctx.jig.state.state-key.objectName`

### Within the jig

Reads the value in the jig's context (the jig where the expression is used), for example: `@ctx.jig.state.[key]`

Define your state key in the jig file. The value can be any value or object, and you can access it anywhere within the jig. The [set-jig-state]() action is an easy way to define the jig state and [reset-jig-state]() action sets the state back to the initial key values.

:::CodeblockTabs
jig-initial-state.jigx

```yaml
title: Global Inc
description: Welcome to Gobal Inc 
type: jig.default
# Configuer the initial jig state key values.
state:
  predefinedtext:
    initialValue: "Committed to excellence and innovation"
  address:
    initialValue: 
      street: 145 Morrissey Blvd
      city: Boston
      zip code: O2125 
```

action.set-jig-state (write)

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

action.reset-jig-state (write)

```yaml
# Reset the jig state keys to their initial values.
- type: action.reset-jig-state
        options:
          title: Reset state
          changes:
            - predefinedtext
            - address
```

jig-a.jigx (read)

```yaml
title: Global Inc
# Read the jig state key value.
description: =@ctx.jig.state.predefinedtext
type: jig.default
```
:::
::::

:::ExpandableHeading
## Component state (read state)

Define your state \[key] for a single component or all components in a jig. Navigating away from the jig clears your component's state as the data is stored in the live memory.

### Within the current component

Reads the value of \[key] in the current component (the component where the expression is used), for example: `@ctx.component.state.[key]`

### Within all components in the current jig

Reads the value of \[key] in the current jig and components with `instanceId`, for example:`@ctx.components.[instanceId].state.[key]`

### Within all jigs and components in the solution

Reads the value of \[key] from the available jigs with `jigId` and components with `instanceId`. For example:&#x20;
`@ctx.jigs.[jigId].components.[instanceId].state.[key]`
:::

::::ExpandableHeading
## Action state (write state)

You can use actions to set or reset a state either in a solution, jig, or component. These actions can be configured under the `actions` node or under an event node, such as `onPress`.&#x20;

The following **set-state** actions are available:

- [action.set-state]()&#x20;
- `action.set-solution-state`
- `action.set-jig-state`
- `action.set-custom-component-state`

The following **reset-state** actions are available:

- [action.reset-state]()&#x20;
- `action.reset-solution-state`
- `action.reset-jig-state`
- `action.reset-custom-component-state`

The only difference between these states are the scope where they are used. See the table below.

| **Action**                            | **Solution** | **Jig** | **Component** | **custom component (alpha)** |
| ------------------------------------- | ------------ | ------- | ------------- | ---------------------------- |
| `action.set-state`                    | ✅            |         | ✅             |                              |
| `action.reset-state`                  | ✅            |         | ✅             |                              |
| `action.set-solution-state`           | ✅            | ✅       |               | ✅                            |
| `action.reset-solution-state`         | ✅            | ✅       |               | ✅                            |
| `action.set-jig-state`                |              | ✅       |               | ✅                            |
| `action.reset-jig-state`              |              | ✅       |               | ✅                            |
| `action.set-custom-component-state`   |              |         |               | ✅                            |
| `action.reset-custom-component-state` |              |         |               | ✅                            |

### Setting a state using an action (set-states)

The basic `set-state` actions code structures are shown below:

:::CodeblockTabs
set-solution-state-action

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

set-jig-state-action

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

set-state-action

```yaml
- type: action.set-state
        options:
          title: Set state
          state: =@ctx.solution.state.global-key
          value: '12345'
```
:::

### Reset a state using an action (reset-states)

The basic `reset-state` actions code structures are shown below:

:::CodeblockTabs
reset-solution-state-action

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

reset-jig-state-action

```yaml
# Reset the jig state keys to their initial values.
- type: action.reset-jig-state
        options:
          title: Reset state
          changes:
            - predefinedtext
            - address
```

reset-state-action

```yaml
- type: action.reset-state
        options:
          title: Reset solution state
          state: =@ctx.solution.state.global-key
```
:::

### Setting a state on an event using an action

You can use the `set-states` or `reset-states` actions with the following events:

- onFocus
- onLoad
- onPress
- onRefresh
- onChange

:::CodeblockTabs
onFocus-set-solution-state

```yaml
onFocus: 
  type: action.set-solution-state
  options:
    changes:
      status: =@ctx.datasources.company[0].mottos
```
:::
::::

## Examples of state

The table below provides links to various examples of configuring state in the [jigx-samples ]().

| **Scenario**                                                          | **Key**               | **GitHub jigx-samples examples**                                                                                                                                                                                                                            |
| --------------------------------------------------------------------- | --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Set an item to active with onPress                                    | ActiveItemId          | <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-list/advanced-lists/static-data/list-with-active-item-sd.jigx" target="_blank">List with active items</a>                                            |
| searchText (component level)                                          | searchText            | <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/dropdown/static-data/dropdown-searchable.jigx" target="_blank">Dropdown with search</a>                                                            |
| filter and searchText (jig level)                                     | filter&#xA;searchText | <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-list/advanced-lists/dynamic-data/list-filter-search-label-dd.jigx" target="_blank">List with filter and search</a>                                   |
| Saving data to a provider                                             | value                 | <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/field-row/dynamic-data/form-row-children-dd.jigx" target="_blank">Update service form</a>                                                          |
| Evaluating an amount                                                  | amount                | <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/product-item/dynamic-data/product-item-example/product-item-example-dynamic.jigx" target="_blank">Product item maximum tag</a>                     |
| Evaluating if an item is selected                                     | checked               | <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list-item/dynamic-data/list-with-right-elements/list-with-right-checkbox-dd.jigx" target="_blank">Highlight selected list of cleaning services</a> |
| Evaluating selected items                                             | selected              | <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/progress-bar/progress-bar-dynamic.jigx" target="_blank">Evaluate progress to show helper and error text</a>                                        |
| Reset a form                                                          | reset-state (action)  | <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/actions/reset-state/static-data/reset-state-action-form.jigx" target="_blank">Reset a form</a>                                                                     |
| Set state on an active item in a list when the onPress event executes | set-state (action)    | <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-actions/action-list/action-list-onPress.jigx" target="_blank">Color a choosen item when pressing on an item in a list</a>                                     |

## See Also

- [set-state]()
- [reset-state]()

