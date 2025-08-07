# Validation

Validating fields (text or other) is crucial for ensuring that data entered by users meets specific criteria or formats and for maintaining data integrity and security.

In Jigx Builder you can use regular expressions (regex) for text validation. They allow for pattern matching and can enforce complex rules for text fields such as email addresses, phone numbers, usernames, passwords, and more. When applied to text validation, regex can be used to check if the input text matches the desired format. If it is not valid, an invalid message is displayed.

In Jigx you combine a [JSONata expression](./Expressions.md) with a [Regex expressions](https://docs.jigx.com/examples/regex-expressions) to create a validation pattern and provide a message if the pattern does not match.

## Creating the validation expression:

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![Valid email address](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/NP-TE2sDghjEcBbxXZURF_email-valid.PNG "Valid email address")
:::

:::VerticalSplitItem
![Invalid email address](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/47lx4W1RTiP8bQd4wCB_u_email-invalid.PNG "Invalid email address")
:::
::::

1. JSONata expression - `=@ctx.components.email.state.value `
2. Regex expression - `/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/`
3. Validation message - `not an email`

Combine the three above to validate an email address in the `text-field` component.

:::CodeblockTabs
YAML

```yaml
- type: component.text-field
          instanceId: email
          options:
            label: Email
            errorText: =$contains(@ctx.components.email.state.value, /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/) ? '' :'not an email'

```
:::

## Regex and JSONata Expression examples

Here are some common validation expressions to create and use for text field validation.

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="254">
  <tr>
    <td selected="false" align="left">
      <p><strong>Validation</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Expected result</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#1Txjd">Phone number</a></p>
    </td>
    <td selected="false" align="left">
      <p>+271234556789</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#hk-Na">Email</a></p>
    </td>
    <td selected="false" align="left">
      <p><a href="mailto:name@example.com">name@example.com</a></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#BJCon">Credit Card</a></p>
    </td>
    <td selected="false" align="left">
      <p>Typically 13-16 digits, with spaces or dashes optional, and includes checks for Visa, MasterCard, American Express, and Discover. 1111-1111-1111-1111 or 1111 1111 1111 1111</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#GK4pj">ZIP/Postal code (US)</a></p>
    </td>
    <td selected="false" align="left">
      <p>5-digit codes, e.g. 10036</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#Jhwil">Social Security Number (US)</a></p>
    </td>
    <td selected="false" align="left">
      <p>XXX-XX-XXXX</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#rtVZq">National Insurance (UK)</a></p>
    </td>
    <td selected="false" align="left">
      <p>AA123456C</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#oEzBT">US Date (DD/MM/YYYY)</a></p>
    </td>
    <td selected="false" align="left">
      <p>23/07/2024</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#YCAik">Date (MM/DD/YYYY)</a></p>
    </td>
    <td selected="false" align="left">
      <p>03/28/2023</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#rNdkI">Date (DD Month YYYY)</a></p>
    </td>
    <td selected="false" align="left">
      <p>25 July 2024</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#pwS2M">Date (yyyy/mm/dd)</a></p>
    </td>
    <td selected="false" align="left">
      <p>2024/08/30</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#eyUy1">Decimal</a></p>
    </td>
    <td selected="false" align="left">
      <p>111,25</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#7tIMj">Time (H:MM AM/PM)</a></p>
    </td>
    <td selected="false" align="left">
      <p>12:15 AM or 08:45 PM</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#ExOYs">Date (MM:SS or HH:MM)</a></p>
    </td>
    <td selected="false" align="left">
      <p>08:10</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#_faOT">Time in 24-hour format</a></p>
    </td>
    <td selected="false" align="left">
      <p>01:00</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#ankaP">URL</a></p>
    </td>
    <td selected="false" align="left">
      <p>example.com or <a href="https://example.com">https://example.com</a></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#jcfEA">ISBN</a></p>
    </td>
    <td selected="false" align="left">
      <p>978-1-4302-1998-9</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#-Rg7S">Strict alpha numeric</a></p>
    </td>
    <td selected="false" align="left">
      <p>JohnSmith</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#kttOe">Alpha numeric with spaces</a></p>
    </td>
    <td selected="false" align="left">
      <p>John Smith</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="https://docs.jigx.com/examples/regex-expressions#8Fe2B">Numbers and spaces only</a></p>
    </td>
    <td selected="false" align="left">
      <p>56575 76 6</p>
    </td>
  </tr>
</table>

## See Also

- [Regex expressions](https://docs.jigx.com/examples/regex-expressions)
- [Expressions](./Expressions.md)
- [Expressions - cheatsheet](<./Expressions/Expressions - cheatsheet.md>)
- [Expression-examples](https://docs.jigx.com/examples/expressions)

