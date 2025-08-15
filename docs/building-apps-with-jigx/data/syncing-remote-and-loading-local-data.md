# Syncing remote and loading local Data

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-4Cy8fOUMAzzsz5gefQL2R-20241119-092849.gif" size="74" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-4Cy8fOUMAzzsz5gefQL2R-20241119-092849.gif" caption width="1120" height="1616" darkWidth="1120" darkHeight="1616"}

Key:

1. **Sync data from the cloud** Use a `sync-entities` action to fetch data from the cloud and store it in the local SQLite database. Use the `onLoad`, `onFocus`, `onRefresh`, or any other event where actions are defined.
2. **Load data from SQLite to use on a jig** Use the `DATA_PROVIDER_LOCAL` in the datasource defined in the jig or a global datasource to execute an SQLite query.
3. **Save data to SQLite ONLY** To save data locally only and not sync to the cloud, use an `execute-entity` action with the `DATA_PROVIDER_LOCAL`.
4. **Save data to SQLite and sync data to the cloud** Update the local SQLite and sync to the cloud in a single action to ensure high-performing user experiences without lag. Use `execute-entity` or `execute-entities` actions with `DATA_PROVIDER_REST` or `DATA_PROVIDER_SQL`. Specify the function call to make, the local entity/table to update, and the method to perform on the local table. If the method is an update, delete, or save, specify the record's ID.
5. **Save data to the cloud ONLY** Use `execute-entity` or `execute-entities` actions with `DATA_PROVIDER_REST` or `DATA_PROVIDER_SQL`. Set the method to functionCall and specify the function to be called. The local tables will not be updated; you must sync the data from the cloud before it is available to display on a jig.

:::hint{type="info"} Dynamic Data automatically syncs its data with the cloud when server-side or device-side updates are made to the tables, using `DATA_PROVIDER_DYNAMIC`. :::

## Using sync-entities action

1. Use the `sync-entities` action to sync data from the remote data store (REST and SQL) to the local SQLite data provider. Syncing data locally results in high performance with minimal lag and ensures that all data is available in the app when the device is offline.
2. Best practice is to configure a global action, the `sync-entities` action, with the REST or SQL data provider, allowing reuse throughout the solution.
3. Add the global sync action to the `onFocus` and `onLoad` events in the index.jigx file ensures data is synced to the local data provider as soon as the app loads or is focused on the device.
4. Add the global sync action to the `onRefresh` or `onFocus` events in a jig when data is changed, for example, on the list of customers, this ensures that when a new customer is created, the list is updated immediately when navigating to it or refreshing the list with a downward swipe.

## Using Execute-entity/entities action

There are two options when using the `execute-entity` and `execute-entities` actions with remote data, such as REST or SQL.

1.  **To update BOTH the local SQLite table and the remote data store (REST and SQL)**. To update the local table, specify CREATE, UPDATE, or DELETE methods in the `method` property of the data provider, then specify the function to use in the `function` property, and under `parameters` specify the exact data to be updated in the remote data store (REST/SQL). Under `data` specify the exact data to be updated in the local SQLite table. After execution, a tempId is created, and then synced to the local table.

    ![Update local and REST providers](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-cE8AAHc7mhUv7fJS4z56u-20250804-142244.png)
2.  **To ONLY update the remote data store (REST and SQL)**. To update the remote data store specify `functionCall` in the `method` property. Then specify the function to be called in the `function` property and under `parameters` specify the exact data to be updated. Note that the data will not be visible on the jig until a `sync-entities` action is executed.

    ![Only update REST Service](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-VncgH7oeM4bADxWiBlFd_-20250804-143743.png)

### Consideration

* Using the `save` method in `execute-entity/entities` action will perform an upsert in the local SQLite table.
* Dealing with offline remote data is fundamental to ensuring data synchronization and consistency between the mobile app and the remote data source, allowing users to continue using the app and performing actions without interruption. [Offline remote data handling](offline-remote-data-handling.md) explains how to configure solutions to deal with data when the device is offline.

## Using local data provider in a jig's datasources

1. Once the data has been synced using the `sync-entities` action the data is available in the local data provider.
2. Reference the local data provider in the jig's `datasource` property to define the data required in the jig.
3. Write a SQLite query to define the exact data required.
4. Use IntelliSence and expressions to reference the specific datasource values to use in each component, such as `data: =@ctx.datasources.customers`

![Local data provider](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/YU-9h42X5xPRI1t_zBBsq_rest-localdatasource.png)
