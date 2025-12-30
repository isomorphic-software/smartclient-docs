# XJSONDataSource Documentation

[← Back to API Index](../reference.md)

---

## Class: XJSONDataSource

*Inherits from:* [DataSource](DataSource.md#class-datasource)

### Description
A DataSource preconfigured to use the ["scriptInclude"](../reference_2.md#type-rpctransport) transport (sometimes called "JSONP") for cross-domain calls to JSON services.

To use this DataSource, provide the URL of the service as [DataSource.dataURL](DataSource.md#attr-datasourcedataurl), and provide [fields](DataSource.md#attr-datasourcefields) that describe the structure of the data you want to extract from the service's response.

[DataSource.recordXPath](DataSource.md#attr-datasourcerecordxpath) and [DataSourceField.valueXPath](DataSourceField.md#attr-datasourcefieldvaluexpath) can be used to extract data from the JSON structure returned by the service. See [Client-Side Data Integration](../kb_topics/clientDataIntegration.md#kb-topic-client-side-data-integration) for an overview of how to control what parts of the JSON structure are included in the [DSResponse](DSResponse.md#class-dsresponse) object, and hence provided to [DataBoundComponent](../reference.md#interface-databoundcomponent)s that are bound to this DataSource.

This XJSONDataSource is really a subclass of DataSource with just a few property settings:

```
    dataFormat : "json",
    dataTransport : "scriptInclude"
    callbackParam : "callback"
 
```

If you are also writing the server side code to respond to requests from this DataSource, see the [tutorial provided by Yahoo!](http://developer.yahoo.net/common/json.html#callbackparam) for a good overview of how this transport mechanism works. Note, as indicated in the tutorial above, the server is responsible for writing out not just the data, but also a JavaScript function call that tells the client that the response has arrived. The client passes the name of the function to call as the "callback" URL parameter.

NOTE: if you use this DataSource to contact Yahoo web services, remember to include output=json in the dataURL, as well as a [Yahoo developer ID](http://developer.yahoo.net/).

---
