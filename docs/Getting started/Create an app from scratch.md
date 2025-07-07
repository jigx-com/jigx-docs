---
title: Create an app from scratch
slug: s2xAkEBhQIcz1yt3BtEmf
description: This document provides a comprehensive guide on using Jigx to create mobile apps. Learn about basic Jigx concepts, such as data collection and navigation, and follow step-by-step instructions to build a complete mobile solution called "Hello-Jigx." From m
createdAt: Tue Apr 04 2023 06:20:14 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Feb 21 2025 14:24:14 GMT+0000 (Coordinated Universal Time)
---

## What you will learn

In this quick guide, you will learn the basics of Jigx and how easy it is to create mobile apps. Basic Jigx concepts are introduced, such as collecting information, working with data in SQLite, navigating between screens, and passing parameters.

## What you will create

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{alt="Hello Jigx Solution" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ksTOZ1JgHnObj7nOh158G_widgetscustoml.PNG" size="60" caption="Hello Jigx Solution" position="center"}
:::

:::VerticalSplitItem
The solution is named **Hello-Jigx** and consists of a map showing a location, a calendar with events, a form to capture and view data, and a list showing the captured data. The table below guides you through building each element of the solution.
:::
::::

:::hint{type="info"}

1. Before you start building your first solution ensure you have created a [Creating an account](<./Creating an account.md>) and [Install the Jigx Builder](<./Install the Jigx Builder.md>). Get an overview of the [Jigx platform](<./../Understanding the basics/Architecture.md>) and an understanding of the [Jigx Concepts](<./../Understanding the basics/Jigx Concepts.md>).
2. We recommend you build out all the solution steps below, as each solution step builds on the previous step until you have a functioning mobile app.
   :::

## Solution Steps

There are several [types](https://docs.jigx.com/examples/jig-types) of jigs you can build. They are default, document, calendar, composite, and list. Below are step-by-step guides that use these jig types. Each solution step builds on the previous step until you have a functioning mobile app. Each solution provides an overview, explaining the Jigx's concepts introduced in the step, and code samples with comments.

<a href="https://docs.jigx.com/create-the-hello-jigx-solution-project" target="_blank">Step 1: Create the Hello Jigx solution project</a>
Start by creating the Hello Jigx project in VS Code
**Build time**: 2 min

<a href="https://docs.jigx.com/create-the-map" target="_blank">Step 2: Create the Map</a>
Build a map jig that displays a specific location on a map, with an icon for the jig.
**Build time**: 10 min

<a href="https://docs.jigx.com/create-the-calendar" target="_blank">Step 3: Create the Calendar</a>
Next, add a calendar jig that displays a week with the events, meetings, and relevant details.
**Build time**: 10 mins

<a href="https://docs.jigx.com/create-data-form-and-list" target="_blank">Step 4: Create Data - forms & lists</a>
Build a jig to add a new customer by capturing the customer's details using a form. Then add a jig to list all the customers created using the form. Add the ability to view, and edit these customer records.
**Build time**: 20 mins

<a href="https://docs.jigx.com/combine-the-solutions-elements" target="_blank">Step 5: Combine the solution's elements</a>
Now you have built a solution that shows a location on a map, a calendar with detailed entries, and a new customer form and list in a single solution. Let us expand the solution further by joining the new customer form and list into one jig, then add a jig header to the new customer jig.
**Build time**: 15 mins

<a href="https://docs.jigx.com/customize-the-hello-jigx-solution" target="_blank">Step 6: Customize the Hello-Jigx solution
</a>Extend your solution with styling changes and additional functionality. Replace the map icon with a location widget in the map.jigx file, and replace the people icon with the image widget in the composite.jigx file. Change the calendar icon and add a badge to display the number of events for the week.
**Build time**: 10 mins

## What's next?

Why not build your own app? See how to [plan your app](<./Planning your app.md>), then learn how to [Use templates to create apps](<./Use templates to create apps.md>) or explore the various available UI elements in Jigx by adding the **Jigx-samples** [prebuilt solution](<./Use pre-built solutions.md>) to your organization and viewing the solution in the Jigx App.
