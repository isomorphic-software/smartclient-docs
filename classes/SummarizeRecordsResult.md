# SummarizeRecordsResult Documentation

[← Back to API Index](../reference.md)

---

## Attr: SummarizeRecordsResult.recordSummaries

### Description
If any batch is non-successful or the [SummarizeRecordsRequest.aiFieldRequest](SummarizeRecordsRequest.md#attr-summarizerecordsrequestaifieldrequest) is [numerical](AI.md#classmethod-aiisaifieldrequestnumerical), `null`; otherwise, the generated summaries (text) or unordered categories for the corresponding [records](SummarizeRecordsRequest.md#attr-summarizerecordsrequestrecords) of the [request](../reference_2.md#object-summarizerecordsrequest).

### See Also

- [SummarizeRecordsResult.recordNumericalSummaries](#attr-summarizerecordsresultrecordnumericalsummaries)

**Flags**: IR

---
## Attr: SummarizeRecordsResult.partialResults

### Description
All partial results. There will be at most one [SummarizeRecordsPartialResult](../reference.md#object-summarizerecordspartialresult) covering each [record](SummarizeRecordsRequest.md#attr-summarizerecordsrequestrecords) of the [request](../reference_2.md#object-summarizerecordsrequest). Note: there may be no `SummarizeRecordsPartialResult` for a record if the record summarization operation is canceled or fails early.

The order of `SummarizeRecordsPartialResult` objects in the array is unspecified.

This property may be `null` if an error occurs early.

**Flags**: IR

---
## Attr: SummarizeRecordsResult.recordNumericalSummaries

### Description
If any batch is non-successful or the [SummarizeRecordsRequest.aiFieldRequest](SummarizeRecordsRequest.md#attr-summarizerecordsrequestaifieldrequest) is not [numerical](AI.md#classmethod-aiisaifieldrequestnumerical), `null`; otherwise:

*   If the `valueClass` is "ordinal", the 0-based index of the category in the ordered list of [AIFieldRequest.categories](AIFieldRequest.md#attr-aifieldrequestcategories)
*   The computed numerical value

.. for the corresponding [records](SummarizeRecordsRequest.md#attr-summarizerecordsrequestrecords) of the [request](../reference_2.md#object-summarizerecordsrequest).

### See Also

- [SummarizeRecordsResult.recordSummaries](#attr-summarizerecordsresultrecordsummaries)

**Flags**: IR

---
