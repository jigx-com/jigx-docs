---
title: Data policies
slug: es3E-r
description: Learn how to configure data policies in this comprehensive document. Set restrictions on a per solution and per table basis, granting custom permissions or denying access to operations such as create, read, update, and delete. Use caution when applying th
createdAt: Mon Sep 25 2023 17:54:30 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Oct 30 2023 09:48:56 GMT+0000 (Coordinated Universal Time)
---

Data policies are set per solution and table, with restrictions set per operation.&#x20;

## Permissions

1. Only the solution `Owner` can configure data policies on the solution tables. See [Permissions - User Roles](<./../../Permissions - User Roles.md>) for more information.&#x20;
2. As the solution `Owner` you can **disable** the data policy on a solution level using the *Policy Checks Active* switch at the top right of the screen. This will ignore all restrictions set in the table. &#x20;

## Operations

The following **operations** are available on each table:

- **CREATE** - the ability to create new records in the table
- **READ** - the operation allows users to read or list the records in a table
- **UPDATE** - the ability to update existing records in a table
- **DELETE** - allows records to be deleted from the table

## Restrictions

The following **restrictions** are configurable on each operation, or you can set the restriction on the solution level which is applied to app operations:

- **Custom** - configure which groups, owners, or members can perform an operation
- **Allow everyone** - grants all users of the solution rights to perform an operation&#x20;
- **Deny all **- prevents all users of the solution from performing an operation

## Considerations

- Setting the *Deny all* restriction on the table level will remove all the operations from the list below. Caution must be used when using this restriction as it can create a complete lock on the table.  &#x20;
- Important - In a custom restriction data policy, if you add a group to `Members`, all users in that group can see all records in the table.&#x20;
- Setting the Policy Checks Active to disabled removes all restrictions, giving all users access to the data.

## Configuring data policies

![Data Policy configuration](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3k5jtWF8lVdAGRuTZY40m_rls-datapolicyconfig.png "Data Policy configuration")

1. Open Jigx Management, select the **solution** option and browse to the solution you want to set the data policy on.
2. Click on the **Data Policies **option in the navigation pane.
3. Select the required **table** from the Tables list in the right-hand pane.
4. To apply a restriction for all operations on the table, use the **Restrictions** field under the table name. Select the required restriction from the dropdown list.
5. To apply a restriction per operation, click on the operation in the list to open the configuration pane on the right.&#x20;
6. Select the required restriction from the dropdown list and click **Save**.&#x20;
7. Selecting the Custom restriction requires selecting specific groups, owners, and members. &#x20;



