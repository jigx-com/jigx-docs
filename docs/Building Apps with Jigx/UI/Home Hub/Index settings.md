---
title: Index settings
slug: t7tB-index-settings
description: Learn about the essential solution settings stored in the index.jigx file for a jig. This includes crucial information such as the solution's name, title, category, and description. Explore how properties like Widgets, home, and stories contribute to the 
createdAt: Tue Apr 04 2023 12:00:55 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Apr 29 2025 11:11:26 GMT+0000 (Coordinated Universal Time)
---

In the `index.jigx` file, you set solution settings, including the primary information about the solution, the [Home Hub](<./../Home Hub.md>) set up, and properties reusable throughout the solution.

## Name, title, category, description

- **Name** - Your internal solution name.
- **Title** - This name will be displayed in your app and <a href="https://manage.jigx.com" target="_blank">management</a>.
- **Category** -  A predefined list of solution categories to choose from.
- **Description** - A description you provide for your solution.

:::CodeblockTabs
index.jigx

```yaml
title: jigx-samples
name: jigx-samples
category: personal
description: A solution displaying all features and functions available in Jigx.
```
:::

## Tabs

- Tabs are properties used to build your navigation bar that displays at the bottom of the Home Hub.
- You can configure multiple tabs. The first four tabs are displayed in the Home Hub bottom navigation. Additional tabs appear when the *More* (ellipsis) button is tapped.
- Each tab is associated with a jig that is displayed when pressed. The first tab by default displays when the app is opened.
- Setting the [grid]() jig as the first tab's jig creates a visually appealing and easy-to-navigate home screen.

| **Core Structure** |                                                                           |
| ------------------ | -------------------------------------------------------------------------------- |
| `tabs`             | The top level property under which the various tabs are configured.              |
| `icon`             | The icon to be shown on the navigation bar for the tab, for example a home icon. |
| `jigId`            | The name/ unique identifier of the jig that will open when the tab is pressed.   |

| **Other options** |                                                                                                                                                                                                            |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `badge`           | Optional property - Enhance your tab with a customizable badge for instance showing the number of events this week or the number of new orders. Add the `badge` property to the tabs section with an expression. |
| `label`           | Give the tab a title. The title displays under the icon in the navigation bar.                                                                                                                                   |
| `when`            | The condition when the tab will be displayed or hidden (optional). Use an [expression](./../../Logic/Expressions.md) that evaluates to a boolean.                                                                |

:::CodeblockTabs
index.jigx

```yaml
name: jigx-samples
title: Jigx Samples
category: business
      
# Configure one or more tabs, shown in the navigation bar at the bottom of the app.
tabs:
  # Give each tab a name. First tab.
  home:
    # Optional - provide a label to display under the tab icon.
    label: home 
    # This jig is the home screen and is visible when the app opens.    
    jigId: grid-home
    # Select an icon of your choice.    
    icon: home-apps-logo
  # Second tab.    
  Services:
  # Reference the jig that will open when the tab icon is pressed. 
    jigId: grid-components
    icon: cleaning-bucket-bubble
  # Third tab    
  Bookings:
    jigId: grid-booking
    icon: calendar
    # Configure a badge showing a dot or a numbered dot on the top right of the icon.
    # Use a expression or number to set the badge.    
    badge: =$count(@ctx.datasources.guests)
  # Fourth tab    
  Reviews: 
    jigId: feedback
    icon: online-class-student
```
:::

## OnLoad, OnFocus, OnRefresh

These properties allow you to configure [Actions]() executed in various scenarios.

- **OnLoad** - when the solution loads for the first time the configured actions execute. This is recommended for best performance when working with data, sync the data when the solution loads and ensures the data is available from the beginning and throughout the rest of the solution.
- **OnFocus** - when the Home Hub receives focus the configured actions execute.
- **OnRefresh** - when pulling down on the Home Hub the action configured for `onRefresh` executes.

:::CodeblockTabs
index.jigx (onLoad)

```yaml
onLoad: 
  type: action.set-state
  options:
    state: =@ctx.solution.state.loginTimestamp
    value: =$now()
```

index.jigx (onFocus)

```yaml
onFocus: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_DYNAMIC
    entities:
      - entity: default/test
```

index.jigx (onRefresh)

```yaml
onRefresh: 
  type: action.execute-entity
  options:
    provider: DATA_PROVIDER_DYNAMIC
    entity: default/test
    method: update
    goBack: previous
    data:
      id: =@ctx.datasources.test.id
      action: 'Execute-entity onRefresh'
```
:::

## Global Expressions

Use the `expressions` property to set expressions that are reusable throughout the solution in various jigs.

:::CodeblockTabs
index.jigx

```yaml
expressions:
  user: =@ctx.user.displayName
  timezone: =@ctx.system.timezone.name
  altitude: =@ctx.system.geolocation.coords.altitude
```

jig.jigx

```yaml
title: Shared expressions example
type: jig.default

children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Current User
            value: =@ctx.expressions.user
        - type: component.entity-field
          options:
            label: Current Timezone
            value: =@ctx.expressions.timezone
        - type: component.entity-field
          options:
            label: Current Altitude
            value: =@ctx.expressions.altitude
```
:::

For more details and examples refer to the *Shared Expressions* section in [Expressions](./../../Logic/Expressions.md).

## Dependencies

In the `dependencies` property, you can define the mobile app build version compatible with the YAML configuration.

:::::VerticalSplit{layout="middle"}
::::VerticalSplitItem
If the current mobile app build version does not meet the criteria, the *Out of date* screen will appear, with a message that an update is required. Tapping the *Update* button redirects you to your app settings to update the version of the app.

:::CodeblockTabs
index.jigx

```yaml
dependencies:
  mobileApp: '>1.0.0'
```
:::


::::

:::VerticalSplitItem
::Image[]{alt="Out of date app screen" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/hWcGWw7RfFME2LiyAQ0Mw_img8725iphone13blueportrait.png" size="80" caption="Out of date app screen" position="center"}
:::
:::::

## See Also

- [Home Hub](<./../Home Hub.md>)



