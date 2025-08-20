---
title: Jigx color palette
slug: AlXC-jig
createdAt: Wed Sep 13 2023 09:35:19 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Feb 26 2025 07:15:38 GMT+0000 (Coordinated Universal Time)
---

# Jigx color palette

The Jigx mobile app color palette, or color scheme, is a predefined selection of colors used consistently throughout the mobile application's user interface (UI). The color palette is essential for creating a visually appealing and cohesive user experience.

### Default color palette

Below is an image showing the Jigx default color palette, and which UI interfaces use the color.

![Jigx color palette](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-XY2wHDc9hppM5cFpNjaXn-20250226-071535.png)

### Selecting default colors in Jigx Builder

While creating your solution you can configure certain components, and widget colors in the YAML to use either the default primary, semantic, or complementary colors. Use intelliSense (ctrl+space) to determine if you can specifiy a color. If you can choose a color from the list of available colors.

![Selecting colors in Jigx Builder](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/YIX7ZpFqH3NJVIlDexv82_yamlcolorfinal.gif)

### Changing the default colors

You can define colors for branded apps in Jigx Management [Organization Settings](../administration/organization-settings/organization-settings.md). Note that any changes to colors in a branded app requires the app to be re-uploaded to the app stores.

### Applying colors based on specific conditions

Colors can be configured based on specific conditions. For example, a payment amount exceeding a certain threshold can be displayed in red. However, conditional color configurations are only available in areas that support conditions, such as list items. In contrast, direct color options are more widely supported, for example, `lists` allow both conditional and direct setups, whereas `interactive-images` only support direct options. Additionally, certain areas restrict the available color choices, while UI elements support the predefined set of fourteen colors.

* When configuring the `color` property, select the `color condition`boption.
* Under the `when` property, add an expression that defines the condition under which the specified color should be applied.&#x20;

{% code title="color-condition" %}
```yaml
color:
   - when: =@ctx.current.item.registered = true 
     color: color2
   - when: =@ctx.current.item.registered = false
     color: color4          
```
{% endcode %}

{% code title="color (no condition)" %}
```yaml
options:
  color: color2
```
{% endcode %}
