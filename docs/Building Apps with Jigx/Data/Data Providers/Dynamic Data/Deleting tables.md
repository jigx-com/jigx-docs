---
title: Deleting tables
slug: Ieb6-de
createdAt: Wed Nov 29 2023 08:59:07 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Nov 29 2023 09:27:47 GMT+0000 (Coordinated Universal Time)
---

Deleting a table is a critical operation that should be performed with caution. Before proceeding with the deletion, please back up the table data, as it cannot be recovered once deleted. 

![Deleting tables](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rZrpBiZnyf1AO6qI-GR3h_jm-delete-dd-tables.png "Deleting tables")

To delete a table, follow these steps:
1. In Jigx Builder remove a table from the **default.jigx** file and publish the solution.
2. In  Jigx Management  as the solution `owner` navigate to the solution and select the **Data** option.
3. The table is visible in the **Unused** tab.
4. Optional: make a table backup by clicking the **Download** button. A JSON file containing the data records is downloaded.
5. Click the **Delete Table** button at the top of the screen.
6. Confirm you want to delete the table.

### What you need to know about deleting tables
* You can only delete a table not currently used in a solution.
* Deleting tables will delete all data records in the table, which is not recoverable. Delete tables with caution.
* Only the solution `owner` can delete a table.
* The *Unused tab* is only visible to the solution `owner`.
* Removing a table from default.jigx file in Jigx Builder and publishing the solution means the table is no longer used in the solution. In  Jigx Management under Data, the table moves to the *Unused tab*.
* If there are no unused tables the *Unused tab* is not visible in the Data option.
* [Row Level Security](docId\:xy4a9JXqIEBPICKan-N0M) still applies to the data records in the unused table. Even as the solution owner, you will only see data records you are authorized to see. It is important to note that even though you cannot see all the data, deleting the table will delete *ALL* records and the table.
* You can choose to only delete the records in the unused table by selecting the checkbox in front of the record. The **Delete Selected** button appears at the top.
* Make a backup of the unused table's data** by clicking the **Download** button at the top of the screen. The data is downloaded in a JSON file. If needed, you can reuse the data by importing (upload) data into a new table. *Important*: the data in the downloaded JSON file is the data you are authorized to see.
* Existing records in the unused table can be edited, but you cannot add new records.
* [Authorized Users (RLS)](docId\:xy4a9JXqIEBPICKan-N0M) access can be applied to existing records in the unused table.
* You cannot apply [Data policies](docId\:es3EARyGcuVJpv8KFQDx4) to unused tables.
* If you want to use the table in the solution again, simply add the table back to the *default.jigx* file and publish the solution. The table moves back to the **Available** tab in the Jigx Management>Data.
