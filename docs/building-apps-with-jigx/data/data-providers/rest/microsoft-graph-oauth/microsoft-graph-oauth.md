---
title: Microsoft Graph OAuth
slug: LkgK-microsoft-graph
createdAt: Sun Mar 26 2023 16:59:31 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon May 06 2024 15:10:22 GMT+0000 (Coordinated Universal Time)
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

# Microsoft Graph OAuth

This section contains steps to create an OAuth app for MS Graph, add the OAuth configuration to Jigx Management and then use the configuration in a Jigx solution. Various code samples showing how to use the Microsoft Graph API with the REST data provider are provided.

{% hint style="info" %}
To use Jigx with Microsoft Graph you will need an administrative account for Microsoft AAD to configure a Jigx Enterprise App, allowing Jigx to use OAuth authentication with Microsoft Graph.

Follow the steps in [Configuring OAuth for MS Graph](configuring-oauth-for-ms-graph/configuring-oauth-for-ms-graph.md) to configure OAuth for the Microsoft environment being used and add the necessary settings to Jigx Cloud.&#x20;
{% endhint %}

### Examples and code snippets

1. [Graph User Profile](https://docs.jigx.com/examples/graph-user-profile) - provides sample code to get a user's profile information from Microsoft Graph. It includes a [code sample](https://docs.jigx.com/examples/update-profile-photo) for updating a user's profile picture in Microsoft Graph.
2. [Graph Calendar](https://docs.jigx.com/examples/graph-calendar) - provides sample code to get a list of the user's calendars and renders a calendar in a schedule view on a jig. It includes a code sample on adding calendar entries to a user's Microsoft 365 calendar in Exchange.
3. [Graph Mail](https://docs.jigx.com/examples/graph-mail) - provides sample code to get a list of emails for a user and displays the emails in a list jig. Press on an email to view the content of the email.
4. [Graph tasks](https://docs.jigx.com/examples/graph-tasks) - provides sample code to get a list of To-do tasks for a user and displays the tasks in a list jig.
5. [Graph Insights](https://docs.jigx.com/examples/graph-insights) - provides sample code to get insights that include a list of documents trending around the user and displays the list in a list jig.
