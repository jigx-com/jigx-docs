---
title: Change an icon and add a badge
slug: 9vsQ-change-an-icon-and-add-a-badge
description: Learn how to customize widgets on HomeHub by changing icons and adding badges with this step-by-step guide. From changing the calendar icon to displaying the number of events for the week, this document provides detailed instructions. It even includes a c
createdAt: Mon Apr 17 2023 07:32:10 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Nov 01 2023 06:56:50 GMT+0000 (Coordinated Universal Time)
---

# Overview

You can easily customize widgets on the Home Hub by changing their icons and adding additional components such as badges to the widgets. In this section, you learn to change the calendar icon and add a badge [using an expression](<./../../../Building Apps with Jigx/Logic/Expressions.md>) on the calendar jig to show the number of calendar events for the week.

:::hint{type="info"}
For a view of the icons in a list see the *Types - List - List with all icons* in the *jigx-samples solution* available in <a href="https://manage.jigx.com/quickstart" target="_blank">Quick start</a>.
:::

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/jTIkWACM58-HE8chrcKfe_widgetloclight.PNG" size="62" caption="Solution with Calendar -3 icon" position="center" alt="Solution with Calendar -3 icon"}
:::

:::VerticalSplitItem
::Image[]{alt="Solution with calendar badge" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/TjmDI17-njZImLC9Ix51n_calenderbadgel.PNG" size="62"  caption="Solution with calendar badge"}
:::
::::

### Steps

### Change an widget icon

1. Open the Hello-Jigx solution in Jigx Builder in VS Code, click on the calendar.jigx file.
2. Replace `icon: calendar-3` with  `icon: calendar`.

### Add a badge to the calendar widget

1. Under icon add a new line for the badge code that shows the number of calendar events for the week. Add `badge:` Then use the `=$count(@ctx.datasources.calendar-data.id)` [expression](<./../../../Building Apps with Jigx/Logic/Expressions.md>) to count the events in the calendar and show the number in the badge on the Home Hub.

:::hint{type="info"}
Expressions are JSONata language-based. Learn more about <a href="https://jsonata.org/" target="_blank">JSONata</a> and try out your expressions in their <a href="https://try.jsonata.org/" target="_blank">JSONata Exerciser</a>. The root element of Expressions in .jigx files always starts with "@ctx" vs. "$$." in JSONata Exerciser (e.g. @ctx.data vs. $$.data). Jigx supports shorthand $ expressions for JSONata.
:::

:::CodeblockTabs
calendar.jigx

```yaml
# The system name that uniquely identifies the jig
title: Calendar
# The jig type used to display a calendar with the current date
type: jig.calendar
# icon that displays on the widget on the home hub
icon: calendar
# Add a badge to the calendar widget and use an expression to count the entries in the calendar by id
badge: =$count(@ctx.datasources.calendar-data.id)
# The expression that structures the data from the datasource before binding it to the jig. Expressions are JSONata based
data: =@ctx.datasources.calendar-data
item:
  options:
    title: =@ctx.current.item.title
    from:
      format:
        dateFormat: lll
      text: =$fromMillis($toMillis($now()) + @ctx.current.item.eventStart * 3600000)
    location: =@ctx.current.item.location
    people: =@ctx.current.item.people
    tags: =@ctx.current.item.tags
    to:
      format:
        dateFormat: lll
      text: =$fromMillis($toMillis($now()) + @ctx.current.item.eventEnd * 3600000)
  type: component.event
```
:::

4\. **Save** and **publish** the Hello-Jigx solution.
5\. **Run** the Hello-Jigx solution on your mobile device to see the change to the calendar icon and see the badge displaying 3 events for the week on the Home Hub.

