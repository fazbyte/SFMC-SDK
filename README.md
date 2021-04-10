# Salesforce Marketing Cloud SDK

Modern library to handle various API tasks with Salesforce Marketing Cloud.

## Background

This library is based on the work in https://github.com/salesforce-marketingcloud/FuelSDK-Node which has not been updated for 2 years.
Due to the naming onf Fuel being removed from all Marketing it also sends the wrong message about what it does.

This library attempts to overcomes some of the complexity/shortcomings of the original work

-   Uses Axios instead of Request which is outdated/no longer supported
-   Assumes Server-Server Credentials due to being the overwhealming case
-   Assumes that OAuth2 is in place
-   Allows for both REST and SOAP methods
-   Is opinionated about how Auth should be managed (only accepts a standard Auth method)
-   Only uses Promises/Async-Await, no callbacks

## Usage

### Initialization

Initializes the Auth Object in the SDK.
The SDK will automatically request a new token if none is valid

```javascript
const SDK = require('sfmc-sdk');
const sfmc = new SDK({
    client_id: 'XXXXX',
    client_secret: 'YYYYYY',
    auth_url: 'https://ZZZZZZZ.auth.marketingcloudapis.com/',
    account_id: 7281698,
});
```

### SOAP

SOAP currently only supports retrieve, will be updating soon for other types.

```javascript
const soapResponse = await sfmc.soap.retrieve('DataExtension', ['ObjectID'], {});
```

### REST

REST supports GET, POST, PUT, PATCH and DELETE.

```javascript
const restResponse = await sfmc.rest.get('/interaction/v1/interactions');
const restResponse = await sfmc.rest.post('/interaction/v1/interactions', jsonPayload);
const restResponse = await sfmc.rest.patch('/interaction/v1/interactions/IDHERE', jsonPayload); // PUT ALSO
const restResponse = await sfmc.rest.delete('/interaction/v1/interactions/IDHERE');
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## To Do

-   No tests are in place
-   Improve handling for other SOAP Actions than Retrieve
-   Look at persisting access tokens across sessions as an option
-   Validation improvement
-   Support Scopes in API Requests

## License

[BSD-3](https://opensource.org/licenses/BSD-3-Clause)