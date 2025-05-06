---
title: REST
slug: jrba-rest
description: Jigx's REST provider allows you to fetch or post data to and from REST services that return JSON, XML, or binary data. (Or accept JSON, XML, or binary data)
createdAt: Sun Mar 26 2023 16:55:00 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Oct 18 2024 07:32:29 GMT+0000 (Coordinated Universal Time)
---

The REST data provider is one of the most frequently used data providers in Jigx solutions.

The REST data provider allows you to fetch or post data to and from REST services that return JSON, XML, or binary data (or accept JSON, XML, or binary data).

## Use the REST data provider

To use the REST data provider in Jigx , follow these high-level steps:

1. **Choose your data source **
   - Identify the REST API you will use as your data source. Ensure you understand its endpoint structure, request requirements (like headers and query parameters), and the format of the data it returns.
2. **Define a REST Service in a **Jigx** function  in **Jigx Builder:
   - Navigate to the [functions]() folder in Jigx Builder.
   - Use [IntelliSense](<./../../Jigx Builder _code editor_/Editor.md>) to configure the REST data provider.
   - Enter the base URL of the REST API.
3. **Configure REST Authentication**:
   - If the API requires [authentication](<./REST/REST Authentication.md>) (such as OAuth, API keys, etc.), configure these settings. This might involve adding headers, query parameters, or setting up OAuth tokens.
4. **Define data operations in the function**:
   - Set up different operations your application can perform using this API, such as GET, POST, PUT, DELETE, etc.
   - For each operation, create a new function to specify the endpoint, required headers, URL parameters, input and output transforms, continuation, and body content if applicable.
5. **Reference the Jigx functions in **jig**s**:
   - [Reference the function]() in your jigs. This step is crucial for integrating the API data seamlessly into your Jigx solution.
6. **Publish your solution**:
   - [Publish your solution](<./../../Jigx Builder _code editor_/Publishing a solution.md>) and use the app to interact with the REST data provider. Make sure to handle any API limits or errors gracefully.
7. **Test the Data Provider**:
   - Use Jigx Builder [developer tools](<./../../Jigx Builder _code editor_/Debugging.md>) to test the data provider configurations. Check if the data provider can connect to the API successfully and perform operations like GET (fetch), PUT (create), POST (update), or DELETE data.

Following these steps, you can effectively integrate external REST APIs into your Jigx solutions, allowing you to enhance your apps with data and functionalities from diverse external sources.


::embed[]{url="https://vimeo.com/848055698"}

## Jigx functions

The Jigx function contains the URL of the REST service, details of the required parameters, and an ability to MAP your Jigx parameters to complex JSON for either input or output purposes. In the sections below, we will explain each part of the function definition and how you can define any REST service and use it within your Jigx application. Here is an example of a Jigx function to send an email:

```yaml
provider: DATA_PROVIDER_REST
method: POST
url: "https://api.sendgrid.com/v3/mail/send"
inputTransform: >-
  $.{"personalizations": [{ "to": [ { "email": emailto, "name": name }]}],"from": {"email": emailfrom, "name": name}, "reply to": {"email": emailfrom, "name": name },"subject": subject, "content": [{ "type": "text/html", "value": content}]}
parameters:
  Authorization:
    location: header
    type: string
    value: Bearer XXXXXX
    required: true
  emailfrom:
    location: body
    type: string
    required: true
  emailto:
    location: body
    type: string
    required: true
  name:
    location: body
    type: string
    required: true
  subject:
    location: body
    type: string
    required: true
  content:
    location: body
    type: string
    required: true
```

## Referencing a Jigx function

Here is an example of a Jigx solution screen that calls the sendmail function. We have not shown the entire jig, but you can see the call to the REST service within the **actions** section of the form below, which calls the function **rest-send-email** and sends each field in the form as a parameter to the REST service.

