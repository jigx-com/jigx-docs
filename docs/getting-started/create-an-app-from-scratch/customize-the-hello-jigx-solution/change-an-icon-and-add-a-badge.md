# Change an icon and add a badge

## Change an icon and add a badge

## Overview

You can easily customize widgets on the Home Hub by changing their icons and adding additional components such as badges to the widgets. In this section, you learn to change the calendar icon and add a badge [using an expression](../../../building-apps-with-jigx/logic/expressions.md) on the calendar jig to show the number of calendar events for the week.

{% hint style="info" %}
For a view of the icons in a list see the _Types - List - List with all icons_ in the _jigx-samples solution_ available in :Link\[https://manage.jigx.com/quickstartQuick]{href="https://manage.jigx.com/quickstart" newTab="true" hasDisabledNofollow="false"} start.
{% endhint %}

::::VerticalSplit{layout="middle"} :::VerticalSplitItem ::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/jTIkWACM58-HE8chrcKfe\_widgetloclight.PNG" size="62" caption="Solution with Calendar -3 icon" position="center" alt="Solution with Calendar -3 icon" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/jTIkWACM58-HE8chrcKfe\_widgetloclight.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"} :::

:::VerticalSplitItem ::Image\[]{alt="Solution with calendar badge" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/TjmDI17-njZImLC9Ix51n\_calenderbadgel.PNG" size="62" caption="Solution with calendar badge" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/TjmDI17-njZImLC9Ix51n\_calenderbadgel.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"} ::: ::::

#### Steps

#### Change an widget icon

1. Open the Hello-Jigx solution in Jigx Builder in VS Code, click on the calendar.jigx file.
2. Replace `icon: calendar-3` with `icon: calendar`.

#### Add a badge to the calendar widget

1. Under icon add a new line for the badge code that shows the number of calendar events for the week. Add `badge:` Then use the `=$count(@ctx.datasources.calendar-data.id)` [expression](../../../building-apps-with-jigx/logic/expressions.md) to count the events in the calendar and show the number in the badge on the Home Hub.

{% hint style="info" %}
Expressions are JSONata language-based. Learn more about [https://jsonata.org/](https://jsonata.org/)JSONata and try out your expressions in their [https://try.jsonata.org/](https://try.jsonata.org/)JSONata Exerciser. The root element of Expressions in .jigx files always starts with "@ctx" vs. "$$." in JSONata Exerciser (e.g. @ctx.data vs.$$.data). Jigx supports shorthand $ expressions for JSONata.
{% endhint %}

{% code title="calendar.jigx" %}
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
{% endcode %}

4\. **Save** and **publish** the Hello-Jigx solution. 5. **Run** the Hello-Jigx solution on your mobile device to see the change to the calendar icon and see the badge displaying 3 events for the week on the Home Hub.
