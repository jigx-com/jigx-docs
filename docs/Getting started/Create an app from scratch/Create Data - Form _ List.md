---
title: Create Data - Form & List
slug: Aoch-hello-jigx-customer-forms-and-list
description: Learn how to build forms and store customer data in Jigx's Dynamic Data store with this comprehensive document. Discover two methods for saving form data to a database and gain step-by-step instructions for creating forms, lists, views, and more. Enhance 
createdAt: Wed Apr 12 2023 10:36:33 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Feb 12 2025 18:00:25 GMT+0000 (Coordinated Universal Time)
---

## Overview

Learn how to build [forms](<./../../Building Apps with Jigx/UI/Jigs _screens_/Forms.md>) that create a new customer record that gets stored in the built-in Jigx  data store called [Dynamic Data](<./../../Building Apps with Jigx/Data/Data Providers/Dynamic Data.md>). The data record is created in the data store by using the submit [action](). Once the record is created you can view, edit and list the data records using queries that return the record details from SQLite. For more information on the supported data providers read the [Data](<./../../Building Apps with Jigx/Data.md>) section.

:::hint{type="info"}
There are **two methods** to save data collected on a form to a database. 

**The first method is to use the form submit action.** The submit form action automatically matches the `instanceIds` of the controls on the jig and creates a record in the local SQLite table with each `instanceIds` as a property for the JSON object in the Data column.

**The second method is to use an execute entity action.** The execute entity action allows you to specify the data properties for the SQLite table. You have more granular control over the saved values and can include expressions.
:::

::::Tabs
:::Tab{title="Form & list widgets"}
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/aiM8WcC5QYFbhGg92rDll_formlistlight.PNG" size="30" caption="Form and list widgets" alt="Form and list widgets"}
:::

:::Tab{title="New customer form"}
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/AVD4yyxxzg_aAqfhOQoUW_newcustomerlight.PNG" size="30" caption="New customer form" alt="New customer form"}
:::

:::Tab{title="View customer"}
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZU-8wX65Q12CBTnocab62_viewcustomerlight.PNG" size="30" caption="View customer jig" alt="View customer jig"}
:::

:::Tab{title="Edit customer"}
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Ga3y05NxNud10RQnBSp1b_editcustomerlight.PNG" size="30" caption="Edit customer jig" alt="Edit customer jig"}
:::
::::

:::hint{type="success"}
We recommend you build out all the solution steps for the [Create an app from scratch](docId:8SeLgEopqiL70vPoV72WY), as each solution step builds on the previous step until you have a functioning mobile app.
:::

## Steps

1. Open the Hello-Jigx solution in the Jigx Builder in VS Code.
2. [Create a new customer form](<./Create Data - Form _ List/Create a new customer form.md>): Add the `new-customer.jigx` file with type `jig.default`, the form uses a two-column layout.  Add the `component.form` to create the three fields on the form. Add the `action.submit-form` to submit the form data to the Jigx SQLite dynamic data store.
3. [Create a customer list with data](<./Create Data - Form _ List/Create a customer list with data.md>) Add the `list-customer.jigx` file with type `jig.list`. Specify the dynamic data provider and the `query` that returns the customer's details in the list.
4. [Create a view of the customer record](<./Create Data - Form _ List/Create a view of the customer record.md>): Add the `view-customer.jigx` file with type `jig.default`, specify the `datasource.sqlite`, and the `query` to return a view of the customer and their details.
5. [Edit a customer record](<./Create Data - Form _ List/Edit a customer record.md>): Add the `edit-customer.jigx` file with type `jig.default`, specify the `datasource.sqlite`, the `query` to return the specified customer and their details. Add `component.form` to display the returned data. Then add the `action.submit-form` with the `method: update` to save the changes to the customer's details.
6. [Add the form & list to the Home Hub](<./Create Data - Form _ List/Add the form _ list to the Home Hub.md>) by adding their `jigIds` to the `tabs` in the `index.jigx` file.
7. [Publish your project](<./Create the Calendar/Publish your project.md>).
8. [Run the updated solution](<./Create the Calendar/Run the updated solution.md>) in the Jigx mobile app, click on the customer icon, this opens a new customer form. Add details for a customer. Tap back to return to the Home Hub , the customer will appear in the customer list widget. You can view the customer by tapping on the customer name in the list.

## GitHub Samples

You can download the <a href="https://github.com/jigx-com/jigx-samples/tree/main/quickstart/hello-jigx-solution" target="_blank">Hello Jigx solution :Comment[project]{resolved="true" docCommentId="E51tXIu6Duc-MWAqTpoSp"} </a>on GitHub or build it yourself by following the detailed steps in this section.
