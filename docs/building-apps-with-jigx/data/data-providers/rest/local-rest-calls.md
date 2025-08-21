# Local REST Calls

## Local REST Calls

## Overview

The REST provider populates list data or performs other REST methods using a third-party REST service.

By default, a REST function will split processing between the mobile app (local) and the Jigx REST service (remote). The mobile app wraps the REST call and sends it to the remote Jigx REST function that, in turn, calls the third-party service. Results are returned to the mobile app from the third-party REST service via the remote Jigx REST function. When using the remote Jigx REST service, the size of the data is limited to 6Mb. OAuth, which is configured in Jigx Management is only processed in the remote Jigx REST service. **Remote REST function** calls are helpful when:

* OAuth needs to secure.
* The calling IP addresses on the third-party service need to be allowlisted.

A **local REST function** call allows the mobile app to perform all the processing locally and call the third-party service directly. As a result, data is only transferred between the mobile app and the third-party REST service. The third-party REST service is the only limit to data size when using a local REST function. **Local REST function** calls are useful when:

* There is a requirement not to send any data through the AWS infrastructure
* The third-party REST service has a limit larger than 6Mb on the amount of data that can be transferred

### Considerations

* Only **OAuth** authentication can be used with local REST calls.
* When `useLocalCall: true` is set, functions that rely on secrets or other authentication mechanisms not available locally will not execute.
* Setting `useLocal: false` limits support for REST robustness and `@ctx` features, and may slow down data syncing between the device and the remote system.

### Example

Adding the `useLocalCall: true` property to a REST function directs the function call to use local execution. Leaving the property out of the definition or setting it to `useLocalCall: false` directs the function call to use remote execution.

```yaml
provider: DATA_PROVIDER_REST
url: https://api.weather.gov/alerts/active
useLocalCall: true
parameters:
  area:
    type: string
    location: query
    required: true
    value: WA
```

For examples using Remote REST functions, see [REST Authentication](rest-authentication.md).