```yaml
title: Email Employee
icon: synchronize-arrows-1
type: jig.default

header: 
  type: component.image
  options:
    title: Keep employees updated
    source:
      uri: "https://www.deputy.com/uploads/2018/07/How-to-Write-an-Awesome-Welcome-Email-for-Your-New-Employee_Content-image2-min-1024x569.png"

actions:
  - children:
      - type: action.submit-form
        options:
          formId: form-three-rest
          provider: DATA_PROVIDER_REST
          title: Send updated info
          entity: notify-employee
          function: rest-send-mail
          onSuccess: 
            title: Email has been sent
            description: Done
            actions:
              - type: action.go-to
                options:
                  title: Employees 
                  linkTo: list-four              

children:
  - type: component.form
    instanceId: form-three-rest
    options:
      children:
        - type: "component.text-field"
          instanceId: name
          options:
            label: "Employee Name"
            isHidden: true
            initialValue: Jigx Team
        - type: "component.text-field"
          instanceId: emailfrom
          options:
            label: Email From
            isHidden: true
            initialValue: 'john@jigx.com'
        - type: "component.text-field"
          instanceId: emailto
          options:
            label: "Email to:"
            initialValue: =@ctx.jig.inputs.employee.user_email
        - type: "component.text-field"
          instanceId: subject
          options:
            label: "subject"
            isHidden: true
            initialValue: 'Employee information updated'
        - type: "component.text-field"
          instanceId: message
          options:
            label: "Message"
            isMultiline: true
            textArea: large

```

Jigx supports the concept of a REST service within a form context where each field in the form becomes a parameter, or alternatively, you can call the REST API using a Jigx function using the execute entity action, where you set the function parameters as part of the functions call in YAML.

## Supporting JSON Input and Output

::embed[]{url="https://vimeo.com/848059289"}

REST services typically have simple or complex JSON structures which enable you to provide them with suitable input data as well as return complex data structures. Jigx has built-in capabilities to deal with these structures. These are achieved using:

- Input transforms
- Output transforms

Here is an example of a typical REST service from POSTMAN. This is the “Twilio sendgrid” service to send an email. The URL for the service is https\://api.sendgrid.com/v3/mail/send

The JSON body for this service is:

```json
{
  "personalizations": [
    {
      "to": [
        {
          "email": "anemail@com"
        }
      ]
    }
  ],
  "from": {
    "email": "youremail.com"
  },
  "subject": "Sending with SendGrid is Fun",
  "content": [
    {
      "type": "text/plain",
      "value": "and easy to do anywhere, even with cURL"
    }
  ]
}
```

This is an HTTP POST example and needs an **Input Transform **in order to map the data from a \{} (for example, an employee form) so that it can send an email to an employee. Continuing from the example above, here is the input transform that maps fields on the form to the JSON body described above:

```yaml
provider: DATA_PROVIDER_REST
method: POST
url: "https://api.sendgrid.com/v3/mail/send"
inputTransform: |
  $.{"personalizations": [{ "to": [ { "email": emailto, "name": name }]}],
  "from": {"email": emailfrom, "name": name}, "reply to": {"email": emailfrom, "name": name },
  "subject": subject, "content": [{ "type": "text/html", "value": content}]}
parameters:
  Authorization:
    location: header
    type: string
    value: Bearer SG.testingtestingdemo.2kyqYOFa_bPwlPJbUWtnTWHLs5PuL-VOA22gW1koEIY
    required: true
  emailfrom:
    location: body
    type: string
    required: true
  emailto:
    location: body
    type: string
    required: true
  name:
    location: body
    type: string
    required: true
  subject:
    location: body
    type: string
    required: true
  content:
    location: body
    type: string
    required: true
```

The same logic can be applied to the output from a REST service. The output transform processes JSON data returned by the REST service in the Jigx function definition. 

## JSONata in Input and Output Transforms

