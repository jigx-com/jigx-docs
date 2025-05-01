---
title: Jigx icons
slug: kCd_-icons
description: Improve user navigation and interaction in your mobile app with Jigx's predefined set of icons. Easily incorporate icons into UI components, jigs, and widgets using YAML code. Preview icons by publishing or referring to a list, and for any missing icons, 
createdAt: Wed Sep 13 2023 11:52:15 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Mar 05 2024 14:12:20 GMT+0000 (Coordinated Universal Time)
---

Incorporating icons into your mobile app design enhances user navigation and interaction, making the app more user-friendly and visually appealing. At Jigx we provide you with an extensive list of icons.

### Where can you use icons?

While creating your solution, you can configure certain UI components, jigs, and widgets to use icons in the YAML. Additionally, you can determine the icon's position, size, and interaction. Use IntelliSense (ctrl+space) in the YAML in Jigx Builder to determine if you can specify an icon. Choose an icon from the list and configure the provided properties if you can.  Examples of properties that use icons are `leftElement`, `rightElement`, and `leftIcon`. Here is an example showing you how to specify an icon in a `leftElement` and how to use an [expression](<./../Building Apps with Jigx/Logic/Expressions.md>) to determine which icon to display depending on the current list item.

:::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/EiaXkBq8DHuCxvXli3S2Q_icons.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/EiaXkBq8DHuCxvXli3S2Q_icons.PNG" size="80" width="1240" height="2500" position="center" caption="List icons in a list" alt="List icons in a list"}
:::

::::VerticalSplitItem
:::CodeblockTabs
YAML

```yaml
type: component.list-item
  options:
    title: =@ctx.current.item.service
    subtitle: =@ctx.current.item.time & 'minutes for task completion'
    leftElement: 
      element: icon
      icon: =(@ctx.current.item.materials) = true ? 'home' :'car-garage'
```
:::
::::
:::::

### How do you add an icon?

Icons can be used either in the YAML key position to select an icon, for example `icon: house`, or as the YAML value to determine that a property must use an icon, for example, in a `LeftElement: icon` property. IntelliSense propmts you and shows where the icon can be used in the YAML. &#x20;

**Examples**

:::::VerticalSplit{layout="middle"}
::::VerticalSplitItem
Using the `icon` as a key in YAML to display an alarm bell icon on the Home Hub widget.

:::CodeblockTabs
YAML (icon key)

```yaml
title: Home Security
type: jig.default
icon: alarm-bell
```
:::
::::

::::VerticalSplitItem
Using the icon as a value and then as the key in YAML to display the dollar icon in a `component.summary` .

:::CodeblockTabs
YAML (icon value)

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
:::
::::
:::::

1. &#x20;Next to `icon:` start typing the first two letters of an icon name, for example al, this will open the list of icons starting with two letters.&#x20;
2. A preview of the icon is shown in the right popup with a link to the icon in <a href="https://www.streamlinehq.com/icons/streamline-bold" target="_blank">streamline</a>.
3. Use the up and down arrows on your keyboard to browse through the list with the preview showing.
4. Once you have decided on an icon click Enter.

### Where can you see a preview of the icon?

The list of available icons is extensive and is based off the icons in [https://www.streamlinehq.com/icons/streamline-bold ](https://www.streamlinehq.com/icons/streamline-bold). You welcome to browse this link. In Jigx Builder a preview of each icon is available in the right popup with a link to the icon in <a href="https://www.streamlinehq.com/icons/streamline-bold" target="_blank">streamline</a>. All you need to do is start typing the first two letters of an icon you want.

![Preview of icons](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/bqu2vrN1o5CGLZj0oHqwY_jb-icons.png "Preview of icons")

### Icon assets in solutions

All icons used throughout a solution are automatically added to the **icon.jigx** file under the **assets** folder. This improves performance of the app and ensures that all icons are available when the mobile device is offline and the app is in use.&#x20;

The following applies to the asset list:

- Each icon change detection automatically causes an update in the list in the icon.jigx file.
- All icons from all jig files are added to the list, expect icons referenced or listed within datasources e.g., `=@ctx.datasources.ds.icon`. You can manually add these icons to the asset list in the icon.jigx file.&#x20;
- Icons are added to the icon asset list automatically or you can manually add icons to the list.
  - Automatically generated icons are indicated by a comment `# auto-generated` after the icon name in the list.
  - Manually added icons do not have the comment added

![Icon asset list ](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/qfIHzyzXT-zJFBnIndSJZ_jb-assets.png "Icon asset list")

### Icons in actions

Adding an `icon` property in an action* *only applies to `swipeable`, `secondary`, and `header` actions. Primary actions do not support icon setups.

### Can I add custom icons?

The list of icons is not customizable, and you cannot add custom icons. If you are unable to find the icon you need, contact ****support\@jigx.com****.

