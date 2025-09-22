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

# REST Overview

## Configuring the REST data provider

To use the REST data provider in Jigx , follow these high-level steps:

1. **Choose your datasource**
   * Identify the REST API you will use as your datasource. Ensure you understand its endpoint structure, request requirements (like headers and query parameters), and the format of the data it returns.
2. **Define a REST Service in a Jigx function in Jigx Builder**
   * Navigate to the [functions](functions/) folder in Jigx Builder.
   * Use [IntelliSense](../../../jigx-builder-code-_editor_/editor.md#intellisense) to configure the REST data provider.
   * Enter the base URL, method, parameters of the REST API.
3. **Configure REST Authentication**:
   * If the API requires [authentication](rest-authentication.md) (such as OAuth, API keys, etc.), configure these settings. This might involve adding headers, query parameters, or setting up OAuth tokens.
4. **Define data methods in the function**:
   * Set up different methods your application can perform using this API, such as GET, POST, PUT, DELETE, etc.
   * For each method, create a new function to specify the endpoint, required headers, URL parameters, input and output transforms, continuation, and body content if applicable.
5. Configure properties to handle API limits, errors and file storage.
   * In the function configure the REST provider to cater for [errors](rest-error-handling.md), such as 403, 404 or 500.
   * [Convert](functions/conversions.md) images and files from local-uri to an acceptable storage format, such as base64 or buffer.
   * Add [Continuation](functions/continuation.md) if the REST services limit the number of items to be returned. Jigx REST calls can automatically repeat calls by specifying a continuation block.
6. **Bind data to the UI by referencing the local data and functions in jig﻿s**
   * Use the data from the local database in [datasources](../../datasources/) in jigs and components\
     [components](../../../ui/components-_controls_/components-_controls_.md) to build the required UI.
   * Reference the function﻿ in your jig﻿s in [actions](../../../ui/actions.md). This step is crucial for integrating the API data seamlessly into your Jigx﻿ solution.
7. **Publish your solution**:
   * [Publish your solution](../../../jigx-builder-code-_editor_/publishing-a-solution.md) and use the app to interact with the REST data provider.&#x20;
8. **Test the Data Provider**:
   * Use Jigx Builder [developer tools](../../../jigx-builder-code-_editor_/debugging.md) to test the data provider configurations. Check if the data provider can connect to the API successfully and perform operations like GET (fetch), PUT (create), POST (update), or DELETE data.

Following these steps, you can effectively integrate external REST APIs into your Jigx solutions, allowing you to enhance your apps with data and functionalities from diverse external sources.

### See Also

* [REST examples](https://docs.jigx.com/examples/readme/data-providers/rest)
* [Offline remote data handling](../../offline-remote-data-handling.md)
