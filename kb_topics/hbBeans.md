# Beans and the DSRequest / DSResponse

[← Back to API Index](../reference.md)

---

## KB Topic: Beans and the DSRequest / DSResponse

### Description
This section relates to JPA and Hibernate datasources and describes how submitted data is used and what to expect in `DSResponse` if Smartclient is integrated with Hibernate using "Pre-existing beans" approach (see [hibernateIntegration](hibernateIntegration.md#kb-topic-integration-with-hibernate) for details).

Note that "beanless" integration mode is completely omitted here, since in that case data is represented by `Maps` instead of `Beans`.

#### Data sent in DSRequest
In case of add or update operations [DSRequest data](../classes/DSRequest.md#attr-dsrequestdata) is used to populate associated `Bean`:

*   add - new `Bean` is created and filled with submitted data
*   update - existing `Bean` is retrieved and then submitted data is set overwriting existing values

New values are applied using `DataSource.setProperties(...)` server-side API, which performs automatic conversions of any types that can reasonably be auto-converted, supports inner beans and recursive data structures, see server-side javadocs for details.

#### Data returned in DSResponse
In case of getting access to DSResponse (for example, by manually executing DSRequest in a [DMI](../classes/DMI.md#class-dmi)), DSResponse data can be accessed by calling `DSResponse.getData()` server-side API. See what data will be returned depending on [operation type](../classes/DSRequest.md#attr-dsrequestoperationtype) and other circumstances:

| Operation type | DSResponse data |
|---|---|
| Fetch | Generally fetch operation will return List of Beans or empty List if no records were found. However some features, if used, do break this rule:If [DSRequest.outputs](../classes/DSRequest.md#attr-dsrequestoutputs) (or [OperationBinding.outputs](../classes/OperationBinding.md#attr-operationbindingoutputs)) is set, then only fields listed in outputs are fetched from Database and, accordingly, DSResponse data will return List of Maps each Map holding only requested set of field/value pairs.If Server Summaries feature is used, then DSResponse data will also return List of Maps each Map holding only field/value pairs involved in summary query, i.e. only fields listed in [DSRequest.groupBy](../classes/DSRequest.md#attr-dsrequestgroupby) and [DSRequest.summaryFunctions](../classes/DSRequest.md#attr-dsrequestsummaryfunctions), see [Server Summaries overview](serverSummaries.md#kb-topic-server-summaries) for details. |
| Add | Add operation will return created Bean. |
| Update | If multiple records update is allowed (see [OperationBinding.allowMultiUpdate](../classes/OperationBinding.md#attr-operationbindingallowmultiupdate) and [MultiUpdatePolicy](../reference.md#type-multiupdatepolicy)}), then update operation will return List of Beans, or empty List if no records were actually updated. If multiple records update is not allowed, then update operation will return updated Bean, or null if record was not updated (for example, in case if it does not exist). |
| Remove | If multiple records update is allowed, then remove operation will always return null. If multi records update is not allowed, then remove operation will return a Map holding field/value pairs for [Primary Key fields](../classes/DataSourceField.md#attr-datasourcefieldprimarykey) of the record requested to be removed, no matter if the record was actually removed. Consult DSResponse.getAffectedRows() server-side API to see if the record was removed, or how many records were removed in case of multiple records removal. |

---
