---
title: Add the customer composite jig
slug: M7Ir-add-the-customer-composite-jig
createdAt: Tue Apr 11 2023 17:23:45 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Nov 01 2023 06:01:13 GMT+0000 (Coordinated Universal Time)
---

# Add the customer composite jig

In this section, you learn how to join jigs to create a single jig using the `jig.composite` type, this is useful in our solution as you want to capture a new customer and see the customer added to the list directly below the form, you also add an image header to the composite jig.

## Steps

### Create the composite jig

1. Open the Hello-Jigx solution in Jigx Builder in VS Code, right-click on the jigs node in Explorer, and select New file.
2. Name the file **composite**. The file opens and shows the Jigx's auto-complete popup listing the five types of jigs you can select. Click on Composite to open the skeleton YAML created by the Jigx Builder.
3. Give the jig a title called Customers and provide a description like _Customer form and list_. Add `icon: person` under the description line. This icon displays on the widget on the Home Hub.
4. For this jig you can delete the `onFocus` node.
5. Under the `header` node you can leave it as is or add your own image uri. The `jig-header` component can be used in any type of jig. It serves as a container for specifying headers, such as images. Change the `height` value to small and add a `title: Customers` after options. Here is an example of the header code with an image.

{% code title="YAML" %}
```yaml
header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        title: Customers
        source:
          uri: https://cdn2.webdamdb.com/v1_1280_6enPaxIBt9M3.jpg?1554490336
```
{% endcode %}

### Add the jigIds

1. Next to the `jigIds` add `new-customer` and `list- customer`. The order of the children's `jigIds` determines the display order in the app.
2. You can remove the `inputs:` `recordid: =@ctx.jig.inputs.parameter`
3. Your composite.jigx file should resemble the code below.&#x20;

{% code title="composite.jigx" %}
```yaml
# The system name that uniquely identifies the jig
title: Customers
description: New customer form and list
# The jig type used to join multiple jigs together
type: jig.composite
# icon that displays on the widget on the home hub
icon: person

# A container for specifying jig headers such as images, videos or location
header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        title: Customers
        source:
          uri: https://cdn2.webdamdb.com/v1_1280_6enPaxIBt9M3.jpg?1554490336
      
# Specifiy the jigs to combine by listing the jigIds for each jig.  
children:
  - jigId: new-customer
  - jigId: list-customer
```
{% endcode %}
