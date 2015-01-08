# Authentication

Fuel API methods require an access token. These tokens are managed through the Fuel Authentication Service providing authentication and authorization management for binding API requests to apps, while also handling the validity period of tokens. The Fuel Authentication Service is based on the OAuth 2.0 protocol. 

Before you can start using Fuel API methods, you will need to obtain client credentials by creating an app in Marketing Cloud App Center. This platform provides a console for developers to manage API permissions and build Marketing Cloud apps. 

## Apps 

Apps provide authentication and functional isolation through:

1. Secure delegated access for authorizing third-party access to the Marketing Cloud platform without sharing credentials (user login credentials to a Marketing Cloud account)
2. Permission management at a data and functional level for limiting read/write access to specific Marketing Cloud account data and features.

After creating an app, you can use the supplied client ID and secret with the Fuel Authentication service to request an OAuth access token for authenticating API requests. 

The client ID is considered public information, and can be included in client-side scripts. However, the client secret must be kept confidential. It's recommended not to store the client secret at a code level, but instead store them in environment variables or in files outside of the application source tree.

## App Templates

Four app templates are available in App Center serving different purposes:

1. **API Integration** apps are used for authentication and permission management with Marketing Cloud REST or SOAP API methods.
2. **Marketing Cloud** apps are custom apps built by an organization that can also be published in the HubExchange marketplace after completing a certification process. Marketing Cloud apps use an encoded JSON Web Token (JWT, pronounced "jot") to provide a single sign-on (SSO) authentication context of the logged-in Marketing Cloud account user. These apps are hosted externally and presented within the Marketing Cloud platform through an iframe HTML element.
3. **Application Extension** apps are similar to Marketing Cloud apps in that they provide SSO authentication context, but do not require a certification process and are intended for use with custom Journey Builder Triggers or Activities, Cloud Editor Blocks, or Automation Studio activities.
4. **MobilePush** apps provide authentication and client integration for iOS, Android and Amazon mobile applications enabling push messages, location-aware push messages and in-app messages to be sent to mobile apps using the Journey Builder for Apps SDK.

![App Templates](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/app-center-templates.png "App Templates in Marketing Cloud App Center") *App Templates in Marketing Cloud App Center*

## Creating Apps

