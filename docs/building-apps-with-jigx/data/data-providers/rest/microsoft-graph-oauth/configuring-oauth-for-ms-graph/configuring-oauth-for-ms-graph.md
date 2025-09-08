---
title: Configuring OAuth for MS Graph
slug: lrK_-configuring-oauth-for-ms-graph
createdAt: Mon Nov 21 2022 22:26:03 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Apr 29 2024 12:52:07 GMT+0000 (Coordinated Universal Time)
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

# Configuring OAuth for MS Graph

To make API calls to Microsoft Graph, a user must successfully complete an OAuth loop in the Jigx mobile app.

The following sections provide the steps to configure OAuth in Microsoft Azure Active Directory, add OAuth credentials to the Jigx solution in Jigx Management, and YAML examples that make a function call and display the data on a jig.

1. Configure OAuth access for Microsoft Graph in Microsoft Azure's admin portal by following the steps in [Create and configure a new OAuth app in Microsoft Azure AAD](create-and-configure-a-new-oauth-app-in-microsoft-azure-aad.md).
2. Add a credential configuration to your Jigx solution in the Jigx Management by following the steps in [Adding the OAuth Configuration to the solution in Jigx Management](adding-the-oauth-configuration-to-the-solution-in-jigx-management.md).
3. Implement a function that calls Microsoft Graph and displays the results on a jig by using the YAML examples in [Using the OAuth configuration in a Jigx solution](using-the-oauth-configuration-in-a-jigx-solution.md)
