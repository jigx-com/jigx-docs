# Dynamic Data

Apps need data, while [static](https://docs.jigx.com/examples/static) allows you to add static or testing data into a jig it is very limiting, and you will want access to a database for data. Jigx **Dynamic Data** is a built-in database used to create, read, update, and delete data in an app.

The underlying data store for Dynamic Data is a NoSQL store. This means that each record can have its own field structure, and you can add or remove any fields on a per-record basis. Only the id column is a system column and cannot be changed or removed from the record.

We can visualize how dynamic data works by following the steps below:

![Dynamic Data Overview](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/J1iJYwlRVrWs797temueT_dynami.png)

1. Data is updated on the device (Device 1).
2. Data is immediately synced with the Dynamic Data database in the Jigx cloud.
3. These changes are immediately reflected on any other device that shares the same data (Device 2).

## Capabilities

* A Jigx cloud-hosted NoSQL database that syncs automatically with data on the device.
* A web-based [management](https://docs.jigx.com/data) interface for viewing the Dynamic data tables, browsing and editing data and setting [Data policies](../../../../administration/solutions/row-level-security/data-policies.md) in these tables.
* Rapidly import your own data by uploading any JSON or CSV file to the [management](https://docs.jigx.com/data) interface.
* You can also export your data in JSON for reporting and other integration needs.
* Changes made on your device are stored locally and immediately reflected in the cloud-hosted database.
* Realtime data syncing between your device, Dynamic data in the cloud, and other devices.
* Devices continue to operate offline and any local changes will be synced to the database once the device established a connection.

:::hint{type="warning"} Jigx does not recommend storing images in Dynamic Data (via any conversion), as the max file size per record is 350K. :::

## How to create Dynamic Data

To create and use Dynamic data see the following:

1. [Creating tables](creating-tables.md)
2. [Creating columns & data records](creating-columns-_-data-records.md)
3. [Deleting tables](deleting-tables.md)
4. [Using Dynamic Data](using-dynamic-data.md)

::::VerticalSplit{layout="middle"} :::VerticalSplitItem ::embed\[]{url="https://vimeo.com/830296571?share=copy"} :::

:::VerticalSplitItem ::embed\[]{url="https://vimeo.com/829863168?share=copy"} ::: ::::

:::hint{type="info"} **Supporting file** for the _Working with Dynamic Data_ video. You can use this CSV file if you want to follow the steps in the video. :::

## Examples and code snippets

The following examples with code snippets are provided:

* [Creating Dynamic Data](https://docs.jigx.com/examples/creating-dynamic-data)
* [Reading Dynamic Data](https://docs.jigx.com/examples/reading-dynamic-data)
* [Updating Dynamic Data](https://docs.jigx.com/examples/updating-dynamic-data)
* [Deleting Dynamic Data](https://docs.jigx.com/examples/deleting-dynamic-data)
