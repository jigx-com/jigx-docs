# Permissions - User Roles

Permissions on the Jigx platform are managed with **User Roles**. There are two types namely, **Organization** and **Solution** roles. Roles describe what features and content a user can access and/or manage.

:::hint{type="info"} If you do not see the tabs described in this section of the Jigx Management documentation, check that you have the correct permissions as described below. :::

## Organization Roles

To be able to log into Jigx Management you have to be an `admin`, `Owner`, or `Creator`. Organization roles are set in the [User Profile](Users.md).

![Assign organizational permissions](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/vxzq-89XQHaakzRvzlxGl_jm-orgpermissions.png)

| **ACCESS**                                        | **OWNER**                  | **ADMIN**                  | **CREATOR**                |
| ------------------------------------------------- | -------------------------- | -------------------------- | -------------------------- |
| Log in to the Jigx Management                     | ✅                          | ✅                          | ✅                          |
| Users (View)                                      | ✅                          | ✅                          | ✅                          |
| Users (Invite/Remove)                             | ✅                          | ✅                          | ❌                          |
| Solutions (View)                                  | ✅ (All)                    | ✅ (All)                    | ✅ (Own)                    |
| Solutions - Widgets (Assign Groups)               | ❌ (requires solution role) | ❌ (requires solution role) | ❌ (requires solution role) |
| Solutions - Groups (Add/Remove)                   | ❌ (requires solution role) | ❌ (requires solution role) | ❌ (requires solution role) |
| Solutions - Permissions (Add/Remove/Manage)       | ✅                          | ✅                          | ❌ (requires solution role) |
| Solutions - Data (View)                           | ✅ (All)                    | ✅ (Own)                    | ✅ (Own)                    |
| Solutions - Data (Manage)                         | ❌ (requires solution role) | ❌ (requires solution role) | ❌ (requires solution role) |
| Solutions - Credentials (Manage)                  | ✅ (All)                    | ✅ (All)                    | ✅ (Own)                    |
| Solutions - Connections (Manage)                  | ✅ (All)                    | ✅ (All)                    | ✅ (Own)                    |
| Solutions - Preview/Run SQL, REST, SOAP Functions | ✅ (All)                    | ✅ (All)                    | ✅ (Own)                    |
| Notifications (View)                              | ✅ (Own)                    | ✅ (Own)                    | ❌                          |
| Notifications (Send)                              | ✅                          | ✅                          | ❌                          |
| Organizational Settings (Manage)                  | ✅                          | ❌                          | ❌                          |

## Solution Roles

Solution roles describe to what extent you can manage a solution in Jigx Management and use it at runtime on your mobile device. Solutions' roles are managed on the [Permissions](../administration/solutions/permissions.md) tab.

![Solution Role](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/hm5_6VMKypZ8YNA6_1wuM_jm-userrolel.png)

| **ACCESS**                                           | **OWNER** | **ADMIN** | **EDITOR** | **USER** |
| ---------------------------------------------------- | --------- | --------- | ---------- | -------- |
| Solution (Run on device)                             | ✅         | ❌         | ❌          | ✅        |
| Solution (View in )                                  | ✅         | ✅         | ✅          | ❌        |
| Solution - Widgets (Assign Groups)                   | ✅         | ✅         | ❌          | ❌        |
| Solution - Groups (Add/Remove)                       | ✅         | ✅         | ❌          | ❌        |
| Solution - Permissions (Add/Remove/Manage)           | ✅         | ✅         | ❌          | ❌        |
| Solution - Data (Manage)                             | ✅         | ❌         | ❌          | ❌        |
| Solution - Credentials (Manage)                      | ✅         | ✅         | ✅          | ❌        |
| Solution - Connections (Manage)                      | ✅         | ✅         | ✅          | ❌        |
| Solution - Preview/Run SQL, REST, and SOAP Functions | ✅         | ✅         | ✅          | ❌        |
