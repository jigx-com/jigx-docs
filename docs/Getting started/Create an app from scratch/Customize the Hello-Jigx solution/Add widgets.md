# Add widgets

# Overview

Widgets can be customized in many ways to reflect the styling and functionality you require.  Use the widget [image](#), [location](#), [chart](#), and other elements for customizations. In this section, you will learn how to change your map jig with an icon to a `widget.location`, and add a `widget.image` widget to the `composite.jigx` file.

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/SdU7Wdc0_3pP_9R5d8MEM_locationlight.PNG" size="52" caption="Hello Jigx solution with location icon" alt="Hello Jigx solution with location icon" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/SdU7Wdc0_3pP_9R5d8MEM_locationlight.PNG"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/_vYaNBAdPCrT5JaOx7r9X_widgetscustoml.PNG" size="52" caption="Widget location & image" alt="Widget location & " signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/_vYaNBAdPCrT5JaOx7r9X_widgetscustoml.PNG"}
:::
::::

### Steps

### Add a widget to a jig

1. Open the Hello-Jigx solution in Jigx Builder in VS Code, and click on the map.jigx file.
2. Delete the `icon: location` entry.
3. Add the `widget.location` code below. For the address you use [expressions](<./../../../Building Apps with Jigx/Logic/Expressions.md>) to call the city New York from the static datasource.

:::hint{type="info"}
Expressions are JSONata language-based. Learn more about <a href="https://jsonata.org/" target="_blank">JSONata</a> and try out your expressions in their <a href="https://try.jsonata.org/" target="_blank">JSONata Exerciser</a>. The root element of Expressions in .jigx files always starts with "@ctx" vs. "$$." in JSONata Exerciser (e.g. @ctx.data vs. $$.data). Jigx supports shorthand $ expressions for JSONata.
:::

:::CodeblockTabs
map.jigx

```yaml
# The system name that uniquely identifies the jig
title: Location with address
# The jig type used to display data
type: jig.default

isCollapsible: true
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
# The control used by the jig          
children:
  - type: component.location
    options:
      viewPoint:
        address: =@ctx.datasources.address.street & ',' & @ctx.datasources.address.city & ',' & @ctx.datasources.address.country
        zoomLevel: 9
# The widget that displays on the home hub.    
widgets: 
  map-location: 
    type: widget.location
    options: 
      viewPoint: 
       address: =@ctx.datasources.address.city        
```
:::

4\. Open the `composite.jigx` file and copy the code below. Note the new widgets section using `widget.image` showing a source uri for the image you want displayed.

:::CodeblockTabs
composite.jigx

```yaml
# The system name that uniquely identifies the jig
title: Customers
description: Shows list and new customers together
# The jig type used to join multiple jigs together
type: jig.composite

widgets:
  image:
    type: widget.image
    options:
      source: 
        uri: https://cdn2.webdamdb.com/v1_1280_6enPaxIBt9M3.jpg?1554490336
        
# A container for specifying jig headers such as images, videos or location
header:
  type: component.jig-header
  options:
    children:
      type: component.image
      options:
        title: Customers
        source:
          uri: https://cdn2.webdamdb.com/v1_1280_6enPaxIBt9M3.jpg?1554490336
    height: small    
  
# Specifiy the jigs to combine by listing the jigIds for each jig
children:
  - jigId: new-customer
  - jigId: list-customer
```
:::

5\. **Save** and **publish** the Hello-Jigx solution.
6\. **Run** the Hello-Jigx solution on your mobile device to see the change to the map widget on the  Home Hub.
