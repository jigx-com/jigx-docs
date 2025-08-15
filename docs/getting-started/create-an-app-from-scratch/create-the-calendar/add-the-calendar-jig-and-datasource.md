# Add the calendar jig and datasource

## Add the calendar jig and datasource

## Overview

In this section, you will learn how to add a second jig file to the Hello Jigx project and add the calendar jig next to the map jig on the [home hub](../../../building-apps-with-jigx/ui/home-hub/home-hub.md). You create a data source file in the datasource folder containing the calendar details that provide the data for the week, events, meeting subjects, dates, and times.

:::hint{type="success"} See [Jigx Concepts](<../../../Understanding the basics/Jigx Concepts.md>) to learn what jigs, widgets, and the Home Hub are. :::

### Steps

#### Add the calendar-data.jigx data source file

1. You first need to add data that the calendar jig can read from. For this step, you create a `Static Datasource` in the datasource folder of the project, which is automatically synced to the Jigx Cloud. Likewise, data updated on the Jigx Cloud automatically syncs to the device. **Right-click** on the `datasources` node in Explorer and select **New file**.
2. Name the file **calendar-data**. Jigx automatically adds the **.jigx** extension to your file. The Jigx auto-complete popup displays the data source options. Select **Static datasource** from the list.
3. Under the data node, you need to provide the details for the events in the calendar. The following fields are available for use with each event entry, you can add your own event entries or use the code example below.

:::CodeblockTabs YAML

```yaml
type: datasource.static
options:
  data:
    - id: 1
      eventEnd: 2 
      eventStart: 1 
      location: Redmond, WA 
      people:
        - avatarUrl: https://randomuser.me/api/portraits/men/1.jpg   
          fullName: Tim Cook 
      tags:
        - color: color2 
          title: Negotiation 
      title: Negotiation with Company A
```

:::

4\. Once you have added the fields your calendar-data.jigx file should resemble the code below.

:::CodeblockTabs calendar-data.jigx

```yaml
# A global static datasource that allows easy access and reusability to the data across various jigs and components
type: datasource.static
options:
  data:
    - id: 1
      eventEnd: 2 
      eventStart: 1 
      location: Redmond, WA 
      people:
        - avatarUrl: https://randomuser.me/api/portraits/men/1.jpg   
          fullName: Tim Cook 
      tags:
        - color: color2 
          title: Negotiation 
      title: Negotiation with Company A
    - id: 2
      eventEnd: 4
      eventStart: 2  
      location: Palo Alto, CA
      people:
        - avatarUrl: https://randomuser.me/api/portraits/men/49.jpg
          fullName: Michael Tate
      tags:
        - color: color5
          title: Qualification
      title: Demo for Company B
    - id: 3
      eventEnd: 25
      eventStart: 24
      location: Menlo Park, CA
      people:
        - avatarUrl: https://randomuser.me/api/portraits/men/90.jpg
          fullName: Michael Tong
      tags:
        - color: color6
          title: Verbal
      title: Sign contract  
```

:::

#### Add a calendar jig file

1. Open the Hello-Jigx solution in the Jigx Builder in VS Code,\*\* right-click\*\* on the jigs node in Explorer, and select **New file**.
2. Name the file **calendar**.
3. The file opens and shows the Jigx's auto-complete popup listing the five jig types. For this solution, we will be using the **Calendar** jig to create the UI for displaying data in a calendar format. Click on **Calendar** to open the skeleton YAML created by the Jigx Builder.
4. On the line under `type:`, type `icon:`. To select an icon from the predefined list start typing the first two letters of the name of the icon, in this case \*ca, \*the list of icons starts to populate as you type. Select **calendar-3** from the list. This icon displays on the widget on the Home Hub of the Jigx App.
5. Delete the `header`, `onFocus` and `datasources` section. You created the calendar-data.jigx datasource file in the step above, now you can reference the data from the jig file by using an expression. At the data node add `calenar-data` so that it resembles `data: =@ctx.datasources.calendar-data`. With expressions, you can structure data before binding them to the UI components.

:::hint{type="info"} Expressions are JSONata language-based. Learn more about :Link\[JSONata]{href="https://jsonata.org/" newTab="true" hasDisabledNofollow="false"} and try out your expressions in their :Link\[JSONata Exerciser]{href="https://try.jsonata.org/" newTab="true" hasDisabledNofollow="false"}. The root element of Expressions in .jigx files always starts with "@ctx" vs. "$$." in JSONata Exerciser (e.g. @ctx.data vs.$$.data). Jigx supports shorthand $ expressions for JSONata. :::

6\. The `component.event` type is used to display events related to the data records. Use **(ctrl+space)** next to each field to select the value you want returned.

7\. To display the date in UTC format we use a JSONata expression to convert the date from milliseconds to UTC for both the start and end date. Add the following expression under `from:` for the start date.

`from: =$fromMillis($toMillis($now()) + @ctx.current.item.eventStart * 3600000)`

For the end date under `to:` add the following expression:

`to: =$fromMillis($toMillis($now()) + @ctx.current.item.eventEnd * 3600000)`

For `title`, `location`, `people` and `tags` use **(ctrl+space)** after the `=@ctx.current.item`. to select the value available from the datasource.

:::CodeblockTabs YAML

```yaml
options:
    title: =@ctx.current.item.title
    # Use a jsonata expression to get the date in milliseconds and then convert it to UCT for the start time 
    from: =$fromMillis($toMillis($now()) + @ctx.current.item.eventStart * 3600000)
    # Use a jsonata expression to get the date in milliseconds and then convert it to UCT for the end time
    to: =$fromMillis($toMillis($now()) + @ctx.current.item.eventEnd * 3600000)
    location: =@ctx.current.item.location
    people: =@ctx.current.item.people
    tags: =@ctx.current.item.tags
```

:::

8\. Your calendar.jigx file should resemble the code below.

:::hint{type="info"} The Jigx Builder YAML editor includes **code completion by simultaneously pressing the control and spacebar (ctrl+space)** buttons. Only valid options in the current cursor context are displayed in the code popup. :::

:::CodeblockTabs calendar.jigx

```yaml
# The system name that uniquely identifies the jig
title: Calendar
# The jig type used to display a calendar with the current date
type: jig.calendar
# icon that displays on the widget on the home hub
icon: calendar-3

# The expression that structures the data from the datasource before binding it to the jig. Expressions are JSONata based
data: =@ctx.datasources.calendar-data

item:
  type: component.event
  options:
    title: =@ctx.current.item.title
    # Use a jsonata expression to get the date in milliseconds and then convert it to UCT for the start time 
    from: =$fromMillis($toMillis($now()) + @ctx.current.item.eventStart * 3600000)
    # Use a jsonata expression to get the date in milliseconds and then convert it to UCT for the end time
    to: =$fromMillis($toMillis($now()) + @ctx.current.item.eventEnd * 3600000)
    location: =@ctx.current.item.location
    people: =@ctx.current.item.people
    tags: =@ctx.current.item.tags
```

:::

#### Add the calendar jigId in the index.jigx file

1. Click on the `index.jigx` file to add the calendar jig menu item to appear on the Home Hub screen next to map. Under the `tabs:` section **add** the following: `jigId: calendar`, `jigId: calendar`, `icon: calendar` and **save** the project.
2. Your index.jigx file should resemble the code below.

:::CodeblockTabs index.jigx

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
```

:::
