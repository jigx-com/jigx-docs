---
title: REST Functions
slug: Ozuk-rest-functions
description: Learn how to use the REST data provider functions with this comprehensive guide. Discover how to input parameters, view results in the JSON editor, and even test the JSON output in the powerful JSONata Exerciser tool. Maximize the potential of your soluti
createdAt: Thu Jun 09 2022 09:05:18 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue May 23 2023 10:14:53 GMT+0000 (Coordinated Universal Time)
---

:::hint{type="info"}
REST functions are only visible in the list if the Solution Creator defined functions that use the  [REST data provider](). Make sure that credentials such as API Keys are set up correctly in [Credentials](./Credentials.md) if they are being referenced in the function definition.
:::

You can try out all functions of the solutions that use the REST data provider.

1. On the left side, you will see all input parameters of the function including the initial set values such as the `key` of the credential, in the example below there is an API Key reference called jigx.finnhub.token.
2. Enter values into the input parameter fields and click the **Preview** button at the top of the screen. The JSON editor on the right side will show the results returned by the function.
3. Click on **Show schema** to view the function definition.

:::hint{type="success"}
You can click the **copy to the clipboard** icon at the top and paste the JSON result into JSONata <a href="https://try.jsonata.org/" target="_blank">Exerciser</a>. This allows you to run and test [Expressions](<./../../Building Apps with Jigx/Logic/Expressions.md>) against real REST response data.
:::

![Preview a REST function](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/inwWRpNo1J-sKAeM4d6vk_jm-restfunctionl.png "Preview a REST function")

