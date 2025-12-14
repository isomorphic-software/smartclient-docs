# SummarizeValueRequest Documentation

[← Back to API Index](../reference.md)

---

## Attr: SummarizeValueRequest.dataSource

### Description
If specified, the [DataSource](DataSource.md#class-datasource) where the [SummarizeValueRequest.value](#attr-summarizevaluerequestvalue) originated.

If [SummarizeValueRequest.component](#attr-summarizevaluerequestcomponent) is also specified, then the component should be bound to the same `DataSource` or a `DataSource` inheriting from it.

**Flags**: IR

---
## Attr: SummarizeValueRequest.valueType

### Description
The type of the [SummarizeValueRequest.value](#attr-summarizevaluerequestvalue).

**Flags**: IR

---
## Attr: SummarizeValueRequest.aiRequest

### Description
The natural language description of how to summarize the value, which may include a request for relevant supplemental information.

Note: For more consistently-formatted AI-generated summaries of values, it is often helpful to specify [SummarizeValueRequest.examples](#attr-summarizevaluerequestexamples) that include the desired output form.

**Flags**: IR

---
## Attr: SummarizeValueRequest.component

### Description
If specified, the [DataBoundComponent](../reference.md#interface-databoundcomponent) displaying the [SummarizeValueRequest.value](#attr-summarizevaluerequestvalue).

If [SummarizeValueRequest.dataSource](#attr-summarizevaluerequestdatasource) is also specified, then the component should be bound to the same `DataSource` or a `DataSource` inheriting from it.

**Flags**: IR

---
## Attr: SummarizeValueRequest.examples

### Description
If specified, examples to provide to AI.

Examples that include the desired output form often help to make the formatting of AI-generated summaries of values more consistent.

**Flags**: IR

---
## Attr: SummarizeValueRequest.relevantFieldNames

### Description
If specified, the names of the [DBCField](../reference.md#object-dbcfield)s of the [SummarizeValueRequest.component](#attr-summarizevaluerequestcomponent) (or [DataSourceField](../reference_2.md#object-datasourcefield)s of the [SummarizeValueRequest.dataSource](#attr-summarizevaluerequestdatasource)) that are relevant to the request to summarize the [SummarizeValueRequest.value](#attr-summarizevaluerequestvalue).

**Flags**: IR

---
## Attr: SummarizeValueRequest.record

### Description
If specified, the [Record](../reference.md#object-record) containing the [SummarizeValueRequest.value](#attr-summarizevaluerequestvalue).

If supplying the record, then the [SummarizeValueRequest.component](#attr-summarizevaluerequestcomponent) and/or [SummarizeValueRequest.dataSource](#attr-summarizevaluerequestdatasource) must be specified as well.

**Flags**: IR

---
## Attr: SummarizeValueRequest.fieldName

### Description
If specified, the name of the field containing the [SummarizeValueRequest.value](#attr-summarizevaluerequestvalue).

**Flags**: IR

---
## Attr: SummarizeValueRequest.value

### Description
The value to summarize. Its type is specified by the [SummarizeValueRequest.valueType](#attr-summarizevaluerequestvaluetype).

**Flags**: IR

---
## Attr: SummarizeValueRequest.aiRequestSource

### Description
The source of the [SummarizeValueRequest.aiRequest](#attr-summarizevaluerequestairequest).

**Flags**: IR

---
