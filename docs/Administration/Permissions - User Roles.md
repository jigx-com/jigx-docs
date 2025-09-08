---
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# Permissions - User Roles

Permissions on the Jigx platform are managed with **User Roles**. There are two types namely, **Organization** and **Solution** roles. Roles describe what features and content a user can access and/or manage.

{% hint style="info" %}
If you do not see the tabs described in this section of the Jigx Management documentation, check that you have the correct permissions as described below.
{% endhint %}

## Organization Roles

To be able to log into Jigx Management you have to be an `admin`, `Owner`, or `Creator`. Organization roles are set in the [User Profile](Users.md).

<figure><img src="../.gitbook/assets/JM-OrgPermissions.png" alt="Assign organizational permissions" width="563"><figcaption><p>Assign organizational permissions</p></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ACCESS</th><th width="184.4296875">OWNER</th><th>ADMIN</th><th>CREATOR</th></tr></thead><tbody><tr><td>Log in to the Jigx Management</td><td>✅</td><td>✅</td><td>✅</td></tr><tr><td>Users (View)</td><td>✅</td><td>✅</td><td>✅</td></tr><tr><td>Users (Invite/Remove)</td><td>✅</td><td>✅</td><td>❌</td></tr><tr><td>Solutions (View)</td><td>✅ (All)</td><td>✅ (All)</td><td>✅ (Own)</td></tr><tr><td>Solutions - Widgets (Assign Groups)</td><td>❌ (requires solution role)</td><td>❌ (requires solution role)</td><td>❌ (requires solution role)</td></tr><tr><td>Solutions - Groups (Add/Remove)</td><td>❌ (requires solution role)</td><td>❌ (requires solution role)</td><td>❌ (requires solution role)</td></tr><tr><td>Solutions - Permissions (Add/Remove/Manage)</td><td>✅</td><td>✅</td><td>❌ (requires solution role)</td></tr><tr><td>Solutions - Data (View)</td><td>✅ (All)</td><td>✅ (Own)</td><td>✅ (Own)</td></tr><tr><td>Solutions - Data (Manage)</td><td>❌ (requires solution role)</td><td>❌ (requires solution role)</td><td>❌ (requires solution role)</td></tr><tr><td>Solutions - Credentials (Manage)</td><td>✅ (All)</td><td>✅ (All)</td><td>✅ (Own)</td></tr><tr><td>Solutions - Connections (Manage)</td><td>✅ (All)</td><td>✅ (All)</td><td>✅ (Own)</td></tr><tr><td>Solutions - Preview/Run SQL, REST, SOAP Functions</td><td>✅ (All)</td><td>✅ (All)</td><td>✅ (Own)</td></tr><tr><td>Notifications (View)</td><td>✅ (Own)</td><td>✅ (Own)</td><td>❌</td></tr><tr><td>Notifications (Send)</td><td>✅</td><td>✅</td><td>❌</td></tr><tr><td>Organizational Settings (Manage)</td><td>✅</td><td>❌</td><td>❌</td></tr></tbody></table>

## Solution Roles

Solution roles describe to what extent you can manage a solution in Jigx Management and use it at runtime on your mobile device. Solutions' roles are managed on the [Permissions](../administration/solutions/permissions.md) tab.

<figure><img src="../.gitbook/assets/JM-UserRoleL.png" alt="Solution Role" width="563"><figcaption><p>Solution Role</p></figcaption></figure>

<table><thead><tr><th width="216.46875">ACCESS</th><th>OWNER</th><th>ADMIN</th><th>EDITOR</th><th>USER</th></tr></thead><tbody><tr><td>Solution (Run on device)</td><td>✅</td><td>❌</td><td>❌</td><td>✅</td></tr><tr><td>Solution (View in )</td><td>✅</td><td>✅</td><td>✅</td><td>❌</td></tr><tr><td>Solution - Widgets (Assign Groups)</td><td>✅</td><td>✅</td><td>❌</td><td>❌</td></tr><tr><td>Solution - Groups (Add/Remove)</td><td>✅</td><td>✅</td><td>❌</td><td>❌</td></tr><tr><td>Solution - Permissions (Add/Remove/Manage)</td><td>✅</td><td>✅</td><td>❌</td><td>❌</td></tr><tr><td>Solution - Data (Manage)</td><td>✅</td><td>❌</td><td>❌</td><td>❌</td></tr><tr><td>Solution - Credentials (Manage)</td><td>✅</td><td>✅</td><td>✅</td><td>❌</td></tr><tr><td>Solution - Connections (Manage)</td><td>✅</td><td>✅</td><td>✅</td><td>❌</td></tr><tr><td>Solution - Preview/Run SQL, REST, and SOAP Functions</td><td>✅</td><td>✅</td><td>✅</td><td>❌</td></tr></tbody></table>
