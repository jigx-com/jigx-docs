# Jigx icons

Incorporating icons into your mobile app design enhances user navigation and interaction, making the app more user-friendly and visually appealing. At Jigx we provide you with an extensive list of icons.

### Where can you use icons?

While creating your solution, you can configure certain UI components, jigs, and widgets to use icons in the YAML. Additionally, you can determine the icon's position, size, and interaction. Use IntelliSense (ctrl+space) in the YAML in Jigx Builder to determine if you can specify an icon. Choose an icon from the list and configure the provided properties if you can. Examples of properties that use icons are `leftElement`, `rightElement`, and `leftIcon`. Here is an example showing you how to specify an icon in a `leftElement` and how to use an [expression](../building-apps-with-jigx/logic/expressions.md) to determine which icon to display depending on the current list item.

:::::VerticalSplit{layout="middle"} :::VerticalSplitItem ::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/EiaXkBq8DHuCxvXli3S2Q\_icons.PNG" size="80" position="center" caption="List icons in a list" alt="List icons in a list" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/EiaXkBq8DHuCxvXli3S2Q\_icons.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"} :::

::::VerticalSplitItem :::CodeblockTabs YAML

```yaml
type: component.list-item
  options:
    title: =@ctx.current.item.service
    subtitle: =@ctx.current.item.time & 'minutes for task completion'
    leftElement:
      element: icon
      icon: =(@ctx.current.item.materials) = true ? 'home' :'car-garage'
```

::: :::: :::::

### How do you add an icon?

Icons can be used either in the YAML key position to select an icon, for example `icon: house`, or as the YAML value to determine that a property must use an icon, for example, in a `LeftElement: icon` property. IntelliSense propmts you and shows where the icon can be used in the YAML.

**Examples**

:::::VerticalSplit{layout="middle"} ::::VerticalSplitItem Using the `icon` as a key in YAML to display an alarm bell icon on the Home Hub widget.

:::CodeblockTabs YAML (icon key)

```yaml
title: Home Security
type: jig.default
icon: alarm-bell
```

::: ::::

::::VerticalSplitItem Using the icon as a value and then as the key in YAML to display the dollar icon in a `component.summary` .

:::CodeblockTabs YAML (icon value)

```yaml
summary:
  children:
    type: component.summary
    options:
      layout: default
      title: Add to cart
      leftIcon:
        element: icon
        icon: currency-dollar-circle
```

::: :::: :::::

1. Next to `icon:` start typing the first two letters of an icon name, for example al, this will open the list of icons starting with two letters.
2. A preview of the icon is shown in the right popup with a link to the icon in :Link\[streamline]{href="https://www.streamlinehq.com/icons/streamline-bold" newTab="true" hasDisabledNofollow="false"}.
3. Use the up and down arrows on your keyboard to browse through the list with the preview showing.
4. Once you have decided on an icon click Enter.

### Where can you see a preview of the icon?

The list of available icons is extensive and is based off the icons in [https://www.streamlinehq.com/icons/streamline-bold ](https://www.streamlinehq.com/icons/streamline-bold). You welcome to browse this link. In Jigx Builder a preview of each icon is available in the right popup with a link to the icon in :Link\[streamline]{href="https://www.streamlinehq.com/icons/streamline-bold" newTab="true" hasDisabledNofollow="false"}. All you need to do is start typing the first two letters of an icon you want.

![Preview of icons](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/bqu2vrN1o5CGLZj0oHqwY_jb-icons.png)

### Icon assets in solutions

All icons used throughout a solution are automatically added to the **icon.jigx** file under the **assets** folder. This improves performance of the app and ensures that all icons are available when the mobile device is offline and the app is in use.

The following applies to the asset list:

* Each icon change detection automatically causes an update in the list in the icon.jigx file.
* All icons from all jig files are added to the list, expect icons referenced or listed within datasources e.g., `=@ctx.datasources.ds.icon`. You can manually add these icons to the asset list in the icon.jigx file.
* Icons are added to the icon asset list automatically or you can manually add icons to the list.
  * Automatically generated icons are indicated by a comment `# auto-generated` after the icon name in the list.
  * Manually added icons do not have the comment added

![Icon asset list](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/qfIHzyzXT-zJFBnIndSJZ_jb-assets.png)

### Icons in actions

Adding an `icon` property in an action only applies to `swipeable`, `secondary`, and `header` actions. Primary actions do not support icon setups.

### Can I add custom icons?

The list of icons is not customizable, and you cannot add custom icons. If you are unable to find the icon you need, contact [**support@jigx.com**](mailto:support@jigx.com).
