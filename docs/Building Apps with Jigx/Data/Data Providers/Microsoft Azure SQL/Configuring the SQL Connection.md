---
title: Configuring the SQL Connection
slug: O8lF-configuring-the-sql-connection
description: Learn how to securely route calls to Azure SQL Server from a mobile app through Jigx Cloud. This document explains the step-by-step process, from creating the Azure SQL connection in Jigx Cloud to testing and saving the configuration. With Jigx's encrypte
createdAt: Wed Mar 15 2023 12:32:37 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue May 21 2024 15:05:21 GMT+0000 (Coordinated Universal Time)
---

:::hint{type="warning"}
Best practice for production apps is to use REST as the data layer to access data and not directly integrate to SQL using the SQL data provider. The SQL data provider will be squiggled in blue to indicate it is not recommended, together with a message to use [REST](docId\:jrbaNsm-OJn3nf4_dn_Hu) instead. See [REST endpoints from Azure SQL](docId\:eOUi2cPYynsdRuK-TobDp) for more information. 
:::

Jigx will route all calls to Azure SQL Server from a Jigx mobile app through the Jigx cloud. No data is stored or cached in Jigx cloud. The encrypted SQL connection information is stored in non-user-readable secure storage in Jigx cloud and allows for IP allowlisting for Azure SQL database servers. 

To complete these steps, the user will need Jigx credentials with **admin** privileges for the solution being configured and **Azure SQL administrative credentials** to configure the allowlisted IP addresses for the Azure SQL Server being used in the Jigx solution.

Following these steps to configure a new Azure SQL connection for the solution in Jigx cloud before adding the Jigx cloud IP addresses to the allowlisted IP addresses in Azure SQL.

## Creating an Azure SQL connection in Jigx cloud

1. Sign in to Jigx management at <a href="https://manage.jigx.com" target="_blank">https\://manage.jigx.com</a> and navigate to the solution being configured.
2. Click on the **Connections** menu option on the left of the solution screen.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/wcL-jZnv7HBqcJvoiILMQ_az-addconnection.png" size="66" position="center" caption="Connections in Jigx Management" alt="Connections in Jigx Management"}

3\. Click **Add Connection** on the top right of the Connections screen.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/XtnVR4Befd3rXAy_lRR6v_image.png" size="56" position="center" caption="Add a new connection" alt="Add a new connection"}

4\. Enter the connection information for the new Azure SQL Connection.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ENtp0x8UdqB7Vq4ZMTjZM_az-connection.png" size="50" position="center" caption="Azure SQL connection" alt="Azure SQL connection"}

- In the **Name** field, enter your server's name, which will be the connection name Jigx functions will refer to when you create SQL functions. We recommend that this be the same as your SQL instance, for example, jigx1.database.windows.net.
- In **Type** – Select Azure SQL for both Azure SQL and on-premise SQL Servers.
- Optionally enter any descriptive text in the **Description** field.
- In **Server** enter the name of Azure SQL or SQL on-premise database server. The Azure administrator or database administrator will assist with this name.
- In **Database** enter the name of the SQL Server database you want to connect to. 
- In **User** enter the user name that will connect to SQL Server.
- In **Password** enter a valid password for the SQL Server.
- In **Options** configure other connection options such as non-standard ports or other specific connection information that the database server may need. 

5\. Before saving or testing the connection, click the **IP allowlist** link in the middle of the new connection screen. Note the two IP addresses listed. The calls from Jigx Cloud to Azure SQL will always originate from one of these IP addresses. These IP addresses will be added to the Azure SQL Server.

:::hint{type="info"}
These IP addresses will vary depending on the Jigx cloud region being used.
:::

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/CSDvejsKUcPUVMwJR4xmI_az-allowlist.png" size="54" position="center" caption="Jigx IP address" alt="Jigx IP address"}

6\. Navigate to the administrative portal for the Azure SQL Server instance hosting the database used in the Jigx solution. Under the Security section, select **Networking**. Please refer to <a href="https://learn.microsoft.com/en-us/azure/azure-sql/database/firewall-configure?view=azuresql" target="_blank">Azure SQL firewall connection documentation</a> for detailed instructions.



::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-hTKyHRhP9hQ51Og4nbzg_image.png" size="40" width="530" caption="Azure administrative portal" alt="Azure administrative portal"}

7\. Add the two Jigx IP addresses to the IP addresses allowlist for this Azure SQL instance.

![Adding IP addresses](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/wA4LuzjcE8nP0_T6FGDZ4_image.png "Adding IP addresses")

8\. In Jigx Management, click **Test connection**. If all the settings are configured correctly, the connection will succeed. Click **Save**.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/80XX88URNJuz0lysoAich_image.png" size="46" position="center" caption="Testing SQL connection" alt="Testing SQL connection"}

9\. The connection can now be used in your Jigx project to execute SQL queries or stored procedures to read and write data to Azure SQL.
