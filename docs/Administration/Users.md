---
title: Users
slug: hy9S-users
createdAt: Tue Jun 07 2022 09:54:10 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Oct 02 2024 12:19:37 GMT+0000 (Coordinated Universal Time)
---

# Users

In the Users area, you can manage all users in your organization. All users who can log in to your organization's mobile app are listed here. You can only assign [Solutions](../administration/solutions/solutions.md) to users, who are in this list.

### User Overview

In the Users list, you can view each user's current **organizational role**, assigned solutions, and their invite status (_Active_ vs. _Invited_). **Click on a user's name** to see the user's details, manage the user's solutions and change their role for each assigned solution. You can also filter the user list by organizational role, invite status, and solution assignment.

<figure><img src="../.gitbook/assets/JM-UserOverL.png" alt="Managing Organization Users"><figcaption><p>Managing Organization Users</p></figcaption></figure>

### Inviting Users

{% hint style="info" %}
Before you can invite users to your organization via email, check the **Invites** setting in [Organization Settings](../administration/organization-settings/organization-settings.md). The language-specific invite templates have to be set up before you can start inviting users. At least one language and the corresponding invite template setup is required.
{% endhint %}

To add users to your organization, you need to invite them. Click on **Invite User** at the top right of the screen to open the side panel. Fill in the user's details, select a default language to be used for the invite email, and click **Invite**. Next assign [Solutions](../administration/solutions/solutions.md) to the invited user by clicking on the user's name in the list and then navigating to Solutions. Click on **Add solutions** at the top right of the screen to open the side panel. Select the solutions you want to assign to the user and click **Add solution**.

The user will receive an invite email with instructions on how to onboard. Once the user onboards successfully, the invite status will change to _Active_ in the user overview.

{% hint style="success" %}
To bulk invite users, contact Jigx support at _**support@jigx.com**_.
{% endhint %}

<figure><img src="../.gitbook/assets/JM-InviteL.png" alt="Inviting Users" width="563"><figcaption><p>Inviting Users</p></figcaption></figure>



### Re-inviting Users

If you want to re-invite the user because they did not accept your invitation or an error occurred, click on the user's name and click the **Resend invite** link at the top of the page. Next, select a language for the invite, a message displays stating that the invite has been sent.

{% hint style="warning" %}
If users don't receive the invite emails, ask them to **check their junk or spam email folder**.
{% endhint %}

### Assigning Solutions to Users

Click on the user's name in the list and navigate to the [Solutions](../administration/solutions/solutions.md) menu option by clicking on the solution icon in the left navigation pane, Click on **Add solutions** at the top right of the screen to open the side panel. Select the solutions you want to assign to the user and click **Add solution.**

<figure><img src="../.gitbook/assets/JM-AddSolutionL.png" alt="Assigning Solutions to User"><figcaption><p>Assigning Solutions to User</p></figcaption></figure>

### Assigning an Organization Role to Users

Each user in the user list has an **organization role** assigned. When you invite users, their default organization role is set to **User**. You can change the user's organization role by **clicking on the Organization role** in the user's profile. All changes made to the organization's roles take effect immediately. Refer to [Permissions - User Roles](<Permissions - User Roles.md>) to get a detailed overview on the roles used in an organization and solutions-level.

<figure><img src="../.gitbook/assets/JM-OrgPermissions (1).png" alt="Assign organizational permissions" width="563"><figcaption><p>Assign organizational permissions</p></figcaption></figure>

### Assigning a Solution Role to Users

Each user in the user list is assigned a solution role. When you invite users, or add solutions to users their default solution role is set to **User**. You can change the user's solution role by **clicking on the role** in the Role column. All changes made to the solution role takes effect immediately. Refer to [Permissions - User Roles](<Permissions - User Roles.md>) to get a detailed overview on the roles used in an organization and solutions-level.

<figure><img src="../.gitbook/assets/JMRolesD.png" alt="Solution Role Selection"><figcaption><p>Solution Role Selection</p></figcaption></figure>

### Remove a user from the organization

Click on the user's name in the list and click the **Remove from organization** button at the bottom left of the screen. You need `Admin` or `Owner` permissions to be able to remove a user from an organization.

<figure><img src="../.gitbook/assets/jm-removeuser.png" alt="Remove user from Organization" width="563"><figcaption><p>Remove user from Organization</p></figcaption></figure>

### Troubleshooting (User Profile)

Troubleshooting in Jigx Management helps identify problems when an app crashes, or when issues and errors occur while using and running solutions on the Jigx App. Think of this as runtime troubleshooting performed by support or your organization's administrator versus design time debugging which is available in the Jigx Builder for creators who are building solutions.

<figure><img src="../.gitbook/assets/JM-UserTroubleL.png" alt="User troubleshooting" width="563"><figcaption><p>User troubleshooting</p></figcaption></figure>

#### Jigx Management troubleshooting levels

There are three levels of troubleshooting in Jigx Management.

1. [Troubleshooting (Organization)](docId:pQc4nyhx_9tTLoyDm4MVu)- provides troubleshooting context for all users and solutions in that organization. The exact Correlation ID is required to start troubleshooting.
2. [Users](docId:hy9SNgXQZpRAbe51imv7Q) - provides troubleshooting context only for that specific user, and spans across all solutions assigned to that user
3. [Troubleshooting (Solution)](docId:tzQJID9go54bvHZap88co) - provides troubleshooting context only for that specific solution, and spans across users using that solution. When clicking on the Correlation ID the next level of detail shows who the user was at the top right of the screen.

#### Configure logging on the Jigx App

<figure><img src="../.gitbook/assets/JM-Troubleshooting.PNG" alt="Solution troubleshooting" width="563"><figcaption><p>Solution troubleshooting</p></figcaption></figure>

To configure logging on the mobile device perform the following steps:

1. Open the Jigx App on your mobile device
2. Click on your **Profile icon** in the top right-hand corner of the app
3. Tap **Troubleshooting**
4. The following settings are configurable:
   * **Error and crash logging** - enabled by default. Logs any errors displayed while using the app and logs when the app crashes
   * **Basic logging** - logs basic flow when using the solutions in the app
   * **Detailed logging** - logs errors, app crashes, and flow of the app, and exposes some data. Tap on the field to see the available categories. Enable the categories you require, use the _Selected_ tab to see what is enabled.
     * _Debug categories_ - select from the listed categories
     * _Trace Categories_ - Select from the listed categories

#### Use troubleshooting information

Troubleshooting allows you to drill down into the detail logged for each Correlation ID.

1. Click on the **Correlation ID** to drill down to see the log information.
2. The following levels are logged depending on the troubleshooting settings enabled on the mobile device: - WARNING - ERROR - DEBUG - INFO
3. **Category** - shows the area where the issue occurred such as REST-provider, action.sync.entities, or jig.default.
4. **Message**: Provides exact details of the issue such as execute failed, or Failed to sync entity 'user-profile/get-user..'.
5. Click on a specific level entry in the list to drill down into the log detail. The side pane opens displaying the solution Id, correlation Id, device id, App id, message, and additional parameters.
6. Use the copy to clipboard icon to use the values elsewhere.
