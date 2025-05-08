---
title: Groups
slug: dgNv-groups
description: Learn how to assign users to groups in your solution to control the visibility of widgets and stories. Discover how to create new groups, add or remove users, and ensure that the right content is displayed to the right audience.
createdAt: Tue Jun 07 2022 10:00:03 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Dec 09 2024 09:18:00 GMT+0000 (Coordinated Universal Time)
---

Users who have access to a solution can be assigned to *Groups* within the scope of that solution. *Groups* can then be used to toggle the visibility of [Widgets](./Widgets.md).

For example, a CRM app configured with two Groups: Managers and *Employees*. Managers should have access to widgets that display metrics about all sales opportunities across all employees and employees should only have access to see widgets with information about their own sales opportunities.

::::VerticalSplit{layout}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/gHO03QqpV_4D0YI6LyH1E_widgets1iphone13blueportrait.png" size="70" position="center" caption="Manager View" alt="Manager View"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/nfgVL47qAYwdBTgOvyKll_groups2iphone13blueportrait.png" size="70" position="center" caption="Employee View" alt="Employee View"}
:::
::::

## Creating Groups

Groups are specific to a solution and do not appear globally in all your organization's solutions. You need to create groups per solution.

1. Click on the solution's name in the Solutions list, the solutions menu opens and the options are visible in the left navigation pane. Select the **Groups** icon.
2. Click the **Add group** button at the top right of the screen.
3. Type the name of the group to be created.
4. Click **Add**.

The new group is displayed in the list. Next you need to add users to your groups. The users you going to add to the group must have the solution assigned to their [User profile](./../Users.md).

![Creating Groups](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Dr50nr29_4G8BCTX9TdfV_jm-groupsl.png "Creating Groups")

## Removing Groups

In the event that you want to remove a group from the solution, click the **remove** link next to the group in the Groups list and click **Ok** to the remove message.

You can remove groups but keep in mind that [Widgets](./Widgets.md) that had these groups assigned previously will be hidden to users in the removed groups.

## Adding Users to Groups

Each group requires members. The members must have access to the solution to be visible in the **Add user to group** pane.

1. Click on the name of the group you want to add users to.
2. Click on the **Add users to Group:** *Name* button in the top right of the screen.
3. Select the checkbox of the users to be added to the group.
4. Click **Apply**.

![Solution Groups for Managers and Employees](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/85orZxJjvh49NKyiyS-hG_jm-groupusersl.png "Solution Groups for Managers and Employees")

## Removing Users from Groups

Users can be removed from group membership. For example, a user changes positions in your organization and nolonger is a manager.

1. Click on the group name in the list.
2. On the **Permissions** screen, select the checkbox of the user to be removed from the group.
3. Click on the **Remove** link and click **Ok** to the remove message.



