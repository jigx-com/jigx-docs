---
title: Release Notes - 2023
slug: kbG0WVknevH5r3wq0Vax-
description: Jigx release notes provide information on new features, enhancements, and bug fixes
createdAt: Thu Nov 03 2022 10:41:24 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Feb 12 2024 16:33:33 GMT+0000 (Coordinated Universal Time)
---

## Release 2023.13

::embed[]{url="https://vimeo.com/894412134?share=copy"}

|                          | **Versions & dates** |
| ------------------------ | -------------------- |
| **Release date**         | 14 December 2023     |
| **iOS version**          | 1.15.0               |
| **Android version**      | 1.0.0                |
| **Jigx Builder version** | 1.24.0               |

### Mobile Apps

New Features & improvements

- Added ability to have a solution with only a custom Home Hub and without a widget-based (default) Home Hub.  See [Home Hub]() and [Custom Home Hub]() for more information.
- Added global/shared actions to solutions. See [Actions]() for more information.
- Improved the general file and photo upload experience.

Bug Fixes

- Fixed issue with animated icons/placeholders on iOS 17+ devices.
- Fixed an issue with the app restarting when the auth token fails.
- Fixed various theming/UI issues.

### Components

New Features & improvements

- Added auto-include of http/https URI prefixes in various components, e.g., `action.open-url`

Bug Fixes

- Fixed an issue with `mediaType:any` in components that upload files to OneDrive.
- Fixed an issue with the `component.signature` that was not working correctly on Android 13+ devices.

### Builder

New Features & improvements

- Shared (Global) actions - Shared actions enable creators to define an effort once and reuse it across multiple Jigs. New solutions open with the action folder structure; existing solutions will not have the folder; you need to manually add the folder for these solutions. See [global actions]() for more information.
- [Salesforce]() provider now recognizes standard Salesforce objects and provides a list of these when using IntelliSense in Jigx Builder. Note that custom objects need to be manually added and will be squiggled in blue to indicate the Salesforce entity is unknown. Ignore this warning if the entity is custom.&#x20;

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
**Previous Salesforce YAML**

![Previous entity structure](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ld-_WFvssZH8N8LvmU4SK_salesforce-previous.png "Previous entity structure")
:::

:::VerticalSplitItem
**New Salesforce YAML**

![IntelliSense for Salesforce entities](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3bKta_nxnecc_e9T0I1kn_salesforce-new.png "IntelliSense for Salesforce entities")
:::
::::

