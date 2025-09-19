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

## State scopes & performance

### Decision Tree

Use the decision tree below to guide you through the process of selecting the most appropriate state management scope and approach for application components, helping determine whether to use local component state, shared state, or global state management solutions based on data usage patterns and component relationships.

```
Need data across multiple screens? 
├─ YES → solution.state (USE SPARINGLY - causes app-wide re-render)
│  └─ Examples: projectId, auth session, theme
└─ NO → Screen-specific data?
   ├─ YES → jig.state (PREFERRED - screen-local, performant)
   │  └─ Examples: search filters, form flags, selection
   └─ NO → Component input/validation?
      └─ YES → component.state (automatic - user input, validation)
         └─ Examples: form values, isDirty, isValid
```

### Performance Impact Table

<table><thead><tr><th width="152.01953125">Scope</th><th width="135.2734375">re-render impact</th><th width="178.9765625">Use when</th><th>Avoid when</th></tr></thead><tbody><tr><td><code>solution.state</code></td><td>Entire app</td><td><ul><li>Authorization</li><li>Global selections that rarely change</li></ul></td><td><ul><li>UI filters</li><li> Form state</li><li>Temporary flags</li></ul></td></tr><tr><td><code>jig.state</code></td><td>Current screen</td><td><ul><li>Screen filters</li><li>Selection,</li><li>Wizard progress</li></ul></td><td><ul><li>Cross-screen data</li><li>Component values</li></ul></td></tr><tr><td><code>component.state</code></td><td>Single component</td><td><ul><li>User input</li><li>Validation</li></ul></td><td><ul><li>Cross-component data</li><li>Screen logic</li></ul></td></tr></tbody></table>

### Performance best practice

* **Scope Minimization**: Use narrowest scope  (component → jig → solution)
* **Avoid Global Overuse**: `solution.state` triggers app-wide re-render, prefer `jig.state` over `solution.state`
* **Initialize Explicitly**: Always set `initialValue` to avoid undefined behavior
* **Clean Up**: Reset transient state after actions/navigation
* **Pass vs Store**: Prefer navigation parameters over state storage
* **Passing data**: Pass data via parameters, not state
* **Clear  state**: on refresh/navigation

## State syntax

States vary based on the context in which they are used. Use IntelliSense in [expressions](expressions.md) to determine where you can make use of states. IntelliSense can assist by directing you to the context tree, showing which states are available for use within the context of the jig.

{% hint style="warning" %}
Avoid using state keywords, such as `component`, as `instanceId` values in expressions. Doing so will cause an "Expression is not valid" error in the app.
{% endhint %}

### Solution (Global) State

<table><thead><tr><th width="183.21484375">Syntax</th><th width="148.13671875">Key</th><th>Area</th></tr></thead><tbody><tr><td>=@ctx.solution.state.</td><td><p>activeItem </p><p>key </p><p>now</p></td><td><ul><li>Global variable used throughout a solution.</li><li>Your variable that can be set and read.</li></ul></td></tr></tbody></table>

### Jig (local) State

| Syntax               | Key                                                                                                                                                                                  | Area                                                                                                           |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------- |
| =@ctx.jig.state.     | <p>activeItem <br>activeItemId<br>amounts</p><p>filter </p><p>isHorizontal </p><p>isRefreshing </p><p>isSelectable isSelectActive </p><p>searchText </p><p>selected </p><p>value</p> | <p></p><ul><li>Applies to a list jig.</li></ul><ul><li>The creator configures the state in the YAML.</li></ul> |
| =@ctx.jig.instanceId |                                                                                                                                                                                      | <p></p><ul><li>Used to push the jig instance (state) to the navigation stack.</li></ul>                        |

### Component (local) State

