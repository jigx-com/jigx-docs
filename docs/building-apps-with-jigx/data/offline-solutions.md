---
title: Offline Solutions
slug: 8G5Q-offline-solutions
createdAt: Tue Jun 07 2022 09:48:47 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Jan 15 2024 09:38:53 GMT+0000 (Coordinated Universal Time)
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

# Offline Solutions

The Jigx platform syncs all data to a local SQL database from where it is used in [Expressions](../logic/expressions.md) and user interfaces ([jigs](../ui/jigs-_screens_/jigs-_screens_.md)). Once the data syncs, it is available without the need for an internet connection.

Data is synced to the device from one of five supported locations:

* [Dynamic Data](data-providers/dynamic-data/dynamic-data.md): A built-in Jigx data source that automatically syncs data in real time between devices and the cloud.
* [REST](data-providers/rest/rest.md) Services: REST-based web services that return data in JSON format.
* [Microsoft Azure SQL](data-providers/microsoft-azure-sql/microsoft-azure-sql.md): Either Azure SQL Database or Microsoft SQL Server.
* [Salesforce](data-providers/salesforce/salesforce.md): A Jigx provider for syncing Salesforce.com data.
* SOAP: A data provider for syncing data from SOAP-based services such as SAP.

When the app is online, data is synced from the cloud to the local SQLite database, from where it is accessed using data sources in jigs.

The command is put on a queue when data is saved to the cloud. The queue is immediately executed when the device is online, and the data is sent to the applicable cloud service. When the device is offline, the cloud commands continue to be added to the queue until the device goes online.

The best practice for a robust offline solution is to sync as much data as is needed as early as possible in the usage cycle. This is typically when the solution launches. After that, the solution design should ensure the latest data is synced to the device to avoid just-in-time data loading.

Refer to the [Data lifecycles in Jigx](data-lifecycles-in-jigx.md) and [Syncing remote and loading local Data](syncing-remote-and-loading-local-data.md) sections to understand how to build robust solutions that go offline.

{% hint style="warning" %}
When a Jigx solution switches from offline to online, the queue is processed on a first-in-first-out basis. Jigx does not do conflict resolution. It assumes that the cloud-based system will handle its own data integrity.
{% endhint %}
