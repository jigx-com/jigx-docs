---
title: Edit the index.jigx file
slug: fK6K-edit-the-indexjigx-file
createdAt: Tue Apr 11 2023 17:26:11 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Feb 21 2025 14:25:29 GMT+0000 (Coordinated Universal Time)
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

# Edit the index file

The index.jigx file includes links to the jigs you want accessible as top-level navigation elements. In the previous steps you created a composite jig, and a static datasource, now you will add these to the `index.jigx` file to appear on the Home Hub, and remove the new customer and the list customer widgets which are now joined in the composite jig. In this step, the `jigId` is used to reference the composite jig. The order of the `jigId` determines the order in which the tabs appear on the Home Hub. You add the composite jig first in this solution as you want it to be the first bottom tab to display.

## Steps

### Add jigs to the index.jigx file

1. Click on the `index.jigx` file. Under `tabs:` **remove** the `jigId: new-customer`, and the `jigId: list-customer`. Now **add** the `jigId: composite`.
2. Your index.jigx file should resemble the code below.

{% code title="index.jigx" %}
```yaml
# The system name that uniquely identifies the solution
name: hello-jigx-solution
# The friendly name of the solution
title: Hello-Jigx Solution
# The built-in category selected for this solution
category: business
#The tabss that act as bottom-level navigation elements for jigs
tabs:
  customer: # The first tab of the app.
    jigId: composite
    icon: people
  home: 
    jigId: map
    icon: location
  calendar:
    jigId: calendar
    icon: calendar
```
{% endcode %}
