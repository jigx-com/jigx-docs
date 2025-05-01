---
title: Dynamic Data
slug: KuL3-dynamic-data
description: Jigx Dynamic Data is a built-in database that can be used to create, read, update, and delete data in an app.  
createdAt: Tue Jun 07 2022 09:44:38 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Jan 22 2024 18:50:10 GMT+0000 (Coordinated Universal Time)
---

Apps need data, while <a href="https://app.archbee.io/docs/8V3ZMfuUrYN39zECOfqs5/Bn6YYLjSwkrsJ1-bbwSs1" target="_blank">Static data</a> allows you to add static or testing data into a jig it is very limiting, and you will want access to a database for data. Jigx **Dynamic Data** is a built-in database used to create, read, update, and delete data in an app. &#x20;

The underlying data store for Dynamic Data is a NoSQL store. This means that each record can have its own field structure, and you can add or remove any fields on a per-record basis. Only the id column is a system column and cannot be changed or removed from the record.&#x20;

We can visualize how dynamic data works by following the steps below:

![Dynamic Data Overview](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/J1iJYwlRVrWs797temueT_dynami.png "Dynamic Data Overview")

1. Data is updated on the device (Device 1).
2. Data is immediately synced with the Dynamic Data database in the Jigx cloud.
3. These changes are immediately reflected on any other device that shares the same data (Device 2).

## &#x20;Capabilities

- A Jigx cloud-hosted NoSQL database that syncs automatically with data on the device.
- A web-based [management](https://docs.jigx.com/data) interface for viewing the Dynamic data tables, browsing and editing data and setting [Data policies](<./../../../Administration/Solutions/Row Level Security/Data policies.md>) in these tables.
- Rapidly import your own data by uploading any JSON or CSV file to the [management](https://docs.jigx.com/data) interface.
- You can also export your data in JSON for reporting and other integration needs.
- Changes made on your device are stored locally and immediately reflected in the cloud-hosted database.
- Realtime data syncing between your device, Dynamic data in the cloud, and other devices.
- Devices continue to operate offline and any local changes will be synced to the database once the device established a connection.

:::hint{type="warning"}
Jigx does not recommend storing images in Dynamic Data (via any conversion), as the max file size per record is 350K.
:::

## How to create Dynamic Data

To create and use Dynamic data see the following:&#x20;

1. [Creating tables](<./Dynamic Data/Creating tables.md>)
2. [Creating columns & data records](<./Dynamic Data/Creating columns _ data records.md>)&#x20;
3. [Deleting tables](<./Dynamic Data/Deleting tables.md>)
4. [Using Dynamic Data](<./Dynamic Data/Using Dynamic Data.md>)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::embed[]{url="https://vimeo.com/830296571?share=copy"}
:::

:::VerticalSplitItem
::embed[]{url="https://vimeo.com/829863168?share=copy"}
:::
::::

:::hint{type="info"}
**Supporting file** for the *Working with Dynamic Data* video. You can use this CSV file if you want to follow the steps in the video.
:::

## Examples and code snippets

The following examples with code snippets are provided:

- [Creating Dynamic Data]()
- [Reading Dynamic Data]()
- [Updating Dynamic Data]()
- [Deleting Dynamic Data]()

