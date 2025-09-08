---
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# SOAP Functions

{% hint style="info" %}
SOAP functions are only visible in the list if the Solution Creator defined functions that use the [SOAP data provider](https://docs.jigx.com/data-providers). Make sure that credentials such as API Keys are set up correctly in [Credentials](credentials.md) if they are being referenced in the function definition.
{% endhint %}

You can try out all functions of the solutions that use the SOAP data provider.

1. On the left side, you will see all input parameters of the function including the initial set values.
2. Enter values into the input parameter fields and click the **Preview** button at the top of the screen. The JSON editor on the right side will show the result returned by the function.
3. Click on **Show schema** to view the function definition.

{% hint style="success" %}
You can click the **copy to the clipboard** icon at the top and paste the JSON result into [JSONata Exerciser](https://try.jsonata.org/). This allows you to run and test [Expressions](../../building-apps-with-jigx/logic/expressions.md) against real SOAP response data.
{% endhint %}
