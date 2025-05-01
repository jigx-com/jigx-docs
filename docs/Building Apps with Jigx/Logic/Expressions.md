---
title: Expressions
slug: 381L-expressions
description: Learn how to use expressions in Jigx to efficiently structure and manipulate data before binding it to UI components. This comprehensive document covers shared expressions for overall solution use, as well as specific expressions set within individual jig
createdAt: Tue Jun 07 2022 09:48:29 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Apr 23 2025 08:45:48 GMT+0000 (Coordinated Universal Time)
---

Expressions allow you to structure and manipulate data before binding it to the UI components. Expressions are JSONata-based. JSONata is a lightweight query and transformation language for JSON data. It also provides a rich complement of built-in operators and functions for manipulating and combining data.

:::hint{type="info"}
Expressions are JSONata language-based. Learn more about <a href="https://jsonata.org/" target="_blank">JSONata</a> and try out your expressions in their <a href="https://try.jsonata.org/" target="_blank">JSONata Exerciser</a>. The root element of Expressions in .jigx files always starts with "@ctx" vs. "$$." in JSONata Exerciser (e.g. @ctx.data vs. $$.data). Jigx supports shorthand $ expressions for JSONata.
:::

## Shared expressions

The shared expressions can be set either in the index.jigx file or in the jig itself. The expressions property is used for this and allows you to choose a custom name for the expression and save a value.

### Global expressions set in the index.jigx

Expressions that are set in the index.jigx are reusable throughout your whole solution by referencing the global expression in the jig. Create the reference to the global expression by using `=@ctx.expression.``name` in the jig.

:::CodeblockTabs
index.jigx

```yaml
title: jigx-samples
name: jigx-samples

expressions:
  lat: =@ctx.system.geolocation.coords.latitude
  lng: =@ctx.system.geolocation.coords.longitude
```

expressions.jigx

```yaml
title: Shared expressions example
type: jig.default

children:
  - type: component.entity
    options:
      children:
        - type: component.section
          options:
            title: Coordinates
            children:
              - type: component.entity-field
                options:
                  label: Current Latitude
                  value: =@ctx.expressions.lat
              - type: component.entity-field
                options:
                  label: Current Longitude
                  value: =@ctx.expressions.lng
```
:::

### Expressions set inside the jig

These expressions are only available in the jig itself.

:::CodeblockTabs
```yaml
title: Shared expressions example
type: jig.default

expressions:
  numberOfEmployees: =$count(@ctx.datasources.employee-list.id)
  address: =@ctx.datasources.employee-detail.street & ', ' &   @ctx.datasources.employee-detail.county & ', ' & @ctx.datasources.employee-detail.city
  employee: =@ctx.datasources.employee-detail.name & ' ' & @ctx.datasources.employee-detail.surname & ', ' & @ctx.datasources.employee-detail.position 
    
children:
  - type: component.entity
    options:
      isCompact: true
      children:
        - type: component.section
          options:
            title: All Employees
            children:
              - type: component.entity-field
                options:
                  label: Number of Employees
                  value: =@ctx.expressions.numberOfEmployees
        - type: component.section
          options:
            title: Employee detail
            children:
              - type: component.entity-field
                options:
                  label: Employee
                  value: =@ctx.expressions.employee
              - type: component.entity-field
                options:
                  label: Employee address
                  value: =@ctx.expressions.address
```

datasource.jigx

```yaml
datasources:
  employee-list:
    type: datasource.static
    options:
      data:
        - id: 1
          name: Karl 
          surname: Fisher
        - id: 2
          name: Lucy
          surname: Nelson
        - id: 3
          name: Mary
          surname: Gomez
        - id: 4
          name: John
          surname: Doe
  employee-detail:
    type: datasource.static
    options:
      data:
        - id: 1
          street: 89-55 Hudson Rd
          county: Bellerose
          city: NY
          name: Karl 
          surname: Fisher
          position: UX Designer
```
:::

## Expression structure&#x20;

:::hint{type="warning"}
Avoid using state keywords, such as `component`, as `instanceId` values in expressions. Doing so will cause an "Expression is not valid" error in the app.
:::

