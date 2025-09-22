# Expressions - Common Patterns

## State Access

```yaml
=@ctx.solution.state.counter         # Global app state
=@ctx.jig.state.filter               # Screen state
=@ctx.components.email.state.value   # Component value
=@ctx.current.item.name              # Current list item
=@ctx.jig.inputs.customerId          # Navigation parameters
=@ctx.datasources.customers[0].name  # Datasource data
=@ctx.solution.state[@ctx.user.id]   # Dynamic bracket notation
```

## Safe Defaults

```yaml
=@ctx.user.displayName ?: @ctx.user.email ?: 'Unknown'  # Elvis - falsy fallback
=@ctx.solution.state.note ?? 'N/A'                      # Null coalesce
=@ctx.jig.state.total ~> $type = 'number'               # Type guard
=@ctx.components.form.state.isValid ? 'valid' : 'invalid'
```

## Actions Context

```yaml
=@ctx.actions.save.state.isPending    # Action status
=@ctx.actions.save.state.response     # Action result
=@ctx.actions.save.state.value        # Action value
=@ctx.actions.export.outputs.fileUri  # Action outputs
```

## Function Context (REST/SQL/SOAP)

```yaml
=@ctx.response                         # Function response
=@ctx.response.status                  # HTTP status  
=@ctx.response.body.items[0].id        # Response data
=@ctx.response.headers['Content-Type'] # Headers
=@ctx.function.parameters.search       # Function params
```

## Functions

### Built-in Functions

```yaml
# String
$uppercase("hello")         # "HELLO"
$lowercase("WORLD")         # "world" 
$substring("hello", 1, 3)   # "ell" 
$length("hello")            # 5
$trim("  spaces  ")         # "spaces"
$contains("hello", "ell")   # true
=@ctx.current.item.first & ' ' & @ctx.current.item.last

# Array  
$count(array)               # Length
$sum(numbers)               # Sum
$max(numbers) $min(numbers) # Min/max
$distinct(array)            # Unique values
$sort(array)                # Sort array
$reverse(array)             # Reverse order
$in(value, array)           # Check if value exists in array
=$filter(arr, function($v){ $v.active })
=$map(arr, function($v){ {'id':$v.id, 'name':$v.name} })

# Date/Time
$now()                      # Current timestamp
$toMillis('2025-01-01')     # To milliseconds
$formatDateTime($now(), '[Y0001]-[M01]-[D01]') // 1972-05-27
```

## Data Filtering

### Filtering & Conditionals

```yaml
# Predicate filtering
=@ctx.datasources.users[status = 'active']
=@ctx.datasources.products[price >= 10 and price < 50]
=$filter(@ctx.datasources.items, function($v) {
  $v.category = 'electronics' and $v.inStock and $v.price < 100
})

# Conditionals
=@ctx.system.isOnline ? 'Online' : 'Offline'
=(@ctx.jig.state.type = 'premium') ? 'Premium' : 'Standard'

# Objects
={'userId': @ctx.user.id, 'timestamp': $now(), 'data': @ctx.jig.state.selected}
```

### Validation

```yaml
# Required field
=$length(@ctx.components.email.state.value ?: '') > 0

# Email validation
=@ctx.components.email.state.value ~> /.+@.+\..+/

# Number range
=(@ctx.components.age.state.value ~> $type = 'number') and 
 @ctx.components.age.state.value >= 18 and @ctx.components.age.state.value <= 100

# Form validity
=@ctx.components.form.state.isValid
```
