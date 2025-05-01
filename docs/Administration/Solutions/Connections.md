---
title: Connections
slug: 5NIM-connections
description: Learn how to easily manage connection settings for your Azure SQL database instances in this comprehensive guide. Discover step-by-step instructions on adding, updating, and removing connections on the Connections tab. You'll also gain insights into the i
createdAt: Tue Jun 07 2022 09:54:22 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Feb 12 2024 17:24:40 GMT+0000 (Coordinated Universal Time)
---

Manage connection settings for Azure SQL database instances on the Connections tab. Solutions reference the connection using the `key`.

![Managing Connections](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/JiPwcxpHci5jJx-Z-s54U_jm-azurel.png "Managing Connections")

## Adding a Connection

:::hint{type="info"}
In order for the Azure SQL connection to function, you need to allowlist the Jigx IPs for your database instance using the Azure Portal (Azure SQL Server Instance -> Networking -> Firewall Rules). Click on **IP Allowlist** in the side pane to view the Jigx IPs you need to allowlist.
:::

1. Click on the blue **Add connection** button to open the Add connection side pane.
2. Fill in your Azure SQL connection settings or **Show schema. **You can add additional properties for your connection using the **Options** section at the bottom. Click on the **help icon **to see a list of all available connection options you can include in the JSON schema.** **
3. Before clicking **Save,** click on **Test connection** to ensure that the settings are working corectly.

![Adding a new Connection](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Scu8nZHKoi5_2RLR8dW_l_jm-azureeditl.png "Adding a new Connection")

## Updating a Connection

1. Click on the connection name in the list and update the configuration settings. When making changes to any setting, you must re-enter the password before you can **Save**.
2. Click **Save**.

## Removing a Connection

Click on the **Remove** link in the last column of a record. Be aware, that the functions in the solution that are referencing the connection will stop working as they cannot connect to the database connection anymore.

## Considerations

- Creating a copy of a solution duplicates the structure of the credentials and connections, to allow for easy configuration by only having to respecify secrets.