Using IntelliSense in Jigx Builder shows where and when you can add an expression by displaying the `=$` or `=@ctx`. In Jigxexpressions alwasy start with `=`. Jigx converts `@ctx.` to `$$.` when executing expressions in JSONata.

Adding an empty array index \[] in the path forces jsonata to return an array of one item versuses the normal behavior where it returns the item directly.

```none
=@ctx.datasources.value
[{}] => {}
[{},{}] => [{},{}]

=@ctx.datasources.value[]
[{}] => [{}] ← notice array of one
[{},{}] => [{},{}]
```

Expressions can be used in many ways when creating apps, here are common use cases:

| **Use**      | **Description**                                                     | **Example**                            |
| ------------ | ------------------------------------------------------------------- | -------------------------------------- |
| datasource   | To call data from a datasource                                      | `=@ctx.datasource.mydata.datacolumn`   |
| component    | Used inside a component to reference data in that component         | `=@ctx.component.state.value`          |
| components   | Used in a jig to reference data from various components in that jig | `=@ctx.components.list.state.filter`   |
| current item | Use data in the current component                                   | `=@ctx.current.item.value`             |
| jig          | Pull data in from another jig                                       | `=@ctx.jig.inputs.jigname.description` |
| jigs         | Pull data in from multiple jigs                                     | `=@ctx.jigs.`                          |
| organization | Reference the name or id of the Jigx [organization]()               | `=@ctx.organization.name`              |
| solution     | Reference the Jigx [solution]()                                     | `=@ctx.solution.name`                  |
| system       | Get data about various [system]() values such as offline status     | `=@ctx.system.isOffline`               |
| user         | Reference data about the current Jigx [user]()                      | `=@ctx.user.displayName`               |

## Advanced expressions

Advanced expressions are helpful when you need to filter an array of records to display specific data and perform expression transformations over the data. So, instead of writing complicated procedures and statements, you can run [JSONata expressions]() to get the result. You can format the expression strings and have them inline or multiline.

### Inline&#x20;

When you are writing advanced expressions, make sure you have the expression starting with '=' inside the quotes, as shown below:&#x20;

:::CodeblockTabs
advanced-expression.jigx

```yaml
text: "=(@ctx.datasources.table.field1 = '1' ? 'Jane' :'Rob') 
        & ' ' &
        (@ctx.datasources.table.field2 = '2' ? 'Derek' :'Doe')" 
```
:::

### Multiline&#x20;

You can write advanced expressions as multiline, for better readability and cleaner code formatting. When writing a multiline expression, make sure you have the expression in quotes and the next line must be indented on the same level as shown below.

:::CodeblockTabs
advanced-expression.jigx

```yaml
title: "=(@ctx.datasources.table.field1 = '1' ? 'Jane' :'Rob')
        & ' ' & 
        (@ctx.datasources.table.field2 = '2' ? 'Derek' :'Doe')" 
```
:::

## JavaScript expressions

You can use JavaScript functions in expressions to build logic into your solution. This makes repetitive and complex tasks less taxing and makes the code easier to read, understand, and debug. JavaScript functions surface as an expression in the YAML in Jigx Builder.

Wherever you can add an expression, you can use JSONata, Regex, JavaScript functions, or a combination of these to create logic in your app.

### What is Supported?

- Only .js files containing JavaScript functions are supported. Creating any file in the scripts folder, automatically adds the .js extension.
- Currently, only <a href="https://date-fns.org/" target="_blank">date-fns</a> libraries are supported. If you require other JavaScript libraries, contact <a href="https://mailTo:support@jigx.com" target="_blank">support\@jigx.com</a>.
- Functions that call web services are not supported.

### How does it work?

![JavaScript functions](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-qPGps_FEg_j8bYY9gcbaP-20240930-074153.gif "JavaScript functions")

**Create the JavaScript function**

- Open a solution in Jigx Builder.
- Create a new file under the **scripts/expressions** folder and save it with a .js extension, for example, functions.js.
- Within this file, you can define your functions.&#x20;
  - For a single functions, you simply write the function definition.
  - &#x20;For multiple functions, you can define each function in a single file or separate then into their own files.
- Each function must be prefixed with **export**, for example,&#x20;
  `export function helloWorld() {
  return 'Hello World'
  }`
