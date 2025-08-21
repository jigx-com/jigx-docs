# Deep links

Deep linking in mobile apps is a powerful tool that enhances user experience by creating seamless navigation between the app and external sources. Deep linking allows you to land directly on specific content or pages within an app, bypassing the need to navigate through a series of menus. This is particularly useful in marketing campaigns, social media links, or emails where you want to direct a person to a specific product, article, or feature within your app.

{% hint style="success" %}
Contact [_support@jigx.com_](mailto:support@jigx.com) to get your branded app's deep link.
{% endhint %}

## Format

Deep linking uses a uniform resource identifier (URI) to link to an app or a specific location within a mobile application. The deep link is built up in stages, and the depth depends on where in the app you want to land. The full URI format is shown below:

`https://{app.domainname.com}/{appname}/app/solution/{solutionId}/jig/{jigname}?{inputname=inputvalue}`

An example of a built-up deep link:

[https://app.jigx.com/jigx/app/solution/8e535f78-4e36-4716-8c01-4567bea60bj9/jig/support-form?email=support@jigx.com](https://app.jigx.com/jigx/app/solution/8e535f78-4e36-4716-8c01-4567bea60bj9/jig/support-form?email=john@global.com)

The URI is built up with the following values:

<table><thead><tr><th width="132.19140625">URI elements</th><th>Description</th></tr></thead><tbody><tr><td>app.jigx.com</td><td>For all jigx apps, use the app domain app.jigx.com.</td></tr><tr><td>jigx</td><td>name of the app.</td></tr><tr><td>solutionId</td><td>The solutionId is found in , for example, 8e535f78-4e36-4716-8c01-3465bea60bj9.</td></tr><tr><td>jigname</td><td>jigId/jig-name, for example, support-form.</td></tr><tr><td>inputname</td><td>The name used in the input expression, i.e. <code>=@ctx.jig.input.{inputname}</code>.</td></tr><tr><td>inputvalue</td><td>The value to be used as the input.</td></tr></tbody></table>

### Link to an app

To open a Jigx or branded app, use the following deep link:

`https://{app.jigx.com}/{jigx}/app/`

* If you are logged out of the app and click the link, you will be directed to the login screen.
* If you are currently logged into the app, the link will open the app and display the Home Hub.

### Link to a jig screen (basic deep link)

A deep link to a jig screen directs you to a specific location within the app if it has already been installed.

`https://{app.jigx.com}/{jigx}/app/solution/{solutionId}/jig/{jigname}`

### Link to a jig with inputs (contextual deep link)

A contextual deep link includes additional information, such as user data, input value, or a parameter, providing a personalized experience. For example, a link that opens a form and prepopulates a field with an email address.

**Input:**

`https://{app.domainname.com}/{appname}/app/solution/{solutionId}/jig/{jigname}?{inputname=inputvalue}`

An example of the built-up deep link:

[https://app.jigx.com/jigx/app/solution/8e535f78-4e36-4716-8c01-34657bea60bj9/jig/support-form?email=john@global.com](https://app.jigx.com/jigx/app/solution/8e535f78-4e36-4716-8c01-34657bea60bj9/jig/support-form?email=john@global.com)

In the solution, the YAML code to accept the deep link input is:

{% tabs %}
{% tab title="YAML" %}
```yaml
 value: =@ctx.jig.inputs.email
```
{% endtab %}

{% tab title="input-query-parameter" %}
```yaml
datasources:
  participantList: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/hikers
      query: |
        SELECT
          id,
          '$.name',
          '$.contact',
          '$.photo',
          '$.participant-group',
          '$.hiker-email'
        FROM
        [default/hikers]    
        WHERE '$.hiker-email' = @email
    # create a query parameter for the deeplink input
      queryParameters:
        email: =@ctx.jig.inputs.email
```
{% endtab %}
{% endtabs %}

### Link to an external app from a jig

Add a deep link in a jig that directs you to a different mobile application, even to a specific location within that application. This link allows you to navigate seamlessly from one app directly to a particular page or piece of content in another app, without having to navigate through the app's homepage or menu. For example, tapping on an address link in a contacts jig could directly open Google Maps showing the location.

**Considerations**

* Deep linking to an external app can only be configured in actions and swipeable actions using the `action.open-url`.
* An app's deep links often differ depending on the mobile OS (iOS or Android). This will require you to configure a deep link for each OS in the jig. See the example below that deep links into the iOS and Android Google Maps app:

{% tabs %}
{% tab title="iOS-open-url" %}
```yaml
actions:
  - children:
      - type: action.open-url #iOS
        options:
          title: Directions
  # Add the external app's iOS deep link in the url    
          url: comgooglemaps://?center=32.7347483943,-117.150943196&zoom=14
```
{% endtab %}

{% tab title="Android-open-url" %}
```yaml
actions:
  - children:  
      - type: action.open-url #android
        options:
          title: Directions
          # Add the external app's Android deep link in the url
          url: google.navigation:q=2920+Zoo+Dr,San+Diego,CA+92101,United+States
 
```
{% endtab %}
{% endtabs %}
