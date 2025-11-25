# FacadeDataSource Documentation

[← Back to API Index](../main.md)

---

## Class: FacadeDataSource

*Inherits from:* [DataSource](DataSource.md#class-datasource)

### Description
Extends an arbitrary [DataSource](DataSource.md#class-datasource) with the ability to queue requests made on it and dispatch the queued requests on demand. To use, create a FacadeDataSource instance with the [inheritsFrom](DataSource.md#attr-datasourceinheritsfrom) property set to the DataSource that you wish to extend.

This advanced class is intended to be used for testing data-bound components. This should not be used in production code.

See also the overview of the [DataSource Facade pattern](../kb_topics/dsFacade.md#kb-topic-datasource-facade-pattern).

---
## Attr: FacadeDataSource.queuedRequests

### Description
An array of derived DS requests that are queued to be [executed](DataSource.md#method-datasourceexecute) on the underlying [inherited](DataSource.md#attr-datasourceinheritsfrom) DataSource.

When a DS request is made on this FacadeDataSource, if [queueRequests](#attr-facadedatasourcequeuerequests) is true, then a new DS request is created based on the given DS request and added to this queue.

To clear the queue, set [queueRequests](#attr-facadedatasourcequeuerequests) to false or call [clearQueue()](#method-facadedatasourceclearqueue).

**Flags**: R

---
## Attr: FacadeDataSource.queueRequests

### Description
Should requests be queued?

When DS requests are made on the FacadeDataSource, a new, derived DS request on the underlying [inherited](DataSource.md#attr-datasourceinheritsfrom) DataSource is created. If queueRequests is true, then the derived DS request is added to the [queuedRequests](#attr-facadedatasourcequeuedrequests) array. If false, then the derived DS request is [executed](DataSource.md#method-datasourceexecute) immediately on the inherited DataSource.

**Flags**: IRW

---
## Method: FacadeDataSource.clearQueue

### Description
Shorthand to clear the [request queue](#attr-facadedatasourcequeuedrequests) without changing the value of [queueRequests](#attr-facadedatasourcequeuerequests).

---
## Method: FacadeDataSource.setQueueRequests

### Description
Setter for [queueRequests](#attr-facadedatasourcequeuerequests).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| queueRequests | [boolean](../main.md#type-boolean) | false | — | — |

### See Also

- [FacadeDataSource.clearQueue](#method-facadedatasourceclearqueue)

---
