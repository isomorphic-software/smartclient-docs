# SummarizeRecordsResult Documentation

[← Back to API Index](../reference.md)

---

## Attr: SummarizeRecordsResult.recordSummaries

### Description
If any batch is non-successful or the [SummarizeRecordsRequest.aiFieldRequest](#attr-summarizerecordsrequestaifieldrequest) is [numerical](#classmethod-aiisaifieldrequestnumerical), `null`; otherwise, the generated summaries (text) or unordered categories for the corresponding [records](#attr-summarizerecordsrequestrecords) of the [request](#object-summarizerecordsrequest).

### See Also

- [SummarizeRecordsResult.recordNumericalSummaries](#attr-summarizerecordsresultrecordnumericalsummaries)

**Flags**: IR

---
## Attr: SummarizeRecordsResult.recordNumericalSummaries

### Description
If any batch is non-successful or the [SummarizeRecordsRequest.aiFieldRequest](#attr-summarizerecordsrequestaifieldrequest) is not [numerical](#classmethod-aiisaifieldrequestnumerical), `null`; otherwise:

*   If the `valueClass` is "ordinal", the 0-based index of the category in the ordered list of [AIFieldRequest.categories](AIFieldRequest.md#attr-aifieldrequestcategories)
*   The computed numerical value

.. for the corresponding [records](#attr-summarizerecordsrequestrecords) of the [request](#object-summarizerecordsrequest).

### See Also

- [SummarizeRecordsResult.recordSummaries](#attr-summarizerecordsresultrecordsummaries)

**Flags**: IR

---