<table><thead><tr><th width="299.9140625">Syntax</th><th width="129.2265625">Key</th><th>Area</th></tr></thead><tbody><tr><td>=@ctx.jigs.<em>jigInstanceId</em>.components.<em>componentInstanceId</em>.state.</td><td><p>data <br>isDirty </p><p>isValid </p><p>response</p></td><td><ul><li>Read the state of a component in a specific jig using the instanceId of both the jig and component.</li><li>Referencing components on a composite jig.</li></ul></td></tr><tr><td>=@ctx.component.state.</td><td><p>amount checked selected </p><p>value</p></td><td>State is the variable of /or for each component.</td></tr><tr><td>=@ctx.components.componentInstanceId.state.</td><td><p>data </p><p>filter isValid<br>isDirty isPending searchText selected response value</p></td><td><ul><li>State of components, using the component's instanceId.</li><li>Can use interaction from the user to add a value to the component's state, such as email-field, text-field, or number-field.</li></ul></td></tr><tr><td>=@ctx.current.state.</td><td>amount checked</td><td>Applies to a list, list.item, product-item, and stage components. The list's data is an array of records. The <code>=@ctx.current.state</code> is the state of the current object in the array.</td></tr></tbody></table>

## State Lifecycle

#### Lifetime

* `solution.state`: in-memory; cleared on logout (app-wide re-render on change).
* `jig.state`: per jig instance; persists while on navigation stack; resets on new instance.
* `component.state`: per component; cleared when navigating away from jig.

#### Initialization

```typescript
// ✅ Always use initialValue
jig.setState({ 
  searchQuery: { initialValue: '' },
  filters: { initialValue: { category: 'all' } },
  selected: { initialValue: [] }
})
```

#### Navigation

```typescript
// ✅ Pass data via parameters, not state
listItem.onPress.goto(SCREEN.DETAIL)
  .parameter('id', '=@ctx.current.item.id')
  .parameter('mode', 'view')

// Read on destination
detailText.value('=@ctx.jig.inputs.id')
```

#### Cleanup

```typescript
// ✅ Clear transient state on refresh/navigation
screen.onRefresh.resetjigState({ keys: ['searchQuery', 'selected'] })
screen.onLoad.resetjigState({ keys: ['error', 'draft'] })
```

## State Core operations

### **Initialize state:**&#x20;

* Sets up the initial state structure when the screen loads
* Defines default values to avoid `undefined` errors
* Creates the state "schema" for your screen

<pre class="language-yaml"><code class="lang-yaml"><strong>state:
</strong>  StateKey1: 
    # String
    initialValue: 
      value: string
  StateKey2: 
    # Array
    initialValue: 
      - one
      - two
      - three
  StateKey3:
    # object
    initialValue:
      - property: value
</code></pre>

### **Update state:**

* Updates only the specified state key
* Triggers re-render only for components that use that state
* Can chain multiple state changes
* Works with expressions and static values

{% tabs %}
{% tab title="solution" %}
```yaml
actions:
- numberOfVisibleActions: 1
  children:
    - type: action.reset-solution-state
      options:
        changes:
          - StateKey1
```
{% endtab %}

{% tab title="jig/screen" %}
```yaml
actions:
  - numberOfVisibleActions: 1
    children:
      - type: action.set-jig-state
        options:
          changes: 
            StateKey1: "New Value"       
```
{% endtab %}

{% tab title="component" %}
```yaml
actions:
- numberOfVisibleActions: 1
  children:
    - type: action.execute-entity
      options:
        title: Update Record
        provider: DATA_PROVIDER_LOCAL
        entity: products
        method: update
        data:
          textInput: =@ctx.components.textInput.state.value
```
{% endtab %}
{% endtabs %}

### **Clear state:**

* Resets specified keys back to their `initialValue`
* Can reset multiple keys at once
* Useful for cleanup and form resets

{% tabs %}
{% tab title="solution" %}
```javascript
actions:
- numberOfVisibleActions: 1
  children:
    - type: action.reset-solution-state
      options:
        changes:
          - StateKey1
          - StateKey2
          - StateKey3
```
{% endtab %}

