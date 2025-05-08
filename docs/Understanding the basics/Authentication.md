---
title: Authentication
slug: 7E_k-authentication
description: Learn about the various authentication options available in JigxApp, including the Jigx User Manager and Jigx User Manager with Secondary credentials. Understand how data flows with REST and Microsoft SQL, and the importance of secure storage for OAuth co
createdAt: Wed Jun 07 2023 08:24:44 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Sep 11 2023 09:49:02 GMT+0000 (Coordinated Universal Time)
---

There are several options available to verify the identity of an individual using the Jigx App. The authentication options are:

:::ExpandableHeading
### Jigx User Manager

When a user logs into the app on a mobile device, they need to be <a href="http://manage.jigx.com/register" target="_blank">registered</a> in Jigx and assigned a Jigx account. This can either be through an email invitation, registering at [http://manage.jigx.com/register](http://manage.jigx.com/register), or requesting to join an organization on the app's Home Hub.  Jigx user manager uses AWS Cognito for Authentication. Passwords are encrypted and cannot be read by users in Jigx Cloud.

When the user signs in, the credentials are matched in Jigx Cloud, and if valid, a Jigx token is returned to the device, where it is stored in the device keychain. All subsequent calls are made using the Jigx token in an SSL tunnel.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/KS2j3hhgoPgrdC1rs4TH__jigxauth.gif" size="80" position="center" caption}
:::

:::ExpandableHeading
### Jigx User Manager with Secondary credentials

Jigx user manager with Secondary credentials or authentication providers. This requires users to sign in with their Jigx user credentials and secondary credentials such as Microsoft or Salesforce. Secondary credentials are set up on a solution using OAuth. The OAuth is referenced by name in the REST (OAuth) function call.

An organization is configured for auto provisioning or a per-user invite, requiring administrative approval. The AAD or Okta configuration is stored in AWS-secured storage in Jigx Cloud. When the user signs in, the configuration for the organization is retrieved and sent to the mobile device. The configuration information runs the user through an OAuth loop with the configured external IDP, AAD, or Okta.

When auto-provisioning is enabled, if the user is validated by AAD or Okta and does not yet exist in the organization, Jigx will automatically create the user and do the necessary Jigx token creation and assignment. If the user exists in the Jigx Cloud and is authenticated successfully by AAD or Okta, the user is assigned a Jigx token for all subsequent calls. If the organization does not enable auto-provisioning, the user can request access, which needs to be approved by an administrator. Once approved, the user will be provisioned in Jigx.

- See [REST Authentication](<./../Building Apps with Jigx/Data/Data Providers/REST/REST Authentication.md>) for OAuth configuration steps in Jigx Management
- See [Create and configure a new OAuth app in Microsoft Azure AAD](<./../Building Apps with Jigx/Data/Data Providers/REST/Microsoft Graph OAuth/Configuring OAuth for MS Graph/Create and configure a new OAuth app in Microsoft Azure AAD.md>)
- See [Configuring OAuth for MS Graph](<./../Building Apps with Jigx/Data/Data Providers/REST/Microsoft Graph OAuth/Configuring OAuth for MS Graph.md>)

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/5S388_dxAsUNinE66FD5b_jigxauth2nd.gif" size="80" position="center" }

**Data flow with REST**

1. Jigx fetches the solution definition with a valid Jigx token.
2. Function calls are made to the [REST](<./../Building Apps with Jigx/Data/Data Providers/REST.md>)-enabled cloud service using the Jigx Cloud as a proxy, for example, for IP Allowlisting. The function calls can use OAuth, secrets, and tokens, but not basic authentication. OAuth configuration, secrets, tokens, and basic authentication are securely encrypted and stored in AWS. They are not user readable and are only used when the function call is made by a device with a valid Jigx token. The result is processed in the Jigx Cloud, including all function transforms, continuation, and error transforms, and sent to the device. The data is never stored in the Jigx Cloud and is only ever kept in memory while the function is executing. Function calls can be made directly from the device to the REST-enabled cloud service using the [local execution model](<./../Building Apps with Jigx/Data/Data Providers/REST/Local REST Calls.md>).
3. OAuth configuration, secrets, and tokens are stored in the secure keychain on the device when the solution definition is synced.  The result is processed on the device, including all function transforms, continuation, and error transforms, and the result is stored in SQLite on the device. The data never travels through the Jigx Cloud. SQL Server is currently not supported for local on-device execution.

**Data flow with Microsoft SQL**

1. Jigx fetches the solution definition with a valid Jigx token.
2. Jigx function calls are made from the device to SQL Azure or Microsoft SQL Server, using the Jigx Cloud as a proxy, for IP Allowlisting. The function calls use the connection configuration stored as a secure encrypted secret in Jigx Cloud on AWS. The SQL credentials are never sent to the mobile device. Once saved, the SQL credentials are not user readable and are only used by the Jigx Cloud when the function call is made by a device with a valid Jigx token. The result is processed in the Jigx Cloud, including all function transforms, continuation, and error transforms, and sent to the device. The data is never stored in the Jigx Cloud and is only ever kept in memory while the function is executing.
:::

:::ExpandableHeading
### Single Sign-on (SSO)

[Single Sign-On (SSO)](<./../Administration/Organization Settings/Single Sign-On _SSO_.md>) authenticates the user against a 3rd Party Identity Provider (IDP). When a user logs into the app, Jigx checks if SSO is enabled for the organization, the check is based on the domain of the emails linked to the organization. Next, the OAuth configuration is checked to see if it points to the same domain. The OAuth redirect URL is verified for a match against the app configuration. The user is then authenticated against the 3rd party IDP. If the user is a match in Jigx and the 3rd party IDP, a Jigx access token is generated, and the user is granted access to the app. SSO is enabled in Jigx Management on an organizational level. The diagram below explains the Jigx SSO flow. See the [Single Sign-On (SSO)](<./../Administration/Organization Settings/Single Sign-On _SSO_.md>) and [OAuth Configurations](<./../Administration/Organization Settings/OAuth Configurations.md>) sections to learn how to enable SSO and OAuth.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/8lp09AVrYKq3fhu8hxSEr_sso.gif" size="80" position="center" }


:::