- **Import** is used to define the format for a specific function, for example,
  `import { addDays, isWeekend, format } from 'date-fns';
  export function getNextBusinessDay(date) {
    let nextDay = addDays(date, 1);
    while (isWeekend(nextDay)) {
      nextDay = addDays(nextDay, 1);
    }
    return format(nextDay, 'MMMM d, yyyy');
  }`

**Call the JavaScript function in an expression**

- In a jig, where you configure an expression, use IntelliSense to surface the defined functions from the script/expression js files. &#x20;
- IntelliSense provides the javascript language options for selection starting with the  `=$` shortcut followed by the JavaScript file name and then the function name, such as `=$functionFileName.functionName`, for example, `=$jsfunctions.helloWorld()`.

### Considerations

- One or more functions can be defined in a single JavaScript file. This caters for the exporting of files.
- Multiple JavaScript files can be added under the script > expression folder.&#x20;
- In an expression, you can have functions inside functions, see [tax calculation]() for an example.
- JavaScript files are recognized throughout the solution and can by reused in multiple jigs.
- JavaScript functions are not a replacement for JSONata expressions. Each has its purpose; combining the two will empower you while creating apps. In certain instances, JSONata is inline and can be quicker and easier than using a JavaScript function, such as concatenating first and last names.
- JavaScript functions can be used instead of regex expressions used for validation. For example, JavaScript functions can be used to format a phone number rather than regex to validate if it is in the correct format.&#x20;
- Use *F12* to navigate from an expression to the JavaScript function script file. See [Go to Definition](<./../Jigx Builder _code editor_/Editor.md>).&#x20;
- From the script file use *shift + F12* or right-click and select [Go to References](<./../Jigx Builder _code editor_/Editor.md>) to see where all the script file is used in expressions.

## JSONata and Regular expressions

In Jigx you can combine a JSONata expression with a Regex expression to create a validation pattern and provide a message if the pattern does not match. See [validation](./Validation.md) and [regex expression examples]() for more information.

## Expression examples

Expressions are a powerful and flexible way to transform and extract data for use in a Jigx App. Below are links to examples showing how JSONata expressions can be used when creating apps.&#x20;

| **JSONata expressions**    | **Example of use**                                                                                                                                                                                                        |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Arrays]()                 | Create filtered lists from arrays and handling arrays with SQL and Dynamic Data                                                                                                                                           |
| [Aggregation]()            | To return minimum, maximum or an average value in an array.                                                                                                                                                               |
| [Boolean]()                | Evaluate data to find a true or false result.                                                                                                                                                                             |
| [Comparison Operators]()   | Compare values in data and use the value in a conditional logical expression, e.g., is an amount greater than 100.                                                                                                        |
| [Date & Time]()            | Return a date and time in various formats, e.g., ISO 8601.                                                                                                                                                                |
| [Path Operators]()         | Navigate and access specific elements or properties within a data set, e.g., for filtering or searching.                                                                                                                  |
| [Functional Programming]() | Compare values or display data based on certain conditions and using logical statements, e.g., adding HTML variable in content, or a multi-select as a functionParameter.                                                 |
| [Jigx Variables]()         | Jigx variable set used in expressions to manipulate data specific to a Jigx App, e.g., determining the logged-in user, or the organization and solution.                                                                  |
| [Predicate Queries]()      | Used for query refinement.                                                                                                                                                                                                |
| [String]()                 | There are many uses for using string expressions, these can be to concatenate two strings to display multiple data records in one row or write numbers as strings, or select only a few characters from the whole string. |
| [Advanced expressions]()   | Advanced expressions are helpful when you need to filter an array of records to display specific data and perform expression transformations over the data.                                                               |
| [Regex + JSONata]()        | Create validation for text fields by combining JSONata and Regex expressions.                                                                                                                                             |
| [JavaScript expressions]() | JavaScript functions allow you to write modular and reusable code, by encapsulating specific functionality within JavaScript functions and calling the function in an expression.                                         |

### See Also

- [Expressions - cheatsheet](<./Expressions/Expressions - cheatsheet.md>)
- [Expression Examples ]()
- [Regex expressions]()
- [JavaScript expressions]()&#x20;

