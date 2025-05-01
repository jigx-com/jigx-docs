---
title: Data
slug: aI2F-data
description: Jigx data concepts, including data lifecycles, syncing and loading data, and how to work with REST, Azure SQL, and Dynamic Data
createdAt: Fri Jun 17 2022 09:30:01 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Mar 26 2024 12:20:36 GMT+0000 (Coordinated Universal Time)
---

Data is the most crucial aspect of developing a mobile app; leveraging this data intelligently can transform a good app into a great one, harnessing the power of data within mobile applications drives engagement, personalization, and functionality.

This section covers data concepts, lifecycles, syncing and loading data, and data providers integrating with other systems to expose data.

## Concepts

1. [Data Lifecycles in Jigx](<./Data/Data lifecycles in Jigx.md>) explains when data is loaded when it is cached and what triggers loading from cache vs loading from tables.
2. [Syncing Remote and Loading Local Data](<./Data/Syncing remote and loading local Data.md>) explains how to sync data from the cloud and how to display it on a jig. It also explains the difference between coordinating local and remote updates and their effect on a user's experience.
3. [When To Load Data](<./Data/When to load data.md>) is probably one of the most important topics when you design your solution. The timing of this will determine how robust the solution will work in offline environments and how loading data just in time can affect the user's experience.
4. [Offline Solutions](<./Data/Offline Solutions.md>) access to data while a device is offline, for example, in airplane mode or without an internet signal. Once the device is back online, how is the data synced.

## Data Providers

1. [Dynamic Data](<./Data/Data Providers/Dynamic Data.md>) is a Jigx-specific data source that automatically syncs data in real time between devices. It is a great platform for disposable data, defining data that is not already available in existing systems, and how to sync data in real time between users and their devices, regardless of where it is updated.&#x20;
2. [Microsoft Azure SQL]() provides an overview of working with Microsoft Azure SQL and a guide on configuring secure access and Jigx functions to read, update and delete data with queries and stored procedures.
3. [Microsoft OneDrive](<./Data/Data Providers/Microsoft OneDrive.md>) integration allows you to create, updated, and delete files in OneDrive. In a solution, you can list, and download files from OneDrive.
4. [REST](<./Data/Data Providers/REST.md>) provides an overview of working with REST services, including how data is returned, transformed, and used in the solution. This section explains selective data updates and how to configure security and more complex REST calls.
5. [Salesforce](<./Data/Data Providers/Salesforce.md>) provider allows you to integrate with your Salesforce instance, with access to share data about sales, customers&#x20;
6. LOCAL - Stores data locally inside your solution until the app closes.
7. SOAP - works with APIs based on SOAP protocols.

## Datasources

[Datasources](./Data/Datasources.md) are sets of data referenced when building solutions in Jigx. These are:&#x20;

1. [Global](./Data/Datasources.md) - the data set is defined once and is available throughout your solution to be reused in multiple jigs.
2. [Local](./Data/Datasources.md) - the data sets are available inside the individual jig.

## Entities

Entities refer to tables in data providers or datasources where data is saved, created, updated, read, and deleted.  [Actions](./UI/Actions.md) provide the ability to execute the CRUD methods, sync data, and refresh data on individual rows ([execute-entity]()) or multiple rows ([execute-entities]()).