{% tab title="jig/screen" %}
```yaml
actions:
- numberOfVisibleActions: 1
  children:
    - type: action.reset-jig-state
      options:
        changes: 
          - StateKey1
          - StateKey2
          - StateKey3
```
{% endtab %}

{% tab title="component" %}
```yaml
actions:
- numberOfVisibleActions: 1
  children:
    - type: action.reset-state
      options:
        state: =@ctx.components.instanceid.state.value
```
{% endtab %}
{% endtabs %}

## How to use State

### Solution state (global read and write state)

You can define your solution state to store objects and values temporarily and then read them in multiple places in your solution. These are not stored in any local or remote data store but only in live memory. If you log out your solution state is cleared.

* Configure the initial solution state in the **index.jigx** file by providing a `State Key` with a value.
* You can update the state using the `action.set-solution-state` action.
* To revert back to the initial state, simply use the `action.reset-solution-state` action.
* Multiple states can be added in index.jigx and `initialValues` support nested objects, strings, and arrays.
* To call nested objects in a state expression use: `=@ctx.solution.state.state-key.objectName`

#### Write solution state

Define your state key in the solution, either in a jig or in the index.jigx file. The value can be any value or object, and you can access it anywhere within your solution. The set-solution-state action are easy ways to define the solution state.

#### Read solution state

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
      - type: action.reset-solution-state
        options:
          title: Rest state
          changes:
            - status
```
{% endtab %}

{% tab title="Read state value" %}
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

### Jig state (read and write state)

Defines the state \[key] for the jig/screen that can be read from within the current jig.

* Configure the initial jig state in the desired jig file.
* In any jig, you can update the state using the `action.set-jig-state` action.
* To revert back to the initial state, simply use the `action.reset-jig-state` action.
* Multiple states can be added and `initialValues` support nested objects.
* To call nested objects in a state expression use `=@ctx.jig.state.state-key.objectName`

#### Within the jig

Reads the value in the jig's context (the jig where the expression is used), for example: `@ctx.jig.state.[key]`

Define your state key in the jig file. The value can be any string, array, or object, and you can access it anywhere within the jig. The `set-jig-state` action is an easy way to define the jig state and `reset-jig-state` action sets the state back to the initial key values.

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

### Component state (read state)

Define your state \[key] for a single component or all components in a jig. Navigating away from the jig clears your component's state as the data is stored in the live memory.

#### Within the current component

Reads the value of \[key] in the current component (the component where the expression is used), for example: `=@ctx.component.state.[key]`

#### Within all components in the current jig

Reads the value of \[key] in the current jig and components with `instanceId`, for example:`=@ctx.components.[instanceId].state.[key]`

#### Within all jigs and components in the solution

Reads the value of \[key] from the available jigs with `jigId` and components with `instanceId`. For example: `=@ctx.jigs.[jigId].components.[instanceId].state.[key]`

### Action state (write state)

You can use actions to set (update) or reset (clear) a state either in a solution, jig, or component. These actions can be configured under the `actions` node or under an event node, such as `onPress`.

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

#### Setting a state using an action (set-states)

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

#### Reset a state using an action (reset-states)

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

#### Setting a state on an event using an action

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

#### Action state patterns

{% tabs %}
{% tab title="Async Operations" %}
```typescript
// ✅ Pattern: Action states are automatic
buttons.add.executeEntity({ instanceId: 'save-action' })

// Read states
spinner.isVisible('=@ctx.actions.save-action.state.isPending')
successMsg.isVisible('=@ctx.actions.save-action.state.isSuccess')
errorMsg.text('=@ctx.actions.save-action.state.error.message')

// Access outputs
detailText.value('=@ctx.actions.save-action.outputs.recordId')
```
{% endtab %}

{% tab title="Loading States" %}
```typescript
// ✅ Pattern: Loading with error handling
screen.setState({ 
  isLoading: { initialValue: false },
  loadError: { initialValue: null }
})

