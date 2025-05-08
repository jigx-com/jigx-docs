---
title: Home Hub
slug: 4FlX-home-experience
description: Jigx home hub functionality and components explained 
createdAt: Thu Jan 26 2023 10:34:22 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Apr 30 2025 10:13:03 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Having a good home screen is essential for any mobile app as it is the first screen that users see when they open the app. A home screen should provide users with quick access to the most important features of the app, while also being visually appealing and easy to navigate. It should be intuitive and provide users with a clear understanding of what the app does and how to use it.  Careful consideration should be given during the [design](<./../../Getting started/Planning your app/Home screen.md>) process. In Jigx the home screen is called the Home Hub and is accessed after signing into the app.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-w5fDciaaOqvoKxuVxeQJQ-20250430-101252.png" size="60" position="center" caption="Home screen" alt="Home screen"}


:::
::::

Jigx allows you to use various options when personalizing your Home Hub.&#x20;

The main elements used are:

1. Tabs in [Index settings](<./Home Hub/Index settings.md>)
2. [grid]() and [grid-item]()

:::ExpandableHeading
### tabs

- Create a landing page/ home screen by configuring the navigation tabs that show at the bottom of the app. You can configure a maximum of four tabs.
- Each tab is associated with a jig that is displayed when pressed. The first tab by default displays when the app is opened.
- Setting the [grid]() jig as the first tab's jig creates a visually appealing and easy-to-navigate home screen. 
:::

:::ExpandableHeading
### grid and grid-item

- The [grid]()  and [grid-item]() are available in 5 different `sizes`: 1x1, 2x2, 4x2, 2x4, and 4x4.
- The `jigId` property refers to the name/ unique identifier of the jig we are using.
- There is also an optional property `when` that allows the grid-item to be displayed/hidden in a particular situation based on the expression.
- Within the grid-item you can select to show [widgets](https://docs.jigx.com/examples/oVbi-widgets), an [image]() , and [Custom Components (Alpha)](<./Custom Components _Alpha_.md>).
- Add an `onPress` event to a grid-item to configure an action such as `open-url` without going to jig.
:::

For a code example see [Creating a Home Hub](<./Home Hub/Creating a Home Hub.md>).

