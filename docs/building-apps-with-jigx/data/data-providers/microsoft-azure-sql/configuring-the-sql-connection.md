# Configuring the SQL Connection

:::hint{type="warning"} Best practice for production apps is to use REST as the data layer to access data and not directly integrate to SQL using the SQL data provider. The SQL data provider will be squiggled in blue to indicate it is not recommended, together with a message to use [REST](configuring-the-sql-connection.md) instead. See [REST endpoints from Azure SQL](configuring-the-sql-connection.md) for more information. :::

Jigx will route all calls to Azure SQL Server from a Jigx mobile app through the Jigx cloud. No data is stored or cached in Jigx cloud. The encrypted SQL connection information is stored in non-user-readable secure storage in Jigx cloud and allows for IP allowlisting for Azure SQL database servers.

To complete these steps, the user will need Jigx credentials with **admin** privileges for the solution being configured and **Azure SQL administrative credentials** to configure the allowlisted IP addresses for the Azure SQL Server being used in the Jigx solution.

Following these steps to configure a new Azure SQL connection for the solution in Jigx cloud before adding the Jigx cloud IP addresses to the allowlisted IP addresses in Azure SQL.

## Creating an Azure SQL connection in Jigx Cloud

1. Sign in to Jigx management at [https://manage.jigx.com](https://manage.jigx.com)[https://manage.jigx.com](https://manage.jigx.com) and navigate to the solution being configured.
2. Click on the **Connections** menu option on the left of the solution screen.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/wcL-jZnv7HBqcJvoiILMQ\_az-addconnection.png" size="66" position="center" caption="Connections in Jigx Management" alt="Connections in Jigx Management" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/wcL-jZnv7HBqcJvoiILMQ\_az-addconnection.png" width="800" height="386" darkWidth="800" darkHeight="386"}

3\. Click **Add Connection** on the top right of the Connections screen.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/XtnVR4Befd3rXAy\_lRR6v\_image.png" size="56" position="center" caption="Add a new connection" alt="Add a new connection" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/XtnVR4Befd3rXAy\_lRR6v\_image.png" width="800" height="508" darkWidth="800" darkHeight="508"}

4\. Enter the connection information for the new Azure SQL Connection.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ENtp0x8UdqB7Vq4ZMTjZM\_az-connection.png" size="50" position="center" caption="Azure SQL connection" alt="Azure SQL connection" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ENtp0x8UdqB7Vq4ZMTjZM\_az-connection.png" width="800" height="1497" darkWidth="800" darkHeight="1497"}

* In the **Name** field, enter your server's name, which will be the connection name Jigx functions will refer to when you create SQL functions. We recommend that this be the same as your SQL instance, for example, jigx1.database.windows.net.
* In **Type** – Select Azure SQL for both Azure SQL and on-premise SQL Servers.
* Optionally enter any descriptive text in the **Description** field.
* In **Server** enter the name of Azure SQL or SQL on-premise database server. The Azure administrator or database administrator will assist with this name.
* In **Database** enter the name of the SQL Server database you want to connect to.&#x20;
* In **User** enter the user name that will connect to SQL Server.
* In **Password** enter a valid password for the SQL Server.
* In **Options** configure other connection options such as non-standard ports or other specific connection information that the database server may need.&#x20;

5\. Before saving or testing the connection, click the **IP allowlist** link in the middle of the new connection screen. Note the two IP addresses listed. The calls from Jigx Cloud to Azure SQL will always originate from one of these IP addresses. These IP addresses will be added to the Azure SQL Server.

:::hint{type="info"} These IP addresses will vary depending on the Jigx cloud region being used. :::

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/CSDvejsKUcPUVMwJR4xmI\_az-allowlist.png" size="54" position="center" caption="Jigx IP address" alt="Jigx IP address" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/CSDvejsKUcPUVMwJR4xmI\_az-allowlist.png" width="800" height="943" darkWidth="800" darkHeight="943"}

6\. Navigate to the administrative portal for the Azure SQL Server instance hosting the database used in the Jigx solution. Under the Security section, select **Networking**. Please refer to:Link\[ Azure SQL firewall connection]{href="https://learn.microsoft.com/en-us/azure/azure-sql/database/firewall-configure?view=azuresql" newTab="true" hasDisabledNofollow="false"} documentation for detailed instructions.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-hTKyHRhP9hQ51Og4nbzg\_image.png" size="40" width="800" caption="Azure administrative portal" alt="Azure administrative portal" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-hTKyHRhP9hQ51Og4nbzg\_image.png" height="598" darkWidth="800" darkHeight="598"}

7\. Add the two Jigx IP addresses to the IP addresses allowlist for this Azure SQL instance.

![Adding IP addresses](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/wA4LuzjcE8nP0_T6FGDZ4_image.png)

8\. In Jigx Management, click **Test connection**. If all the settings are configured correctly, the connection will succeed. Click **Save**.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/80XX88URNJuz0lysoAich\_image.png" size="46" position="center" caption="Testing SQL connection" alt="Testing SQL connection" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/80XX88URNJuz0lysoAich\_image.png" width="800" height="409" darkWidth="800" darkHeight="409"}

9\. The connection can now be used in your Jigx project to execute SQL queries or stored procedures to read and write data to Azure SQL.
