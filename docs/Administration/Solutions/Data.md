# Data

The Data tab allows you to manage all the [Dynamic Data](<./../../Building Apps with Jigx/Data/Data Providers/Dynamic Data.md>) tables and table contents used by the solution. All changes made in Jigx Management will be synced bi-directionally with the devices in real-time.

Although the User Interface of the Data tab presents all data in a two-dimensional table layout, the underlying data store (Dynamic Data) is a NoSQL store. This means that each record can have its field structure, and you can add or remove any fields on a per-record basis. Only the `rid` column is a system column and cannot be changed/removed from the record.

Use [Row Level Security](<./Row Level Security.md>) to protect and secure your dynamic data by determining the operations users can perform on the database, such as creating or deleting records and controlling users' access to the data records in the tables, for example, the ability to see sensitive information.

1. [Data policies](<./Row Level Security/Data policies.md>) - get set on the solution level and determine who can CREATE, READ, UPDATE, and DELETE records in a table.
2. [Authorized users](<./Row Level Security/Authorized users.md>) - restricts access on a granular level and determines the exact data records in a table users can see.

:::hint{type="info"}
Tables will only show if the solution is published in Jigx Builder includes [Dynamic Data](<./../../Building Apps with Jigx/Data/Data Providers/Dynamic Data.md>) table definitions.
:::

![Contents of the Products tablets](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/vLG_i97La3Jsm2i2VwFP9_jm-datal.png "Contents of the Products table")

## Adding new records

You can add records to a data table manually or by uploading a JSON or CSV file to populate the records in the columns in the table. To *manually* create a record:

1. Click on the table you want to add a record to in the right-hand **Tables** pane.
2. Click on the blue **New record** button. If you already have records in the table, you will see all existing columns of all records.&#x20;
3. In the **New record** pane add the data values for each column.&#x20;
4. **Add new columns** to your record by defining a column name and clicking on the **+** button right next to the new column name. As you add data the field displays the type under the entry, such as number, string or boolean.
5. Once you set the data values of the fields you want to include in your record, click **Save**.

## Editing a record

Edit an exisitng data record by:

1. Clicking on the table in the right-hand **Tables** pane that you want to edit a record in.
2. Click on the **record** entry to be updated, the **Edit record **side pane with the record's fields displays.
3. Update the data values as required.
4. Add a new column to your record using the + button at the bottom if required.
5. Click **Save**, the record will be updates to the table and synced to online devices instantly.

![Updating a record](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/OyK-D-REpra9E-gAgWZ_w_jm-editdatal.png "Updating a record")

See [Dynamic files](<./../../Building Apps with Jigx/Data/Data Providers/Dynamic Files.md>) to learn how to configure a solution in Jigx Builder to upload, download, delete, and track the status of files.

## Deleting a record

You can select single or multiple records to delete in the table by:

1. **Delete a single record** - click on the record and select **Delete** at the bottom of the side pane (as shown in the image above).
2. **Delete Multiple records** - select the checkboxes next to the records you want to delete. Then click the red **Delete selected** button at the top of the screen. The records will instantly be removed from the Jigx Cloud store and online devices.

![Deleting multiple records](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/OPX2ZoWZTBXuFkdaOmsSM_jm-deletedatal.png "Deleting multiple records")

## Adding and deleting files from records&#x20;

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-QnWsC0B1rSmeA622gNi0T-20250523-093602.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-QnWsC0B1rSmeA622gNi0T-20250523-093602.png" size="68" width="1946" height="1580" position="center" caption="Dynamic files" alt="Dynamic files"}

1. Click on a record and select the **File** tab.
2. The file **status**, **thumbnail**, **name**, **content type** and **size** are displayed.
3. To download the file from Managment, use the **Download file** link at the top of the record.
4. To delete a file, click the **X** next to the file preview.
5. To view the file thumbnail in the table, ensure **File** is checked in the **Column settings** pane.

## Deleting a table

![Deleting tables](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rZrpBiZnyf1AO6qI-GR3h_jm-delete-dd-tables.png "Deleting tables")

To delete a table, follow these steps:

1. In Jigx Builder remove a table from the **default.jigx** file and publish the solution.
2. In  Jigx Management  as the solution `owner` navigate to the solution and select the **Data** option.
3. The table is visible in the **Unused** tab.
4. Optional: make a table backup by clicking the **Download** button. A JSON file containing the data records is downloaded.
5. Click the **Delete Table** button at the top of the screen.
6. Confirm you want to delete the table.

### What you need to know about deleting tables

- You can only delete a table not currently used in a solution.
- Deleting tables will delete all data records in the table, which is not recoverable. Delete tables with caution.
- Only the solution `owner` can delete a table.
- The *Unused tab* is only visible to the solution `owner`.
- Removing a table from default.jigx file in Jigx Builder and publishing the solution means the table is no longer used in the solution. In  Jigx Management under Data, the table moves to the *Unused tab*.
- If there are no unused tables the *Unused tab* is not visible in the Data option.
- [Authorized Users (RLS)](docId\:xy4a9JXqIEBPICKan-N0M) still applies to the data records in the unused table. Even as the solution owner, you will only see data records you are authorized to see. It is important to note that even though you cannot see all the data, deleting the table will delete *ALL* records and the table.
- You can choose to only delete the records in the unused table by selecting the checkbox in front of the record. The **Delete Selected** button appears at the top.
- Make a backup of the unused table's data by clicking the **Download** button at the top of the screen. The data is downloaded in a JSON file. If needed, you can reuse the data by importing (upload) data into a new table. *Important*: the data in the downloaded JSON file is the data you are authorized to see.
- Existing records in the unused table can be edited, but you cannot add new records.
- [Authorized Users (RLS)](docId\:xy4a9JXqIEBPICKan-N0M) access can be applied to existing records in the unused table.
- You cannot apply [Data policies](docId\:es3EARyGcuVJpv8KFQDx4) to unused tables.
- If you want to use the table in the solution again, simply add the table back to the *default.jigx* file and publish the solution. The table moves back to the **Available** tab in the Jigx Management>Data.

## Column Settings

The **gear icon** at the top of the screen allows you to configure the columns in a table. The columns displayed in the Column settings side pane are the aggregated set of all columns for all records in that table. The `rid` and `Authorised Users` column are system columns, which are not shown by default.

1. **Visibilty** - check the checkbox next  to the column you want displayed in the table records. Similarily uncheck the column you want to hide in the table records. The `rid` and `Authorised Users` column is hidden by default. You can select to show the id if required. Click **Apply** at the bottom of the pane.
2. **Column order** - change the order of the columns in the table by grabbing the hamburger icon on the right of the column name and drag it to the required position in the table.

## Exporting / Downloading a table

You might require the data from the table for various reasons such as reporting or to backup the table before you delete it. Use the **Download** button at the top of the screen to download the data into a **JSON file**.

## Importing / Uploading data to a table (JSON or CSV)

If you have multiple records to add to a table you can import the data by uploading a CSV or JSON file that will populate the records in the columns in the table.

1. Click on the **Upload** button at the top of the screen.
2. By default the JSON upload window is shown. You can switch to upload CSV using the **Switch to CSV** button in the top right. Provide the property name for the unique identifier otherwise by default the rid property is used. Drag and drop the file in the designated area.
3. For CSV uploads select the type of **comma-delimited** used in the **CSV file.** Drag and drop the file in the designated area.
4. Click **Add**.
5. This will add new `rid` records to the table or update existing `rid` records in the table.

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![JSON upload](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/efNld6uIk2ZFcnXO3osn-_jm-jsonupload.png "JSON upload")
:::

:::VerticalSplitItem
![CSV upload](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/h1PYzElvGBREbM6qfG5Pb_jm-csvupload.png "CSV upload")
:::
::::

## Set Authorized Users per data row

See [Authorized users](<./Row Level Security/Authorized users.md>) for more information.

## Change a data record type

![Data record types](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/cty9dl5ipKSbOno8I_7B5_jm-sparklerdd.gif "Data record types")

In Dynamic Data each data record's field in a table has a type, such as string, number, boolean. You can toggle between data types using the *sparkler* on the right of each data field and then saving the record. Each data record must be edited manually to toggle and save the data type.
