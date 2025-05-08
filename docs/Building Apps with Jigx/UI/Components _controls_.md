---
title: Components (controls)
slug: AaWo-c
createdAt: Mon Jan 15 2024 10:26:38 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Mar 19 2025 10:13:22 GMT+0000 (Coordinated Universal Time)
---

Jigx comprises of UI elements known as components, which are an essential part of the app. These components can be in the form of images, avatars, forms, lists, progress bars, charts, and more. They are modular, customizable, and reusable, which ensures consistency and ease of use across the app. These components have predefined behaviors but can be customized to suit your specific requirements. Utilizing these components allows you to create visually appealing and interactive screens that enhance the overall user experience.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/s1GDSrLC9kJ9N1FmhgN6q_componentoverview.png" size="82" position="center" caption="Components" alt="Components"}

## Considerations

- [Planning](<./../../Getting started/Planning your app.md>) the design of each app screen helps decide which component is best suited to achieve the desired functionality.
- Components can be shown in the [Content widget components](), for example, a pie chart or image displays in the widget either on the Home Hub or on a jig.
- Certain components can only be used in specific [jig types](<./Jigs _screens_.md>), for example, [event]() can only be used with [jig.calendar](). Use IntelliSense (*ctrl+space*) in each jig type to see a list of available components for that jig or reference the table below.

## List of components

| **Type**           | **Component**                                                                                                                                                                                                                       | **Jig Type**                                             |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| Content containers | [card]()                                                                                                                                                                                                                            | default                                                  |
|                    | [carousel]()                                                                                                                                                                                                                        | default                                                  |
|                    | [expander]()                                                                                                                                                                                                                        | default&#xA;list                                         |
|                    | [image]()                                                                                                                                                                                                                           | default                                                  |
|                    | [jig-header]()                                                                                                                                                                                                                      | default&#xA;calendar&#xA;list&#xA;document&#xA;composite |
|                    | [list]()&#xA;[list-item]()&#xA;[product-item]()&#xA;[stage]()                                                                                                                                                                       | list&#xA;default                                         |
|                    | [location]()                                                                                                                                                                                                                        | default&#xA;full-screen                                  |
|                    | [segmented-control]()                                                                                                                                                                                                               | default                                                  |
|                    | [stepper]()                                                                                                                                                                                                                         | default                                                  |
|                    | [web-view]()                                                                                                                                                                                                                        | default                                                  |
|                    | [video-player]()                                                                                                                                                                                                                    | default                                                  |
| Display            | [divider]() &#xA;[entity]()&#xA;[field-row]()&#xA;[entity-field]()&#xA;[section]()                                                                                                                                                  | default                                                  |
| Informational      | [avatar]()                                                                                                                                                                                                                          | default                                                  |
|                    | [bar-chart]()                                                                                                                                                                                                                       | default&#xA;list                                         |
|                    | [countdown]()                                                                                                                                                                                                                       | default                                                  |
|                    | [count-up]()                                                                                                                                                                                                                        | default                                                  |
|                    | [event]()                                                                                                                                                                                                                           | calendar                                                 |
|                    | [line-chart]()                                                                                                                                                                                                                      | default                                                  |
|                    | [pie-chart]()                                                                                                                                                                                                                       | default&#xA;list                                         |
|                    | [progress-bar]()                                                                                                                                                                                                                    | default                                                  |
|                    | [summary]()                                                                                                                                                                                                                         | default&#xA;list&#xA;document                            |
| Input controls     | [chat]() &#xA;[choice-field]() &#xA;[duration-picker]() &#xA;[form]()&#xA;[media-field]()&#xA;[text-field]()&#xA;[email-field]()&#xA;[number-field]()&#xA;[dropdown]()&#xA;[checkbox]()&#xA;[date-picker]()&#xA;[signature-field]() | default                                                  |
| Interactive        | [interactive-image]()&#xA;[interactive-image-item]()                                                                                                                                                                                | default                                                  |
| Navigation         | [widgets]()                                                                                                                                                                                                                         | default&#xA;composite&#xA;list&#xA;document              |

## YAML structure for components

In Jigx Builder the YAML format for a component is `type: component.avatar` and is configured at a specific level, and under a property depending on the jig type.

- In **default jigs** components are configured under the `children:` property.
- In **full-screen jigs** components are configured under the `component:` property.
- In **list** and **calendar jigs** components are configured under the `item:` property.

:::CodeblockTabs
default-jig

```yaml
title: Name
description: Description of your Jig
type: jig.default

children:
  - type: component.avatar
    options:
      title: Jane
```

full-screen-jig

```yaml
title: Name
type: jig.full-screen

component: 
  type: component.chat
  instanceId: myChat
```

list+calendar-jig

```yaml
title: Name
description: Description of your Jig
type: jig.list
icon: contact

data: =@ctx.datasources.mydata
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.datasourcefield
    subtitle: =@ctx.current.item.datasourcefield
```
:::

Multiple components can be added in certain jig types such as the default jig which is the most versitle. The components are configured at the same level as the first component; or are nested under other components but will be preceeded by a `children:` property.&#x20;

:::CodeblockTabs
multiple-components

