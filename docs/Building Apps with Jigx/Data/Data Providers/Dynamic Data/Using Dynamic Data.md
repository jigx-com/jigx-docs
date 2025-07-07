---
title: Using Dynamic Data
slug: cStY-using
createdAt: Tue Nov 21 2023 12:07:20 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu Aug 08 2024 09:35:26 GMT+0000 (Coordinated Universal Time)
---

Once you have created the Dynamic Data [tables](<./Creating tables.md>) as well as, [columns and data records](<./Creating columns _ data records.md>) the data can be used in multiple places in a solution.&#x20;

Dynamic Data can be:

- **Protected** - add Row Level Security (RLS) through security policies and authorization. For more information, see [Row Level Security](<./../../../../Administration/Solutions/Row Level Security.md>), [Data policies](<./../../../../Administration/Solutions/Row Level Security/Data policies.md>) and [Authorized users](<./../../../../Administration/Solutions/Row Level Security/Authorized users.md>).
- **Created** - create new records in Dynamic Data tables, for example, adding new employees. For code examples and snippets, see [Creating Dynamic Data](https://docs.jigx.com/examples/creating-dynamic-data).
- **Read** - Read the data to populate a [form](https://docs.jigx.com/examples/form), [list](https://docs.jigx.com/examples/LQFt-list), show a [location](https://docs.jigx.com/examples/foRN-location) and more. For code examples and snippets, see [Reading Dynamic Data](https://docs.jigx.com/examples/reading-dynamic-data).
- **Updated** -update existing records in Dynamic Data tables, for example, updating an employee's address. For code examples and snippets, see [Updating Dynamic Data](https://docs.jigx.com/examples/updating-dynamic-data).
- **Deleted** - delete existing records in Dynamic Data tables, for example, remove old contacts or out-of-stock products. For code examples and snippets, see [Deleting Dynamic Data](https://docs.jigx.com/examples/deleting-dynamic-data).

### As a datasource

The Dynamic Data provider is used in Jigx Builder in the SQLite datasource either inside a single jig (locally) or under the datasources folder structure (global), allowing the data to be called once and reused throughout the solution in multiple jigs. Write SQLite queries to return the exact data you need to work with.

:::CodeblockTabs
sqlite-datasource-dd

```yaml
# use the sqlite datasource with the dynamic data provider
type: "datasource.sqlite"
options:
  provider: DATA_PROVIDER_DYNAMIC
  entities:
    - entity: default/employee
  # write sqlite query syntax to return data needed in the jig/solution
  query: |
    SELECT 
      id, 
      '$.firstname', 
      '$.lastname', 
      '$.photo', 
      '$.birthdate', 
      '$.gender', 
      '$.email', 
      '$.phone', 
      '$.street', 
      '$.city', 
      '$.state', 
      '$.country', 
      '$.category', 
      '$.modify' 
    FROM [default/employees] WHERE '$.category' = "employee-detail"
```

:::

### In components

Once you have created the `datasource.sqlite` with the Dynamic Data provider as shown above, the data is referenced in components using [Expressions](./../../../Logic/Expressions.md), such as `=@ctx.datasources.employee`

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.dropdown
          instanceId: dropdown-in
          options:
            # use an expression to reference the dynamic data datasource to use in the form
            data: =@ctx.datasources.employee
            label: Select employees
            isSearchable: true
            item:
              type: component.dropdown-item
              instanceId: =@ctx.current.item.firstname
              options:
                # use an expression to reference the exact data entry to use in the drop-down component on the form
                value: =@ctx.current.item.firstname
                title: =@ctx.current.item.firstname
                subtitle: =@ctx.current.item.lastname
                leftElement:
                  element: avatar
                  text: ""
                  uri: =@ctx.current.item.photo
```

### In actions

**Execution** actions are designed to interact with specifically with data. The following actions can be used with the Dynamic Data provider either to create, update, delete, or sync data.

- [execute-entity](https://docs.jigx.com/examples/execute-entity)
- [execute-entities](https://docs.jigx.com/examples/execute-entities)
- [submit-form](https://docs.jigx.com/examples/submit-form)
- [sync-entities](https://docs.jigx.com/examples/sync-entities) for getting data to the device.

**Events** actions execute after an event is performed by a user or device. This event can be configured to use the Dynamic Data provider, for example, when refreshing a list jigby pulling down (onRefresh) use the `action.sync-entities` with the provider to refresh the data in the list. The following event actions are available.

- onRefresh
- onFocus
- onPress
- onLoad (only on index.jigx)
- onChange
- onDelete
- onButtonPress (only on calendar jigs)

For the complete list and code examples of available actions, see [actions](https://docs.jigx.com/examples/actions).

### Examples and code snippets

The following examples with code snippets are provided:

- [Creating Dynamic Data](https://docs.jigx.com/examples/creating-dynamic-data)
- [Reading Dynamic Data](https://docs.jigx.com/examples/reading-dynamic-data)
- [Updating Dynamic Data](https://docs.jigx.com/examples/updating-dynamic-data)
- [Deleting Dynamic Data](https://docs.jigx.com/examples/deleting-dynamic-data)
