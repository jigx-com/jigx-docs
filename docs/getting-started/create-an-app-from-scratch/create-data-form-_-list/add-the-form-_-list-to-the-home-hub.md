---
title: Add the form & list to the Home Hub
slug: K6to-add-the-form-and-list-to-the-home-hub
createdAt: Wed Apr 12 2023 13:49:39 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Feb 21 2025 14:33:42 GMT+0000 (Coordinated Universal Time)
---

# Add the form & list to the Home Hub

## Overview

In this step, you will add the new customer form and the customer list widgets to the Home Hub of the Jigx mobile app.

## Steps

#### Add jigIds to index.jigx file

1. Click on the `index.jigx` file to add the new customer form and list jigs to appear on the Home Hub screen under the `home` and `calendar` tabs. The `jigId` is used to reference the form and list jig that will be displayed, and **save** the project.
2. Your index.jigx file should resemble the code below. :&#x20;

{% code title="index.jigx" %}
```yaml
# The system name that uniquely identifies the solution
name: hello-jigx-solution
# The friendly name of the solution
title: Hello-Jigx Solution
# The built-in category selected for this solution
category: business
#The widgets that act as top-level navigation elements for jigs
tabs:
  home:
    jigId: map
    icon: location
  calendar:
    jigId: calendar
    icon: calendar
  customer:
    jigId: new-customer
    icon: person
  list:
    jigId: list-customer 
    icon: list 
```
{% endcode %}
