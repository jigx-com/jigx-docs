---
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

# Deleting tables

Deleting a table is a critical operation that should be performed with caution. Before proceeding with the deletion, please back up the table data, as it cannot be recovered once deleted.

<figure><img src="../../../../.gitbook/assets/JM-delete-DD-tables (1).png" alt="Deleting tables"><figcaption><p>Deleting tables</p></figcaption></figure>

To delete a table, follow these steps:

1. In Jigx Builder remove a table from the **default.jigx** file and publish the solution.
2. In Jigx Management as the solution `owner` navigate to the solution and select the **Data** option.
3. The table is visible in the **Unused** tab.
4. Optional: make a table backup by clicking the **Download** button. A JSON file containing the data records is downloaded.
5. Click the **Delete Table** button at the top of the screen.
6. Confirm you want to delete the table.

### What you need to know about deleting tables

* You can only delete a table not currently used in a solution.
* Deleting tables will delete all data records in the table, which is not recoverable. Delete tables with caution.
* Only the solution `owner` can delete a table.
* The _Unused tab_ is only visible to the solution `owner`.
* Removing a table from default.jigx file in Jigx Builder and publishing the solution means the table is no longer used in the solution. In Jigx Management under Data, the table moves to the _Unused tab_.
* If there are no unused tables the _Unused tab_ is not visible in the Data option.
* [Row Level Security](deleting-tables.md) still applies to the data records in the unused table. Even as the solution owner, you will only see data records you are authorized to see. It is important to note that even though you cannot see all the data, deleting the table will delete _ALL_ records and the table.
* You can choose to only delete the records in the unused table by selecting the checkbox in front of the record. The **Delete Selected** button appears at the top.
* Make a backup of the unused table's data by clicking the **Download** button at the top of the screen. The data is downloaded in a JSON file. If needed, you can reuse the data by importing (upload) data into a new table. _Important_: the data in the downloaded JSON file is the data you are authorized to see.
* Existing records in the unused table can be edited, but you cannot add new records.
* [Authorized Users (RLS)](deleting-tables.md) access can be applied to existing records in the unused table.
* You cannot apply [Data policies](deleting-tables.md) to unused tables.
* If you want to use the table in the solution again, simply add the table back to the _default.jigx_ file and publish the solution. The table moves back to the **Available** tab in the Jigx Management>Data.
