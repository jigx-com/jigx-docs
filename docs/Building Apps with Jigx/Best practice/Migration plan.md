---
title: Migration plan
slug: migration-plan
createdAt: Tue Dec 03 2024 11:46:40 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Feb 24 2025 09:27:39 GMT+0000 (Coordinated Universal Time)
---

[Release 2025.1]() - introduces several updates to the index.jigx file, widgets, and location. Some properties have been deprecated, and a new grid jig type and a grid-item component have been added. These updates provide more versatility in app design, enhance layout options, and optimize screen space usage. To take advantage of these new features in your existing solutions, follow the guidance below to update your implementation.

### Existing solutions

Existing solutions will continue to function in the mobile app as before.
The navigation menu at the bottom of the app will now display as a bar and includes the profile icon that has been moved from the top right-hand corner into the navigation bar. In Jigx Builder, deprecated or changed YAML properties are highlighted with a red squiggle. Before making changes, carefully review the **affected areas** and the **migration steps** outlined below. Plan your updates thoroughly, as multiple files may be impacted and require updates or code relocation to new files.

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-OvOQIgZAvCxcVq4vXFSp6-20241206-142101.png" size="60" position="center" caption="Existing solutions before update" alt="Existing solutions before updatesting Solutions"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-2Pkaf7KdAuYIlsSwwgqHa-20241206-142117.png" size="60" position="center" caption="Existing solutions after update" alt="Existing solutions after update"}
:::
::::

### New solutions

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
New solutions now offer greater versatility.

1. The updated index.jigx with `tabs`, and new [jig.grid]()  functionality let you define the app layout precisely from the start, ensuring easy navigation and better utilization of space on the Home Hub.
2. The `location` now supports custom markers, state-based markers, user location display, radius, and location tracking.


:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-hjybhSon5vYuP5IXwXQrR-20241206-142830.png" size="60" position="center" caption="New solution layout " alt="New solution layout"}
:::
::::

## Affected areas&#x20;

The table below outlines the areas impacted by the introduction of bottom tab navigation, and the deprecation of the `stories`, `home`, and `widgets` properties in the index.jigx file.

| **Old**                                                      | **New**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `widgets` property in index.jigx file.                       | `tabs` property in index.jigx file. See [tabs](<./../UI/Home Hub.md>)  for more information.                                                                                                                                                                                                                                                                                                                                                                                                 |
| `widgets` property in jig files.                             | `widgets` in jig files now require a `widgetId` (Widget Name) property and remove the size, e.g. `1x1`.                                                                                                                                                                                                                                                                                                                                                                                      |
| `stories` property in index.jigx&#xA;`story-group` component | Deprecated.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `home` property in index.jigx file.                          | Reference the jig previously referenced in `home` as the custom Home Hub now in the `tabs` property. &#xA;The first jig configured under the `tabs` property becomes is the first screen displayed when the app is opened.                                                                                                                                                                                                                                                                   |
| N/A                                                          | `jig-grid` - a new jig type used to configure jigs and components in a grid layout.  See [jig.grid]() for more information.                                                                                                                                                                                                                                                                                                                                                                  |
| `component.widgets`                                          | `grid` and `grid-item` component - a new component used to add a grid layout in a jig. This allows you to combine a grid layout with other components. See [grid]() and [grid-item]() for more information.                                                                                                                                                                                                                                                                                  |
| User profile                                                 | User profile has moved to the bottom tabs navigation. The user avatar will always show as the last tab in the navigation bar.                                                                                                                                                                                                                                                                                                                                                                |
| Solutions (Home)                                             | Solution switching has moved into the user profile screen. A *switch* button opens the solution list for selection.<br />::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-NGrWw9SMNv_vpn6k1f6rE-20250130-102419.png" size="44" position="center" caption="Switch solutions" alt="Switch solutions"} |
| `component.location`                                         | The location component's YAML structure now supports custom markers, state-based markers, user location display, and location tracking.                                                                                                                                                                                                                                                                                                                                                      |

## Migration steps

### index.jigx

1. Remove the `stories` property.
    - Delete the stories property and any associated jigs. Stories are deprecated and no longer displayed in the app.
    - To replicate this functionality, consider using the [video-player]() or [carousel]() components.
