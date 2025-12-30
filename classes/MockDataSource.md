# MockDataSource Documentation

[← Back to API Index](../reference.md)

---

## Class: MockDataSource

*Inherits from:* [DataSource](DataSource.md#class-datasource)

### Description
A special kind of [client-only DataSource](DataSource.md#attr-datasourceclientonly) that can be configured with ["mock data"](#attr-mockdatasourcemockdata) - a simple text format for table or tree data.

MockDataSources are produced by the Reify Mockup Importer when starting from mockup formats that use the mock data format. The docs for the [Reify Mockup Importer](../kb_topics/balsamiqImport.md#kb-topic-mockup-importer) explain various steps for converting a `MockDataSource` to a real DataSource.

`MockDataSource` is primarily intended as a temporary form of DataSource used during the process of converting a mockup into a real application. Generally, if creating a client-only DataSource in JavaScript , there is no reason to use the mock data format, as the mock data is not especially readable when written as a String literal. The mock data format _can_ be a slightly more compact and readable as compared to declaring [DataSource.cacheData](DataSource.md#attr-datasourcecachedata) in XML.

Note: If a MockDataSource has [addGlobalId](DataSource.md#attr-datasourceaddglobalid) set to true, it will be made available in global scope.

Unlike other DataSources, if a MockDataSource is created with an ID that is already in use by another DataSource, the existing DataSource will not be `destroy()`'d and the new MockDataSource will not be available by ID.  
Similarly, if a MockDataSource exists and a new DataSource is created with the same ID the MockDataSource will be `destroy()`'d automatically without logging a warning to the developer console.  
This means if application code changes to replace a MockDataSource with a "real" dataSource it will function as expected, without warnings, even if the MockDataSource creation code was not removed, regardless of the order in which the MockDataSource and "real" dataSource are created.

---
## Attr: MockDataSource.mockData

### Description
Data intended for a [ListGrid](ListGrid_1.md#class-listgrid) or [TreeGrid](TreeGrid.md#class-treegrid), expressed in a simple text format popularized by mockup tools such as [balsamiq](http://balsamiq.com) and now commonly supported in a variety of mockup tools.

Balsamiq publishes documentation of the grid format [here](https://docs.balsamiq.com/cloud/editing-controls/#the-data-grid-table-control), with a simple example of using tree-specific formatting [here](https://docs.balsamiq.com/cloud/editing-controls/#the-tree-pane).

MockData can also be provided as XML, CSV or JSON text by setting [MockDataFormat](../reference_2.md#type-mockdataformat) to the correct format.

An alternative format of data consisting of an array of [Records](../reference.md#object-record) can also be provided. In this case the records are converted to "grid" [format](../reference_2.md#type-mockdatatype).

**Flags**: IR

---
## Attr: MockDataSource.mockDataFormat

### Description
Format of data provided in [MockDataSource.mockData](#attr-mockdatasourcemockdata). See [MockDataFormat](../reference_2.md#type-mockdataformat).

**Flags**: IR

---
## Attr: MockDataSource.mockDataType

### Description
When [MockDataSource.mockDataFormat](#attr-mockdatasourcemockdataformat) is "mock", whether [MockDataSource.mockData](#attr-mockdatasourcemockdata) is in the "grid" or "tree" format. See [MockDataType](../reference_2.md#type-mockdatatype).

If not specified, the type will be detected from the data.

**Flags**: IR

---
