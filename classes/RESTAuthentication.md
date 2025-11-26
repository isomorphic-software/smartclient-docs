# RESTAuthentication Documentation

[← Back to API Index](../reference.md)

---

## Attr: RESTAuthentication.authToken

### Description
For a [RestConnector DataSource](../kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector) using [bearerToken authentication](../reference_2.md#type-restauthenticationtype), the token to use. This attribute is for use when you are using bearerToken auth with a long-lived token, such as a fixed API key, rather than a regularly changing refresh/accept pattern. If you need to use the refresh/accept token pattern, omit this attribute and instead declare an [authentication dataSource](#attr-restauthenticationdatasource)

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: RESTAuthentication.password

### Description
For a [RestConnector DataSource](../kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector), the password to authenticate with if you are using [basic authentication](../reference_2.md#type-restauthenticationtype). Note, for services that support Basic authentication but require an API key rather than a password, you still use this property, just set it to the API key instead

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: RESTAuthentication.authHeader

### Description
For a [RestConnector DataSource](../kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector) using [authHeader authentication](../reference_2.md#type-restauthenticationtype), the complete, well-formed header value to set for the "Authorization" HTTP header. This attribute is for use when you are using authHeader authentication with a long-lived token, such as a fixed API key, rather than a regularly changing refresh/accept pattern. If you need to use the refresh/accept token pattern, omit this attribute and instead declare an [authentication dataSource](#attr-restauthenticationdatasource)

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: RESTAuthentication.username

### Description
For a [RestConnector DataSource](../kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector), the username to authenticate with if you are using [basic authentication](../reference_2.md#type-restauthenticationtype)

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: RESTAuthentication.type

### Description
For a [RestConnector DataSource](../kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector), the authentication type to use. Note, as well as the formal header-based authentication types used by most REST services, `RestConnector` can also support more ad-hoc auth schemes, such as sending a username/password or authentication token in the body of a request. Whether or not such non-standard auth schemes are a good idea is academic; if the REST endpoint you need to target is expecting a token in a URL param, that's what you have to provide.

Because `RestConnector` is so configurable, it is easy to achieve this. Assuming you have an API token that must be passed as parameter "Token", and that token is stored in your `system.properties` file, achieving this is as easy as adding the following to your [serverConfig](DataSource.md#attr-datasourceserverconfig):

```
    <params>
        <Token>$config['myrestservice.apikey']</Token>
    </params>
 
```
Note, if the REST service you are targeting does have a non-standard auth scheme that does not use the HTTP Authorization header, you should simply omit the [auth block](DataSource.md#attr-datasourceauth)

### Groups

- serverRestConnector

**Flags**: IR

---
## Attr: RESTAuthentication.dataSource

### Description
For a [RestConnector DataSource](../kb_topics/serverRestConnector.md#kb-topic-server-side-rest-connector), a second dataSource that is capable of fetching tokens that this dataSource can use to authenticate requests. This property is required for [bearerToken](../reference_2.md#type-restauthenticationtype) and [authHeader](../reference_2.md#type-restauthenticationtype) authentication types.

Typically, this dataSource will be a separate "rest" dataSource that connects to the token vending endpoint of an authorization server, passing in a "refresh" token and getting back an "access" token. Access tokens are typically short-lived, to minimize their usefulness to attackers if the token should somehow be exposed. When an access token expires it must be refreshed by again connecting to the token vending endpoint of the authorization server. `RestConnector` handles all the mechanics of this for you; you just have to provide a dataSource that can do the fetch.

Note, `RestConnector` will issue a straightforward fetch with null criteria on the authentication dataSource when it needs to refresh its access token. This means that the authentication dataSource must be able to supply the refresh token to the REST auth endpoint without context from the dataSource fetch request. As mentioned above, the authentication dataSource is typically another "rest" dataSource, so you can use `RestConnector`'s extensive request templating features to accomplish this - for example, by embedding a reference to a `server.properties` property in the [dataURL](DataSource.md#attr-datasourcedataurl)

A `RestConnector` authentication dataSource should include the following fields. Note, the "Field name" shown in the table is just the default; you can override the name of any of these fields by setting the property shown in the "Customize" column. So, eg, if you set `tokenField: "custom_token"` in the [auth](../reference.md#object-restauthentication) config block, we will expect the dataSource to contain a field called "custom\_token" instead of the default "access\_token"

| Field name | Description | Customize |
|---|---|---|
| access_token | For "bearerToken" auth only, field containing the bearer token to be set in the Authorization header (SmartClient will add the "Bearer" text) | tokenField |
| authorizationheader | For "authHeader" auth only, field containing the complete, well-formed header value to be set in the Authorization header | headerAuthorizationField |
| expires | Absolute point in time when this token expires, expressed as milliseconds since the epoch (midnight on January 1st 1970) | expiresField |
| expires_in | Length of time from now before this token expires, expressed as a number of seconds. If "expires" is also present, "expires" is used in preference to "expires_in". If neither value is present, the token is considered to be one that does not expire | expiresInField |

### Groups

- serverRestConnector

**Flags**: IR

---
