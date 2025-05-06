---
title: Permissions - User Roles
slug: R7Zn-user-roles
description: Learn how permissions are managed on the Jigx platform using User Roles. Discover the different types of roles - Organization Roles and Solution Roles - and understand how they determine a user's access and management capabilities within JigxManagement. G
createdAt: Thu Jun 09 2022 09:26:39 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Jan 15 2024 08:36:42 GMT+0000 (Coordinated Universal Time)
---

Permissions on the Jigx platform are managed with **User Roles**. There are two types namely, **Organization** and **Solution** roles. Roles describe what features and content a user can access and/or manage.

:::hint{type="info"}
If you do not see the tabs described in this section of the Jigx Management documentation, check that you have the correct permissions as described below.

## Organization Roles

To be able to log into Jigx Management you have to be an `admin`, `Owner`, or `Creator`. Organization roles are set in the [User Profile](./Users.md).

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/vxzq-89XQHaakzRvzlxGl_jm-orgpermissions.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/vxzq-89XQHaakzRvzlxGl_jm-orgpermissions.png" size="60" width="1078" height="1350" position="center" caption="Assign organizational permissions" alt="Assign organizational permissions"}

| **ACCESS**                                        | **OWNER**                       | **ADMIN**                       | **CREATOR**                    |
| ------------------------------------------------- | ------------------------------- | ------------------------------- | ------------------------------ |
| Log in to the Jigx Management                     | ✅                               | ✅                               | ✅                              |
| Users (View)                                      | ✅                               | ✅                               | ✅                              |
| Users (Invite/Remove)                             | ✅                               | ✅                               | ❌                              |
| Solutions (View)                                  | ✅&#xA;(All)                     | ✅<br />(All)                    | ✅&#xA;(Own)                    |
| Solutions - Widgets (Assign Groups)               | ❌<br />(requires solution role) | ❌<br />(requires solution role) | ❌&#xA;(requires solution role) |
| Solutions - Groups (Add/Remove)                   | ❌<br />(requires solution role) | ❌<br />(requires solution role) | ❌&#xA;(requires solution role) |
| Solutions - Permissions (Add/Remove/Manage)       | ✅                               | ✅                               | ❌&#xA;(requires solution role) |
| Solutions - Data (View)                           | ✅&#xA;(All)                     | ✅&#xA;(Own)                     | ✅&#xA;(Own)                    |
| Solutions - Data (Manage)                         | ❌&#xA;(requires solution role)  | ❌&#xA;(requires solution role)  | ❌&#xA;(requires solution role) |
| Solutions - Credentials (Manage)                  | ✅&#xA;(All)                     | ✅&#xA;(All)                     | ✅&#xA;(Own)                    |
| Solutions - Connections (Manage)                  | ✅&#xA;(All)                     | ✅&#xA;(All)                     | ✅&#xA;(Own)                    |
| Solutions - Preview/Run SQL, REST, SOAP Functions | ✅&#xA;(All)                     | ✅&#xA;(All)                     | ✅&#xA;(Own)                    |
| Notifications (View)                              | ✅&#xA;(Own)                     | ✅&#xA;(Own)                     | ❌                              |
| Notifications (Send)                              | ✅                               | ✅                               | ❌                              |
| Organizational Settings (Manage)                  | ✅                               | ❌                               | ❌                              |

## Solution Roles

Solution roles describe to what extent you can manage a solution in Jigx Management and use it at runtime on your mobile device. Solutions' roles are managed on the [Permissions](./Solutions/Permissions.md) tab.

![Solution Role](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/hm5_6VMKypZ8YNA6_1wuM_jm-userrolel.png "Solution Role")

| **ACCESS**                                           | **OWNER** | **ADMIN** | **EDITOR ** | **USER** |
| ---------------------------------------------------- | --------- | --------- | ----------- | -------- |
| Solution (Run on device)                             | ✅&#xA;    | ❌         | ❌           | ✅        |
| Solution (View in )                                  | ✅         | ✅         | ✅           | ❌        |
| Solution - Widgets (Assign Groups)                   | ✅         | ✅         | ❌           | ❌        |
| Solution - Groups (Add/Remove)                       | ✅         | ✅         | ❌           | ❌        |
| Solution - Permissions (Add/Remove/Manage)           | ✅         | ✅         | ❌           | ❌        |
| Solution - Data (Manage)                             | ✅         | ❌         | ❌           | ❌        |
| Solution - Credentials (Manage)                      | ✅         | ✅         | ✅           | ❌        |
| Solution - Connections (Manage)                      | ✅         | ✅         | ✅           | ❌        |
| Solution - Preview/Run SQL, REST, and SOAP Functions | ✅         | ✅         | ✅           | ❌        |

