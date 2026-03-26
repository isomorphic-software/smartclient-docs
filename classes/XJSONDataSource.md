# XJSONDataSource Documentation

[← Back to API Index](../reference.md)

---

## Class: XJSONDataSource

*Inherits from:* [DataSource](DataSource.md#class-datasource)

### Description
A DataSource preconfigured to use the ["scriptInclude"](../reference.md#type-rpctransport) transport (sometimes called "JSONP") for cross-domain calls to JSON services.

To use this DataSource, provide the URL of the service as [DataSource.dataURL](DataSource.md#attr-datasourcedataurl), and provide [fields](DataSource.md#attr-datasourcefields) that describe the structure of the data you want to extract from the service's response.

[DataSource.recordXPath](DataSource.md#attr-datasourcerecordxpath) and [DataSourceField.valueXPath](DataSourceField.md#attr-datasourcefieldvaluexpath) can be used to extract data from the JSON structure returned by the service. See [Client-Side Data Integration](../kb_topics/clientDataIntegration.md#kb-topic-client-side-data-integration) for an overview of how to control what parts of the JSON structure are included in the [DSResponse](DSResponse.md#class-dsresponse) object, and hence provided to [DataBoundComponent](../reference.md#interface-databoundcomponent)s that are bound to this DataSource.

This XJSONDataSource is really a subclass of DataSource with just a few property settings:

```
    dataFormat : "json",
    dataTransport : "scriptInclude"
    callbackParam : "callback"
 
```

---
