# Configuring error alerts

Configure a user-friendly message of the error to be sent to users, for example, "_It looks like our system is unavailable_."

## Alert configuration properties

<table><thead><tr><th width="182.37890625">Properties</th><th>Description</th></tr></thead><tbody><tr><td><code>actions</code></td><td>Interactive buttons or controls displayed within the alert let users respond or take specific actions. Use IntelliSense to see the list of available <a href="../../../../ui/actions.md">actions</a>.</td></tr><tr><td><code>title</code></td><td>The main heading text is displayed at the top of the alert.</td></tr><tr><td><code>description</code></td><td>The detailed message content that explains the alert’s purpose, provides instructions, or delivers additional information to the user.</td></tr><tr><td><code>dismiss</code></td><td><p>Configures how users can dismiss the alert. You can enable a gesture dismissal and set an automatic dismissal time.</p><ul><li><code>autoAfter</code> - specify the number of seconds after which the alert is automatically dismissed. Has no effect when <code>dismiss</code> is disabled.</li><li><code>isEnabled</code> - When set to <code>true</code> (default), allowing manual dismissal by swiping down. When set to <code>false</code>, the alert cannot be dismissed manually.</li></ul></td></tr><tr><td><code>icon</code></td><td>The icon displayed alongside the alert content provides visual context and helps users recognize the alert’s type or purpose. The alert’s <code>style</code> property determines the icon color. If no style is set, the default <code>isWarning</code> style is applied.</td></tr><tr><td><code>group</code></td><td>Grouping allows you to manage multiple alerts under a shared identifier. This ensures that only one alert from a group is visible at a time, preventing alert overload and improving the user experience.</td></tr><tr><td><code>group</code></td><td><p><code>id</code> - Identifier for the alert group. Only one alert per group can be visible at a time. If a new alert with the same group ID is triggered while another is active, it will be skipped.</p><p>Use <code>groupId</code> to manage multiple alerts for the same issue. When using <code>modal</code> presentation, alerts with the same <code>groupId</code> are grouped so that only the first alert appears and subsequent ones are automatically skipped. When using <code>toast</code> presentation, alerts are also grouped, preventing duplicates. Users can tap the <code>toast</code> to view details — if multiple alerts exist, they stack and display a count at the top. Swiping left lets users view each alert’s details within the stack.</p></td></tr><tr><td><code>group</code></td><td><p><code>presentAs</code>: Specifies how the alert is presented to the user. Options include:</p><ul><li> <code>toast</code> (default):  For brief, lightweight notifications. </li><li><code>modal</code>: For important messages that require attention and may include additional information. Modal alerts are more disruptive since they block the UI and are typically used for critical information.</li></ul></td></tr><tr><td><code>style</code></td><td><p>Visual styling options let you set the tone of the alert:</p><ul><li><code>isPositive</code> (success/confirmation)</li><li><code>isNegative</code> (error) styling to convey the appropriate tone and urgency. </li><li><code>isWarning</code> (warning) styling is used by default.</li></ul></td></tr><tr><td><code>subtitle</code></td><td>Secondary text that appears below the <code>title</code>, providing additional context or supplementary information.</td></tr></tbody></table>

## Alert presentation types

When an error occurs, Jigx can present alerts to users in two ways:&#x20;

* As a **toast**&#x20;
* As a **modal**

Choosing the right presentation type depends on the severity of the error and how disruptive you need the notification to be.

## Automatic vs custom error grouping

### Automatic error grouping

Errors are automatically grouped by default to prevent alert overload, unless a custom error handler is explicitly configured.<br>

* Errors are auto-grouped using the following key:

```yaml
{solutionId}/{hostUrl}/{errorCode}
```

* If the hostUrl cannot be resolved, grouping falls back to:

```yaml
{functionId}
```

* When multiple functions encounter the same error on the same host, only one alert is shown, the first failure triggers the alert.
* Custom error handlers that specify a different `groupId` are not auto-grouped and will display as separate alerts.
* To reduce user frustration in edge cases where not all errors are grouped, the **Close All** option is available. You can further refine grouping behavior by explicitly defining `groupId` values in your error handler configuration.

### Custom error grouping

You can explicitly control how errors and alerts are grouped by assigning a `groupId`. Grouping ensures that only one alert per group is shown at a time, helping to reduce duplicate or repetitive messages.

When an alert is triggered with a `groupId` that matches an active alert, subsequent alerts in the same group are skipped.

* **Modal alerts**: Alerts with the same `groupId` are grouped so that only the first alert is displayed.
* **Toast alerts**: Alerts are grouped to prevent duplicates. If multiple alerts exist, they stack and display a count indicator. Users can tap the toast to view details and swipe left to navigate between alerts in the stack.

Use custom error grouping when you want precise control over how related errors are presented to users, especially when handling recurring or function-specific failures.

## Examples and code snippets

```yaml
 alert:
      title: System Offline
      description: 
        It looks like our system is temporarily unavailable.
        Please try again in a little while. Thank you for your patience!
      icon: server-error-403-hand-forbidden
      style:
        isNegative: true
      # Presentation style (overlays the current screen), can be modal or toast.   
      presentAs: toast
      # Grouping allows you to manage multiple alerts under a shared identifier. 
      # This ensures that only one alert from a group of errors is visible.
      group:
        id: code403
    # Configure information to be logged in the datasync-error table.  
    title: System Offline
    description: System is temporarily unavailable.
    details: =@ctx.response.body
```
