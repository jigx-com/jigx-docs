# Jigx Concepts

Jigx uses concepts, terminology, and elements you might not be familiar with. Below is an explanation of the main core concepts to help you understand and use Jigx better.

## Jigx Solutions

Jigx refers to a native mobile app as a *solution*. With Jigx you can build and publish more than one solution to your Jigx mobile app. You can *switch* between solutions by tapping the *More* ellipsis icon in the navigation bar and selecting your desired solution. The currently active solution is highlighted with a checkmark icon. If only one solution is available, the *More* icon is hidden.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-_wNc-4qfpMvnhWhjpKEx8-20250429-113930.png" size="76" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-_wNc-4qfpMvnhWhjpKEx8-20250429-113930.png" caption}

## Home Hub

The *home hub* is the first screen you see when you open and sign into the Jigx mobile app. The Home Hub can display navigational menu blocks called *grid-items*, containing *images*, *widgets*, or custom controls. Once you tap on a grid-item, you are directed to a jig, which is a screen used to display various forms of content. The *index.jigx* file ﻿is the place to configure the bottom navigation bar. In addition to grid-items, you can style the Home Hub by adding a [video-player](#) or [carousel](#) at the top of the Home Hub. For more information, see ﻿[Home Hub](<./../Building Apps with Jigx/UI/Home Hub.md>) and [Creating a Home Hub](<./../Building Apps with Jigx/UI/Home Hub/Creating a Home Hub.md>).

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-U_hOcdAx5wOjx7J-NL2gi-20250203-100429.png" size="66" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-U_hOcdAx5wOjx7J-NL2gi-20250203-100429.png" caption}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-UX8IZKVoOjAPqk1NVos4K-20250225-122017.png" size="66" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-UX8IZKVoOjAPqk1NVos4K-20250225-122017.png" caption}
:::
::::

## Jigx Builder

Native mobile solutions are built in Microsoft Visual Studio Code, a development environment installed on many platforms, including Windows and Mac. Jigx extends VS Code with the [Jigx Builder](<./../Building Apps with Jigx/Jigx Builder _code editor_.md>), which is an extension that allows you to build, test, and publish Jigx mobile app solutions. The Jigx Builder\*\* **extension uses YAML, SQL, JSON, and JSONata. A YAML editor is provided that includes IntelliSense, which allows for code completion by simultaneously pressing the control and spacebar** (ctrl+space)\*\* keys. Only valid options in the current cursor context are displayed in the code popup. There is built-in [debugging](<./../Building Apps with Jigx/Jigx Builder _code editor_/Debugging.md>) functionality to assist with troubleshooting your development. Predefined code snippets are provided in the .jigx files to help make development easier and faster. The Jigx Builder loads with a [folder structure](<./../Building Apps with Jigx/Jigx Builder _code editor_/Editor.md>) to categorize the various files needed to build app solutions. These folders are actions, assets, databases, datasources, functions, jigs, and translations.

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/a3BeBpSf7SYH-LJZfNEEN_debug-1.png)

## index.jigx file

The *index.jigx* file is located at the root of the Jigx solution project in the Jigx Builder.  In the index.jigx file, you configure what must be displayed on the home screen (Home Hub) of your solution on the Jigx mobile app. The file opens with a pre-populated code snippet to help you configure the Home Hub. For more information, see [Index settings](<./../Building Apps with Jigx/UI/Home Hub/Index settings.md>), and [Creating a Home Hub](<./../Building Apps with Jigx/UI/Home Hub/Creating a Home Hub.md>).

![](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-azAL6hODEfRAYi74InkkG-20250212-183522.png)

## Widgets

Widgets are navigational menu blocks set up on jigs, allowing them to be utilized in various parts of the solution, including the Home Hub and multiple jigs (screens). These widgets are configurable to display various UI elements, such as locations, images, charts, and more. For more information, see  [Content widget components](#).

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-U_hOcdAx5wOjx7J-NL2gi-20250203-100429.png" size="36" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-U_hOcdAx5wOjx7J-NL2gi-20250203-100429.png" caption}

## Jig

