---
title: Release Notes - 2022
slug: 9MQc39I7box5lL2QP17qN
description: Jigx release notes provide information on new features, enhancements, and bug fixes
createdAt: Thu Nov 03 2022 10:41:24 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Feb 12 2024 07:51:27 GMT+0000 (Coordinated Universal Time)
---

## Release 2022.7

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/8b8TKP4NQyFt3_cZLxmsz_release20227.jpg)

### Mobile Apps

New Features

- Added new lifecycle event `onFocus` to the solution index.jigx schema
- Errors are now being displayed as dismissable toast
- Added `when` condition with expression support to standalone `actions` and actions in `action-list`

Bug Fixes

- Improved performance of expression evaluations for `component.list-item`
- Added complete deletion of local SQLite database files when user logs out
- Fixing an issue with missing android permissions for retrieving device location on Android

### Components

New Features

- Added expression support to `when` option of `widget.status `

Bug Fixes

- Fixed issue with cropped content of non-scrollable `jig.default` Jigs types
- Fixed issue with `component.expander` spacing in lists
- Fixed issue with spacing of `component.expander` children
- Fixed chart `alignment` option
- Changed icon of `component.drop-down`
- Fixed issue with home button alignment of `component.summary`
- Added vertical spacing between components on `jig.default`
- Fixed center position of `component.avatar`

### Builder

New Features

- 🎉 Jigx Builder extension is now available in <a href="https://marketplace.visualstudio.com/items?itemName=Jigx.jigx-builder" target="_blank">Microsoft Visual Studio Marketplace</a>
- Improved stability of device connectivity with Builder
- Added the ability to clear all records from SQLite tables on the device
- Moved Jigx Logs to its own tab in the bottom panel of VS Code

Bug Fixes

- Fixed an issue where Inputs displayed `[object][object]` when passing an object as a Parameter
- Fixed an issue where index.jigx did not validate the YAML in real-time
- Fixed an issue where syntax validation incorrectly showed an error when an object was passed as an input

Deprecated Functionality

- Moving forward, Datasource Providers can only be configured by selecting from Dynamic Data, SQLite Data (local), Static Datasource, and System Datasource. Use the sync-entity action to sync remote data to the device. For more information, see <a href="https://docs.jigx.com/syncing-remote-and-loading-local-data" target="_blank">Syncing Remote and Loading Local Data</a>

### Jigx Management

New Features

- General performance and stability improvements

### Breaking Changes

None

### Known Issues

- Push Notifications
  - We re-enabled push notifications on Android. Now notifications are back and fully operational on both iOS and Android. Targeting/Deep linking into a specific Jig from a push notification is still disabled and we will re-enable it soon as well.

## Release 2022.6

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/iuHsHfLVJzenj0YXo2ONi_release20226.jpg "Release 2022.6")

### Mobile Apps

Bug Fixes

- Fixed an issue with home hub padding on Android tablets
- Fixed an issue with deleting local database files when logging out
- Various performance improvements including Improved performance of local SQL lite datastore layer

### Components

New Features

- Added ability to add media files (e.g images and avatars) to a form when being offline
- Improved performance of `drop-down` search with large set of items
- Improved layout of `status` widget type

Bug Fixes

- Fixed issue with positioning of button on `list-item`
- Fixed issue with colors of `trend` component on widgets

### Builder

New Features

- Added headers to all Jig snippets
- Added the ability for Jigx Builder to update automatically
- Added the ability for Jigx Builder to update schemas automatically
- Added functionality to reload the mobile app when connecting Dev Tools to ensure Jigx Builder and mobile app cache is in sync
- Added a new setting to enable/disable system messages in Jigx Builder output window

Bug Fixes

- Fixed an issue where Intellisense did not return the correct fields for static datasources
- Fixed issues with `@ctx.current.item` validation and Intellisense for complex data expressions
- Fixed issues where Dev Tools displayed incorrect state when hovering over components in the YAML

### Jigx Management

New Features

- <a href="https://manage.jigx.com/troubleshooting" target="_blank">Troubleshooting</a> (available from main menu using CorrelationID, and also by viewing the last logs of solution or user)
- Personal access tokens (Check out your user profile -> Bottom left corner)

Bug Fixes

- Organization selector - fixes and improvements around `DENY` and change password
- Refined notification audience targets
- Languages always show English / EN first

### Breaking Changes

None

### Known Issues

- Push Notifications
  - We re-enabled push notifications on Android. Now notifications are back and fully operational on both iOS and Android. Targeting/Deep linking into a specific Jig from a push notification is still disabled and we will re-enable it soon as well.

## Release 2022.5

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/FOC1M8y_fLG3N-EBvUWwX_release20225.jpg)

### Mobile Apps

New Features

- Added option to have persistent global state
- Disable Hermes on Android for better performance
- Improved error messages and UI

### Components

New Features

- Added a debounce to the search input field of lists
- Added ability to set the initial collapsed state of `component.expander`

Bug Fixes

- Fixed an issue with the dropdown search field holding old values
- Fixed an issue with the `isDirty` form state and empty fields
- Improved list performance in general
- Fixed an issue with photo cropping not working when the camera is being used

### Builder

New Features

- Single file publish will now publish the complete solution if the solution has not been published yet
- Added ability for creators to upload large/complex solutions

Bug Fixes

