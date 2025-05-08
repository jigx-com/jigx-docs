---
title: Data planning
slug: sgE5-data-planning
description: Learn how to create a data plan for app development to optimize data usage, save time, and ensure accurate implementation. Follow the steps of mapping data, determining sources, visualizing through tables and joins, creating entity relationship diagrams, 
createdAt: Wed Jul 12 2023 18:38:34 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Jul 17 2023 14:55:27 GMT+0000 (Coordinated Universal Time)
---

Why create a data plan? Data is used throughout the Jigx App, knowing where the data is coming from or going to, how to use that data on the device, whether online or offline, what data you can prefetch and made available on the device, and what data you will fetch just in time is important to design before building apps. This saves developers time and ensures the correct data is used from the beginning.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/PyB3x5G_IxY_H6nhO74jm_dataplanning.png" size="70" position="center" caption="Data visualization" alt="Data visualization"}

### Steps

1. Map out the data for the app. This includes the data that will be used on each screen.
2. Are you using pre-existing data sets or creating new data sets?&#x20;
3. Decide where the data is coming from or going to, for example, [Microsoft Azure SQL](<./../../Building Apps with Jigx/Data/Data Providers/Microsoft Azure SQL.md>), [REST](<./../../Building Apps with Jigx/Data/Data Providers/REST.md>), [Dynamic Data](<./../../Building Apps with Jigx/Data/Data Providers/Dynamic Data.md>) (local or global), Salesforce or [Microsoft OneDrive](<./../../Building Apps with Jigx/Data/Data Providers/Microsoft OneDrive.md>).
4. Map out the tables and joins that will help visualize the data and assist when building the data out.
5. Create an entity relationship diagram to model the app data.
6. Draw where the data points are needed on your sketch or Miro board created in the solution design step.
7. Most importantly, decide when to load data in the app and on the screens. For example, when must you cache fresh data from SQL vs. using local data, this helps with offline capabilities. See [When To Load Data](<./../../Building Apps with Jigx/Data/When to load data.md>) to understand the various options, benefits, and drawbacks.

### Considerations

- Design the data flow with offline in mind. This helps to know when to plan the loading of data on an app.
- Privacy and keeping data safe are important, in this instance, it would be better to use an SQL server that provides this functionality.
- Data grows with time, plan for scalability.
- Data must be structured in the backend. Clean data ensures you show the latest and applicable data to your users. You can add filters and search fields to assist users in the app screens. Using relevant clean data from the start creates a real user experience while developing.
- Having the screens drawn out, as described in the Solution Design section above, helps visualize what data you need and when to load the data.
- Determine when you want to save or send data to a database, for example - only once a submit button is pressed. This is important as it determines what code is required at build time.
- In Jigx if the same data is reused in multiple screens, you can decide whether to create a global data source that can be reused in different jigs. Include this on the data plan as it helps the creator know where to build the datasource.  In Jigx Builder global data is created under the datasources folder and referenced in multiple jigs, and local data is created  in the jig file for use in that single jig.

### Tip

- Having to create a database can be time-consuming or daunting, use tools such as ChatGPT to create a database, a database script, or build a CSV file for a data structure.
- For Dynamic Data a CSV file can be [uploaded](./../../Administration/Solutions/Data.md) to Jigx Management to create the tables and data.
- In Jigx use [actions]() to move data from screen to screen.
- When using REST or SQL, you need functions and stored procedures. Decide what the functions will do. Use Postman to understand the properties required.
- Be smart in the design of data by thinking of creating experiences, for example, data can be shown as charts rather than lists.

