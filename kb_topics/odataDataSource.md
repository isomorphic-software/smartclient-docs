# Server-side OData DataSource

[← Back to API Index](../reference.md)

---

## KB Topic: Server-side OData DataSource

### Description
`ODataDataSource` is a built-in server-side [DataSource](../classes/DataSource.md#class-datasource) implementation that extends [RestConnector](serverRestConnector.md#kb-topic-server-side-rest-connector) to add functionality for REST webservices that follow the [OData protocol](https://www.odata.org/). Everything that applies to `RestConnector` also applies to `ODataDataSource` - it is configured in the same way, provides the same support for pervasive Velocity templating, etc.

In addition to the regular `RestConnector` facilities, `ODataDataSource` adds the following support, specifically for REST services that follow the OData protocol

*   Generate an OData-compliant "$filter" query from standard SmartClient criteria. Note, the generated filter query will convert [textMatchStyle](../classes/DSRequest.md#attr-dsrequesttextmatchstyle) to the corresponding OData function ("`substring`" becomes "`contains`" and "`startsWith`" becomes "`startswith`"; other textMatchStyles just generate straight equality checks), but there is no current support for true [AdvancedCriteria](../reference.md#object-advancedcriteria)
*   Generate an OData "$orderby" parameter from the SmartClient sortBy information
*   Generate an OData "$select" parameter from the SmartClient "outputs" information
*   Derive "$skip" and "$top" attributes from the SmartClient startRow and endRow
*   Derive and apply the necessary "maxpagesize" Prefer header to encourage the remote server to allow the page size we would like to use
*   Request the OData "$count" property and make use of it to populate totalRows.
*   Modify certain things to match the OData defaults, where that differs from the normal `RestConnector` defaults
*   Apply all these generated and derived properties to the REST call

---
