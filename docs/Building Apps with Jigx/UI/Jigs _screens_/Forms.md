---
title: Forms
slug: zMXR-forms
description: Building forms that use data in your Jigx app
createdAt: Tue Jun 07 2022 12:14:00 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Feb 12 2025 18:56:21 GMT+0000 (Coordinated Universal Time)
---

:::::VerticalSplit{layout}
:::VerticalSplitItem
::Image[]{alt="Form" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/_B209h4pNhxbCGth1pKtj_forms.PNG" size="60" caption="Form"  position="center" }
:::

::::VerticalSplitItem
In this guide, you will learn how to create forms with Jigx. Forms are mainly used to collect and update data for various data sources.

We will use Dynamic Data to store the data. If you want to learn more about Dynamic Data and its capabilities, check out this guide: [Dynamic Data](<./../../Data/Data Providers/Dynamic Data.md>)

:::hint{type="success"}
As we will use Dynamic Data for storing the data in this guide, please read the section below about *Defining a Dynamic Data table* before proceeding to the next part.
:::
::::
:::::

## Defining a Dynamic Data table

Before we can start creating records in Dynamic Data, our table has to be defined in the solution:

1. In your solution, go to the *default.jigx* file in the *databases* folder and add the following YAML:

:::CodeblockTabs
databases/default.jigx

```yaml
tables:
  form: null
```
:::

The next time when you will publish your solution to Jigx, it will create a table in Dynamic Data for your solution. You can always log in to the<a href="https://manage.jigx.com" target="_blank"> Jigx Management </a>and navigate to the *Data* area of your solution to check the tables and contents. We will use this table in this guide for storing the form data.

Now you can proceed to the next part, [Creating a Record](<./Forms/Creating a Record.md>) to get familiar with forms.

