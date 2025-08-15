# Salesforce

Jigx easily integrates with your Salesforce instance, allowing you to share data about customers, sales processes, marketing campaigns, and more. The Jigx Salesforce provider exposes the standard and custom Salesforce objects. You can manage your customer data, such as leads, contacts, accounts, and opportunities, using CRUD methods.

::embed\[]{url="https://vimeo.com/846066533"}

::::VerticalSplit{layout="middle"} :::VerticalSplitItem The endless possibilities depend on your specific needs and objectives and the type of data you want to show in your app. Build an app that provides current data about sales opportunities; deals won, leading sales teams, and open cases or tasks, through interactive Jigx components such as [charts](https://docs.jigx.com/examples/charts), [lists](https://docs.jigx.com/examples/LQFt-list), [widgets](salesforce.md), or [steppers](https://docs.jigx.com/examples/stepper). :::

:::VerticalSplitItem ::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/HVVwC60g4xu-W3wdJBW8O\_salesfdashboard.PNG" size="76" position="center" caption="Salesforce Dashboard" alt="Salesforce Dashboard" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/HVVwC60g4xu-W3wdJBW8O\_salesfdashboard.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"} ::: ::::

## Architecture

The Salesforce provider uses the Jigx Cloud service, where the data passes through the service and is not stored. There is an intermediate layer between the mobile device and Salesforce. Many records can exist in Salesforce; as a result, Jigx fetches the records in batches.

## Prerequisites

1. You must have an active Salesforce account.
2. Permissions set in Salesforce are adhered to in the Jigx App. This means you can see the same data in the app as in Salesforce. When viewing the data in the Jigx App you will be prompted to sign in with your Salesforce credentials.
3. Building apps using the Salesforce provider requires a pre-existing knowledge of Salesforce objects, their records, fields, tables, and variables. Take note of the required fields for each table. An overview of Salesforce objects is available in the Salesforce platform; follow the path Settings > Setup Home > Object Manager > Schema Builder or refer to the :Link\[Salesforce object reference documentation]{href="https://developer.salesforce.com/docs/atlas.en-us.object\_reference.meta/object\_reference/sforce\_api\_objects\_concepts.htm" newTab="true" hasDisabledNofollow="false"}. Tools such as [https://workbench.developerforce.com/login.php](https://workbench.developerforce.com/login.php) are helpful when building queries to return the correct Salesforce data.

## Supported methods:

* [Create](https://docs.jigx.com/examples/create-records-in-objects)
* [Delete](https://docs.jigx.com/examples/delete-records-in-objects)
* [Save](https://docs.jigx.com/examples/save-and-update-records-in-objects)
* [Update](https://docs.jigx.com/examples/save-and-update-records-in-objects)
* [Read/list](https://docs.jigx.com/examples/list-records-in-objects)

## Syncing data

By default, the provider returns all Salesforce fields and columns. Consider the data size shown in the app and the number of columns you want returned. Salesforce can have many records, and showing large numbers of records can impact the performance of the app, your data plan, and your mobile device. Try to return just the data you require in the app and restrict the columns; this is achievable using queries. Below is an example of a query returning data between specific dates from the Salesforce Opportunity object.

```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_LOCAL
  entities:
    - Opportunity
  query: >
    select id , sum(json_extract(data , '$.Amount')) as totalsales  from
    Opportunity
    where 
    json_extract(data, '$.StageName') = 'Closed Won'
    and json_extract(data, '$.CloseDate') between '2020-01-01' and '2020-03-31'
```

## Considerations

1. The permission set assigned to a user in Salesforce determining what they can view and interact with is adhered to in the Jigx App allowing the user to view and interact with only the data they have rights to.
2. Limitation - you can use the Salesforce provider to create a list of reports in Salesforce but cannot run the report from the app.
3. See [Using the Salesforce provider](using-the-salesforce-provider.md) section for code examples on referencing multiple Salesforce objects, queries that define the data to be returned and creating joins between objects using expressions.
4. Salesforce is set up for your individual organization and each instance will be different, the examples in th section are provided for guidance on using the Salesforce provider's methods and must be adapted to work with your specific instance.
5. Tools such as [https://workbench.developerforce.com/login.php](https://workbench.developerforce.com/login.php) are helpful when building queries to return the correct Salesforce data. You can copy and paste the queries into Jigx Builder.

## Examples and code snippets

The following examples with code snippets are provided:

* [Create records in objects](https://docs.jigx.com/examples/create-records-in-objects)
* [Delete records in objects](https://docs.jigx.com/examples/delete-records-in-objects)
* [Save & update records in objects](https://docs.jigx.com/examples/save-and-update-records-in-objects)
* [List records in objects](https://docs.jigx.com/examples/list-records-in-objects)
