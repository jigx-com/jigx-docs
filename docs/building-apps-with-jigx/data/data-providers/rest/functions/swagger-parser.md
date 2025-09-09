# Swagger parser

The Swagger parser function allows you to convert Swagger, open API, and Postman collection data to Jigx functions in the Jigx Builder.

## How to use the Swagger parser

The command to start the Swagger parser function is (command + shift + p): Generate Jigx Functions

<figure><img src="../../../../../.gitbook/assets/REST-swaggerParser.png" alt="Generate Jigx functions" width="563"><figcaption><p>Generate Jigx functions</p></figcaption></figure>

Both remote and local files can be used, and only JSON format is allowed.

<figure><img src="../../../../../.gitbook/assets/REST-fileOptions.png" alt="File options" width="563"><figcaption><p>File options</p></figcaption></figure>

All files created by the Swagger parser function saves in your functions folder.

### Variable replacement

You can replace variables in your Postman collection, for example, replacing the baseUrl. As you add the value 'google.com' to the variable all functions requiring this variable will be updated.

<figure><img src="../../../../../.gitbook/assets/REST-variableReplacement.png" alt="" width="563"><figcaption></figcaption></figure>
