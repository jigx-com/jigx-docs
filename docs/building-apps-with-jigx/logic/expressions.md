# Expressions

Expressions allow you to structure and manipulate data before binding it to the UI components. Expressions are JSONata-based. JSONata is a lightweight query and transformation language for JSON data. It also provides a rich complement of built-in operators and functions for manipulating and combining data.

{% hint style="info" %}
Expressions are JSONata language-based. Learn more about [JSONata](https://jsonata.org/) and try out your expressions in their [JSONata Exerciser](https://try.jsonata.org/). The root element of Expressions in .jigx files always starts with "@ctx" vs. "$$." in JSONata Exerciser (e.g. @ctx.data vs.$$.data). Jigx supports shorthand $ expressions for JSONata.
{% endhint %}

## Shared expressions

The shared expressions can be set either in the index.jigx file or in the jig itself. The expressions property is used for this and allows you to choose a custom name for the expression and save a value.

### Global expressions set in the index.jigx

Expressions that are set in the index.jigx are reusable throughout your whole solution by referencing the global expression in the jig. Create the reference to the global expression by using `=@ctx.expression.``name` in the jig.

{% tabs %}
{% tab title="index.jigx" %}
```yaml
title: jigx-samples
name: jigx-samples

expressions:
  lat: =@ctx.system.geolocation.coords.latitude
  lng: =@ctx.system.geolocation.coords.longitude
```
{% endtab %}

{% tab title="expressions.jigx" %}
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
{% endtab %}
{% endtabs %}

### Expressions set inside the jig

These expressions are only available in the jig itself.

{% tabs %}
{% tab title="shared-expression" %}
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
{% endtab %}

{% tab title="datasource" %}
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
{% endtab %}
{% endtabs %}

## Expression structure

{% hint style="warning" %}
Avoid using state keywords, such as `component`, as `instanceId` values in expressions. Doing so will cause an "Expression is not valid" error in the app.
{% endhint %}

Using IntelliSense in Jigx Builder shows where and when you can add an expression by displaying the `=$` or `=@ctx`. In Jigx expressions always start with `=`. Jigx converts `@ctx.` to `$$.` when executing expressions in JSONata.

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

<table><thead><tr><th width="142.046875">Use</th><th width="221.66015625">Description</th><th>Example</th></tr></thead><tbody><tr><td>datasource</td><td>To call data from a datasource</td><td><code>=@ctx.datasource.mydata.datacolumn</code></td></tr><tr><td>component</td><td>Used inside a component to reference data in that component</td><td><code>=@ctx.component.state.value</code></td></tr><tr><td>components</td><td>Used in a jig to reference data from various components in that jig</td><td><code>=@ctx.components.list.state.filter</code></td></tr><tr><td>current item</td><td>Use data in the current component</td><td><code>=@ctx.current.item.value</code></td></tr><tr><td>jig</td><td>Pull data in from another jig</td><td><code>=@ctx.jig.inputs.jigname.description</code></td></tr><tr><td>jigs</td><td>Pull data in from multiple jigs</td><td><code>=@ctx.jigs.</code></td></tr><tr><td>organization</td><td>Reference the name or id of the Jigx <a href="https://docs.jigx.com/organization-settings">organization</a></td><td><code>=@ctx.organization.name</code></td></tr><tr><td>solution</td><td>Reference the Jigx <a href="https://docs.jigx.com/solution-details">solution</a></td><td><code>=@ctx.solution.name</code></td></tr><tr><td>system</td><td>Get data about various <a href="https://docs.jigx.com/examples/jigx-variables#quSXJ">system</a> values such as offline status</td><td><code>=@ctx.system.isOffline</code></td></tr><tr><td>user</td><td>Reference data about the current Jigx <a href="https://docs.jigx.com/users">user</a></td><td><code>=@ctx.user.displayName</code></td></tr></tbody></table>

## Advanced expressions

Advanced expressions are helpful when you need to filter an array of records to display specific data and perform expression transformations over the data. So, instead of writing complicated procedures and statements, you can run [JSONata expressions](https://docs.jigx.com/examples/advanced-expressions) to get the result. You can format the expression strings and have them inline or multi line.

### Inline

When you are writing advanced expressions, make sure you have the expression starting with '=' inside the quotes, as shown below:

{% code title="advanced-expression.jigx" %}
```yaml
text: "=(@ctx.datasources.table.field1 = '1' ? 'Jane' :'Rob')
  & ' ' &
  (@ctx.datasources.table.field2 = '2' ? 'Derek' :'Doe')"
```
{% endcode %}

### Multiline

You can write advanced expressions as multiline, for better readability and cleaner code formatting. When writing a multiline expression, make sure you have the expression in quotes and the next line must be indented on the same level as shown below.

{% code title="advanced-expression.jigx" %}
```yaml
title: "=(@ctx.datasources.table.field1 = '1' ? 'Jane' :'Rob')
  & ' ' &
  (@ctx.datasources.table.field2 = '2' ? 'Derek' :'Doe')"
```
{% endcode %}

## JavaScript expressions

You can use JavaScript functions in expressions to build logic into your solution. This makes repetitive and complex tasks less taxing and makes the code easier to read, understand, and debug. JavaScript functions surface as an expression in the YAML in Jigx Builder.

Wherever you can add an expression, you can use JSONata, Regex, JavaScript functions, or a combination of these to create logic in your app.

### What is Supported?

* Only .js files containing JavaScript functions are supported. Creating any file in the scripts folder, automatically adds the .js extension.
* Currently, only [date-fns](https://date-fns.org/) libraries are supported. If you require other JavaScript libraries, contact [support@jigx.com](https://mailTo:support@jigx.com).
* Functions that call web services are not supported.

### How does it work?

![JavaScript functions](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-qPGps_FEg_j8bYY9gcbaP-20240930-074153.gif)

**Create the JavaScript function**

* Open a solution in Jigx Builder.
* Create a new file under the **scripts/expressions** folder and save it with a .js extension, for example, functions.js.
* Within this file, you can define your functions.
  * For a single functions, you simply write the function definition.
  * For multiple functions, you can define each function in a single file or separate then into their own files.
* Each function must be prefixed with **export**, for example, `export function helloWorld() { return 'Hello World' }`
* **Import** is used to define the format for a specific function, for example, `import { addDays, isWeekend, format } from 'date-fns'; export function getNextBusinessDay(date) { let nextDay = addDays(date, 1); while (isWeekend(nextDay)) { nextDay = addDays(nextDay, 1); } return format(nextDay, 'MMMM d, yyyy'); }`

**Call the JavaScript function in an expression**

* In a jig, where you configure an expression, use IntelliSense to surface the defined functions from the script/expression js files.
* IntelliSense provides the javascript language options for selection starting with the `=$` shortcut followed by the JavaScript file name and then the function name, such as `=$functionFileName.functionName`, for example, `=$jsfunctions.helloWorld()`.

### Considerations

* One or more functions can be defined in a single JavaScript file. This caters for the exporting of files.
* Multiple JavaScript files can be added under the script > expression folder.
* In an expression, you can have functions inside functions, see [tax calculation](https://docs.jigx.com/examples/javascript-expressions#QhBMT) for an example.
* JavaScript files are recognized throughout the solution and can by reused in multiple jigs.
* JavaScript functions are not a replacement for JSONata expressions. Each has its purpose; combining the two will empower you while creating apps. In certain instances, JSONata is inline and can be quicker and easier than using a JavaScript function, such as concatenating first and last names.
* JavaScript functions can be used instead of regex expressions used for validation. For example, JavaScript functions can be used to format a phone number rather than regex to validate if it is in the correct format.
* Use _F12_ to navigate from an expression to the JavaScript function script file. See [Go to Definition](../jigx-builder-_code-editor_/editor.md).
* From the script file use _shift + F12_ or right-click and select [Go to References](../jigx-builder-_code-editor_/editor.md) to see where all the script file is used in expressions.

## JSONata and Regular expressions

In Jigx you can combine a JSONata expression with a Regex expression to create a validation pattern and provide a message if the pattern does not match. See [validation](validation.md) and [regex expression examples](https://docs.jigx.com/examples/regex-expressions) for more information.

## Expression examples

Expressions are a powerful and flexible way to transform and extract data for use in a Jigx App. Below are links to examples showing how JSONata expressions can be used when creating apps.

<table><thead><tr><th width="212.01171875">JSONata expressions</th><th>Example of use</th></tr></thead><tbody><tr><td><a href="https://docs.jigx.com/examples/arrays">Arrays</a></td><td>Create filtered lists from arrays and handling arrays with SQL and Dynamic Data</td></tr><tr><td><a href="https://docs.jigx.com/examples/aggregation">Aggregation</a></td><td>To return minimum, maximum or an average value in an array.</td></tr><tr><td><a href="https://docs.jigx.com/examples/boolean">Boolean</a></td><td>Evaluate data to find a true or false result.</td></tr><tr><td><a href="https://docs.jigx.com/examples/comparison-operators">Comparison Operators</a></td><td>Compare values in data and use the value in a conditional logical expression, e.g., is an amount greater than 100.</td></tr><tr><td><a href="https://docs.jigx.com/examples/date-and-time">Date &#x26; Time</a></td><td>Return a date and time in various formats, e.g., ISO 8601.</td></tr><tr><td><a href="https://docs.jigx.com/examples/path-operators">Path Operators</a></td><td>Navigate and access specific elements or properties within a data set, e.g., for filtering or searching.</td></tr><tr><td><a href="https://docs.jigx.com/examples/functional-programming">Functional Programming</a></td><td>Compare values or display data based on certain conditions and using logical statements, e.g., adding HTML variable in content, or a multi-select as a functionParameter.</td></tr><tr><td><a href="https://docs.jigx.com/examples/jigx-variables">Jigx Variables</a></td><td>Jigx variable set used in expressions to manipulate data specific to a Jigx App, e.g., determining the logged-in user, or the organization and solution.</td></tr><tr><td><a href="https://docs.jigx.com/examples/predicate-queries">Predicate Queries</a></td><td>Used for query refinement.</td></tr><tr><td><a href="https://docs.jigx.com/examples/string">String</a></td><td>There are many uses for using string expressions, these can be to concatenate two strings to display multiple data records in one row or write numbers as strings, or select only a few characters from the whole string.</td></tr><tr><td><a href="https://docs.jigx.com/examples/advanced-expressions">Advanced expressions</a></td><td>Advanced expressions are helpful when you need to filter an array of records to display specific data and perform expression transformations over the data.</td></tr><tr><td><a href="https://docs.jigx.com/examples/regex-expressions#1Txjd">Regex + JSONata</a></td><td>Create validation for text fields by combining JSONata and Regex expressions.</td></tr><tr><td><a href="https://docs.jigx.com/examples/javascript-expressions">JavaScript expressions</a></td><td>JavaScript functions allow you to write modular and reusable code, by encapsulating specific functionality within JavaScript functions and calling the function in an expression.</td></tr></tbody></table>

### See Also

* [Expressions - cheatsheet](expressions-1/expressions-cheatsheet.md)
* [Expression Examples](https://docs.jigx.com/examples/expressions)
* [Regex expressions](https://docs.jigx.com/examples/regex-expressions)
* [JavaScript expressions](https://docs.jigx.com/examples/javascript-expressions)
