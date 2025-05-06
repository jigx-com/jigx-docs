---
title: Validation
slug: t2Ms-validation
createdAt: Tue Mar 05 2024 09:05:11 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Aug 05 2024 14:25:18 GMT+0000 (Coordinated Universal Time)
---

Validating fields (text or other) is crucial for ensuring that data entered by users meets specific criteria or formats and for maintaining data integrity and security.

In Jigx Builder you can use regular expressions (regex) for text validation. They allow for pattern matching and can enforce complex rules for text fields such as email addresses, phone numbers, usernames, passwords, and more. When applied to text validation, regex can be used to check if the input text matches the desired format. If it is not valid, an invalid message is displayed.

In Jigx you combine a [JSONata expression](./Expressions.md) with a [Regex expressions]() to create a validation pattern and provide a message if the pattern does not match.

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
2. Regex expression -  `/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/`
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

| **Validation**                  | **Expected result**                                                                                                                                                          |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Phone number]()                | +271234556789                                                                                                                                                                |
| [Email]()                       | name\@example.com                                                                                                                                                            |
| [Credit Card]()                 | Typically 13-16 digits, with spaces or dashes optional, and includes checks for Visa, MasterCard, American Express, and Discover. 1111-1111-1111-1111 or 1111 1111 1111 1111 |
| [ZIP/Postal code (US)]()        | 5-digit codes, e.g. 10036                                                                                                                                                    |
| [Social Security Number (US)]() | XXX-XX-XXXX                                                                                                                                                                  |
| [National Insurance (UK)]()     | AA123456C                                                                                                                                                                    |
| [US Date (DD/MM/YYYY)]()        | 23/07/2024                                                                                                                                                                   |
| [Date (MM/DD/YYYY)]()           | 03/28/2023                                                                                                                                                                   |
| [Date (DD Month YYYY)]()        | 25 July 2024                                                                                                                                                                 |
| [Date (yyyy/mm/dd)]()           | 2024/08/30                                                                                                                                                                   |
| [Decimal]()                     | 111,25                                                                                                                                                                       |
| [Time (H\:MM AM/PM)]()          | 12:15 AM or 08:45 PM                                                                                                                                                         |
| [Date (MM\:SS or HH\:MM)]()     | 08:10                                                                                                                                                                        |
| [Time in 24-hour format]()      | 01:00                                                                                                                                                                        |
| [URL]()                         | example.com or https\://example.com                                                                                                                                          |
| [ISBN]()                        | 978-1-4302-1998-9                                                                                                                                                            |
| [Strict alpha numeric]()        | JohnSmith                                                                                                                                                                    |
| [Alpha numeric with spaces]()   | John Smith                                                                                                                                                                   |
| [Numbers and spaces only]()     | 56575 76 6                                                                                                                                                                   |

## See Also

- [Regex expressions]()
- [Expressions](./Expressions.md)
- [Expressions - cheatsheet](<./Expressions/Expressions - cheatsheet.md>)
- [Expression-examples]()

