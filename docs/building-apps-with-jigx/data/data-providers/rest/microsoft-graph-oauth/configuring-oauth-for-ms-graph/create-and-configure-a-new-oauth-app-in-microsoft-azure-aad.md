---
title: Create and configure a new OAuth app in Microsoft Azure AAD
slug: X-IE-create-and-configure-a-new-oauth-app-in-microsoft-azure-aad
createdAt: Mon Nov 21 2022 22:30:28 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Apr 29 2024 13:12:03 GMT+0000 (Coordinated Universal Time)
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

# Create and configure a new OAuth app in Microsoft Azure AAD

{% hint style="info" %}
This topic is specific to Microsoft Azure OAuth and not a feature of Jigx. Jigx requires an OAuth app to authenticate with Microsoft Graph.

To successfully complete these steps, you will need a Microsoft Office 365 Administrator account with access to the Azure Active Directory Administration portal.&#x20;
{% endhint %}

1.Login to [https://admin.microsoft.com](https://admin.microsoft.com/)

2\. Expand the menu on the left by clicking on the hamburger icon on the top left of the page.

<figure><img src="../../../../../../.gitbook/assets/Graph-Step1.png" alt="Microsoft Admin center" width="375"><figcaption><p>Microsoft Admin center</p></figcaption></figure>

3\. Click on the **three dots** next to Show All.

4\. Click on **Azure Active Directory** under Admin Centers.

<figure><img src="../../../../../../.gitbook/assets/Graph-AAD.png" alt="AAD" width="375"><figcaption><p>AAD</p></figcaption></figure>

5\. In the left menu, click on **Enterprise Applications**.

<figure><img src="../../../../../../.gitbook/assets/Graph-AdminCenter.png" alt="AAD admin center" width="375"><figcaption><p>AAD admin center</p></figcaption></figure>

6\. Click **New application** on the toolbar in the top middle of the page.

<figure><img src="../../../../../../.gitbook/assets/Graph-newApp.png" alt="New application" width="375"><figcaption><p>New application</p></figcaption></figure>

7\. Click on **Create your own application** on the toolbar at the top of the page.

<figure><img src="../../../../../../.gitbook/assets/Graph-OwnApp.png" alt="New application" width="375"><figcaption><p>New application</p></figcaption></figure>

8\. Enter a name for your app. In this document, we will use Jigx Mobile.

9\. Make sure **Integrate any other application you don't find in the gallery (Non-gallery)** is selected, and click on the **Create** button at the bottom of the screen.

<figure><img src="../../../../../../.gitbook/assets/Graph-jigxApp.png" alt="New application" width="375"><figcaption><p>New application</p></figcaption></figure>

10\. Under Manage, click on **Properties**.

<figure><img src="../../../../../../.gitbook/assets/Graph-properties.png" alt="Properties" width="375"><figcaption><p>Properties</p></figcaption></figure>

11\. Set **Assignment required** to false and click on **Save** on the menu bar at the top left.

<figure><img src="../../../../../../.gitbook/assets/Graph-assignment.png" alt="New application" width="375"><figcaption><p>New application</p></figcaption></figure>

12\. Click on the **application registration link** at the top right of the page.

13\. Click on **Authentication** in the left menu.

<figure><img src="../../../../../../.gitbook/assets/Graph-jigxAuth.png" alt="Authentication" width="375"><figcaption><p>Authentication</p></figcaption></figure>

14\. Click on **Add a platform**.

<figure><img src="../../../../../../.gitbook/assets/Grahp-platform.png" alt="Authentication" width="375"><figcaption><p>Authentication</p></figcaption></figure>

15\. Click on **Mobile and desktop applications**. **Do not** select iOS/macOS or Android.

<figure><img src="../../../../../../.gitbook/assets/Graph-Apps.png" alt="Applications" width="375"><figcaption><p>Applications</p></figcaption></figure>

16\. Select the **three checkboxes** and add [https://oauth.jigx.com/jigx/](https://oauth.jiigx.com/jigx/) in the custom URL section. If you are configuring this for a Jigx Branded app replace /jigx/ with the name of the branded app as specified in its app configuration. For example, [https://oauth.jigx.com/companyname/. ](https://oauth.jiigx.com/companyname/)Click on **Configure** to save the changes.

<figure><img src="../../../../../../.gitbook/assets/Graph-desktop.png" alt="Redirect URLs" width="375"><figcaption><p>Redirect URLs</p></figcaption></figure>

If you are planning on using **Postman** to test calls to Microsoft Graph using the Jigx Mobile OAuth configuration, click on Add URI and add the following URL: [https://oauth.pstmn.io/v1/callback](https://oauth.pstmn.io/v1/callback) then click on **Save** at the bottom of the screen.

17\. Click on **API permissions**. Depending on the functionality you want to expose to Jigx Mobile, you will have to specify specific API permissions, also referred to as scopes.

<figure><img src="../../../../../../.gitbook/assets/Graph-scopes.png" alt="Scopes" width="375"><figcaption><p>Scopes</p></figcaption></figure>

18\. For this example, click on **Add a permission** and then **Microsoft Graph** at the top of the next screen.

<figure><img src="../../../../../../.gitbook/assets/Graph-APIPerm.png" alt="API permissions" width="375"><figcaption><p>API permissions</p></figcaption></figure>

19\. Click on **Delegated permissions** since we want the Jigx solution user to access the API using his identity and access rights.

<figure><img src="../../../../../../.gitbook/assets/Graph-delgatePerm.png" alt="API permissions" width="375"><figcaption><p>API permissions</p></figcaption></figure>

20\. Enable **email, openid, profile and User.Read, offline\_access**. These are the minimum scopes needed by Jigx to access the API. **To find User.Read,** enter it in the search box. Click on **Add permissions** at the bottom of the screen.

<figure><img src="../../../../../../.gitbook/assets/Graph-AddAPIPerm.png" alt="API permissions" width="375"><figcaption><p>API permissions</p></figcaption></figure>

21\. Click on **Grant admin consent** on the toolbar above the API permissions. Your API permissions should look similar to the image below.

<figure><img src="../../../../../../.gitbook/assets/Graph-GrantConsent.png" alt="API permissions"><figcaption><p>API permissions</p></figcaption></figure>

22\. Click on **Overview** on the top left.

<figure><img src="../../../../../../.gitbook/assets/Graph-overview.png" alt="API permissions overview" width="375"><figcaption><p>API permissions overview</p></figcaption></figure>

23\. Copy the **Application (Client) ID** and save this for later.

<figure><img src="../../../../../../.gitbook/assets/Graph-APIID.png" alt="Application ID" width="375"><figcaption><p>Application ID</p></figcaption></figure>

24\. Click on **Endpoints** in the toolbar. Select the **portion of the URL** up to the / after v2.0 of the OpenID Connect metadata document field and save this for later.

<figure><img src="../../../../../../.gitbook/assets/Graph-endpoints.png" alt="Endpoints"><figcaption><p>Endpoints</p></figcaption></figure>

25\. At this stage, the **OAuth app** is configured and ready to use.

In the next section, add the configuration to the Jigx solution in Jigx Management.