2. Replace the `widgets` property.
   - Replace the `widgets` property with a new `tabs` property.
   - Define the `tabs` you want to display in the bottom tab navigation.
     Note:
     - A maximum of four tabs can be rendered.
     - The last tab will display the user avatar, linking to the user profile (previously located in the top-right corner).
     - The first jig listed under the `tabs` property will become the initial screen shown when the app is opened, the Home Hub .
3. Configure the `tabs` property.
   - For each tab, specify the following required properties: `Tab Name`, `jigId`, and `icon`.
   - Optional properties include `badge` and `when`.
   - `Inputs` previously specified in the index.jigx file must now be defined within the corresponding jig or in the `grid-item`.
4. Remove the `home` property.
   - Reference the custom Home Hub `jigId` in the first `tabs` property to maintain the same functionality.
5. Unchanged properties.
   - All other properties, such as `expressions`, `onLoad`, `onRefresh`, and `scripts`, remain unchanged.

:::CodeblockTabs
old-index.jigx

```yaml
name: student-app
title: Student-app
category: analytics
# Stories have been deprecated.
stories:
  - story-group-video
  - story-group-image
# Home has been replaced with tabs, see new-index.jigx example.   
home:
  - instanceId: home-jig
    jigId: home-jig
# Widgets have been replaced with tabs and inputs must be specified in the jig iteself,
# or in the grid-item component.
widgets: 
  - size: 2x2
    jigId: student-courses
  - size: 1x1
    jigId: students-details
    inputs:
      name: =@ctx.user.displayName
      number: 350.66
      boolean: true
      array: [{name: John, age: 30}, {name: Melany, age: 35}, {name: Scott, age: 21}]
```

new-index.jigx

```yaml
name: student-app
title: Student-app
category: analytics

tabs:
  home: 
    jigId: home-jig
    icon: home-apps-logo
  course:
    jigId: student-courses
    icon: online-class-student
  details:
    jigId: student-details
    icon: people-man-1 
```
:::

### custom home-hub

To maintain the same functionality, reference the custom Home Hub `jigId` in the first `tabs` property. Alternatively, take this opportunity to design a new Home Hub by configuring a jig with both standard and custom components to be used in the `tabs` property.

:::CodeblockTabs
old-index.jigx

```yaml
name: Expo 
title: Expo
category: business

# home and instanceId needs to be removed in the new structure.
home:
  - instanceId: custom
    jigId: yoga-wellness
    
# Data is still synced in the index.jigx file.
onLoad: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_DYNAMIC
    entities:
      - default/events
```

new-index.jigx

```yaml
name: expo 
title: Expo
category: business

# Add tabs and reference the previous home jig as a tab,
# you can even call the tab home and give it a home icon.
tabs: 
  home: 
    jigId: yoga-wellness 
    icon: home 
    
# data is still synced inthe index.jigx file
onLoad: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_DYNAMIC
    entities:
      - default/events   
```
:::

### widgets in jigs

In jig files using the `component.widgets` property, the YAML structure must be updated. Replace the `size` (e.g., 2x2) with a `widgetId`. The size is now configured in the `grid-item` property.

:::CodeblockTabs
old-widget-property

```yaml
widgets:
# Replace 2x2 with a name for the widget that becomes the widgetId.
  2x2: 
    type: widget.avatar
    options:
      text: LS
      uri: https://i.pravatar.cc/150?img=68
      bottom:
        type: component.titles
        options:
          align: center
          title: Leo Siphron
          subtitle: React Web Developer
```

new-widget-property

```yaml
widgets:
# Specify a widgetId.
  dev-avatar: 
    type: widget.avatar
    options:
      text: LS
      uri: https://i.pravatar.cc/150?img=68
      bottom:
        type: component.titles
        options:
          align: center
          title: Leo Siphron
          subtitle: React Web Developer
```

grid-item

```yaml
children:
  - type: component.grid-item
    options:
# Specifiy the size of the widget    
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: jig-a
# The widgetId will automatically populate,
# if you have specified one in the jig's widget property.          
          widgetId: dev-avatar
```
:::

### location

