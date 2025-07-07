# Adding the Map Jig

# Overview

In this section, there are two files to edit, namely, `index.jigx` and `myfirstjig.jigx`. In the `index.jigx` file, you configure the bottom navigation tab to display the `myfirstjig.jigx` on the Jigx mobile app [Home Hub](<./../../../Building Apps with Jigx/UI/Home Hub.md>) screen. In the myfirstjig jigx file, you will specify the default [type]() of jig, assign an icon for the jig, and provide a [static datasource]() that provides the location on the map.

:::hint{type="success"}
See [Jigx Concepts](<./../../../Understanding the basics/Jigx Concepts.md>) to learn what jigs are.
:::

## Steps

:::hint{type="info"}
The Jigx Builder YAML editor includes code completion by simultaneously pressing the control and spacebar** (ctrl+space)** buttons. Only valid options in the current cursor context are displayed in the code popup.
:::

### Edit the index.jigx file

1. Click on the `index.jigx` file. This file is the menu structure of the app. In the `index.jigx` file you select the size of the widget that will appear on the Jigx mobile app [Home Hub](<./../../../Building Apps with Jigx/UI/Home Hub.md>) screen. The size of the widget displays as `1x1`. To see the available widget sizes, place the cursor in front of the `1x1` and press **ctrl+space**. Select the size `2x2`.
2. **Save** the project.
3. Your index.jigx file should resemble the code below.

:::CodeblockTabs
index.jigx

```yaml
# The system name that uniquely identifies the solution.
name: hello-jigx
# The friendly name of the solution.
title: Hello-Jigx
# The built-in category selected for this solution.
category: business
# The widgets that act as top-level navigation elements
# for jigs.
widgets:
# choose size of the widget on the home hub.
  - size: "2x2" 
    jigId: myfirstjig
```
:::

### Add the map to the jig

1. In Explorer expand the **jigs** folder and right-click on `myfirstjig.jigx` file and rename the file to map.jigx. Click to open the file, the Jigx auto-complete popup listing the five jig types displays. For this solution, we will be using the **default** jig to create the UI for displaying data. Click on **Default** to open the skeleton YAML created by the Jigx Builder.
2. Add ***Location with address*** as the `title` for your jig. The title appears under the widget on the Home Hub. Add a description for the jig, such as map with a marker.
3. On the line under `type:`, type `icon:`. To select an icon from the predefined list start typing the first two letters of the name of the icon, in this case *lo,* the list of icons starts to populate as you type. Select `location` from the list. This icon displays on the widget on the Home Hub.
4. Delete the `header`, and `onFocus` section, you will add a header later in the [Combine the solution's elements](<./../Combine the solution_s elements.md>) section.
5. The map jig needs a `datasource:` defined that provides the location details. You will use a [static datasource]() in this step. The static dataset is created directly inside the jig file of the Jigx solution, and there is no need to specify any database connections or set up any tables. The amount of records that can be created for the static data is unlimited and is used to bind data to the UI components.
6. Replace `mydata:` with `address:` press **ctrl+space **(Intellisense) and select `Static Datasource`.
7. Define the location details for the street, city and country under the
   `data:`
   tag. You can remove `id:1`. Add your own location or use the following as an example:
8. The controls displayed on the jig are defined under the `children:` node on a default jig. The output control is placed on the location component to display a map/location inside the jig. Under the `children:` node press **(ctrl+space)** and select **Location** from the list.
9. For the output control to display the map with the location you will use the address from the datasource using an [expression](<./../../../Building Apps with Jigx/Logic/Expressions.md>) to return the street, city and country to the location component. Next to `options:` press **(ctrl+space)** and select **address** from the list.
   To add the expression next to the `address:` line press **(ctrl+space)** and select **=@ctx** from the list. The root element of expressions in .jigx files always starts with "@ctx" vs. "$." in JSONata Exerciser (e.g. @ctx.data vs. $.data). Add the following to your expression:       `address: =@ctx.datasources.address.street & ',' & @ctx.datasources.address.city & ',' & @ctx.datasources.address.country`
10. To ensure that the location marker can be seen on the map add a `zoomLevel: 9` under the address line.
11. **Save** the project.
12. Your map.jigx file should resemble the code below.

:::CodeblockTabs
map.jigx

```yaml
# The system name that uniquely identifies the jig
title: Location with address
description: map with a marker
# The jig type used to display data
type: jig.default
icon: location

# The type of datasource used to return data in the jig
datasources:
  address: 
  # The static dataset is created directly inside the jig file
    type: datasource.static
    options:
      data:
        - street: 768 5th Ave
          city: New York
          country: US
# The control used by the jig to display a location          
children:
# The component location is an interactive map displaying the location using the address
  - type: component.location
    options:
      viewPoint:
        address: =@ctx.datasources.address.street & ',' & @ctx.datasources.address.city & ',' & @ctx.datasources.address.country
        zoomLevel: 9
```
:::

### Update the jigId in the index.jigx file&#x20;

1. Click on the `index.jigx`.
2. Change the `JigId` from myfirstjig to map.
3. Your index.jigx file should resemble to the code below.

:::CodeblockTabs
index.jigx

```yaml
# The system name that uniquely identifies the solution.
name: hello-jigx-solution
# The friendly name of the solution.
title: Hello-Jigx Solution
# The built-in category selected for this solution.
category: business
# The tab that act as top-level navigation elements for jigs.
tabs:
  home:
    jigId: map   
    icon: location
```
:::

## See Also

- [Jigx overview]()
- [Jigx Concepts]()

