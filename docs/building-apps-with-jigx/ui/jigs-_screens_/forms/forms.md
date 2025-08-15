# Forms

:::::VerticalSplit{layout="middle"} :::VerticalSplitItem ::Image\[]{alt="Form" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/\_B209h4pNhxbCGth1pKtj\_forms.PNG" size="60" caption="Form" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/\_B209h4pNhxbCGth1pKtj\_forms.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"} :::

::::VerticalSplitItem In this guide, you will learn how to create forms with Jigx. Forms are mainly used to collect and update data for various data sources.

We will use Dynamic Data to store the data. If you want to learn more about Dynamic Data and its capabilities, check out this guide: [Dynamic Data](../../../data/data-providers/dynamic-data/dynamic-data.md)

:::hint{type="success"} As we will use Dynamic Data for storing the data in this guide, please read the section below about _Defining a Dynamic Data table_ before proceeding to the next part. ::: :::: :::::

## Defining a Dynamic Data table

Before we can start creating records in Dynamic Data, our table has to be defined in the solution:

1. In your solution, go to the _default.jigx_ file in the _databases_ folder and add the following YAML:

:::CodeblockTabs databases/default.jigx

```yaml
tables:
  form: null
```

:::

The next time when you will publish your solution to Jigx, it will create a table in Dynamic Data for your solution. You can always log in to the :Link\[Jigx Management]{href="https://manage.jigx.com" newTab="true" hasDisabledNofollow="false"} and navigate to the _Data_ area of your solution to check the tables and contents. We will use this table in this guide for storing the form data.

Now you can proceed to the next part, [Creating a Record](creating-a-record.md) to get familiar with forms.