Existing solution location components will continue to function as before, with one notable change: the default red markers will now appear as smaller black markers. To retain the red marker, configure the location marker `icon` to use the `end-marker` value. However, once a solution is republished, you must update the `component.location` YAML to ensure the location continues to function as expected.

Multiple enhancements were made to the `location` component which changed the YAML structure, these include:

- User's location display
- Follow a user location
- A new action, `action.open.map`, opens a modal, allowing you to select a map app on your device for navigation to an address.

:::CodeblockTabs
old-location-component

```yaml
children:
  # Basic location component with address.
  - type: component.location
    options:
      address: |
        =@ctx.datasources.address.street & ',' & 
        @ctx.datasources.address.city & ',' & 
        @ctx.datasources.address.country
      zoomLevel: 9

  # Basic address with latitude and longitude.
  - type: component.location
    options:
      address: |
        40.759412, 
        -73.912306 

  # Location component with paths.
  - type: component.location
    options:
      pathsData: =@ctx.datasources.coordinates
      isAnimationDisabled: true          

  # Location component with markers.
  - type: component.location
    options:
      markersData: |
        =@ctx.datasources.live_location.
        {"lat":$.latitude, 
        "lng":$.longitude}  
      zoomLevel: 12
      isAnimationDisabled: false                
```

new-location-component

```yaml
children:
  # Basic address.
  - type: component.location
    options:
      viewPoint:
        centerPosition: middle 
        address: 768 5th Ave, New York, US
        zoomLevel: 14 
      markers:
        data: =@ctx.datasources.address
        item:
          type: component.marker-item
          options:
            address: =@ctx.datasources.address[0].street
            children:
              type: component.icon
              options:
                color: negative
                icon: pin-1-map
                  
  # Basic address with latitude and longitude.
  - type: component.location
    options:
      viewPoint:
        centerPosition: middle
        latitude: =@ctx.datasources.appointments[0].latitude
        longitude: =@ctx.datasources.appointments[0].longitude
      markers:
        data: =@ctx.datasources.appointments
        item:
          type: component.marker-item
          options:
            latitude: =@ctx.current.item.latitude
            longitude: =@ctx.current.item.longitude
            children:
              type: component.icon
              options:
                color: negative
                icon: pin-1-map  
      
  # Multiple markers.         
  - type: component.location
    options: 
      viewPoint:
        centerPosition: middle
        address: =@ctx.datasources.address[1].street 
      markers:
        data: =@ctx.datasources.points
        
  # Location with paths.
  - type: component.location
    options:
      paths:
        data: =@ctx.datasources.points
      viewPoint:
        centerPosition: middle
        latitude: 40.759412
        longitude: -73.912306
        isAnimationEnabled: true
          
# A new action opens a modal, 
# allowing you to select a map app on your device for navigation to an address. 
actions:
  - children:
      - type: action.open-map
        options:
          icon: landmark-empire-state
          title: Empire State Building
          address: 20 W 34th St., New York, NY 10001, United States    
```

datasources

```yaml
datasources:
  # First datasource used in the basic address example.
  address: 
    type: datasource.static
    options:
      data:
        - id: 1
          street: 768 5th Ave
          city: New York
          country: US
        - id: 2
          street: 137 W 111th St
          city: New York
          country: US  
  # Second datasource used in location with paths example.
  points:
    type: datasource.static
    options:
      data:
        - lat: 40.759412
          lng: -73.912306
        - lat: 40.745368
          lng: -74.057189
  # Third datasource used in basic address - latitude and longitude.
  appointments:
    type: datasource.static
    options:
      data:
        - id: 1
          name: Empire State Building
          latitude: 40.748676182418976
          longitude: -73.98567513213604
          address: 20 W 34th St., New York, NY 10001, United States
          icon: home
        - id: 2
          name: Great Lawn Softball Field 6
          latitude: 40.782091612607864 
          longitude: -73.9655512166898
          address: 86th St Transverse, New York, NY 10024, United States
          icon: stadium-1-building 
  # Fourth datasource used in the old-location component with paths.
  coordinates:
      type: datasource.static
      options:
        data:
          - id: 1
            latitude: 40.769702
            longitude: -74.038241
          - id: 2
            latitude: 40.759412
            longitude: -73.912306
          - id: 3
            latitude: 40.803495
            longitude: -73.950694           
```
:::

