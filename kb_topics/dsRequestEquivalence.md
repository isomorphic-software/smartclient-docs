# dsRequestEquivalence

[← Back to API Index](../reference.md)

---

## KB Topic: dsRequestEquivalence

### Description
Various subsystems have a need to compare DataSource requests and understand if they are equivalent or affect the same data (examples include [automatic cache synchronization](../classes/ResultSet.md#class-resultset) and [offline caching and synchronization](../classes/DataSource.md#attr-datasourceuseofflinestorage)).

Aside from basic properties that would clearly make two DSRequests non-equivalent (dataSource, operationType and data, as well as sortBy, startRow, endRow and textMatchStyle for a "fetch"), [DSRequest.operationId](../classes/DSRequest.md#attr-dsrequestoperationid) is the only property that will cause two DSRequests to be considered distinct (non-equivalent) requests.

Bearing this in mind, the best practice is:

*   everything that will be treated as criteria or as values on the server side should be part of [DSRequest.data](../classes/DSRequest.md#attr-dsrequestdata). Do not "smuggle" data that will ultimately be used as criteria or values in other dsRequest properties, such as [HTTP parameters](../classes/RPCRequest.md#attr-rpcrequestparams).
*   use [DSRequest.operationId](../classes/DSRequest.md#attr-dsrequestoperationid) as the sole piece of information in the request that modifies how the request as a whole is executed. If two or more pieces of information are required, combine or encode them into a single operationId String. If this becomes awkward because there are many operation variants, consider including additional fields in [DSRequest.data](../classes/DSRequest.md#attr-dsrequestdata) instead.

[DataSource.cloneDSRequest](../classes/DataSource.md#method-datasourceclonedsrequest) can be used to create an equivalent DSRequest.

---
