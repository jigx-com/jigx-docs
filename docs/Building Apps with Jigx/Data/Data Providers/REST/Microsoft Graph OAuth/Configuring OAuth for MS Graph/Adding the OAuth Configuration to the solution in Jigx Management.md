---
title: Adding the OAuth Configuration to the solution in Jigx Management
slug: I2Eu-adding-the-oauth-configuration-to-the-solution-in-jigx-management
description: Learn how to easily add OAuth credentials to your Jigx Management solution with this step-by-step guide. Discover how to login, navigate to the Credentials section, and effortlessly add a new credential with a name and OAuth redirect URL. Find out how to 
createdAt: Mon Nov 21 2022 23:25:24 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Apr 29 2024 13:21:27 GMT+0000 (Coordinated Universal Time)
---

:::hint{type="info"}
To complete these steps, you must be an **Owner or Creator of the solution** in Jigx Management and **your **Jigx** solution has been published at least once** and is available in Jigx Management.
:::

1. Log in to Jigx Management at [https://manage.jigx.com](https://manage.jigx.com/) and open your solution.
2. In the menu on the left, click on **Credentials**.

![Solution Crenentials](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/wYELJKXpYN6O_jDEa1ClY_image.png "Solution Crenentials")

3. Click **Add Credential **on the top right of the screen.
4. **Enter a name** for the credential, for example, microsoft.OAuth.
5. Select **OAuth** as the type.
6. Enter the **OAuth redirect URL** you specified when configuring the OAuth app in Microsoft Azure. In the case of the default app, the redirect URL is [https://oauth.jigx.com/jigx/](https://oauth.jigx.com/jigx/). If you are configuring this for a Jigx Branded app replace /jigx/ with the name of the branded app as specified in its app configuration. For example, [https://oauth.jigx.com/nintex/](https://oauth.jiigx.com/nintex/)
7. Enter the **Application (Client) ID** copied from the Azure OAuth configuration in the **Client ID** field. 
8. Leave the **Secret field empty** for Microsoft openid-based OAuth.
9. Enter the **portion** of the URL copied from the **OpenID Connect metadata document** field in Azure in the **Issuer** field.
10. Add the **scopes** selected when the OAuth application was defined in Azure. Note that scopes are case-sensitive.
11. To allow a user to **switch accounts** when they are prompted during the OAuth loop, **expand the Options section** and replace the \{} with the following: \{"additionalParameters": \{"prompt": "select\_account"}}.
The **completed configuration** should be as follows:

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/FeMtP0NvdY1s70--W2mnA_image.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/FeMtP0NvdY1s70--W2mnA_image.png" size="40" width="878" height="1934" position="center" caption="Credentials" alt="Credentials"}

12. Click on **Save** to store the credential.

The **credential** is now ready for use in a function in a Jigx mobile app to prompt the user for their OAuth credentials when an API in Microsoft Graph is called. 

