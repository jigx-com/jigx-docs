---
title: Configuring OAuth for MS Graph
slug: lrK_-configuring-oauth-for-ms-graph
description: Learn how to configure OAuth in Microsoft Azure Active Directory and add OAuth credentials to the Jigx mobile app with this document. It includes detailed instructions, YAML examples for making API calls to Microsoft Graph, and displaying the data on a ji
createdAt: Mon Nov 21 2022 22:26:03 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Apr 29 2024 12:52:07 GMT+0000 (Coordinated Universal Time)
---

To make API calls to Microsoft Graph, a user must successfully complete an OAuth loop in the Jigx mobile app.

The following sections provide the steps to configure OAuth in Microsoft Azure Active Directory, add OAuth credentials to the Jigx solution in Jigx Management, and YAML examples that make a function call and display the data on a jig.

1. Configure OAuth access for Microsoft Graph in Microsoft Azure's admin portal by following the steps in [Create and configure a new OAuth app in Microsoft Azure AAD](<./Configuring OAuth for MS Graph/Create and configure a new OAuth app in Microsoft Azure AAD.md>).
2. Add a credential configuration to your Jigx solution in the Jigx Management by following the steps in [Adding the OAuth Configuration to the solution in Jigx Management](<./Configuring OAuth for MS Graph/Adding the OAuth Configuration to the solution in Jigx Management.md>).
3. Implement a function that calls Microsoft Graph and displays the results on a jig by using the YAML examples in [Using the OAuth configuration in a Jigx solution](<./Configuring OAuth for MS Graph/Using the OAuth configuration in a Jigx solution.md>)
