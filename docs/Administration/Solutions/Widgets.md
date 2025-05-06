---
title: Widgets
slug: eZcu-widgets
description: Learn how to manage widget visibility on HomeHub using JigxManagement. With customizable options, you can control which widgets are visible to specific user groups, ensuring personalized data is shown. Discover how to assign or remove group access for wid
createdAt: Thu Jun 09 2022 09:04:02 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Feb 12 2024 17:19:38 GMT+0000 (Coordinated Universal Time)
---

Widgets are a great way to inform users about the most important data and actions of a solution right on the Home Hub. You have the ability to control which widgets are visible to certain user groups.

:::hint{type="info"}
- You can only toggle the visibility of widgets using Jigx Management. The solution creators are responsible for ensuring that *only personalized data* is being shown to users.
- If you don't grant explicit access for a jig containing widgets to any groups, everyone with access to the solution will have the widgets visible on the Home Hub.
:::

::::VerticalSplit{layout}
:::VerticalSplitItem
::Image[]{alt="Widgets permissions set for Finance" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/t0pg111f7WjdzPi6IBGxJ_jm-financewidget.PNG" size="84" width="1240" height="2500" caption="Widgets permissions set for Finance" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/t0pg111f7WjdzPi6IBGxJ_jm-financewidget.PNG"}
:::

:::VerticalSplitItem
::Image[]{alt="Widgets permissions set for Manager" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/bFqKXjGtBErJ3Gi1wYLOv_jm-managerwidget.PNG" size="84" width="1240" height="2500" caption="Widgets permissions set for Manager" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/bFqKXjGtBErJ3Gi1wYLOv_jm-managerwidget.PNG"}
:::
::::

## Managing Widget Permissions

![Widgets and their associated groups](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3T2YNiC25WduYqQ1_EfqG_jm-widgetsl.png "Widgets and their associated groups")

In the above example, only users in the *Finance* group can see the accounts and product widgets, while the *Managers* group can see the orders and product widgets. The widget settings will update immediately on the affected users' devices.

:::hint{type="info"}
Make sure that you have configured [Groups](./Groups.md) and assigned users to these groups in [Permissions](./Permissions.md) before you start configuring widget permissions.
:::

## Assigning group access

To toggle visibility for specific widgets:

1. Click on the widget name.
2. Select the groups you want to assign access to in the right-hand access pane.
3. Click **Change**.

### Allow use of Everyone group

To allow the sharing of the widgets in this solution with everyone in your organization, check the **Allow use of Everyone group** checkbox. If selected, it allows you to assign widgets to everyone. Once assigned to one or more widgets, this means that the solution will show on everyone's devices, but with the relevant additional permissions applied.

## Removing group access

To remove group visibility for specific widgets:

1. Click on the widget name.
2. Select the groups you want to remove access for in the right hand access pane.
3. Click **Change**.
4. The group's name no longer appears next to the widget.

### Considerations

- When no groups are assigned to any widgets in the solution, everyone can view all the widgets in the app.
- When certain widgets are assigned group access any widgets with no group assigned will not be accessible by anyone. These are noted with a *No Access* message in the Groups with explicit access column. Once access is applied, access is granted according to the applied permissions.

  ![Widget no access](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/bRBgf__8SjFkg-rGuFUq9_jm-widgetnoaccess.png)

