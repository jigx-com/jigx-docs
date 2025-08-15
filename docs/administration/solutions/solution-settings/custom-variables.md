---
title: Custom variables
slug: f4oT-custom
createdAt: Wed Aug 14 2024 09:07:45 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Apr 15 2025 13:23:50 GMT+0000 (Coordinated Universal Time)
---

# Custom variables

Defining custom variables enables you to create reusable values that can be dynamically controlled, eliminating the need for hardcoding. This approach offers flexibility, allowing values to be updated instantly and seamlessly applied throughout the app. Custom variables are particularly effective for storing environment-specific values that change over time, such as URLs.

### Creating and setting variables

Custom variables are created and set in the [Solution Settings](solution-settings.md) page in [Jigx Management](<../../../Administration/Management Overview.md>) and consist of a variable name and a variable value.

![Custom Variables](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-RA_r561Nvc-59iw8KrHaE-20240819-075737.gif)

1. Open [Jigx Management](<../../../Administration/Management Overview.md>), navigate to the solution where the variables will be used.
2. Select [Solution Settings](solution-settings.md) in the left navigation pane.
3. Select the **Custom** tab.
4. Type a name for the variable in the text field and click the **+** sign. This creates the **variable name**, which appears at the top of the field.
5. Next, type the **variable value** in the text field.
6. Click **Save** in the top right-hand corner.

Now that your variables are set, you can use the variables throughout the solution in Jigx Builder.

### Using variables

Custom variables are expression based, meaning you can use it wherever expressions are configurable in Jigx Builder. To reference the variable, the following expression is used:

```yaml
=@ctx.solution.settings.custom.{{variableName}} 
```

Use IntelliSense to select the `variableName` you set in _Management > Solution Settings_.

#### Reloading variables in Jigx Builder

After adding a new custom variable in Management, you can use the _Reload Solution Settings_ option in Jigx Builder to refresh IntelliSense and make the variable available.

![Reload variables in Jigx builder](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Xlz4cUJDzdSHr1WCVNU3a-20250408-093707.gif)

### Considerations

* Do not store API keys, passwords or secrets in custom variables, as they are not encrypted or secure.
* Variables are solution specific, and cannot be used across multiple solutions.
* Custom variable values are read only in the mobile app.
* Best practice is to use custom variables to configure environment variables, relating to:
  * Production, development, or test URLs.
  * Customer preferences, for example, a base solution that is used for multiple customers, departments, stores. Simply change the variable value to apply to each customer.
