# DSResponse Documentation

[← Back to API Index](../reference.md)

---

## Class: DSResponse

*Inherits from:* [RPCResponse](RPCResponse.md#class-rpcresponse)

### Description
Response sent by the server in response to a [DataSource request](../reference.md#object-dsrequest). Contains all the properties available on the basic [RPCResponse](RPCResponse.md#class-rpcresponse), in addition to the properties listed here.

---
## Attr: DSResponse.offlineTimestamp

### Description
Timestamp (millisecond value) to indicate when this dsResponse was cached in [offline storage](Offline.md#class-offline). Not applicable if the response has never been stored offline.

### Groups

- offlineGroup

**Flags**: R

---
## Attr: DSResponse.dataSource

### Description
The DataSource of this DSResponse.

### Groups

- dsResponse

**Flags**: IR

---
## Attr: DSResponse.fromOfflineCache

### Description
If set, indicates that this response came from the offline cache, not the server. This flag is the only reliable way for application code to determine the source of a response.

### Groups

- offlineGroup

**Flags**: R

---
## Attr: DSResponse.startRow

### Description
Starting row of returned server results, when using paged result fetching

Note that startRow and endRow are zero-based, inclusive at the beginning and exclusive at the end (like substring), so startRow: 0, endRow: 2 is a response containing two records.

### Groups

- paging

**Flags**: R

---
## Attr: DSResponse.data

### Description
For "fetch" operations, this is the array of Records fetched. For "update", "add", and "remove" operations, this is typically an array containing a single Record representing the record that was updated, added, or removed.

### Groups

- dsResponse

**Flags**: IR

---
## Attr: DSResponse.endRow

### Description
End row of returned server results, when using paged result fetching

Note that startRow and endRow are zero-based, inclusive at the beginning and exclusive at the end (like substring), so startRow: 0, endRow: 2 is a response containing two records.

### Groups

- paging

**Flags**: R

---
## Attr: DSResponse.errors

### Description
Server-side validation errors for an attempted "update" or "add" operation, as a JS Object where each property name is a field name from the record and each property value contains error information.

To extract just the simple error strings for each field we recommend passing this object to [DataSource.getSimpleErrors](DataSource.md#classmethod-datasourcegetsimpleerrors)

The Java API DSResponse.addError(fieldName, errorMessage) is used to send server-side errors to the client. See the Java Server Reference for details.

### Groups

- errorHandling

### See Also

- [DataSource.handleError](DataSource.md#method-datasourcehandleerror)

**Flags**: R

---
## Attr: DSResponse.httpHeaders

### Description
HTTP headers returned by the server as a map from header name to header value.

Headers are available only when the default [RPCTransport](../reference_2.md#type-rpctransport) "xmlHttpRequest" is in use, and browsers may limit access to headers for cross-domain requests or in other security-sensitive scenarios.

**Flags**: R

---
## Attr: DSResponse.clientContext

### Description
The [DSRequest.clientContext](DSRequest.md#attr-dsrequestclientcontext) object as set on the [DSRequest](../reference.md#object-dsrequest).

### See Also

- [DSRequest.clientContext](DSRequest.md#attr-dsrequestclientcontext)
- [RPCResponse.clientContext](RPCResponse.md#attr-rpcresponseclientcontext)

**Flags**: R

---
## Attr: DSResponse.invalidateCache

### Description
Optional flag that can be set by the server to force ResultSets to drop any caches of records from the DataSource that was the target of the operation.

### Groups

- cacheSync

**Flags**: R

---
## Attr: DSResponse.operationType

### Description
The operation type of the request corresponding to this DSResponse.

### Groups

- dsResponse

**Flags**: IR

---
## Attr: DSResponse.queueStatus

### Description
An extra property of each DSResponse to a queued request that indicates whether the queue as a whole succeeded. A queueStatus of [RPCResponse.STATUS_SUCCESS](RPCResponse.md#classattr-rpcresponsestatus_success), or 0, indicates that the queue succeeded whereas a queueStatus of [RPCResponse.STATUS_FAILURE](RPCResponse.md#classattr-rpcresponsestatus_failure), or -1, indicates that the queue failed.

For example, if two "update" requests are sent in a queue and the first succeeded, but the second failed validation, then both DSResponses' queueStatus would be -1, but the [status](#attr-dsresponsestatus) of the first would be [RPCResponse.STATUS_SUCCESS](RPCResponse.md#classattr-rpcresponsestatus_success) and the status of the second would be an error code such as [RPCResponse.STATUS_VALIDATION_ERROR](RPCResponse.md#classattr-rpcresponsestatus_validation_error).

### Groups

- errorHandling

**Flags**: IR

---
## Attr: DSResponse.operationId

### Description
The operation ID of the request corresponding to this DSResponse.

### Groups

- dsResponse

**Flags**: IR

---
## Attr: DSResponse.status

### Description
Same meaning as [RPCResponse.status](RPCResponse.md#attr-rpcresponsestatus), except DSResponses have additional error codes, such as [validation failure](RPCResponse.md#classattr-rpcresponsestatus_validation_error).

### Groups

- errorHandling

### See Also

- [dataSourceOperations](../kb_topics/dataSourceOperations.md#kb-topic-datasource-operations)

**Flags**: IR

---
## Attr: DSResponse.totalRows

### Description
Total number of rows available from the server that match the current filter criteria, when using paged result fetching.

### Groups

- paging

**Flags**: R

---