- Fixed an issue where single file publish included \`index.jigx\`
- Multiple expression parser fixes when formulating complex datasources

### Jigx Management

New Features:

- Added a new <a href="https://manage.jigx.com/quickstart" target="_blank">Quickstart</a> solution -> *jigx-widgets* (Plenty ***awesome*** widgets samples fo you!)

### Breaking Changes

None

### Known Issues

- Push Notifications
  - We re-enabled push notifications on Android. Now notifications are back and fully operational on both iOS and Android. Targeting/Deep linking into a specific Jig from a push notification is still disabled and we will re-enable it soon as well.

## Release 2022.3

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/0nhbZuENLJP0PECzUKgWg_release20223.jpg)

### Mobile Apps

New Features

- Added `$base64encode/decode` JSONata functions
- Added ability to hide Jig titles on composite Jigs&#x20;
- Added new function properties for entity syncing:
  - `forRowsWithMatchingIds`
  - `forRowsWithValues`
  - `forRowsInRange`
- Improved public screen for unauthenticated users of branded apps
- Re-enabled basic push notifications for Android

### Components

New Features

- Added a placeholder when using document Jig on composite Jig (not supported)
- Smarter display of „Show more“ action on list component and list widget
- Added ability to display a custom label for link entity-fields

Bug Fixes

- Fixed and issue with shared state of interactive-image
- Fixed an issue with datetime picker selection
- Fixed an issue with the isDirty state of a form
- Fixed expression evaluation in onButtonPress option of a calendar
- Fixed an issue with accessing base64 state of media-picker with multiple images

### Builder

New Features

- Added function execution parameters to the logs in output&#x20;
- Added ability to connect Builder with branded apps

Bug Fixes

- Multiple expression parser fixes when using special JSONata syntax

### Jigx Management

New Features

- Lists
  - Refresh buttons disabled while busy loading
- Solution credentials and connections
  - Can now be manipulated via schema
  - Name can be copied (previously shown as key)
  - Connection test status indicated on the button
  - Fixed schema display settings in dark mode
  - OAuth credentials UI extended to easily adapt scopes and other frequent settings
- Preventing the invite of users until an invite template is set up for the organization
- Improved error handling

### Breaking Changes

None

### Known Issues

- Push Notifications
  - We re-enabled push notifications on Android. Now notifications are back and fully operational on both iOS and Android. Targeting/Deep linking into a specific Jig from a push notification is still disabled and we will re-enable it soon as well.

## Release 2022.2

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/pIJcEcWrlKzfUkE4Wgzk4_release20222.jpg)

### Mobile Apps

New Features

- Improved Home Hub UI
- New solution switcher on Home Hub
- Ability to use a Jig instead of widgets as solution home screen
- Improved rendering performance of composite Jigs
- Added input parameters to widgets on home hub
- Added profile avatar upload indicator

### Components

New Features

- Added ability to listen to JS events in WebView component
- Added clear button to input field of DatePicker component
- Added support for colors to DatePicker and DropDown components
- Added ability to reset a component on a specific Jig or within a composite Jig
- Added isDirty state to Form component
- Added amount state to List Jig type
- Added background actions to Submit Form action
- Added ability to retrieve blob of image from media- and avatar-field
- Added ability to specify image quality for media- and avatar-field uploads

Bug Fixes

- Fixed flashing of modals
- Fixed issue with using datasource fields in Jig titles
- Fixed issue with retrieving dropdown state
- Fixed UI of public content screen
- Fixed crashing issue with list widgets
- Fixed issue with loading certain remote image URLs on Android
- Fixed dynamic sizing of checkbox component
- Improved performance of lists and dropdowns
- Fixed date picker UI issue on Android
- Perform logout on oAuth providers

### Builder

New Features

- Added the ability to validate expressions and highlight any issues
- Added support for Quick Fix suggestions
- Added an ability to cancel deployment of a solution
- Introduced heartbeat support to manage the connection between device and builder when debugging solutions
- Added functionality to highlight the active Jig in Explorer when using dev tools
- Added expression support for global data sources

Bug Fixes

- Fixed missing state for @ctx.current
- Fixed missing state for Interactive image control
- Fixed an issue where incorrect state was displayed for a nested structure
- Fixed missing data types issue with function parameters
- General UI improvements and fixes for state window

### Jigx Management

New Features

- Added user search by email to permissions
- Added region information to organization details UI

Bug Fixes

- Fixed optional function parameters form validation
- Fixed UI issue with group assignments
- Fixed background color of clipboard content in dark mode

### Breaking Changes

- Change of OAuth Redirect URL
  - If you are using OAuth in your solution, please make sure you change your OAuth Redirect URL to [https://oauth.jigx.com/jigx ](https://oauth.jigx.com/jigx/You)
  - You can change the Redirect URL in the Customer Portal ([https://manage.jigx.com](https://manage.jigx.com)) in the Solution -> Credentials settings. Also make sure to change/register the new Redirect URL in your backend (e.g. Azure).
- Usage of static instanceId on item-level
  - If you are using static strings for the instanceId of items (e.g. list-item, interactive-image item etc.), please
    - remove the instanceId completely (preferable) or
    - replace the instanceId with an expression that returns a unique identifier (e.g. instanceId: =@ctx.current.item.id)

### Known Issues

- Push Notifications on Android
  - Push Notifications on Android are currently disabled for the generic Jigx app. We will enable them again with the next release (2022.3). This does not affect in-app notifications as they will continue to work as before