- General improvements have been implemented in snippets to enhance usability.
- In \`index\`, `widget` configuration now provides a quick fix to address problems related to invalid jig references.
- Moved assets (icons and images) from index.jigx to a new assets folder. The icons.jigx and images.jigx files are automatically created for you under the folder.
  1. *Icons - *For **existing** solutions the icon.jigx is automatically created but the assets `icon` entries from the index.jigx file must be manually deleted.&#x20;
  2. *Images - *For **existing** solutions the image.jigx is automatically created with images referenced in jig `headers`, but the assets `image` entries from the index.jigx file must be manually copied over to the images.jigx file and deleted from the index.jigx file.&#x20;

For more information see [Assets]().

![Assets folder](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/p55r-nUQgHaxSfagUPh5D_assets.png "Assets folder")

Bug Fixes

- Resolved a problem related to the preview of `icons`, enhancing visibility
- Addressed a validation issue where an `icon` was incorrectly highlighted if the name consisted of only one character.
- Resolved a problem where deleted items were still accessible in IntelliSense.
- Fixed a validation issue where a valid parameter was erroneously highlighted.

### Jigx Management

New Features & improvements

- Ability to delete unused data tables for Dynamic Data . For more information see [Deleting tables]().
- Add the ability for support to set Organization and Solution limits, read-only access for non-SUPPORT users.

Bug Fixes

- Bug fixes and performance improvements

### Breaking Changes

- When working with the REST or SQL providers that use files, or datastores with files and actions with files, and you used base64 or buffer you must update your YAML to use the new `conversions` property. The change stores the image files as local files on the device and only saves the file uri to the file in the datastore/state. When a component needs the actual binary data, it reads the local file from the file uri.  Previously the call in the jig would be similar to `=@ctx.components.image.state.base64` or `=@ctx.components.profilePicture.state.blob`.
  The new `conversion` property allows for the call to use:
  &#x20;`=@ctx.components.image.state.value` or `=@ctx.components.profilePicture.state.value`.
- For more information, see [File handling]().

## Release 2023.12.1

::embed[]{url="https://vimeo.com/884268897?share=copy"}

### Mobile apps

Bug Fixes

- Fixed an issue with SSO

### Components

New Features & improvements

- Added `plotbands` to [line-chart]() and [bar-chart]()

### Builder

Bug Fixes

- Fixed performance on IntelliSense loading

## Release 2023.12

::embed[]{url="https://vimeo.com/880852874?share=copy"}

### Mobile Apps

New Features & improvements

- Added more than 10.000 new icons 🎉. For more information, see [Jigx icons]().
- Automatically adds icons used in the solution to `assets:` in index.jigx, ensuring icons are visible when the device is offline. For more information, see [Icon assets in solutions]().

Bug Fixes

- Fixed an issue with `isScrollable: false` not setting the location component to full screen
- Fixed an issue with a solution without widgets not opening the settings side panel on tablets

### Components

New Features & improvements

- Added a new component called `component.countdown`. For more information and code samples see [countdown]().
- Added a new component called `component.progress bar`. For more information and code samples see [progress-bar]().

Bug Fixes

- Fixed an issue with location sharing and going offline
- Fixed an issue with the keyboard covering form text fields

### Builder

New Features & improvements

- Jigx Builder will automatically add the `.jigx` file extension if you do not specify it.
- `widgets` are now configurable as part of jig Templates. See more information [Jig Templates]().
- Improved login and Deployment error messages are more descriptive and user-friendly.
- IntelliSense has been improved to support grouping of related code snippets.

Bug Fixes

- Fixed an issue where query parsing listed invalid columns as part of data source intelliSense.
- Fixed an issue where the Placeholder `icon` suggested incorrect options.
- Fixed several issues related to intelliSense performance.
- Fixed an issue where intelliSense incorrectly showed `=@ctx` for properties that only allow `string`.
- Fixed an issue with incorrect intelliSense for `stories`.

### Jigx Management

New features & improvements

- Dynamic Data - Added Row Level Security (RLS) through security policies and authorization. For more information, see [Row Level Security](), [Data policies]() and [Authorized users]().
  - When upgrading to 2023.12, existing Dynamic Data tables will have the `Allow Everyone` restriction set for all CRUD methods in the data policies setting in Jigx Management. No Authorized Users (`Owners` or `Members`) are set for data records. You must manually set the Authorized Users for each data record in each table according to your security requirements.
  - **Recommendation:** With the introduction of row-level-security (RLS), Jigx recommends you re-deploy existing solutions to enforce the latest so that policies work correctly. Enforce minimum version to 2023.12 to ensure policies operate as expected.
- Added JSON support to Dynamic Data. You can upload data using a JSON or CSV file. For more information, see [Dynamic Data]().
- Ability to pin five of your favorite solutions to the top of the solutions page for quick access. See [Favorite Solutions]() for more details.

Bug Fixes

- General improvements

## Release 2023.11

![Release 2023.11](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/NCPhQvxVdc817iZIMPJHm_release2311.png)

### Mobile Apps

New Features & improvements

- Added [Single Sign-On (SSO)]() to provide secure and simple access to your apps.&#x20;

Bug Fixes

- Fixed an issue with `action.set-state` not re-evaluating $now() and $uuid()
- Fixed an issue with the navigation bar displays over the loading screen and action button
- Fixed an issue with the "No internet connection" status not being reliable
- Fixed an issue with `onLoad` not getting executed when using a jig as custom home screen
- Fixed an issue with notifications not working on Android 13
- Fixed an issue with REST continuation if a parameter name is reused from the original request

### Components

Bug Fixes

- Fixed an issue with padding of the icon used in `component.expander`

### Builder

New Features & improvements

- Added a universally unique identifier (\`uuid()\`) function to \`=$\` IntelliSense
- The `jig.calendar` snippet now includes a `header`

Bug Fixes

- Fixed an issue with incorrect ordering of items listed under data and functions of the connected device
- Fixed an issue where the validation error indicator did not align correctly with the incorrect value
- Fixed an issue where validation was inconsistent with duplicate file names

### Jigx Management

Bug Fixes

- General improvements

### Breaking Changes

- When using icon elements in `leftElement`, `rightElement` and `leftIcon`, the property used was `name`. This `name` property has been changed to `icon`.  In Jigx Builder the `name` property displays with red validation squiggles. Hover over the validation issue to see the available icon property. For example:

:::::VerticalSplit{layout="middle"}
::::VerticalSplitItem
:::CodeblockTabs
Before

```yaml
 leftElement:
      element: icon
      name: =@ctx.current.item.icon
      isContained: true
      isDuotone: true
 
 rightElement: 
      element: icon
      name: =(@ctx.current.item.materials = true ? 'attachment' :'alert-triangle')
     
