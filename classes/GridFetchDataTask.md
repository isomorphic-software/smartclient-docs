# GridFetchDataTask Documentation

[← Back to API Index](../reference.md)

---

## Class: GridFetchDataTask

*Inherits from:* [ComponentTask](ComponentTask.md#class-componenttask)

### Description
Fetch data matching specified criteria into grid.

### See Also

- [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata)

---
## Attr: GridFetchDataTask.applyToImplicitCriteria

### Description
Should criteria be applied to the grid as [implicit criteria](ListGrid_1.md#attr-listgridimplicitcriteria)? When criteria is applied this way, it is not shown to the user and cannot be changed by the user.

**Flags**: IR

---
## Attr: GridFetchDataTask.requestProperties

### Description
Additional properties to set on the DSRequest that will be issued to perform the fetch or clear criteria.

**Flags**: IR

---
## Attr: GridFetchDataTask.groupBy

### Description
List of fields to group by in the fetch.

See the [Server Summaries overview](../kb_topics/serverSummaries.md#kb-topic-server-summaries) for examples of usage.

### Groups

- serverSummaries

### See Also

- [GridFetchDataTask.summaryFunctions](#attr-gridfetchdatatasksummaryfunctions)

**Flags**: IR

---
## Attr: GridFetchDataTask.summaryFunctions

### Description
A mapping from field names to [summary functions](../reference_2.md#type-summaryfunction) to be applied to each field in the fetch.

See the [Server Summaries overview](../kb_topics/serverSummaries.md#kb-topic-server-summaries) for examples of usage.

### Groups

- serverSummaries

### See Also

- [GridFetchDataTask.groupBy](#attr-gridfetchdatataskgroupby)

**Flags**: IR

---
## Attr: GridFetchDataTask.criteria

### Description
Criteria to use for fetch. If criteria is `null` or empty, the filter criteria of the grid will be cleared.

**Flags**: IR

---
