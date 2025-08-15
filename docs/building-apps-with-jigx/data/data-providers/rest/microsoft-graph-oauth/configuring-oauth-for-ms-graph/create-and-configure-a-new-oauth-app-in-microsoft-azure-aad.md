---
title: Create and configure a new OAuth app in Microsoft Azure AAD
slug: X-IE-create-and-configure-a-new-oauth-app-in-microsoft-azure-aad
createdAt: Mon Nov 21 2022 22:30:28 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Apr 29 2024 13:12:03 GMT+0000 (Coordinated Universal Time)
description: >-
  Learn how to configure a Microsoft Azure OAuth app for seamless authentication
  with Microsoft Graph using this step-by-step guide. With detailed
  instructions, screenshots, and tips to create the app,
---

# Create and configure a new OAuth app in Microsoft Azure AAD

:::hint{type="info"} This topic is specific to Microsoft Azure OAuth and not a feature of Jigx. Jigx requires an OAuth app to authenticate with Microsoft Graph.

**To successfully complete these steps, you will need a Microsoft Office 365 Administrator account with access to the Azure Active Directory Administration portal.** :::

1.Login to [https://admin.microsoft.com](https://admin.microsoft.com/)

2\. Expand the menu on the left by clicking on the hamburger icon on the top left of the page.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/NUo6KSq4Vn-3HGrVj3Rl7\_graph-step1.png" size="40" position="center" caption="Microsoft Admin center" alt="Microsoft Admin center"}

3\. Click on the **three dots** next to Show All.

4\. Click on **Azure Active Directory** under Admin Centers.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/pDvsPCRHjIm0kuM-LPWah\_image.png" size="30" position="center" caption="AAD" alt="AAD"}

5\. In the left menu, click on **Enterprise Applications**.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/hPgD5UDazwLH3c58v1kLs\_image.png" size="30" position="center" caption="AAD admin center" alt="AAD admin center"}

6\. Click **New application** on the toolbar in the top middle of the page.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/glS1G3RKYWtz2YSxnYvqG\_image.png" size="40" position="center" caption="New application" alt="New application"}

7\. Click on **Create your own application** on the toolbar at the top of the page.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7HlGJXlBEk72kLkgPnezR\_image.png" size="40" position="center" caption alt="New application"}

8\. Enter a name for your app. In this document, we will use Jigx Mobile.

9\. Make sure **Integrate any other application you don't find in the gallery (Non-gallery)** is selected, and click on the **Create** button at the bottom of the screen.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/8UM4qkaP4Sa5VGk8FVQMb\_image.png" size="40" position="center" caption="New application" alt}

10\. Under Manage, click on **Properties**.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/eLQ8BurUBbGjf7ansgsf0\_image.png" size="40" position="center" caption="Properties" alt="Properties"}

11\. Set **Assignment required** to false and click on **Save** on the menu bar at the top left.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/TcDQRF7iYJGhg5IZORevC\_image.png" size="40" position="center" caption="New application" alt}

12\. Click on the \*\*application registration link \*\*at the top right of the page.

13\. Click on **Authentication** in the left menu.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/4YfDpXwaAoe0ctdnzVuMp\_image.png" size="40" position="center" caption="Authentication" alt="Authentication"}

14\. Click on **Add a platform**.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/W5kGnKf2yXFW0s7tPDmSt\_image.png" size="40" position="center" caption alt="Authentication"}

15\. Click on **Mobile and desktop applications**. **Do not** select iOS/macOS or Android.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/8m3H4MSa6irQtbns5rtwb\_image.png" size="40" position="center" caption="Applications" alt="Applications"}

16\. Select the **three checkboxes** and add [https://oauth.jigx.com/jigx/](https://oauth.jiigx.com/jigx/) in the custom URL section. If you are configuring this for a Jigx Branded app replace /jigx/ with the name of the branded app as specified in its app configuration. For example, [https://oauth.jigx.com/companyname/. ](https://oauth.jiigx.com/companyname/)Click on **Configure** to save the changes.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/umUofpRc-T5zTtlCKjjB2\_image.png" size="50" position="center" caption="Redirect URLs" alt="Redirect URLs"}

If you are planning on using **Postman** to test calls to Microsoft Graph using the Jigx Mobile OAuth configuration, click on Add URI and add the following URL: [https://oauth.pstmn.io/v1/callback](https://oauth.pstmn.io/v1/callback) then click on **Save** at the bottom of the screen.

17\. Click on\*\* API permissions\*\*. Depending on the functionality you want to expose to Jigx Mobile, you will have to specify specific API permissions, also referred to as scopes.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VjTPKfYwHW87qpjBo3Pdj\_image.png" size="40" position="center" caption="Scopes" alt="Scopes"}

18\. For this example, click on **Add a permission** and then **Microsoft Graph** at the top of the next screen.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2B9LSFwy5zX6Kg2P6UG-m\_image.png" size="40" position="center" caption="API permissions" alt="API permissions"}

19\. Click on **Delegated permissions** since we want the Jigx solution user to access the API using his identity and access rights.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7yfIHpb6iuyf-1tsqHqTD\_image.png" size="40" position="center" caption alt="API permissions"}

20\. Enable **email, openid, profile and User.Read, offline\_access**. These are the minimum scopes needed by Jigx to access the API. \*\*To find User.Read, \*\*enter it in the search box. Click on **Add permissions** at the bottom of the screen.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/eFrx-qU75Ld5GgGQ1H9Lp\_image.png" size="40" position="center" caption="API permissions" alt="API permissions"}

21\. Click on **Grant admin consent** on the toolbar above the API permissions. Your API permissions should look similiar to the image below.

![API permissions](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ouVtdCw3z8x0qdd5mJqO4_image.png)

22\. Click on **Overview** on the top left.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rgnKizK-RB5jbpWXw8W2u\_image.png" size="40" position="center" caption="API permissions overview" alt="API permissions overview"}

23\. Copy the **Application (Client) ID** and save this for later.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/7gbvElByph-l-owDoc2Lc\_image.png" size="44" position="center" caption="Application ID" alt="Application ID"}

24\. Click on **Endpoints** in the toolbar. Select the **portion of the URL** up to the / after v2.0 of the OpenID Connect metadata document field and save this for later.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/6x96Q3sKcuVvuBxNVWa9r\_image.png" size="80" position="center" caption="Endpoints" alt="Endpoints"}

25\. At this stage, the\*\* OAuth app \*\*is configured and ready to use.

In the next section, add the configuration to the Jigx solution in Jigx Management.
