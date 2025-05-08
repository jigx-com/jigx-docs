---
title: Notifications
slug: d3Ua-notifications
description: Discover how Jigx simplifies the process of sending notifications through push or in-app notifications. With the flexibility to send notifications via JigxManagement or programmatically, easily reach specific users, organizations, or tailored audiences. C
createdAt: Tue Jun 07 2022 09:54:54 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Oct 02 2024 11:27:47 GMT+0000 (Coordinated Universal Time)
---

Notifications are a powerful feature allowing you to engage with your users. With Jigx, notifications are delivered to your users as push notifications (OS-level) and in-app notifications (on the notifications tab). You can send Notifications using Jigx Management or programmatically in your solutions, see [Notifications](<./../Building Apps with Jigx/Additional functionality/Notifications.md>). Notifications can be configured to send to a single user, the entire organization, users of a specific solution, and even users of a specific jig in a specific solution.

::Image[]{alt="In-app & push notifications" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7b3RWMHmrLLf2Li44h3sC_jm-notifications.PNG" size="74" caption="In-app & push notifications" position="center" }

![Notifications list](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/sy-ULx52L4IPdaraUQSkz_jm-notiflistl.png "Notifications list")

## Notifications Overview

The notifications list shows all notifications being sent from your account, either via Jigx Management or programmatically in a solution. Notifications are put on a queue and the current status of your notification delivery is displayed in the first column. You can check the details of the notification by clicking on the notification title.

:::hint{type="info"}
Typically all notifications are delivered **within a 60 seconds timeframe**.
:::

![Notification Details](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/gAXoIGhFvg8bMwCJcNKxm_jm-notifyeditl.png "Notification Details")

## Configure sending a Notification

Create notifications in Jigx Managementby following the steps below:

1. Click on **Send notification** at the top of the screen to open the side pane.
2. Add a title and content, you can use Emojis 🎉 if you want. Both title and content will be displayed to the user in the push notification and in-app notification preview on their devices.
3. Next, decide who your target audience will be:

- **Users**: Send to specific users, e.g. John and Mary. Click the *+ choose specific users* to select users from the organization's global user's list.
- **Solution**: Send to all users that have a specific solution assigned to them, e.g. all users who use the sample-crm solution. Select the solution name from the *Solution dropdown* list.
- **Solution Groups**: Send to all users that are in a group of a specific solution, e.g. all managers using sample-crm. Select the solution name from the *Solution* dropdown, then select the group name from the *Groups* area. If no groups exist on the solution, no group names will display in the area.
- **Organization**: Send to all users in the Organization.

4. On the *Target a specific jig (optional)* tab, select the jigin a specific solution that will trigger the notification. This is an optional step. For example, if sales employees tap on your push notification, the mobile app will navigate directly to their list of all open opportunities.
5. Set input parameters for the jig based on key/value pairs (e.g. accountID / 123456). The solution creator needs to ensure the input parameters are processed.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-9QLHLp1ZBs9aMo88JKpFQ-20241002-112429.png" size="94" position="center" caption="Configuring a notification" alt="Configuring a notification"}

## Notification URL per region

| **Region**                  | **URL**                                                                                                                                                                                                               |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| US                          | <a href="https://us-east-1.api.jigx.com/v2.0/tool/organizations/{organizationId}/notifications" target="_blank"> https\://us-east-1.api.jigx.com/v2.0/tool/organizations/\{organizationId}/notifications</a>          |
| South East (e.g. Australia) | <a href="https://ap-southeast-2.api.jigx.com/v2.0/tool/organizations/{organizationId}/notifications" target="_blank">https\://ap-southeast-2.api.jigx.com/v2.0/tool/organizations/\{organizationId}/notifications</a> |
| Europe                      | <a href="https://eu-central-1.api.jigx.com/v2.0/tool/organizations/{organizationId}/notifications" target="_blank">https\://eu-central-1.api.jigx.com/v2.0/tool/organizations/\{organizationId}/notifications</a>     |