A jig is a container used to configure content. A jig can be configured as a calendar, a form to capture or view data, a PDF or HTML document, a list of data, or even a combination of any one of these. Usually, tapping on a widget in the [Home Hub](<./../Building Apps with Jigx/UI/Home Hub.md>) opens a jig. For more information, see [Jigs (screens)](<./../Building Apps with Jigx/UI/Jigs _screens_.md>) and  [Jig Types](#) sections in this guide.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-likbr1gN2hI0tdoCzt-wk-20250225-122635.png" size="66" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-likbr1gN2hI0tdoCzt-wk-20250225-122635.png" caption}

## Components

Components are elements that can be used when creating a Jigx solution in the Jigx Builder. These elements provide an incredible amount of functionality. Components include interactive images, video players, expanders, and charts. For more information, see [Components (controls)](<./../Building Apps with Jigx/UI/Components _controls_.md>) and [Components](#) example topics in this guide.

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/pRWx0QOGRs51lEaRvvhj7_image-2023-05-11-at-1629.jpeg)

## Actions

Actions allow you to do something, for example, go back to a previous screen, open a URL, or submit a form. For more information on the available actions as well as code samples for each one, see the [actions](<./../Building Apps with Jigx/UI/Actions.md>) and  [action examples](#) sections of this guide.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/EAqLrPaYYsWtn09XM4nsm_image-2023-05-11-at-1916.jpeg" size="70" caption position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/EAqLrPaYYsWtn09XM4nsm_image-2023-05-11-at-1916.jpeg"}

## Functions

Functions enable integration with other platforms through data providers. Creating a new function using one of the provided template options adds the skeleton code to the function definition, making it easier to configure with their authentication requirements. For more information, see [REST Functions](<./../Administration/Solutions/REST Functions.md>), [SOAP Functions](<./../Administration/Solutions/SOAP Functions.md>), and [SQL Functions](<./../Administration/Solutions/SQL Functions.md>).

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/NA6YggelGgOKLscprcO4q_image-2023-05-11-at-1635.jpeg)

## Expressions

Expressions allow you to structure data before binding them to the UI components. Expressions are :Comment[**JSONata**]{resolved="true" docCommentId="FpsxPoV95DbJTsWfLA6hk"} language-based. JSONata is a lightweight query and transformation language for JSON data. JSONata is a rich complement of built-in operators and functions providing options to manipulate and combine data. Learn more about <a href="https://jsonata.org/" target="_blank">JSONata</a> and try out your expressions in their <a href="https://try.jsonata.org/" target="_blank">JSONata Exerciser</a>. The root element of Expressions in .jigx files starts with "@ctx" vs. "$." in JSONata Exerciser (e.g. @ctx.data vs. $.data). Jigx supports shorthand $ expressions for JSONata. For more information, see [Expressions](<./../Building Apps with Jigx/Logic/Expressions.md>), [Expressions - cheatsheet](<./../Building Apps with Jigx/Logic/Expressions/Expressions - cheatsheet.md>) and [Expression examples](#).

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/MYlXNfbJr67D_VvrB8LcU_image-2023-05-11-at-1639.jpeg)

## Datasources

[Datasources](<./../Building Apps with Jigx/Data/Datasources.md>) are sets of data that are available throughout your whole solution (global) or only inside a jig (local). Datasources can be static or dynamic. Jigx **Dynamic Data** is a built-in database that can be used to create, read, update, and delete data in an app. The underlying data store for Dynamic Data is a NoSQL store. This means that each record can have its own field structure, and you can add or remove any fields on a per-record basis. Only the id column is a system column and cannot be changed or removed from the record. Jigx Dynamic Data is managed in Jigx Management. For more information, see [Dynamic Data](<./../Building Apps with Jigx/Data/Data Providers/Dynamic Data.md>) and [Dynamic Data examples](#) .

## Database

A [data provider](<./../Building Apps with Jigx/Data/Data Providers.md>) is a service that accepts data inputs and returns data outputs. Jigx data providers include dynamic, local, REST, Salesforce, SOAP and SQL. For more information see [Data Providers](<./../Building Apps with Jigx/Data/Data Providers.md>) and [Data Provider examples](#).

## Entities

Entities are tables in Jigx Dynamic Data or other databases where your data gets saved, created, updated, and deleted. Use an action such as execute-entity to work with the data. Jigx data is managed in the [Data](./../Administration/Solutions/Data.md) menu option in Jigx Management. Other databases are managed using the [connections](https://docs.jigx.com/connections), [SQL Functions](<./../Administration/Solutions/SQL Functions.md>), [REST Functions](<./../Administration/Solutions/REST Functions.md>), and [SOAP Functions](<./../Administration/Solutions/SOAP Functions.md>) in Jigx Management. For more information, see [execute-entity](#).

## Jigx Management

Jigx Management exposes the Jigx Cloud functionality in a browser-based portal allowing you to manage users and solutions, set up send-and-push notifications, set up data, and view usage metrics of your organization. For more information, see [Management Overview](<./../Administration/Management Overview.md>).

![](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-SqNiXhBUgPV1zdeS8oxjS-20250225-123030.png)

## Jigx App

The Jigx app is available on iOS and Android and works on any device.

- Download the Jigx iOS app from the <a href="https://apps.apple.com/sg/app/jigx/id1495596537" target="_blank">App Store</a>
- Download the Jigx Android app from the <a href="https://play.google.com/store/apps/details?id=com.jigx.android&pli=1" target="_blank">Google Play Store</a>
- The Jigx App is only supported in portrait mode on iOS and Android phones.
- You can brand your app through s [Organization Settings](<./../Administration/Organization Settings.md>)

### See Also

- [Jigx color palette](<./Jigx color palette.md>)
- [Jigx icons](<./Jigx icons.md>)