To create an app, you first need to create an App Center account at [https://appcenter-auth.exacttargetapps.com/create](https://appcenter-auth.exacttargetapps.com/create) and then login to that account. App templates provide a wizard-based interface for guiding developers through the process of creating apps. The different interface steps are explained below.

### Properties

All apps require a name, description and package. Packages are internal identifiers that uniquely identify the app.

![Defining App Properties](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/app-center-define.png "Defining App Properties in Marketing Cloud App Center") *Defining App Properties in Marketing Cloud App Center*

The above interface indicates properties for API Integration apps. Additional properties can be defined for Marketing Cloud apps, Application Extension apps and MobilePush apps:

* **Application Endpoints** are required for Marketing Cloud apps. These define the URL endpoints for Marketing Cloud to send login credentials, logout requests and the redirect page after a user successfully logs in.

* **Application Event Callbacks** can be defined for Marketing Cloud apps and Application Extension Apps. These properties enable callback URLs (or webhooks) to be defined when users install, uninstall and accepts data access requested by the app. Application Event Callbacks are currently not implemented in Marketing Cloud and are reserved for future use.

* **MobilePush Icon** is an optional property when creating a MobilePush app, enabling a custom icon to be uploaded and used to visually represent an app in the Marketing Cloud MobilePush interface. 

### Account Integration

The second step in creating an app is to define which Marketing Cloud user account the app will use when making API requests. Unless you have purchased a separate Sandbox Account license, select the Production Account option. The 'Link to Account' button opens a new window for defining Marketing Cloud account credentials.

Account references are saved in App Center once they are initially defined. These references are then available from the Account menu when creating other apps.

![Defining Marketing Cloud Account](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/app-center-integrate.png "Defining a Marketing Cloud Account in App Center") *Defining a Marketing Cloud Account in App Center*

### Permission

The Data Access step defines account features and data permissions that the app will require access to. You should only select permissions that are inside the scope of the API requests that will be used by the app. These permissions can be modified after the app has been created.

![Defining Access Permissions](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/app-center-access.png "Defining data and functionality access for an app") *Defining data and functionality access for an app*

### Clients

When creating MobilePush apps, the Data Access step is replaced with a Clients step. This interface enables client credentials to be defined for Apple iOS, Google and Amazon apps or projects. The process for obtaining these credentials is beyond the scope of this document, but is explained in Marketing Cloud documentation accessible from the 'How to register?' links in this interface. 

![Defining Client Credentials](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/app-center-clients.png "Defining client credentials for MobilePush apps") *Defining client credentials for MobilePush apps*

### Details

The final step is to review the details of the app. The OAuth Client ID and Client Secret credentials are provided on the details page. These are used with the Fuel Authentication Service to obtain OAuth tokens when using the Fuel APIs.

The Courtesy Limit of 50,000 requests per day indicates a soft capped limit on the number of requests an app can make. If the app exceeds this request limit, it will not be prevented from making requests, however this is monitored by Salesforce and the app may be rate limited or throttled if requests are accidentally or deliberately abused.

Clicking the 'Finish' button will save the app. Once an app is saved, it can be modified or deleted from the App Center Overview page.
 
![App Details](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/app-center-details.png "Details of an app in App Center") *Details of an app in App Center*

### Custom Activities and Triggers

After an app has been saved, Journey Builder Custom Activity and Trigger extensions can optionally be configured for Application Extension and Marketing Cloud apps from the 'Journey Builder Activity' and 'Journey Builder Trigger' tabs in the app interface. The process for creating these extensions is explained in the [Journey Builder Developers documentation](https://code.exacttarget.com/app-development/journey-builder-development/).

![Journey Builder Tabs](https://raw.githubusercontent.com/eliotharper/journey-builder-dev-guide/master/images/app-center-activities-triggers.png "Journey Builder Activity and Triggers tabs") *Journey Builder Activity and Triggers tabs*

## Obtaining OAuth Tokens

To obtain an OAuth token, you first need to perform a HTTP POST request specifying your client ID and client secret in the payload. An example request is provided below.

```
POST https://auth.exacttargetapis.com/v1/requestToken
Content-Type: application/json
{
  "clientId": "gyjzvytv7ukqtfn3x2qdyfsn",
  "clientSecret": "SJbAEenSK2SVBK4d4vBV6NKT"
}
```

This HTTP POST request returns an `accessToken` which is the OAuth token used for subsequent API requests and an `expiresIn` value indicating the expiration period of the OAuth token in seconds. An example response is provided below.

```
{
  "accessToken": "4ae36paatp4mnwkhanyhajp4",
  "expiresIn": 3600
}
```

## Access Token Management

You should not request a new token for each Fuel API request. An OAuth token is valid for one hour (or 3,600 seconds) and should be reused until its expiry. Making authentication requests before each API request is not only inefficient but is also unnecessary and may result in throttling. There are a few different methods for managing access tokens. 

### Fuel SDKs

The Fuel SDKs available at [https://github.com/ExactTarget](https://github.com/ExactTarget) include at their core, an object for acquiring and refreshing OAuth access tokens using client credentials, removing the requirement to manage access tokens at the application layer. 

### Try-Catch

You can also manage access tokens by a Try-Catch method. If you attempt to use an expired token, you will receive a 401 Unauthorized HTTP response. If this occurs, then you can make a new request to obtain an OAuth token.

### Track Expiry

An alternative method would be to convert the `expiresIn` value to a date time stamp and maintain the token state, for example by storing the key-value pairs to in-memory storage then check the token expiration date time prior to making an API request, or use a scheduled cron job to keep access tokens up to date.

## Refresh Tokens

As noted earlier, access tokens have a limited lifetime. If your application needs access to persistently use an API method beyond the lifetime of a single access token, it can obtain a refresh token. When using refresh tokens, instead of requiring a new authorization request when the authorization expires (for a given client ID and client secret), the client can use to the refresh token to retrieve a new access token with the same permissions as the old one, which is more efficient than requesting a new token each time.

To obtain a refresh token, when making the initial authorization request an additional `accessType` key-value pair should be included in the request with a value of `offline`. This is referred to 'offline access' in the oAuth2 protocol, as the user does not have to be present when the application obtains a new access token. A sample authorization request is provided below.

```
POST https://auth.exacttargetapis.com/v1/requestToken
Content-Type: application/json
{
  "clientId": "gyjzvytv7ukqtfn3x2qdyfsn",
  "clientSecret": "SJbAEenSK2SVBK4d4vBV6NKT",
  "accessType":"offline"
}
```

This request will include a refresh token in the response, as indicated below.

```
{
 "accessToken":"7p3byz3znnug6z96ma4wc24w",
  "expiresIn":3600,
  "refreshToken":"cqkbjhvaz44cms65ukcvztub"
}
```

This refresh token can then be used to obtain a new `accessToken` at any time (for example, several hours after the accessToken expires). When making a request to receive a new `accessToken`, you will also receive a new `refreshToken`. This newly provided `refreshToken` must be used in the subsequent call to request a new `accessToken`, since the previous `refreshToken` is now invalid as it has already been used. A sample request  to refresh an existing token is provided below.

```
{
  "clientId": "gyjzvytv7ukqtfn3x2qdyfsn",
  "clientSecret": "tv7ukqtfn3x2",
  "refreshToken":"cqkbjhvaz44cms65ukcvztub",
  "accessType": "offline"
}
```