```yaml
title: Multiple components
type: jig.default

children:
# First component 
  - type: component.avatar
    options:
      title: Jane
# Add second component at the same YAML level as the first      
  - type: component.countdown
    options:
      expiresAt: "2024-08-13"
# Add second component at the same YAML level as the first       
  - type: component.section
    options:
      title: Register
      # Add a nested component under a new children property
      children:
        - type: component.form
          instanceId: RegistrationForm
          options:
          # Add a nested component under a new children property
            children:
              - type: component.text-field
                instanceId: name
                options:
                  label: First and last name
```
:::

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Each components YAML loads with the core required properties. Use IntelliSense under each components `options:` property to discover additional optional properties. These properties usually help with **styling**, **postioning** and **size**.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/qjyoHnYWmeQMpjfAonABr_cc-options.png" size="72" position="center" caption="Optional properties" alt="Optional properties"}
:::
::::

## How to add a UI component

![Adding components](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/kN_gZ2A0gxdTYu8sLRolM_cc-addingcomponent.gif "Adding components")

1. Open or create a solution in Jigx Builder.
2. Open the jig type where the component must be configured. The default YAML structure of the jig prepopulates.
3. Under the correct YAML level (either under `children`, `item`, `component` depending on the jig type), *ctrl+space* to invoke Intellisense for the list of available components.
4. Select the required component, the core properties will load in the code snippet. Configure the properties accordingly using expressions and values.
5. Use IntelliSense under each components `options:` property to discover additional optional properties, relating to styling, positioning or size.
## Adding data to components

Creating dynamic, interactive, and user-centric jigs require components to be functional, and relevant to the user. To achieve this use [data](./../Data.md) when configuring components, and expose the specific data in the compoment by configuring [expressions](./../Logic/Expressions.md), such as:
`type: component.countdown`
`options:`
`expiresAt: =@ctx.datasources.event-dd[2].StartDate`

Certain components make it easy to add data through a `data:` property set at the start of the component allowing the data fields to be easily referenced in expressions. For example:

```yaml
# reference a datasource for context throughout the component
data: =@ctx.datasources.users
item:
  type: component.list-item
  options:
    divider: solid
   # Use the data reference to configure properties in the component 
    title: =@ctx.current.item.title
    subtitle: =@ctx.current.item.subtitle
    description: =@ctx.current.item.description
    color:
      - when: =@ctx.datasources.users.color
        color: =@ctx.current.item.color
```

## Adding actions to components - (single or multiple)

Engaging users on every screen of your app is vital to its success. By adding actions to your components you add an interactive element that keeps the user engaged. For example, in a list component you can press on an item in the list, or swipe left or right to delete/update or go to another jig.
Actions that can be added to components are configured as part of the component YAML and are available by invoking intellisense. Here is a list of actions to use with components:

- `onChange`
- `onDelete`
- `onSuccess`
- `onPress`
- `onFinish`
- `swipeable` &#x20;

:::CodeblockTabs
YAML

```yaml
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.companyName
    subtitle: =@ctx.current.item.firstName & ' ' & @ctx.current.item.lastName
    description: =@ctx.current.item.jobTitle
# The list-item action that defines what to do when swiping left or right on the item    
    leftElement: 
      element: avatar
      text: =$substring(@ctx.current.item.firstName, 0, 1) & $substring(@ctx.current.item.lastName, 0, 1)
      type: action.go-to
      options:
        linkTo: view-contact
        parameters:
          contact: =@ctx.current.item
# The list-item action that defines what to do when swiping left on the item
    swipeable:
      left:
# Add first icon with action when swiping left to delete the list-item     
        - label: DELETE
          icon: delete-2
          color: negative
# The action that defines what to do when pressing on the delete icon after swiping left       
          onPress: 
            type: action.execute-entity
            options:
              provider: DATA_PROVIDER_DYNAMIC
              entity: default/contacts
              method: delete
              data:
                id: =@ctx.current.item.id
# Add a second icon with action when swiping left to edit the list-item                 
        - label: EDIT
          icon: edit-pdf
          color: primary
# The action that defines what to do when pressing on the edit icon after swiping left                 
          onPress: 
            type: action.go-to
            options:
              linkTo: edit-contact
              parameters:
                contact: =@ctx.current.item
```
:::

## Component properties used for layout (columns, rows, and sections)

| **Component/Property** | **Description**                                                                                                                                                                                                                                             |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| entity > section       | Create relevant display [sections]() for the information to be functional yet elegant and neatly organized.                                                                                                                                                 |
| enitiy > enitity-field | [Entity-fields]() are used for display purposes only, such as displaying text, numbers, dates, and currency from a datasource. Entity-fields are available in default jigs and can be nested under field-row and/or section components if required.         |
| entity > field-row     | The [field-row]() component contains other components and displays them on the same row. This component ensures that items are placed next to each other instead of underneath each other. By default all components are automatically placed in a new row. |
| leftElement            | The `leftElement` property is used to place visual elements on the left-hand side in a component, such as an icon, image, text or button.                                                                                                                   |
| rightElement           | The `rightElement` property is used to place visual elements on the right-hand side in a component, such as an icon, image, text or button.                                                                                                                 |
| leftIcon               | The `leftIcon` property is used to place an icon on the left-hand side of a component.                                                                                                                                                                      |
| rightIcon              | The `rightIcon` property is used to place an icon on the right-hand side of a component.                                                                                                                                                                    |

## &#x20;Component templates

See [Component Templates](<./Components _controls_/Component Templates.md>) for steps on how to add components from a preconfigured set of templates.&#x20;

## Examples and code snippets

In the example tab, you can see code examples for each [component]().&#x20;

