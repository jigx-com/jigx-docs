---
title: Organization Settings
slug: KsWo-organization-settings
description: Learn how to configure global organization settings in JigxManagement with this comprehensive document. From organization details to OAuth configurations and single sign-on (SSO), explore all the essential topics to optimize your JigxManagement experience
createdAt: Tue Jun 07 2022 15:07:56 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Oct 02 2024 12:00:37 GMT+0000 (Coordinated Universal Time)
---

As an `ADMIN` or `OWNER` of an organization, you can configure global organization settings in Jigx Management in the **Organization Settings** area.

![Organization Details](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-HE2O4_wN8Dino8kzPyjZR-20241002-113229.png "Organization Details")

## Organization Details

Here you can view the name of your organization and its description, add an external facing marketing URL of your organization, copy your organization's Id, and cloud server region. &#x20;

## Invites

You can invite new [Users](./Users.md) to join your organization and let them receive emails with instructions on how to onboard. Your organization has already been set up with default invite settings. The email invite can be customized to align with your organization's branding or add multiple language email templates.&#x20;

![Configuring email invites](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/QBLXU_93Hzjd1UHS8_Ocl_jm-inviteorg.png "Configuring email invites")

The following configuration is available:

- [Default invite template](<./Organization Settings/Invites.md>)
- [Customize the invite template](<./Organization Settings/Invites.md>)
- [Add invite language templates](<./Organization Settings/Invites.md>)
- [Sending an invite in a specific language](<./Organization Settings/Invites.md>)

## Advanced Settings

In the Advanced Settings screen add the email address where request emails will be sent. In this instance request emails are sent from the mobile app if a user has downloaded the app, tries to log in and has not been invited by your organization. A message will display on the app allowing the user to request access.&#x20;

- **Off (will not be discoverable during registration) **- when this option is set users registering with the same domain as the organization will not be able to join your organization during the registration process. You will need to manually add them to the organization.
- **Request to join (needs approval from owners)** - a request to join will be sent and requires approval for users registering with the same domain as the organization.
- **Automatic can join without approval** - users registering with the same domain as the organization will automatically be added to the organization.

**Jigx support access **- determine the level of access that Jigx support has in Jigx Management to your organization. There are two levels of access you can choose between *Read *or *Write*.&#x20;

![Advanced Settings](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VDOa9z1L0rO_fJwLpL2iD_jm-advancedl.png "Advanced Settings")

**Set **Jigx Management** idle timeout **- Set an *Idle logout* option for Jigx Management. This is an optional security setting that once applied will display a prompt and then log the person out of Jigx Management after being idle for the configured period. Enabling the checkbox has a default of 120 minutes, but is configurable to any number of minutes.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VDzv8idkuNsRXLYUoukpv_jm-idletimeout.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VDzv8idkuNsRXLYUoukpv_jm-idletimeout.png" size="80" width="1736" height="894" position="center" caption="Idle timeout setting " alt="Idle timeout setting "}

## Organization Limits

The organization limits allow you as the organization's owner to view the number of members and solutions in the organization. In the Solution Limit template section set the number of members allowed on new solutions, then restrict the number of rows of data and files allowed per solution.&#x20;

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-VCMpFrybgVQQK23Gj6Ve_-20241002-114414.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-VCMpFrybgVQQK23Gj6Ve_-20241002-114414.png" size="90" width="1870" height="1198" position="center" caption}

## Public Content

Public content allows you to setup links that are visible on your organization's app before a user has onboarded or logged in. For example, a link to a public solution, privacy policy link, your organization's website, or a link to request access to the app. When submitting branded apps to the app stores for publishing it is recommended to include a privacy link as the stores might require you to provide sufficient warning to your users regarding tracking of data and cookies. For configuration details see [Public Content](<./Organization Settings/Public Content.md>).

![Public Content configuration](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/51bc_oWXE11NpGX5dIS1c_jm-publicnew.png "Public Content configuration")

## OAuth Configurations

Use the [OAuth Configurations](<./Organization Settings/OAuth Configurations.md>) option to configure mutiple OAuth configurations at a global organizational level that can be used in SSO and applied to multiple solutions.

## Single Sign-On (SSO)

Configure [Single Sign-On (SSO)](<./Organization Settings/Single Sign-On _SSO_.md>) for your organization, enable auto -provisioning of users and automatically assign solutions to be available on auto-provisioned users apps.  &#x20;

## Organization Secrets

Add your organization's secrets for use in all app solutions. The name you give the secret must match an existing oAuth configuration Client Id. Add the secret to the Secret Value field.&#x20;

