---
title: Widgets
slug: I2vz-widgets
createdAt: Wed Jan 17 2024 12:27:32 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Mar 07 2025 09:34:40 GMT+0000 (Coordinated Universal Time)
---

# Widgets

Widgets are navigational menu blocks shown either on the [Home Hub](home-hub/home-hub.md) or in a [jig (screen)](jigs-_screens_/jigs-_screens_.md) and are used to display information and provide interactivity. Widget sizes and content, such as icons, locations, images, charts, and more, are configurable.

### Configuration Sizes

{% columns %}
{% column %}
A widget can be configured with the following sizes: - 1x1 - 2x2 - 2x4 - 4x2 - 4x4 Consider the layout of the widgets on the mobile app screen. Specific sizes cover the entire width of the screen, for example, 4x4. The image on the right shows the layout of widgets on a mobile app screen.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/WD-layout.png" alt="Widget layouts" width="405"><figcaption><p>Widget layouts</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

### How to configure widgets

#### Widget configuration

1. Add an icon to the top level of your jig.
2. The `jigId`, and `size` are configured in a [jig.grid](https://docs.jigx.com/examples/readme/jig-types/jig_grid) or [grid-item](https://docs.jigx.com/examples/grid-item) component to display the widget.&#x20;

{% tabs %}
{% tab title="jig-with-icon.jigx" %}
```yaml
title: Add new employee
type: jig.default
icon: person
```
{% endtab %}

{% tab title="jig-grid.jigx" %}
```yaml
 - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: jig-with-icon
```
{% endtab %}
{% endtabs %}

#### 2x2, 2x4, 4x2, and 4x4 widgets configured with content

1. Widgets are configured in the YAML in a jig file and a unique `Widget Name` is provided that is referred to as the `widgetId`.
2. The `jigId`, `widgetId`, and `size` are configured in a [jig.grid](https://docs.jigx.com/examples/readme/jig-types/jig_grid) or [grid-item](https://docs.jigx.com/examples/grid-item) component to display the widget.
3. If inputs are required to pass data into the widget then configure them in the `grid-item` under the `inputs` property. Inputs are not mandatory and are dependant on the scenario.

{% tabs %}
{% tab title="jig-with-widget.jigx" %}
```yaml
widgets:
  # Provide a unique name for the widget. This becomes the widgetId.
  dev-avatar:
    # Configure the type of widget to display in the grid-item.
    type: widget.avatar
    options:
      text: LS
      # Configure the widget properties with inputs defined in the grid-item,
      # if data is to be passed into the widget.
      uri: =@ctx.jig.inputs.photo
      bottom:
        type: component.titles
        options:
          align: center
          title: =@ctx.jig.inputs.name
          subtitle: React Web Developer
```
{% endtab %}

{% tab title="jig.grid.jigx" %}
```yaml
children:
  - type: component.grid-item
    options:
      # Specify the size of the grid-item (widget)
      size: "2x2"
      children:
        type: component.jig-widget
        options:
          jigId: jig-with-widget
          widgetId: dev-avatar
          # If the widget requires inputs add it in the grid-item.
          inputs:
            photo: =@ctx.user.avatarUrl
            name: =@ctx.user.displayName
```
{% endtab %}
{% endtabs %}

### Change the widget behavior

By default when tapping on a widget you are directed to the corresponding jig. You can change the behavior of the widget by adding an `onPress` event to the widget configuration. The `onPress` is configured with an action, which is triggered when pressing on the `widget`. Use IntelliSense to see the available list of actions.

{% code title="jig.jigx" %}
```yaml
- type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: company-site
          # Add an onpress to open a specific URL.
          onPress:
            type: action.open-url
            options:
              url: https://docs.jigx.com
```
{% endcode %}

### Change the widget content

There are various UI elements available to make your widget inviting and engaging to end users. Content or information can be shown on the surface of a widget. Here is a list of available content/information widgets:

<table><thead><tr><th width="157.12109375">Widget content</th><th>Description</th></tr></thead><tbody><tr><td><a href="../../Understanding the basics/Jigx icons.md">icons</a></td><td>Choose an icon from thousands of available icons.</td></tr><tr><td><a href="https://docs.jigx.com/examples/readme/actions-buttons">actions (buttons)</a></td><td>Configure a button with an action that executes.</td></tr><tr><td><a href="https://docs.jigx.com/examples/VeUB-avatar">avatar</a></td><td>Display an avatar on the widget.</td></tr><tr><td><a href="https://docs.jigx.com/examples/chart">chart</a></td><td>Configure a bar, line or pie chart to display on the widget.</td></tr><tr><td><a href="https://docs.jigx.com/examples/image">image</a></td><td>Configure an image to display on the widget, consider the <code>size:</code> of the widget to ensure the image displays as expected , 1x1 is not suitable for most images.</td></tr><tr><td><a href="https://docs.jigx.com/examples/list">list</a></td><td>Display a list of data in the widget with additional left and right elements if required.</td></tr><tr><td><a href="https://docs.jigx.com/examples/location">location</a></td><td>Show a location in a map on the widget with markers.</td></tr><tr><td><a href="https://docs.jigx.com/examples/status">status</a></td><td>Configure a visual representation of a status, such as goal status, or sales quarterly status.</td></tr><tr><td><a href="https://docs.jigx.com/examples/value">value</a></td><td>Show values and amounts on the widget, such as Sales target or number of orders to date.</td></tr></tbody></table>

1. To configure the widget content specify the `widget:` property at the bottom of the jig.
2. Provide a `Widget name` for the widget that is referenced as the `widgetId`.
3. Select the `type` of content to display in the widget.

{% hint style="info" %}
You still need to add the widget `size:` and `jigId` to the _grid-item component_ after changing the content of the widget in the jig file.
{% endhint %}

#### 1.Configure an icon

By default widgets are shown on the `grid-item` with an icon. If no `icon` is specified Jigx assigns a default icon to the widget. To configure an icon, add the `icon` property in the jig itself. Start typing the first two letters of an [icon](<../../Understanding the basics/Jigx icons.md>) to see a list of thousands of icons you can choose from.

In the example below the _location_ icon is specified to replace the default icon.

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/WD-icon-default.png" alt="Default icon" width="99"><figcaption><p>Default icon</p></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/WD-icon.png" alt="Location icon on widget" width="136"><figcaption><p>Location icon on widget</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="yoga-location.jigx" %}
```yaml
title: Location
type: jig.default
# add an icon in the jig that displays on the widget.
icon: location

datasources:
  address:
    type: datasource.static
    options:
      data:
        - street: 768 5th Ave
          city: New York
          country: US
children:
  - type: component.location
    options:
      viewPoint:
        centerPosition: middle
        address: |
          =@ctx.datasources.address.street  
          & ',' & @ctx.datasources.address.city
          & ',' & @ctx.datasources.address.country
        zoomLevel: 9
```
{% endtab %}

{% tab title="grid-item.jigx" %}
```yaml
title: Yoga
type: jig.grid

children:
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: yoga-location
```
{% endtab %}
{% endtabs %}

#### 2.Configure the widget content

1. In Jigx Builder open the jig whose widget you want to configure.
2. Use IntelliSense (ctrl+space) at the root level and select `widgets:`.
3. Specify the `Widget Name`.
4. Next choose the `type:` of content to display on the widget, such as `widget.location` use IntelliSense to invoke the list of available types.
5. Depending on the type you selected additional properties are required, see [widget](https://docs.jigx.com/examples/widgets) examples on how to configure each type accordingly.
6. Add the widget (`size` , `jigId`, `widgetId`, and `inputs`) to the [grid-item](https://docs.jigx.com/examples/grid-item).

In the example below the widget content is configured to show a _location_ on the widget surface.

<figure><img src="../../.gitbook/assets/WD-location.PNG" alt="Widget with location content" width="188"><figcaption><p>Widget with location content</p></figcaption></figure>

{% tabs %}
{% tab title="yoga-studio.jigx" %}
```yaml
title: Location
type: jig.default

datasources:
  address:
    type: datasource.static
    options:
      data:
        - street: 768 5th Ave
          city: New York
          country: US
children:
  - type: component.location
    options:
      viewPoint:
        centerPosition: middle
        address: |
          =@ctx.datasources.address.street  
          & ',' & @ctx.datasources.address.city
          & ',' & @ctx.datasources.address.country
        zoomLevel: 9

#Add a location content type to display on the widget surface.
widgets:
  locationWidget:
    type: widget.location
    options:
      viewPoint:
        centerPosition: middle
        address: |
          =@ctx.datasources.address.street  
          & ',' & @ctx.datasources.address.city
          & ',' & @ctx.datasources.address.country
        zoomLevel: 9
```
{% endtab %}

{% tab title="home.jigx" %}
```yaml
title: Home
type: jig.grid

children:
  - type: component.grid-item
    options:
      # Specify the widget size.
      # Ensure the selected size will display the content.t
      size: "2x2"
      children:
        type: component.jig-widget
        options:
          jigId: yoga-studio
          widgetId: locationWidget
```
{% endtab %}
{% endtabs %}

### How to move or rearrange widgets

The widgets display order on a screen is determined by the order of the [grid-item](https://docs.jigx.com/examples/grid-item) in the YAML. You can change the order of the widgets by simply changing the order in the YAML. It is important to take into consideration the configured size of each widget when ordering widgets. Changing the order of the widgets can give your app a completely different look. Placing a `4x2` followed by `4x4` will result in white space next to the `4x2`.

{% columns %}
{% column %}
&#x20;Initial widget order in [grid](https://docs.jigx.com/examples/grid)


{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/WD-order1.PNG" alt="Initial widget order" width="188"><figcaption><p>Initial widget order</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



{% code title="home.jigx" %}
```yaml
title: Yoga
type: jig.grid

children:
  # First widget displayed
  - type: component.grid-item
    options:
      size: "4x2"
      children:
        type: component.jig-widget
        options:
          jigId: yoga-image-widget
          widgetId: yoga-image
  # Second widget
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: my-bookings
  # Third widget
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: yoga-location
  # Fourth widget
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: yoga-info
  # Fifth widget
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: yoga-meals
```
{% endcode %}

{% columns %}
{% column %}
Reordered and resized widgets.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/WD-order2.PNG" alt="Reordered widget" width="188"><figcaption><p>Reordered widget</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% code title="home.jigx" %}
```yaml
title: Yoga
type: jig.grid

children:
  - type: component.grid-item
    options:
      size: "2x2"
      children:
        type: component.jig-widget
        options:
          jigId: my-bookings
  - type: component.grid-item
    options:
      size: "2x2"
      children:
        type: component.jig-widget
        options:
          jigId: yoga-location
  - type: component.grid-item
    options:
      size: "4x2"
      children:
        type: component.jig-widget
        options:
          jigId: yoga-image-widget
          widgetId: yoga-image

  - type: component.grid-item
    options:
      size: "2x2"
      children:
        type: component.jig-widget
        options:
          jigId: yoga-info
  - type: component.grid-item
    options:
      size: "2x2"
      children:
        type: component.jig-widget
        options:
          jigId: yoga-meals
```
{% endcode %}

### Widget labels and titles

Widget labels are shown under the widget, and are read from the configured `title:` property of the jig.

1. To display a widget with no label use `title: ' '` in the jig.
2. To display a label on the widget surface use the widget [titles](https://docs.jigx.com/examples/W2NL-titles).

### Widget badging

{% columns %}
{% column %}
Enhance your widget with a customizable badges for instance showing the number of events this week or the number of new orders. Add the `badge` property to the jig YAML with an expression.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/wd-badging.png" alt="Widget badge" width="188"><figcaption><p>Widget badge</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="calendar-jig" %}
```yaml
# jig file
title: Calendar
type: jig.calendar
icon: calendar-3
# badge counting the number of events in the calendar, the badge shows on the widget
badge: =$count(@ctx.datasources.calendar-data.id)
```
{% endtab %}

{% tab title="new-customer-jig" %}
```yaml
title: New customers
type: jig.default
# Add the badge to show when there are new customers to process
badge: =@ctx.datasources.customer.new = 1 ? 0:1
```
{% endtab %}
{% endtabs %}

### Inputs

Inputs allow you to pass data to the jig associated with the widget. For example, when a customer taps on _My Orders_ widget the input is configured to pass that specific customer's Id and Name to the jig ensuring only the orders for that customer are shown. For more information on inputs see [Passing data using input](jigs-_screens_/passing-data-using-inputs.md)

{% code title=" index.jigx" %}
```yaml
- type: component.grid-item
  options:
    size: "2x2"
    children:
      type: component.jig-widget
      options:
        jigId: my-orders
        widgetId: order-detail
        # Specify the inputs for the widget.
        inputs:
          customer-name: =@ctx.datasources.customer[5].name
          id: =@ctx.datasources.customer[5].id
```
{% endcode %}

### Widget visibility & access

You have the ability to control which widgets are visible as well as when the widget must be visible.

1. Control which widgets are visible to certain user groups by granting permissions on each widget in a solution in [Jigx Management > Widgets](../../Administration/Solutions/Widgets.md). By default everyone with access to the solution has the widgets visible in the app.
2. Use the `when:` property configured by an [expression](../logic/expressions.md) or a boolean statement to determine when a widget must be visible. For example, show the _order_ widget when there are orders awaiting approval.

{% code title="grid.jigx" %}
```yaml
- type: component.grid-item
    # Determine when the widget will display
    when: =@ctx.datasources.get-hiker-level.participant-group = 'easy'
    options:
      size: "4x4"
      children:
        type: component.jig-widget
        options:
          jigId: location
```
{% endcode %}

### Considerations

* The content of the widget will determine the size to select. For example, showing an image or location on a 1x1 widget will not display well rather uses a 4x4 or 4x2.
* Best practice is to arrange widgets that fill the screen with no additional white space. Plan and design the widget layout and size of each widget in a design app or simply draw it on paper. For more information see [Planning your app](../../getting-started/planning-your-app/planning-your-app.md).
* A `1x1` widget will only display an icon.

### Examples and code snippets

See [Widgets](https://docs.jigx.com/examples/widgets) for full code samples.
