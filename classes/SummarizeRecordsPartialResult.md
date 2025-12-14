# SummarizeRecordsPartialResult Documentation

[← Back to API Index](../reference.md)

---

## Attr: SummarizeRecordsPartialResult.startIndex

### Description
Starting index of the batch within the [records](SummarizeRecordsRequest.md#attr-summarizerecordsrequestrecords) of the [SummarizeRecordsRequest](../reference_2.md#object-summarizerecordsrequest).

**Flags**: IR

---
## Attr: SummarizeRecordsPartialResult.recordSummaries

### Description
If successful and the [SummarizeRecordsRequest.aiFieldRequest](SummarizeRecordsRequest.md#attr-summarizerecordsrequestaifieldrequest) is not [numerical](AI.md#classmethod-aiisaifieldrequestnumerical), the generated record summaries (text) or unordered categories for the corresponding records in the batch.

This array will have the same [SummarizeRecordsPartialResult.length](#attr-summarizerecordspartialresultlength) as the batch.

**Flags**: IR

---
## Attr: SummarizeRecordsPartialResult.recordNumericalSummaries

### Description
If successful and the [SummarizeRecordsRequest.aiFieldRequest](SummarizeRecordsRequest.md#attr-summarizerecordsrequestaifieldrequest) is [numerical](AI.md#classmethod-aiisaifieldrequestnumerical),

*   If the `valueClass` is "ordinal", the 0-based index of the category in the ordered list of [AIFieldRequest.categories](AIFieldRequest.md#attr-aifieldrequestcategories)
*   The computed numerical value

.. for the corresponding records in the batch.

This array will have the same [SummarizeRecordsPartialResult.length](#attr-summarizerecordspartialresultlength) as the batch.

**Flags**: IR

---
## Attr: SummarizeRecordsPartialResult.length

### Description
The number of records in the batch.

**Flags**: IR

---
