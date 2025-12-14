# SummarizeRecordsRequest Documentation

[← Back to API Index](../reference.md)

---

## Attr: SummarizeRecordsRequest.aiFieldRequest

### Description
The [AIFieldRequest](../reference_2.md#object-aifieldrequest) generated from a natural language description of how to summarize each record, which may include a request for relevant supplemental information.

### See Also

- [AI.buildAIFieldRequest](AI.md#classmethod-aibuildaifieldrequest)

**Flags**: IR

---
## Attr: SummarizeRecordsRequest.dataSource

### Description
The [DataSource](DataSource.md#class-datasource) containing the [SummarizeRecordsRequest.records](#attr-summarizerecordsrequestrecords).

If [SummarizeRecordsRequest.component](#attr-summarizerecordsrequestcomponent) is also specified, then the component should be bound to the same `DataSource` or a `DataSource` inheriting from it.

**Flags**: IR

---
## Attr: SummarizeRecordsRequest.cancellationController

### Description
If provided, the [CancellationController](CancellationController.md#class-cancellationcontroller) that will be looked to for whether the record summarization operation is canceled.

**Flags**: IR

---
## Attr: SummarizeRecordsRequest.records

### Description
The records to summarize, from [DataSource](DataSource.md#class-datasource) [SummarizeRecordsRequest.dataSource](#attr-summarizerecordsrequestdatasource).

**Flags**: IR

---
## Attr: SummarizeRecordsRequest.component

### Description
If specified, the [DataBoundComponent](../reference.md#interface-databoundcomponent) that is displaying or managing the [SummarizeRecordsRequest.records](#attr-summarizerecordsrequestrecords).

The component should be bound to the same [SummarizeRecordsRequest.dataSource](#attr-summarizerecordsrequestdatasource) of the request or a `DataSource` inheriting from it.

**Flags**: IR

---
## Attr: SummarizeRecordsRequest.maxConcurrent

### Description
Maximum number of batches being summarized at any given time.

**Flags**: IR

---
## Attr: SummarizeRecordsRequest.maxRetries

### Description
The maximum number of retries of any one particular request to an [AIEngine](AIEngine.md#class-aiengine).

**Flags**: IR

---
## Attr: SummarizeRecordsRequest.maxRecordsPerBatch

### Description
If set, the maximum number of records that will be processed via AI in a single request. This can be further or alternatively limited by the [SummarizeRecordsRequest.aiFieldRequest](#attr-summarizerecordsrequestaifieldrequest)'s [maxRecordsPerBatch](AIFieldRequest.md#attr-aifieldrequestmaxrecordsperbatch) setting.

By default, requests will be filled with as many records as will fit into a single request to the selected [AIEngine](AIEngine.md#class-aiengine)(s).

**Flags**: IRA

---
## Attr: SummarizeRecordsRequest.aiFieldRequestSource

### Description
The source of the [SummarizeRecordsRequest.aiFieldRequest](#attr-summarizerecordsrequestaifieldrequest).

**Flags**: IR

---