```
:::
::::

::::VerticalSplitItem
:::CodeblockTabs
After

```yaml
 leftElement:
      element: icon
      icon: =@ctx.current.item.icon
      isContained: true
      isDuotone: true
 
 rightElement: 
      element: icon
      icon: =(@ctx.current.item.materials = true ? 'attachment' :'alert-triangle')
     
```
:::
::::
:::::

## Release 2023.10

![Release 2023.10](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/zLaA3dRyOlFnjM5jKIzHr_release20.png)

### Mobile Apps

New Features & improvements

- Improved tablet UI rendering

Bug Fixes

- Fixed various gradient issues with Android tablets
- Fixed an issue with the drawer icon disappearing on Android
- Fixed an issue with full screen (isScrollable) not working when a jig contains a description
- Fixed an issue with spacing of composite jigs and empty jig titles
- Fixed an issue with a modal's background not filling the whole screen on an Android phone

### Components

New Features & improvements

- Added a `size` option to `component.location`. For more information see [Full screen location]().
- Improved zoom-in animation of `component.location`. For more information see [location displaying path]() example.
- Added support for custom cropping ratio to `component.media-field`. For more information see [media-field]().


Bug Fixes

- Fixed an issue with file uploads to REST endpoints
- Fixed an issue with `component.avatar` center alignment
- Fixed an issue with locally exectuted REST calls (useLocal)
- Fixed an issue with `isHidden` on calendar `onButtonPress` not working correctly
- Fixed an issue with `component.media-picker` with `imageCropping` and `imageQuality` crashing the app
- Fixed an issue with `component.location` throwing a *coordinates must contain numbers* error
- Fixed an issue with `component.location` and manually moving the map on Android
- Fixed various rendering issues of `component.location` on Android

### Builder

New Features & improvements

- Added support for `=$` (JSONata IntelliSense) in functions. For more information see [Expressions](), [Advanced Expressions](), [Example Expressions](), and [Expressions - cheatsheet]()

Bug Fixes

- Fixed performance issues with IntelliSense
- Fixed an issue where `data` was incorrectly shown as required with the `submit-form` action
- Fixed validation errors related to the [OneDrive]() provider

Known Issues

- When clearing a datasource or property configuration in Jigx Builder, no IntelliSense is available to re-start the configuration.&#x20;
  *Workaround*: Navigate away from the file, then return to the file and invoke IntelliSense (ctrl+space).
- When global datasources are configured in Jigx Builder where the schema contains an enum with an empty array, the schema validation incorrectly shows errors.

### Jigx Management

Bug Fixes

- General improvements and bug fixes

### Breaking Changes

Certain properties can be deprecated or changed in Jigx Builder between versions. To ensure that solutions continue to function on the device, Jigx has added the ability to transform a solution's definition to comply with the current application's schema version during runtime. This means that the following can occur:

1. When the Jigx App version is greater than the Jigx Builder version, solutions will continue to work in the Jigx mobile app, while in Jigx Builder the deprecated property displays with red validation squiggles. Hover over the validation issue to see the available property options.&#x20;
2. When the Jigx Builder version is greater than the Jigx App version, the mobile app displays the *Out of date* screen. Update the app by tapping the *Update *button which will direct you to the latest version of the Jigx App in the App Store or Google Play Store.

## Release 2023.9

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/eNlD-QuiYMP1ZdFgHnti5_release239.png)

### Mobile Apps

Bug Fixes

- Fixed an issue with the login email input field keyboard type

### Components

Bug Fixes

- Fixed an issue with `component.dropdown `values not displaying correctly
- Fixed issues with `component.expander` alignments
- Fixed an issue with `component.webview` not clearing the complete cache when signing out
- Fixed an issue with the rendering of sections on tablets
- Fixed an issue with lonpress and alignment of expanders in popups on iOS

### Builder

Bug Fixes

- Fixed an issue where REST calls did not show in Jigx Logs
- Fixed an issue with `EXECUTE` messages in Jigx Logs that did not include any metadata
- Fixed an issue with validation incorrectly underlining valid `providers`

### Jigx Management

Bug Fixes

- General improvements and bug fixes

### Breaking Changes

The text property in `component.avatar` has changed to `title`. You must manually update your YAML to reflect the change and republish your project. Note that when using an avatar within the `leftElement` the `text` property must still be used.

## Release 2023.8

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/pdYToA6-e5lWhO6Tyt04c_release2382x.png" size="98" caption position="flex-start" }

### Mobile Apps

New Features

- Added the ability to show/hide any component conditionally using the `when` property. For more information see [component properties]()
- Interact with files on OneDrive by creating, updating, deleting, and downloading files from your Jigx App. For more information see [Microsoft OneDrive]().

### Components

New Features

- Added the ability to upload documents to OneDrive using `component.media-picker` and `component.media-field`. For more information see [Microsoft OneDrive]().

Bug Fixes

- Increased the maximum amount of latitude and longitude coordinates for `component.location`

### Builder

New Features & improvements

- Builder now includes a template gallery that you can use as a base when creating solutions. Templates are available when creating jigs and adding components to a jig. For more information see [Jig Templates]()
- The SQL editor in Jigx Console gets a refresh and includes several enhancements to improve user experience


Bug Fixes

- Fixed an issue with IntelliSense in multiline expressions
- Fixed an issue with the validation indicator not showing in the correct location

### Breaking Changes

None

## Release 2023.7

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/xxlFKLAyhduE21gdm3pmd_whatsnew20237.png)

### Mobile Apps

Bug Fixes

- Fixed an issue where the app fetched solutions whenever you closed and open the app
- Fixed an issue where the offline status bar displayed at the top of the solution when you were online

### Components

New Features

- Added the ability to limit the max file size of media uploads using the `maximumFileSize` property. For more information see <a href="https://docs.jigx.com/examples/media-field" target="_blank">media-field</a>
- Added the ability to use a `when` condition to hide or show jigs on a composite jig. For more information see [composite jig]()

Bug Fixes

- Fixed an issue where the incorrect actions were displayed in a long-press preview popup
- Fixed the way the `media-field` calculates the media-type
- Fixed an issue with the calendar jig in dark mode
- Fixed an issue with the rendering of event dates and data in a calendar jig
- Fixed an issue with the progress element’s theming
- Fixed an issue with selecting records in a dropdown
- Fixed an issue with the interactive image’s rendering

### Builder

New Features & Improvements

- Jigx watcher is a new window making it easy for creators to monitor the result of one or more expressions during a debug session

 Bug Fixes

- Fixed an issue where REST errors did not get logged in Jigx logs
- Fixed an issue where the Jig column was empty with logs created from index
- Fixed several issues with the reliability of IntelliSense

### Breaking Changes

None

## Release 2023.6

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/4pvAfeaQm4fOPzXfRylz1_release20236.png)

### Mobile Apps

New Features

- Added simplified user onboarding using [OTP]() pin codes
- Added the ability to make REST calls directly from the device to remote endpoints
- Added the ability to define shared expressions on a solution and Jig level
- Added the ability to prefetch images for offline usage
- Added a `data` option to the `submit-form` action to allow for more flexibility

Bug Fixes

- Transform single items into JSONata arrays when binding to data option of lists etc.
- Fixed an issue with `onSuccess` not executing actions in certain configurations
- Fixed an issue with caching of story images

### Components

Bug Fixes

- Fixed an issue of `component.drop-down` not displaying single items

### Builder

New Features & Improvements

- IntelliSense now includes JSONata functions with snippets and inline documentation
- Improved Jig snippets to include `onFocus` configuration
- Improved snippets for `header`, `action-scanner`, and `functionParameters` configuration

Bug Fixes

- Fixed an issue with IntelliSense not providing the correct option in nested expressions
- Fixed an issue with the search functionality in Jigx Logs window
- Fixed an issue with missing logs when `home` is configured in index
- Fixed an issue where `@ctx` was not an IntelliSense option in expressions
- Fixed an issue with incorrect IntelliSense after deleting or renaming a `datasource` file

### Jigx Management

New Features

- We added a default OTP verification email template that organization OWNERS can override in Organization -> Settings -> Invites&#x20;

### Breaking Changes

None

## Release 2023.5

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/D531Lv2VcFj9xnIHq43Jk_release20235.jpg)

### Mobile Apps

New Features

- Improved resizing behavior on Android

Bug Fixes

- Prevent error toasts from closing automatically
- Fixed an issue with the sequential `action-list` in `onLoad` events
- Fixed an issue with `onRefresh` event handling with forms

### Components

Bug Fixes

- Fixed an issue with deep-linking into Google Maps with tracking enabled
- Fixed an issue with charts that only have a single data point in a series
- Fixed an issue with invalid location coordinates crashing the app
- Fixed spacing issues with long-press previews

### Builder

New Features & Improvements

- Implemented several changes to improve the performance of solution publishing
- Warnings and Errors messages get new color treatment to make them easier to discover in Jigx Logs

Bug Fixes

- Fixed an issue where removing `home` configuration from `index` did not reflect immediately on the mobile app after publishing the solution
- Fixed an issue with the validation of nested `function parameters`

### Jigx Management

New Features

- General improvements

### Breaking Changes

None

## Release 2023.4

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ikfXUzF0__4YoBIf2niqi_release20234.jpg)

### Mobile Apps

New Features

- Added when condition for toggling visibility of widgets on home hub
- Re-enabled full push notification functionality
- Added ability to invoke `onRefresh` event handler on composite Jigs

Bug Fixes

- Fixed an issue with the timing of sequential `action-lists`
- Fixed an issue with style of disabled fields readability on dimmed screens
- Fixed an issue with home button on tablet when there is only one solution assigned to user
- Fixed an issue with wiping of tables when a REST call has been executed
- Fixed an issue with flashing screen when searching on a Jig
- Fixed an issue with `header` image and `titles` not showing on long-press preview
- Fixed an issue with the `onFocus` event handler of Jigs on tablets
- Fixed an issue with base64 images not displaying correctly on Android
- Fixed an issue with `goBack` home/previous in actions not correctly working with using `onSuccess` option
- Fixed an issue with the OAuth challenge modal not opening again

### Components

New Features

- Added QR code and barcode scanner `action`
- Added a new component `component.widgets` for displaying widgets on default Jigs
- Added a minLength option to the text-field component
- Added an isHomeButtonHidden option to `jig.document` type

Bug Fixes

- Fixed an issue with DateTime picker `onChange` event timing
- Fixed an issue with `component.list` showing only 3 items in sections
- Fixed an issue with choosing a time outside min/max range of Android
- Fixed an issue with list items format option
- Fixed an issue with the `onPress` action of `jig.calendar`

### Builder

New Features & Improvements

- Jigx Logs introduce many new features and enhancements to support creators better when troubleshooting a solution
- Enhanced the YAML validation to better cater to scenarios where values are determined during runtime. Runtime values will be underlined with yellow instead of red
- Added additional debug information to function messages

Bug Fixes

- Fixed an issue with incorrect IntelliSense suggestions for `component.dropdown`
- Fixed an issue with validation not working correctly when using `ctx.jigs.[instanceId]`
- Fixed an issue where the QR code to connect to the device did not refresh correctly
- Fixed an issue where selecting an option from IntelliSense removed the leading space resulting in invalid YAML
- Improved reliability of IntelliSense in datasources
- Fixed an issue where function parameter validation showed errors for valid values

### Jigx Management

New Features

- General improvements

### Breaking Changes

- Deprecated `onLoad` event handler on Jigs (Note: Please use `onFocus` and `onRefresh` instead)
- Deprecated `onFail` option of actions
- Deprecated description option of `summary` component
- Deprecated rightIconType option of `entity-fields`

## Release 2023.3

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/05kfCTpHxqjOjjOine_os_release20233.jpg)

### Mobile Apps

New Features

- 🎉 Added ability for long-press gestures on iOS to display a `preview` with context actions. See [https://docs.jigx.com/examples/overview](https://docs.jigx.com/examples/overview) for more details
- Improved splash screen performance and startup time
- Improved navigation stack implementation for phone and tablet

Bug Fixes

- Fixed an issue with `onLoad` getting triggered when scrolling home hub
- Fixed an issue with OAuth modal disappearing on the very first app launch
- Fixed an issue with snake-case expressions (e.g. `@ctx.data.get-my-data.field-name`)
- Fixed an issue with `onLoad` getting triggered twice when using `onRefresh`

### Components

New Features

- Added new runtime context properties
  - User ID: `@ctx.user.id`
  - Organization ID: `@ctx.organization.id`
  - Solution ID `@ctx.solution.id`
  - Solution Name: `@ctx.solution.name`
- Added ability to access device location properties:
  - Accuracy: `@ctx.system.geolocation.coords.accuracy`
  - Altitude: `@ctx.system.geolocation.coords.altitude`
  - Altitude Accuracy: `@ctx.system.geolocation.coords.altitudeAccuracy`
  - Heading: `@ctx.system.geolocation.coords.heading`
  - Latitude: `@ctx.system.geolocation.coords.latitude`
  - Longitude: `@ctx.system.geolocation.coords.longitude`
  - Speed: `@ctx.system.geolocation.coords.speed`
  - Timestamp:`@ctx.system.geolocation.timestamp`

Bug Fixes

- Fixed an issue with the `section` of a `component.list` overlapping list-items
- Fixed an issue with shrinked group titles of `component.interactive-image`
- Fixed an issue with incorrect header background in expanders
- Fixed an issue with certain base64 image content on Android not displaying
- Fixed an issue with deep-linking into Google Maps crashing the app on iOS

### Builder

New Features & Improvements

- Added functionality to check for duplicate file names
- Simplified documentation displayed when hovering over elements in the code editor
- Enhanced Jigx Logs to display additional message types
- Enhanced code snippets to merge with existing YAML and avoid duplication resulting in invalid YAML

Bug Fixes

- Fixed an issue where validation returned incorrect values for `entity`
- Fixed an issue where IntelliSense incorrectly listed `@ctx.current.item`
- Added `@ctx.current.state.checked` to `onChange` event for a list
- Fixed an issue with `Goto jig (F12)` did not navigate to the target jig
- Fixed an issue with `Quick Fix` did not move the cursor to the correct location

### Jigx Management

New Features

- General improvements

### Breaking Changes

- None

## Release 2023.2

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/XwfGxiiYHWyDc7EIdcEX5_release20232.jpg)

### Mobile Apps

New Features

- Improved launch time when no solutions are assigned to user
- Improved lifecycle for solutions in `index.jigx` (`OnLoad`, `OnRefresh` and `OnFocus`)
- Added the ability to add custom terms & conditions and imprint to the legal section in profile/settings

Bug Fixes

- Fixed a blank screen issue when logging in with no solutions
- Fixed an issue with the native splash screen not displaying correctly on tablets in landscape mode

### Components

New Features

- Added sections to `jig.default` type to better structure the layout
- Added support for slim `headers` on all Jig types that support headers (see breaking changes)
- Added a new `isCompact` layout option to `component.entity`
- Added continuation support to the `REST` data provider
- Added a new `4x4` group widget type

Bug Fixes

- Fixed various spacing issues
- Fixed alignment of icons in various situations

### Builder

New Features

- Added validations for SQL queries in the datasource configuration of a Jig

Bug Fixes

- Fixed an issue where validation failed on `@ctx.current.item` for `component.list-item` that includes sections configuration
- Fixed an issue where selecting an option from IntelliSense removed trailing `"` and `)`
- Fixed issues with IntelliSense reliability using `@ctx` as part of nested expressions

### Jigx Management

New Features

- General improvements

### Breaking Changes

- Please update your `headers` section in your Jigs as we are adding more flexibility to headers (e.g. slim headers). Check out Jigx Builder Intellisense in the headers section to see the new snippets/options

