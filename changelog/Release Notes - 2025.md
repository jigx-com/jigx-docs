# Release Notes - 2025

## Release 2025.4

![](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-ws06Vbw_rddbPEXhcEO92-20250521-173021.png)

| Release date    | 4 July 2025 |
| --------------- | ----------- |
| iOS version     | 1.146.2     |
| Android version | 1.146.2     |
| Jigx Builder    | 1.38.0      |

### Mobile Apps

New features & improvements

- The `onRefresh` spinner is now persistently visible while an action is executing, preventing users from triggering a redundant pull-to-refresh gesture.
- Enjoy more control over your jigs, by default, the Home button appears on all jigs except the Home Hub, but now you have the flexibility to show or hide it on any jig by simply setting the `isHomeButtonVisible` property on a jig. See [Home button visibility](https://docs.jigx.com/examples/common-jig-type-properties#4XJE6) for more information.
- Enhanced app stability and performance by fetching only necessary image and icon assets and loading them when needed, ensuring a faster and smoother user experience.
- The profile menu has moved to the top left of the header and now appears on all Home Hub screens.
- The solution switch is now available in the bottom navigation menu. Tap the "More" (ellipsis) button to open it. Solutions are listed, with the total count displayed at the top.
- The number of permitted `tabs` in the index.jigx file has been increased. The first four `tabs` are displayed in the Home Hub bottom navigation, and any additional `tabs` appear when the "More" (ellipsis) button is tapped.

![](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-tYaCSucebdLFNh9YN7A_D-20250429-134001.png)

Bug Fixes

- Resolved an issue preventing PDF document previews from displaying correctly in the media-picker component.
- Fixed an issue where translations in header actions were not functioning correctly.
- Enhanced dynamic data syncing between Jigx Management and the mobile app, providing faster updates and significantly reducing delays.
- Fixed an issue on Android where scrolling lists within tabs caused layout problems and resulted in the search bar disappearing.
- Fixed multiple issues with notifications
  - Fixed an issue where viewing a notification with a target jig from the Notifications screen resulted in a "Screen not found" message due to the jig not being properly located.
  - Fixed notification ordering, when pressing on a message it would be sorted to the top of the screen.
  - Resolved an issue where the Notifications screen appeared empty, even when notifications were available.
- Fixed an issue where the sync scope was not correctly limited to the specific solution, ensuring accurate data synchronization.
- Resolved an issue where users could become stuck in an offline state due to a failed network request.
- Resolved an issue where switching from portrait to landscape mode on a tablet caused unintended navigation back, instead of simply adjusting the view. The app now maintains the correct screen during orientation changes.
- Fixed an issue where opening a modal jig from a list item and retrieving its outputs did not work as expected. Outputs are now correctly returned and handled.

### Components and jig types

New features & improvements

- [jig.table](https://docs.jigx.com/examples/jigtable) - The table jig displays structured data in rows and columns, allowing users to view and interact with multiple records within the app.
- [media-field](https://docs.jigx.com/examples/media-field#xvJAM) -The media-field picker allows users to view and upload media files, with configurable filters to restrict document file types (e.g., PDF, DOC, PPT, or plainText) based on your app’s requirements.
- [bottomSheet (Beta)](https://docs.jigx.com/examples/bottomsheet-beta) - The bottomSheet slides up from the bottom of the screen to display contextual content or actions without leaving the current screen. Ideal for menus, filters, forms, or quick actions.
- ***Enhanced field component flexibility***: Components previously only available within the form component can now be used either as standalone components or wrapped within a form component.
- [Dynamic files](https://docs.jigx.com/dynamic-files) extend Jigx's Dynamic Data entities to include file references, allowing files to be securely stored and associated with entities. Files are physically stored in Amazon S3, offering a combination of simplicity, security, and portability.&#x20;
- **Widget customization enhancements** in [jig.grid](https://docs.jigx.com/examples/jiggrid) and [grid-item](https://docs.jigx.com/examples/grid) - You can now override the default widget title and icon using the `title` and `icon` properties. Additionally, widgets can be configured with an `onPress` event, enabling interactive behavior such as opening maps, displaying modals, or triggering actions.

Bug fixes

- Fixed an issue in the `component.location` where the second line of the address was not displaying.
- Fixed an issue where `filters` were not being highlighted in lists on Android devices.

### Actions

New features & improvements

- Improvements have been made to the [generate-file](https://docs.jigx.com/examples/generate-file) functionality, specifically related to encoding reliability and consistency.
- [open-app-settings](https://docs.jigx.com/examples/open-app-settings) - The action directs users straight to the app’s settings page, helping them quickly find and adjust permissions without needing to navigate through their device settings manually.

### Builder

New features & improvements

- Added [F12 code navigation](https://docs.jigx.com/editor#5m93r) functionality that allows quick navigation from within a datasource to the databases/default.jigx file for faster access and improved developer efficiency.
- [Jigx Solution Diagnostics](https://docs.jigx.com/editor#NjUMZ) - is a built-in analysis tool that helps you identify and troubleshoot issues across your entire Jigx solution or a subset of files in the solution. It detects project build errors, missing references, and scans your source code for programmatic errors, warnings, and overall solution health.
- [Custom variables](https://docs.jigx.com/solution-settings#UIqCn) - IntelliSense now displays the variables configured in Jigx Management > Solution Settings when using the `=@ctx.solution.settings.custom.{{variableName}}` expression. After adding a new custom variable in Management, you can use IntelliSense's *Reload Solution Settings* option to update data from Jigx Management and make the variable visible in IntelliSense.

![](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Xlz4cUJDzdSHr1WCVNU3a-20250408-093707.gif)

- **Templates** - Added templates in builder for the following jigs and components.
  - [jig.grid](https://docs.jigx.com/examples/jiggrid)
  - [jig.tabs](https://docs.jigx.com/examples/jigtabs)
  - [jig.table](https://docs.jigx.com/examples/jigtable)
  - [expander with variant](https://docs.jigx.com/examples/expander#sRhC4)
  - [segmented-control](https://docs.jigx.com/examples/segmented-control)
  - [grid-item](https://docs.jigx.com/examples/grid)

Bug fixes

- Fixed issues with JSONata expression validation to ensure more accurate and reliable evaluations.
- Aligned the available options between Quick Fix and IntelliSense in Jigx Builder to ensure a consistent and streamlined developer experience.
- Fixed the YAML in the location and scenario templates.
- The `=@ctx.actions[instanceId].outputs` functionality has been updated to allow configuration outside of a sequential list for generate-file, generate-pdf, and share actions.&#x20;

### Jigx Management

Bug Fixes

- Removed the delay in syncing Dynamic Data between Jigx Management and the mobile app, resulting in faster and more seamless updates.
- Bug fixes, performance improvements and usability improvements.

### Known issues

- *Issue:* `action.share`- When sharing via AirDrop, the item is shared twice instead of once.
- *Issue*: The keyboard expands over input text fields in the `bottomSheet`.

### Updates to Quick-Start sample solutions

| **Solution** | **Additions**                                                         |
| ------------ | --------------------------------------------------------------------- |
| jigx-sample  | [jig.grid](https://docs.jigx.com/examples/jiggrid)                    |
|              | [jig.tabs](https://docs.jigx.com/examples/jigtabs)                    |
|              | [jig.table](https://docs.jigx.com/examples/jigtable)                  |
|              | [bottomSheet (Beta)](https://docs.jigx.com/examples/bottomsheet-beta) |
|              | [segmented-control](https://docs.jigx.com/examples/segmented-control) |
|              | [grid-item](https://docs.jigx.com/examples/grid)                      |

## Release 2025.3

![Release 2025.3](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-4AA-ROd4Ed6oGtDw1SXM1-20250320-135147.png)

| Release date    | 21 March 2025 |
| --------------- | ------------- |
| iOS version     | 1.131.0       |
| Android version | 1.131.0       |
| Jigx Builder    | 1.37.0        |

### Mobile Apps

New features & improvements

- Added the ability to update a user's name and phone number in their profile when using the [update-profile]() action.
- Added the ability to customize the [User Profile]() screen. The new `component.jig` added to the index.jigx file renders any jigs in the profile screen. The customized jig has a width header and actions.
- Added support for customizing the [User Profile]() screen.
  - A new `component.jig` entry in index.jigx renders custom jigs within the profile screen.
  - The customized jig includes a width header and actions.

Bug Fixes

- Allowed text in `titles` to wrap in the `title` container, preventing text from being cut off or blocking the `expander` from opening.
- Fixed an issue where using a deeplink to open a specific jig resulted in a blank screen.
- Resolved an alignment issue on the OTP and Request Access screens that made it difficult to access the app.
- Improved navigation from the Settings screen to the home page after switching solutions.
- Fixed the `onRefresh` event, which was not executing for a list jig on Android devices.

### Components

New features & improvements

- [count-up]() - The count-up component is a display-only element that continuously updates in real-time, showing the elapsed time since a specified start timestamp.

### Builder

New features & improvements

- Added validation to `grid-item` determining when `widgetId` is required.
- Enhanced the way you interact with jigs by introducing the ability to retrieve `outputs` from jigs you navigated to using the following expression `=@ctx.jigs.instance-id-of-the-jig.outputs.[key-of-ouput]`.
- Added the `onTableChange` event, which responds to remote system data changes and updates the mobile device. This event monitors specific data tables (entities) for changes and triggers the configured actions when a change is detected. This ensures data consistency between the remote system and the mobile device, keeping information up to date across the platform.
- Added validation for grid-item, determining when widgetId is required.
- Enhanced interaction with jigs by enabling the retrieval of outputs from navigated jigs using the following expression: `=@ctx.jigs.instance-id-of-the-jig.outputs.[key-of-output]`.

Bug fixes

- General builder, snippets and hover popup improvements.

### Jigx Management

Bug Fixes

- Bug fixes, performance improvements and usability improvements.

## Release 2025.2

![Release 2025.2](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-JhCvM6QU2wXeEshNuhwqq-20250228-113139.png)

| Release date    | 6 March 2025 |
| --------------- | ------------ |
| iOS version     | 1.127.1      |
| Android version | 1.127.1      |
| Jigx Builder    | 1.36.0       |

### Mobile Apps&#x20;

Bug Fixes

- Fixed an issue on legacy widget configurations on index.jigx.
- Fixed an error when opening an `event` in the `jig.calendar`.
- Add the no solution screen when the user doesn't have a sln assigned.
- Fixed an issue when upgrading to release 2025.01, the location component in custom components did not function.
- Fixed the UI alignment on the OTP Request access screen.

### Builder

New features & improvements

- [Jigx Variables]()
  - When invoked within an action, the `=@ctx.system.geolocation` method executes asynchronously.
  - **DEPRECATED: **Set the permissions on location using the system variable `=@ctx.system.locationPermissions`. `PermissionStatus` can be `granted` | `undetermined` | `denied`
- Added Jigx Builder support for `action.sync-status`.
- Implemented `action.execute-sql` in Jigx Builder.

### Jigx Management

Bug Fixes

- Bug fixes and performance improvements.

## Release 2025.1

![Release 2025.1](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-V6gq42u3APtiESK_cg3YA-20250131-072044.png)

| Release date    | February 2025 |
| --------------- | ------------- |
| iOS version     | 1.125.14      |
| Android version | 1.125.14      |
| Jigx Builder    | 1.35.0        |

### Important Updates and Migration Guidance

Release 2025.1 introduces significant changes to existing functionality, components, and actions, along with new features that may impact existing solutions. While every effort has been made to provide [migration plans]() to ensure backward compatibility, once a solution is published on this release, the changes will take effect. The primary areas impacted include the home screen (index.jigx), location component, go-to action, widgets, and stories.

- Jigx strongly recommends thoroughly testing all solutions after publishing to ensure expected behavior and stability.
- The documentation is being updated to reflect the latest product offerings. As a result, some screenshots and code samples may not yet represent the most recent features and improvements.

### Mobile Apps

New features & improvements

- [go-to]() action - The action allows you to open a jig as a modal. Simply set the `isModal` property to `true`.
- [Navigation]() - The [go-to]() action is used to configure the flow of jigs in the app using the `behaviour` property. With the `behaviour` you determine if you want to push the screen into the app history, by using the `new` value, or show the one you already have in history by using the `existing` value.
- [Grid]() and [custom tabs]() used to create Home Hub and bottom navigation bar. For backward compatibility - see [Migration plan]() to understand the changes that are required when republishing the solution.
- [jig.grid]() - Create grid layouts in your app, organizing content into rows and columns for a visually consistent and flexible interface. It helps align elements proportionally, ensuring a structured design. The grid is ideal for creating galleries to display photos or product images, as well as dashboards, menus, and product lists.
- The home button has been removed from jigs and the profile button has been moved to the new bottom navigation tab bar. See [Home Hub]() for more information.&#x20;
- Added the ability to remove the Support menu from the user profile screen. This can be configured via a flag in the build configuration.
- Solution switching has been moved to the Profile settings screen.
  ::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-NGrWw9SMNv_vpn6k1f6rE-20250130-102419.png" size="40" position="center" caption="Profile " alt="Profile" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-NGrWw9SMNv_vpn6k1f6rE-20250130-102419.png" width="800" height="1611" darkWidth="800" darkHeight="1611"}

Bug Fixes

- Improved the experience with errors appearing after logout due to long running sync actions.
- Fixed an issue for REST calls where setting your parameter to an output location would cause it to fail.
- Improvements made to error boundary and handling.
- Changed keyboard panel to match theme's background colors.
- Fixed deep translations, for example, translation of formatting of values such as $.

### Components and jig types

New features & improvements

- [jig.tabs]() - Tabs is a new jig type that allows you to navigate between different jigs with ease, enhancing the user experience by providing an organized layout.
- [jig.grid]() - This jig type enables you to create grid layouts in your app, organizing content into rows and columns for a visually consistent and flexible interface. The grid is ideal for creating galleries to display photos or product images.
- [Grid component]() - create a grid layout as a component in a jig with other components.
- [Divider]() -create a simple divider between components using the `component.divider`. The divider component adds a simple dark horizontal line across the screen. Common use cases include grouping related content or enhancing visual hierarchy.
- [segmented-control]() - create a horizontal control consisting of segments that allows you to** **toggle between multiple options in a compact, efficient way.
- Actions added on [jig-header]() - Configure actions to display as links or icons in the top right corner of the header.
- Enhanced the `media-picker’s` usability by reducing clicks/taps during the upload process.
- `List `and `list-items` improvements include:
  - Added support for using a [list-item outside a list]() component. This allows configuring a single list item with all list-item features, such as left and right elements and swipe actions, without requiring a full list. See a code example [Single list-item in an expander]()
  - Enhanced the `list-item` description to support multiple lines.
  - Added color support to the `value` property of the list's `rightElement`.
- Multiple enhancements made to `location` component, including support for custom markers, different markers based on a state, user's location display, and follow a user location.** Note:** A [Migration plan]() is in place to ensure backward compatibility for existing solutions. However, once a solution is republished, you must update the code to ensure the location component continues to function as expected.
- Multiple improvements made to the `expander` component, including:
  - Determine the background color for header versus body using the `variant` property with `plain` or `emphasis` values.
  - Expander arrow align left or right.
  - Added the ability to add a solid or transparent `divider`.

Bug Fixes

- Fixed the shadow performance on `card` component.
- Consolidated the standard and custom card components.
- Various padding fixes across components.
- Update `entity-fields` compact border setting and content size.

### Actions

New features & improvements

- Added the `numberOfVisibleActions` property, allowing up to two buttons to be displayed in the action panel in a jig. See [Common action properties]() for more information.
- Improved the secondary button's color and appearance.
- Enabled the action buttons to be displayed on the Home Hub.
- Actions added on [jig-header]() - Configure actions to display as links or icons in the top right corner of the header.
- Added multiple new actions, as described in the table below:

| **New actions**                       | **Functionality**                                                                                                                                                                                                                                               |
| ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `action.execute-sql`                  | Execute custom SQL queries on the database securely when the action button is tapped.                                                                                                                                                                           |
| `action.open-map`                     | Open the device's default map app (e.g., Google Maps, Apple Maps, or Waze) with the provided address when the on-screen button is tapped. See [open-map]() for more information.                                                                                |
| `action.open-media-picker`            | Quickly manage selected media files on your device—modify or remove selections with a tap of the on-screen button. See [open-media-picker]() for more information.                                                                                              |
| `action.generate-file`                | Generate files such as PDFs, CSVs, or text files. Content is written to the file, along with an optional encoding parameter. Once generated, the file's URI is returned and included in the action instance output. See [generate-file]() for more information. |
| `action.generate-pdf`                 | Create a PDF file version of HTML content, whether a receipt, report, form, or other document, with just a tap. See [generate-pdf]() for more information.                                                                                                      |
| `action.print`                        | Generate hard copies of invoices, receipts, articles, or any rendered content in raw HTML, that works across different devices and printers. See [print]() for more information.                                                                                |
| `action.set-active-tab`               | Programmatically set the active tab in the `jig.tab` component. See [set-active-tab]() for more information.                                                                                                                                                    |
| `action.share`                        | Share files directly from the app with just a tap. Whether it's a document, image, or report, the share action lets you send files via the devices messaging apps. See [share]() for more information.                                                          |
| `action.set-jig-state`                | Programmatically set the state of the current jig.                                                                                                                                                                                                              |
| `action.reset-jig-state`              | Programmatically reset the state of the current jig.                                                                                                                                                                                                            |
| `action.set-solution-state`           | Programmatically set the state of the solution. Note, this action is similar to `action.set.state`.                                                                                                                                                             |
| `action.reset-solution-state`         | Programmatically reset the state of the solution. Note, this action is similar to `action.reset.state`.                                                                                                                                                         |
| `action.set-custom-component-state`   | Programmatically set the state of the [Custom Components (Alpha)]() in the current jig.                                                                                                                                                                         |
| `action.reset-custom-component-state` | Programmatically reset the state of the [Custom Components (Alpha)]() in the current jig.                                                                                                                                                                       |
| `action.start-sync-scope`             | The action configured to start syncing a specific subset of data with the server, effectively cutting down on network traffic and useful when the app is offline.                                                                                               |
| `action.delete-sync-scope`            | The action configured to delete syncing a specific subset of data with the server, effectively cutting down on network traffic and useful when the app is offline.                                                                                              |
| `action.delete-sync-status`           | Set the action to remove the sync status displayed on the screen (syncing, synced, failed, synced, and interrupted).                                                                                                                                            |
| `action.update-profile`               | Allow the user to update their profile (avatar URL) easily to keep their personal information current and ensure that the app experience is tailored to their preferences.                                                                                      |

Bug Fixes

- Pull-to-refresh is disabled when no `onRefresh` actions are set.

### Builder

New features & improvements

- Determine the version of the app by using [system](https://docs.jigx.com/examples/jigx-variables) states, the expression used is `=@ctx.system.appVersion`.
- REST improvements include:
  - Enabled the use of custom JavaScript in REST function expressions.
  - Added default 401 error handler in the REST provider to retry three times.

Bug Fixes

- Fixed `input` suggestions when no input definitions are provided.
- Fixed IntelliSense options for `leftElement`.
- Enabled field validation for `componentId`.
- Fixed an issue where the preview of expressions honored global expressions over local expressions.
- Changed Jigx Builder to show all components even if they had different properties already configured in a list and provider property.
- Fixed an issue where deploying a single JavaScript file resulted in the entire solution being deployed.
- Updated the validation message for input parameters.
- Fixed an issue where publishing failed when using the publish button next to tabs.
- Fixed an issue whereby IntelliSense did not invoke for certain jigs at a certain position.
- Fixed and improve autocomplete for `swipeable` property in the list component.
- The `isDiscardChangesAlertEnabled` in the form component default value has changed from `true` to `false`.

### Jigx Management

New features & improvements

- Dynamic data improvements include:
  - Support for files.
  - Column filters.
  - View/edit consecutive rows via the record editor.
  - Easily continue adding new rows without closing record editor.
- General UI improvements:
  - Right-sidebar collapsible (where relevant).
  - Improved keyboard accessibility on drawers and alerts.
- Troubleshooting improvements:
  - Expanded filtering, log detail and grouping of log messages.
  - Ability to export logs.
- Performance improvements:
  - Improved performance of bulk actions (like adding/removing dynamic data & solution members) and indication of progress.
- User Preferences enhancements:
  - Expose and persist management preferences like `theme` and `preferred default menu` to streamline experience across devices.
- Users
  - Ability to import users via CSV.
- General
  - Bug fixes and general improvements.

### Change in behavior

- *Backwards compatibility* - When a widget displayed on the Home Hub and no specific icon was configured, a default icon of four squares was shown. In existing solutions the four squares are now replaced with a default heart icon. You can change the icon by configuring the `icon` property in each jig file.

### Deprecated

- The `story-group` component and `stories` property in index.jigx has been removed for all new and existing solutions. If you currently use stories on your home screen they will no longer appear in the app and in Jigx Builder the YAML will have red squiggles. Remove the YAML in Jigx Builder and republish.
- The ability to set access to widgets in a solution in Jigx Management for users and groups has been removed.
- The `home` property in index.jigx used to display a custom Home Hub has been removed. Reference the custom home jig under the new `tabs` property. See [Creating a Home Hub]() for more details.

### Updates to documentation

- **Note:** The documentation is being updated to reflect the latest product offerings. As a result, some screenshots and code samples may not yet represent the most recent features and improvements.