In addition to applying basic “structural” transforms, the JSONata scripting capability is available to apply further functions, and logic transforms within the input and output transforms. More detail on JSONata can be found here: <a href="https://www.jsonata.org" target="_blank">https\://www\.jsonata.org</a>. Below is an example of a JSONata function applied within an output transform that returns videos from the Google YouTube API. Note the use of the $trim() and $substring() functions which provide further rich capability for JSON transforms.

```yaml
provider: DATA_PROVIDER_REST
method: GET
url: "https://www.googleapis.com/youtube/v3/playlistItems"
outputTransform: |
  $.items[].{"id":id, "videoid": snippet.resourceId.videoId,
  "publishedat": $toMillis(snippet.publishedAt), "title":
  $contains(snippet.title, "]") ? $trim($substringAfter(snippet.title, "]")) :
  $trim(snippet.title) , "description": snippet.description, "thumbnail":
  $exists(snippet.thumbnails.maxres) ? snippet.thumbnails.maxres.url :
  snippet.thumbnails.high.url}
parameters:
  key:
    location: query
    type: string
    value: AIzaSyBaQF3E1qaMSRjQGl99q5Kkpa--onhDgiE
    required: true
  playlistId:
    location: query
    type: string
    value: PL_500m6Wb0wjTjKDoM_G7MkIqLWtvCm0o
    required: true
  part:
    location: query
    type: string
    value: snippet
    required: true
  maxResults:
    location: query
    type: string
    value: "500"
    required: true
```

Here is another example of an output transform used to return ingredients from a recipe in a single list-item (on single row). Note the use of $.map and function($ingredient, $idx, $arr).  When using the returned data in a list jig the $.eval() is used to return the individual ingredients. 

:::CodeblockTabs
```yaml
outputTransform: >-
  {
    "id": $.recipes.id,
    "name": $.recipes.title,
    "image": $.recipes.image,
    "desc": $.recipes.summary,
    "ingredients": $map($.recipes.extendedIngredients, function($ingredient, $idx, $arr) {
      {
        "name": $ingredient.name
      }
    }),
    "instructions": $map($.recipes.analyzedInstructions.steps, function($instruction, $idx, $arr) {
      {
        "step": $instruction.step
      }
    })
  }
```

list-jig.jigx

```yaml
 - type: component.section
    options:
      title: Ingredients
      children:
        - type: component.list
          options:
            data: =$eval(@ctx.datasources.randomRecipeData.ingredients)
            item: 
              type: component.list-item
              options:
                title: =@ctx.current.item.name
#         {"name": $ingredient.name}
#       })
```
:::

## Examples and code snippets

The following examples with code snippets are provided:

| **Example**    |                                                                                                                                                                   |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Hello REST]() | In this section, a REST API is used to create a customers Jigx app, allowing you to add new customers and update and view customer details, location, and images. |
| [MS Graph]()   | The MS Graph examples use the User, Calendar, Mail, Insights, and To-do tasks to create a powerful Jigx apps with everything you need in one app.                 |

## Building a REST based app video resources

::::LinkArray
:::LinkArrayItem{headerImage headerColor}
![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Nysik_Qk5eJiV0HDzY7xf_intro-to-rest.png)

1\. <a href="https://vimeo.com/manage/videos/848412406" target="_blank">Introduction to REST API
</a>6:59 min
:::

:::LinkArrayItem{headerImage headerColor}
![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/qdF4Rf2crRLBgcFA62tlj_jsonata-with-rest.png)

2\. <a href="https://vimeo.com/manage/videos/848059289" target="_blank">Exploring REST and JSONata
</a>6:17 min
:::

:::LinkArrayItem{headerImage headerColor}
![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/mbDtpiY-9pmac8QxbpXx5_build-a-rest-app.png)

3\. <a href="https://vimeo.com/manage/videos/848062137" target="_blank">Building a REST based App</a>
9:14 min
:::
::::

## See Also

- [File handling](<./../File handling.md>)
- [Offline remote data handling](<./../Offline remote data handling.md>)

