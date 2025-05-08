---
title: Authorized users
slug: txc_-rls
description: Learn how to assign authorized users in the management system with this comprehensive document. Find instructions on adding users as owners or members, and discover how to add groups as members. Don't miss out on configuring authorized users in YAML using
createdAt: Mon Sep 25 2023 17:55:17 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Oct 30 2023 09:46:43 GMT+0000 (Coordinated Universal Time)
---

## Assigning Authorized Users

![Dynamic data record authorized users](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/yG-30i4j8ttnpK4eaxz_h_rls-authorizeduserconfig.png "Dynamic data record authorized users")

1. Open Jigx Management, select the **solution** option, and browse to the required solution.
2. Click on the **Data **option in the navigation pane.
3. Select the required **table** from the Tables list in the right-hand pane.
4. Click on an individual row to open the **Edit record** pane.
5. &#x20;Click on the **Authorized Users** tab.
6. Add users either as Owners or Members. Groups can only be added as Members.
7. Click **Save**.
8. Selecting the **Custom** restriction requires selecting specific groups, owners, and members. 
9. Open the **Column settings** by clicking the gear icon at the top of the data table and check the Authorized Users checkbox.  The Authorized User column is now visible in the table.

**Authorized users** can be configured in the YAML in Jigx Builder by specifying values for the `Owner` and `Member` keys in the CREATE and UPDATE methods on `action.execute-entity` and `action.submit-form` for the `data_provider_Dynamic`.

:::CodeblockTabs
Dynamic -data-provider

```yaml
actions:
  - children:
      - type: action.submit-form
        options:
          formId: expense-form
          provider: DATA_PROVIDER_DYNAMIC
          title: Create Record
          entity: default/charts
          method: create
          goBack: previous
          authorized:
            members:
            - 'hr-group'
            - 'finance-group'
            - 'mary@global.com'
            owners:
            - =@ctx.components.email.state.value  
```
:::

