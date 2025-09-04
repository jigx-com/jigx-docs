# Expressions - cheatsheet

Jigx wants to help you build solutions quickly and easily. To help you do this, here is a list of functionality or data results you might want to use in your app with the expression used to achieve it. This is a starting point; you can adapt or add to the expression as needed to get the expected data results when building solutions. Refer to the [Expressions](https://docs.jigx.com/expressions) section in the **Examples** tab for working examples and code snippets for various JSONata expressions.

{% hint style="info" %}
Expressions are JSONata language-based. Learn more about [JSONata](https://jsonata.org/) and try out your expressions in their [JSONata Exerciser](https://try.jsonata.org/). The root element of Expressions in .jigx files always starts with "@ctx" vs. "$$." in JSONata Exerciser (e.g. @ctx.data vs.$$.data). Jigx supports shorthand $ expressions for JSONata.&#x20;
{% endhint %}

### Create Filters on a list (Path Operator expression)

{% code overflow="wrap" %}
```yaml
=$filter(@ctx.datasources.filter-list, function($v){$contains($string($v.status), $string(@ctx.components.filter-list.state.filter != null ? @ctx.components.filter-list.state.filter:'')) })[]
```
{% endcode %}

### Create Search for a list (Path Operator expression)

{% code overflow="wrap" %}
```yaml
=$filter(@ctx.datasources.dmsrole-nonlife, function($v){ @ctx.datasources.dmsrole-nonlife ? $contains($string($v.DMSRole),$string(@ctx.components.RosterPositionID.state.searchText != null ? @ctx.components.RosterPositionID.state.searchText:'')) :true})[]
```
{% endcode %}

### Create a placeholder (Boolean expression)

See [tips and tricks when using placeholders](https://community.jigx.com/t/tips-tricks-use-placeholders/78) for additional information.

```yaml
placeholders:
  - when: =$count(@ctx.datasources.employees-dynamic) > 0 ? false :true 
    title: There is no data
    icon: missing-data
```

### Check if a field's value is Null (Boolean expression)

```yaml
=@ctx.solution.state.missionNumber != null ? true: false
```

```yaml
=$type(@ctx.current.item.EngineStop) = 'null' ? true: false
```

```yaml
=$count(@ctx.datasources.data.id) = 0 true:false
```

### Evaluate PathsData (String Function expression)

```yaml
=$eval(@ctx.current.item.pathsData)
```

### Use evaluate to change data text to JSON object

```yaml
=$eval(@ctx.datasources.weatherData.temperatures_max)
```

### Base64 image (String expression)

```yaml
="data:image/png;base64," & @ctx.datasources.mydata.data
```

### String to number (String expression)

```yaml
=($number(@ctx.datasources.tmra-graph.Total) >= 5)
```

```yaml
=($number(@ctx.datasources.tmra-graph.Total) < 8) ? true : false
```

### Number to string (String expression)

```yaml
=$string(@ctx.current.item.ID)
```

### Combining first and last name (Concatenate)

```yaml
=(@ctx.current.item.firstName & ' ' & @ctx.current.item.lastName)
```

### Splitting display name into first and last name (String expression)

{% code overflow="wrap" %}
```yaml
=$substring($substringBefore(@ctx.inputs.info.FromUserDisplayName, ' '), 0, 1)
```
{% endcode %}

### Show text and split name and surname and only displaying name (String expression)

```yaml
='Hello, ' & $substringBefore(@ctx.user.displayName, ' ')
```

### Show text followed by user's display name

```yaml
="Welcome " & @ctx.user.displayName
```

### Two letter placeholder for avatar (String expression)

{% code overflow="wrap" %}
```yaml
=$uppercase($substring($substringBefore(@ctx.current.item.firstName, " "), 0, 1) & $substring($substringAfter(@ctx.current.item.lastName, " ") , 0, 1) )
```
{% endcode %}

### True or False ? (Boolean expression)

```yaml
=$boolean(@ctx.datasources.tmra.TwoPilots) ? true : false
```

### Adding an expression into a string

```yaml
('Hello, my name is ' & @ctx.user.displayname)
('Day ' & @ctx.datasource.mydata.date & ' agenda')
"Day one agenda"
```

### Working with Date and Time expressions

### Convert UTC to milliseconds

```yaml
=$toMillis()
```

### Convert millisecond to UTC

```yaml
=$fromMillis()
```

### Transform any date to new format

{% code overflow="wrap" %}
```yaml
=$fromMillis($toMillis(@ctx.inputs.info.EndDate), '[M01]/[D01]/[Y0001]', @ctx.system.timezone.offset)
```
{% endcode %}

### Add days to date + convert to local timezone + format

{% code overflow="wrap" %}
```yaml
=$fromMillis($toMillis(@ctx.datasources.mission-list-global.CrewNotified) + 86400000,'[Y0001]-[M01]-[D01]T[H01]:[m01]:[s01].[s001]Z',@ctx.system.timezone.offset)
```
{% endcode %}

### Set date and time in datePicker to local timezone + format

{% code overflow="wrap" %}
```yaml
=$fromMillis($toMillis(@ctx.components.datePicker.state.value), '[M01]/[D01]/[Y0001] [H01]:[m01]:[s01]', $string(@ctx.system.timezone.offset))
```
{% endcode %}

### Add days from current date and add additional time from current time

{% code overflow="wrap" %}
```yaml
=$fromMillis($toMillis($now()) + 5 * 60 * 60000 + @ctx.current.item.eventEnd * 3600000)
```
{% endcode %}

### Get currently logged in user (Jigx system expression)

Results can include id, email, name.

```yaml
=@ctx.user.displayName
```

### Is the mobile device offline (Jigx system expression)

```yaml
=@ctx.system.isOffline = true
```

### Get country flag icons using system (Jigx system expression)

### Create a unique GUID

```yaml
=$uuid()
```

### Formatting Numbers (Numeric functions)

```yaml
=$formatNumber(@ctx.inputs.info.TotalSQft, '#,###')
```

### Sorting an array of objects using a lambda (embedded) function

This example with data and the result can be viewed in [JSONata exerciser](https://try.jsonata.org/nRQKeRm2s).

{% code overflow="wrap" %}
```yaml
$sort($.{"id": id,"amount":amount,"name":name}, function($l, $r) { $l.amount > $r.amount})
```
{% endcode %}

### Setting up complex objects with an embedded array

This example with data and the result can be viewed in [JSONata exerciser](https://try.jsonata.org/DrGnGcScd).

```yaml
$.{"message": {"subject": subject,"body": {"contentType": "Text","content":
  messageBody},"toRecipients": toAddresses#$i.{"emailAddress":
  {"address":$}}[]}}
```

### Create a basic join on a static datasource to a local datasource &#x20;

{% code overflow="wrap" %}
```yaml
=@ctx.datasources.staticdatabase@$p.$merge([$p, @ctx.datasources.localdatabase[id = $p.id]]
```
{% endcode %}

### Transform longitude and latitude data to show markers on a location component

{% code overflow="wrap" %}
```yaml
markers:
   data: |
        =@ctx.datasources.jobs.{"lng": $number($.lng), "lat": $number($.lat)}
```
{% endcode %}

### Find the value relative to the current node so all paths are relative to it

```yaml
=$.path.to.value
```

### &#x20;Find the value relative the root node of the supplied context, no matter what is the current node

Jigx converts `@ctx.` to `$$.` when executing expressions in jsonata

```yaml
=$$.path.to.value
```

### Use the JSONata built-in index parameter combined with a filter

```yaml
=@ctx.datasources.questions#$i.answer[$i=3]
```

### Update multiple records in execute-entities (operators > transform)

To update multiple records using the [Execute-entities](https://docs.jigx.com/examples/readme/actions/execute-entities) action, you can use the expression below.

{% code overflow="wrap" %}
```yaml
data: =ctx.datasources.customers ~> | $ | { "customerType": "Bronze "} |  
```
{% endcode %}

### Validate text fields using JSONata + Regex expression

See the examples provided in [Regex expressions](https://docs.jigx.com/expressions#PD18u).

### Use JavaScript functions in expressions

See more examples provided in [JavaScript expressions](https://docs.jigx.com/expressions#_q4V3).

{% code overflow="wrap" %}
```yaml
# Calculate loan repayment expression cofigured in a jig
value: =$jsfunctions.formatCurrency($jsfunctions.calculateLoanPayment(@ctx.components.principal.state.value, @ctx.components.annualRatePercent.state.value, @ctx.components.loanDuration.state.value),'$')
```
{% endcode %}

{% code overflow="wrap" %}
```javascript
/* JS function is added under scripts/expressions folder
*/
export function formatCurrency(amount, currencySymbol) {
  return currencySymbol + parseFloat(amount).toFixed(2).replace(/\d(?=(\d{3})+\.)/g, '$&,');
}
```
{% endcode %}

### JavaScript checking any value for false

Checks for undefined, false, empty string, empty objects, null, empty array, and boolean false. It is better than using (`jsonataTruthy`) or `$empty` or `$exist` in JSONata as it checks for all scenarios and returns false in a single function, whereas using a combination of JSONata functions is necessary to return false.

{% code overflow="wrap" %}
```javascript
export function juthy(input) {
  if (
    input === undefined ||
    input === false ||
    input === '' ||
    (typeof input === 'object' && input !== null && Object.keys(input).length === 0) ||
    input === null ||
    (Array.isArray(input) && input.length === 0)
  ) {
    return false
  }
  return true
}
```
{% endcode %}
