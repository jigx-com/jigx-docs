---
title: Creating tables
slug: JGu8-defining-dynamic-data-tables
description: Learn how to define Dynamic Data tables in Jigx solutions with this comprehensive guide. Discover how to add tables to the *default.jigx* file, publish the project, and create columns for Dynamic Data tables. Explore three methods for creating columns, su
createdAt: Thu Jul 14 2022 09:36:46 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Nov 29 2023 09:04:12 GMT+0000 (Coordinated Universal Time)
---

## Creating tables in Jigx Builder

First step in creating Dynamic Data for a solution is to create the tables that the solution requires. Tables are created in a solution in Jigx Builder in the _default.jigx_ file located in the _database_ folder. All tables are created under the default database. Follow the steps below to create tables:

![Tables in Dynamic Data](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/SpVXMM26nqpr1MZ15x34m_dd-tables.png "Tables in Dynamic Data")

1. Open an existing solution or [create a new solution](<./../../../Jigx Builder _code editor_/Create a new Jigx Solution.md>) in Jigx Builder.
2. Expand the database folder and click on the **default.jigx** file.
3. Use IntelliSense (ctrl+space) in the editor, select **tables**, and press enter.
4. Type the name of your table and provide a null value, for example, `employee: null`. Take note of the table name formats below:
   - Table names must be in lowercase
   - The first character must start with a letter
   - The name can contain alphanumeric or symbols '-' and '\\\_'
   - You can include "-" dash , "\_" underscore and digits as per the regex: "^\[a-z]\[a-z0-9\_-]\{0,28}\[a-z0-9]$"
   - The name cannot contain spaces
   - The name cannot end with special characters
   - The length must be between 2-50 characters
5. Add multiple tables by adding the table names under each other in the default.jigx file.
6. [Publish](<./../../../Jigx Builder _code editor_/Publishing a solution.md>) the solution to create the tables.
7. In [Jigx Management](<./../../../../Administration/Management Overview.md>) browse to your solution and navigate to the [Data](https://docs.jigx.com/data) menu to view your tables. Note that only the tables have been created; next, you must create the [columns and data](<./Creating columns _ data records.md>).

### Considerations

- If _default.jigx_ does not exist, simply use the file / new capability to add a new file called _default.jigx_ and place it within a folder called databases as per the VS Code folder layout shown in the image at the top of this page.
- If you remove a table in the default.jigx file and publish the solution, the table becomes _unused_ in the solution. To include the table and it's records again in the solution, simply add the table back to the default.jigx file and republish the solution.
- A table must be _unused_ before you can [delete ](<./Deleting tables.md>) the entire table.

### Examples and code snippets

The following examples with code snippets are provided:

- [Creating Dynamic Data](https://docs.jigx.com/examples/creating-dynamic-data)
- [Reading Dynamic Data](https://docs.jigx.com/examples/reading-dynamic-data)
- [Updating Dynamic Data](https://docs.jigx.com/examples/updating-dynamic-data)
- [Deleting Dynamic Data](https://docs.jigx.com/examples/deleting-dynamic-data) (deletes records in the Dynamic Data table)

### See also

[Creating columns & data records](<./Creating columns _ data records.md>)