buttons.add.sequential().actions
  .setScreenState().change('isLoading', true)
  .executeEntity({ provider: 'DATA_PROVIDER_REST', functionId: 'fetchData' })
  .setScreenState().change('isLoading', false)

// UI responds to states
spinner.isVisible('=@ctx.jig.state.isLoading')
errorMessage.isVisible('=@ctx.jig.state.loadError != null')
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
message = "hello world"
puts message
```
{% endtab %}
{% endtabs %}

### Quick Validation

```typescript
// State exists check
when: =@ctx.jig.state.searchQuery != null and @ctx.jig.state.searchQuery != ''

// Type safety  
when: =@ctx.jig.state.count ~> $type = 'number'

// Default values
text: =@ctx.jig.state.title ?: 'Default Title'
```

## Common state use cases (patterns)

* **Search & Filter** \
  Mirrors UI state to bind to datasource \
  Filter: `=@ctx.components.filter.state.value`\
  Query parameter: `=@ctx.jig.state.category`
* **List Selection**\
  Tracks selection in `jig.state`\
  The `onPress` action uses the `selectedId` of  `=@ctx.current.item.id`\
  Once selected uses `isSelected` of the `=@ctx.current.item.id`  in `=@ctx.jig.state.selectedId`
* **Field Validation**\
  Real-time validation with `errorText`

{% tabs %}
{% tab title="email-field" %}
<pre class="language-yaml"><code class="lang-yaml"><strong>errorText: =@ctx.components.email.state.isValid = false ? "Invalid email format" : null
</strong></code></pre>
{% endtab %}

{% tab title="text-field" %}
```yaml
errorText: =$length(@ctx.components.username.state.value) < 3 ? "Too short" : null'
```
{% endtab %}

{% tab title="number-field" %}
```ruby
errorText: =@ctx.components.phone.state.value ~> /^[0-9]{10}$/ ? null : "Must be 10 digits"
```
{% endtab %}
{% endtabs %}

* **Form Dirty Tracking**\
  Track changes for discard alert.\
  \- Set jig state ({ formIsDirty: { initialValue: false } })\
  \- `onFocus` then set jig state and change ('formIsDirty', true)\
  \- On the form `isDiscardChangesAlertEnabled` ('=@ctx.jig.state.formIsDirty')

## Examples of state

The table below provides links to various examples of configuring state in the [jigx-samples](https://docs.jigx.com/examples/readme/setting-up-your-solution).

<table><thead><tr><th width="267">Scenario</th><th width="165.6328125">Key</th><th>GitHub jigx-samples examples</th></tr></thead><tbody><tr><td>Set an item to active with onPress</td><td>ActiveItemId</td><td>List with active items</td></tr><tr><td>searchText (component level)</td><td>searchText</td><td>Dropdown with search</td></tr><tr><td>filter and searchText (jig level)</td><td>filter, searchText</td><td>List with filter and search</td></tr><tr><td>Saving data to a provider</td><td>value</td><td>Update service form</td></tr><tr><td>Evaluating an amount</td><td>amount</td><td>Product item maximum tag</td></tr><tr><td>Evaluating if an item is selected</td><td>checked</td><td>Highlight selected list of cleaning services</td></tr><tr><td>Evaluating selected items</td><td>selected</td><td>Evaluate progress to show helper and error text</td></tr><tr><td>Reset a form</td><td>reset-state (action)</td><td>Reset a form</td></tr><tr><td>Set state on an active item in a list when the onPress event executes</td><td>set-state (action)</td><td>Color a chosen item when pressing on an item in a list</td></tr></tbody></table>

## See Also

* [set-state](https://docs.jigx.com/examples/readme/actions/set-state)
* [reset-state](https://docs.jigx.com/examples/reset-state)
