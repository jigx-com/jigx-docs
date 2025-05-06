---
title: My profile
slug: PCpY-my-profile
description: Learn how to effectively manage your profile on a platform with this comprehensive document. Discover step-by-step instructions on accessing and navigating your profile, modifying organization roles, seamlessly switching between organizations, and handlin
createdAt: Mon Mar 06 2023 12:54:07 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Oct 02 2024 12:18:36 GMT+0000 (Coordinated Universal Time)
---

You can access your profile either by clicking on your name in the bottom left of the screen and selecting *My profile* from the menu, or by finding and clicking on your name in the [Users](./Users.md) list. You can easily change *organization roles*, quickly *switch between organizations*, *disable a user*, or *remove a user from an organization*.

<!--
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-40AWNKc-Ai3UlKLD2hcMd-20241002-121213.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-40AWNKc-Ai3UlKLD2hcMd-20241002-121213.png" darkSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-40AWNKc-Ai3UlKLD2hcMd-20241002-121213.png" size="60" width="1582" height="1598" darkWidth="1582" darkHeight="1598" position="center" caption="User Profile screen" alt="User Profile screen"}
-->
<!--![User Profile screen](../../assets/user-profile-screen.png "User Profile screen")-->
<img src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-40AWNKc-Ai3UlKLD2hcMd-20241002-121213.png" size="60" width="1582" height="1598" darkWidth="1582" darkHeight="1598" position="center" caption="User Profile screen" alt="User Profile screen" />

### Organization Role

Here you can see your role in the organization and if you have Admin permissions, you can easily change that role. For more information about the capabilities and permissions of each role, see [Permissions - User Roles](<./Permissions - User Roles.md>).

<!--::Image[]{alt="Role selection" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dUNCLYwYRMNru8sazzrBg_screenshot-2023-03-06-at-161152.png" size="32" width="654" height="518" caption="Role selection" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dUNCLYwYRMNru8sazzrBg_screenshot-2023-03-06-at-161152.png"-->
<img src="(https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dUNCLYwYRMNru8sazzrBg_screenshot-2023-03-06-at-161152.png" size="32" width="654" height="518" caption="Role selection" position="center" />

### All organizations

The list of organizations will only be displayed if you are a member of more than one organization. This impacts your mobile experience and may not be suitable in cases where you want to use apps from different brands. If you belong to more than one organization, you can also change your default organization. The list of organizations include a solution count indicating the number of solutions you are assigned to. Simply switch organizations by clicking on the organization you want to access.

<!--::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/migVYS4zy1AIIXpNDEYh6_jm-solutioncount.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/migVYS4zy1AIIXpNDEYh6_jm-solutioncount.png" size="70" width="1642" height="1560" position="center" caption="Organization with solution count" alt="Organization with solution count"}-->
<img src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/migVYS4zy1AIIXpNDEYh6_jm-solutioncount.png" size="70" width="1642" height="1560" position="center" caption="Organization with solution count" alt="Organization with solution count" />

<!--::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/5rc2fVAUxWokQ-San_PJI_screenshot-2023-03-06-at-162214.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/5rc2fVAUxWokQ-San_PJI_screenshot-2023-03-06-at-162214.png" size="44" width="662" height="230" position="center" caption="Change organizations in management" alt="Change organizations in management"}-->
![Change organizations in management](../../assets/change-organizations-in-management.png "Change organizations in management")

### Advanced actions

Other features include the ability to disable users or remove users from an organization. Before performing these actions, make sure that you have selected the correct user. The advanced actions are only available to people who have Admin and Owner permission. For more information about the capabilities and permissions of each role, see [Permissions - User Roles](<./Permissions - User Roles.md>).

### Personal Access Tokens (PAT)

You can create a personal access token on your Jigx profile that is used in the authorization header of a REST call to Jigx APIs.

- PAT is only accessible under your own user profile.
- Expiry is set for six months after creation.
- The lease for the token auto-extends with two weeks since last use.
- You can extend the lease manually by two weeks. This ensures that the PAT is not kept alive if it isn't used.

**Create a personal access token** by:

![Add personal access token](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/RfNiCAVMSSNmvZdc9a_0E_jm-patcreate.png "Add personal access token")

1. Log into Jigx Management.
2. Open my profile and select the **Personal Access Tokens** menu option.
3. Click the **Add New Token** button, the side pane opens.
4. Click the **Add** button at the bottom of the pane. A secret is generated for you. Make sure you use the **copy key** to copy the secrect to a safe location for use as the secret is onnly shown once.

**Extend the lease of a personal access token** by two weeks:

![Extend token](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Joan23MWAMu_Zt46jJXAM_jm-patextend.png "Extend token")

1. Log into Jigx Management.
2. Open my profile and select the **Personal Access Tokens** menu option.
3. Click on the token to be extended, in the side pane that opens click the **Extend lease** button. You will see the lease expires date in the list is updated by two weeks.

**Delete the personal access token** by:

1. Log into Jigx Management.
2. Open my profile and select the **Personal Access Tokens** menu option.
3. Click on the token you want to delete, in the side pane that opens click the **Delete** button at the bottom of the pane.

