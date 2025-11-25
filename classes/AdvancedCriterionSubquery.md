# AdvancedCriterionSubquery Documentation

[← Back to API Index](../main.md)

---

## Attr: AdvancedCriterionSubquery.queryOutput

### Description
The name of the field that will be used as the output of this query. Only useful if your subquery returns more than one field, and optional even in that case. See the [Subqueries overview](../main.md#object-advancedcriterionsubquery) for more details

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: AdvancedCriterionSubquery.queryFK

### Description
The default for a subquery is that the records are joined to the main DataSource on the first [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) one-to-many relationship found, in field order. So for example, querying `Customer`s with a subquery on `Order`s, we discover `Order.customerId` FK pointing to `Customer.id`. More complicated relations are also auto-discovered: for example, querying `Customer`s with a subquery on `OrderLine`s, we will discover the link to `Customer` via `OrderLine.orderNumber` and then `Order.customerId`.

For many use cases, there is only one relation between any two DataSources, so this default discovery of the relation is often sufficient. However, if you need to, you can optionally specify a `queryFK` as the fieldName of a `foreignKey` from the "many" to the "one". If the relation is indirect - as with the join from `OrderLine` to `Customer` described above - you can specify `queryFK` as a dot-separated path from "many" to "one", like this: `queryFK: "orderNumber.customerId"` (but note that this is optional - often, a start point is all that is required to identify the relation-path to use)

**NOTE:**The `queryFK` property leverages the [includeVia](DataSourceField.md#attr-datasourcefieldincludevia) feature, and so is constrained by the same restrictions as that feature. Primarily, this means that `queryFK` can only name a `foreignKey` field on the [subquery dataSouce](#attr-advancedcriterionsubquerydatasource); it is not valid to name a field on the main dataSource. In practice, this is not usually a restriction because typically the subquery dataSource will be at the "many" end of a direct or indirect relation to the main dataSource, and so is naturally the one that declares the `foreignKey`

You can also specify the special value "\*none\*" for `queryFK`, which means the aggregation query should be done independently from the main query, to simply produce a value separately without any joins to the main dataset. A subquery that specifies `queryFK: "*none*"` is quite unusual because most use cases of subqueries require a join to the parent dataSource; however, valid use cases do exist - see the "Simple valueQuery" example on the [subquery overview page](../main.md#object-advancedcriterionsubquery)

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: AdvancedCriterionSubquery.criteria

### Description
Optional criteria to use for this subquery. Note, subqueries usually have implicit criteria, because they are joined to the main dataSource fetch unless the [queryFK](#attr-advancedcriterionsubqueryqueryfk) is set to the special value "\*none\*".

Also, because subqueries are themselves part of a larger set of criteria, the subquery result is compared to some other value in that larger criteria - it is easy to get confused by this multi-level criteria issue. You may find it helpful to think of this property as "inside criteria" (criteria used inside this subquery to derive its result) and the criterion of which the subquery is a component (as a [fieldQuery](Criterion.md#attr-criterionfieldquery) or [valueQuery](Criterion.md#attr-criterionvaluequery)), as "outside criteria"

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: AdvancedCriterionSubquery.summaryFunctions

### Description
A mapping from field names to [summary functions](../main_2.md#type-summaryfunction) to be applied to each field.

Valid only for an operation of type "fetch". See the [Server Summaries overview](../kb_topics/serverSummaries.md#kb-topic-server-summaries) for examples of usage.

### Groups

- serverSummaries

### See Also

- [DSRequest.groupBy](DSRequest.md#attr-dsrequestgroupby)

**Flags**: IR

---
## Attr: AdvancedCriterionSubquery.canEmbedSQL

### Description
Indicates whether this subquery can be implemented by embedding SQL directly in the wider SQL statement that will be used to resolve the fetch request. This property is considered as part of a set of rules we apply to decide whether a subquery can be resolved by embedding SQL (which is the most efficient thing to do, and may be significantly faster), or if we must resolve by separating the subquery out into its own [DSRequest](../main_2.md#object-dsrequest) and manually applying the results.

There are two reasons why we might decide to run a subquery as its own `DSRequest`: First, if either the "main" dataSource or the subquery dataSource is not an [SQL dataSource](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources), then obviously we cannot merge into a single SQL statement. More subtly, if there is the possibility that customized logic might be in play, we run the subquery separately because in that case we may interfere with - or completely fail to apply - the custom logic if we do not run the subquery as a full-fledged `DSRequest`.

`canEmbedSQL` is intended to allow you to override our heuristics, for cases where you know a particular subquery definitely can, or definitely can't, be embedded.

Note, whether or not we separate out the subquery into its own `DSRequest`, [declarative security rules](../kb_topics/declarativeSecurity.md#kb-topic-declarative-security) are always applied. So, for example, if the current user is not permitted to use the [subquery dataSource](#attr-advancedcriterionsubquerydatasource) or an [operation](#attr-advancedcriterionsubqueryoperationid) explicitly named on the subquery, the entire fetch operation that the subquery is part of will fail. More nuanced, if the current user is prohibited by [field-level security](DataSourceField.md#attr-datasourcefieldcanview) from viewing a field, that field will be stripped out of the subquery, which may lead to the subquery failing in a hard-to-predict way (but note, we always log a warning to the server logs when a field is removed in these circumstances).

The rules around embedding or separating a subquery are, in order, as follows. As you can see, `canEmbedSQL` overrides all rules except the first (we obviously can't embed SQL if one of the dataSources isn't implemented using SQL)

1.  If either the "main" dataSource or the subquery dataSource is not an [sql dataSource](DataSource.md#attr-datasourceservertype), the subquery must by separated. Otherwise,
2.  If the `canEmbedSQL` flag is non-null, we honor it. Otherwise,
3.  If the subquery specifies an explicit operationId, the subquery must be separated. Otherwise,
4.  If the subquery dataSource declares a custom fetch [operation](OperationBinding.md#class-operationbinding) (that is, a fetch operation that does not declare an [operationId](OperationBinding.md#attr-operationbindingoperationid)), the subquery must be separated. Otherwise,
5.  If the subquery dataSource declares either of the dataSource-level customization properties [DataSource.serverObject](DataSource.md#attr-datasourceserverobject) or [DataSource.script](DataSource.md#attr-datasourcescript), the subquery must be separated. Otherwise,
6.  If the subquery DataSource is a direct instance of the base class (ie, its canonical class name is `com.isomorphic.sql.SQLDataSource`), the subquery can be embedded. Otherwise,
7.  We now know that subquery dataSource is a subclass of `SQLDataSource`. We use Reflection to inspect the implementing class: if it overrides any of the methods `execute()`, `executeFetch{}` or `SQLExecute`, the subquery must be separated (note, we cache the results of these tests so Reflection is only used the first time a given dataSource instance is used)
8.  If we get to this point without having decided whether the subquery can be embedded, or must be separated, the subquery can be embedded

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: AdvancedCriterionSubquery.operationId

### Description
[Operation binding](OperationBinding.md#class-operationbinding) to use for this subquery. Note, this refers to an `operationBinding` on the [subquery dataSource](#attr-advancedcriterionsubquerydatasource), not the DataSource associated with the overall fetch request. Also note that specifying an `operationId` will cause SmartClient to run the subquery separately by default, which may have performance implications. This default behavior can be overridden - see [canEmbedSQL](#attr-advancedcriterionsubquerycanembedsql) for details.

### Groups

- operations

**Flags**: IR

---
## Attr: AdvancedCriterionSubquery.dataSource

### Description
The name of the [DataSource](DataSource.md#class-datasource) to use for this subquery

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: AdvancedCriterionSubquery.groupBy

### Description
List of fields to group by when using [server-side summarization](../kb_topics/serverSummaries.md#kb-topic-server-summaries).

Valid only for an operation of type "fetch". See the [Server Summaries overview](../kb_topics/serverSummaries.md#kb-topic-server-summaries) for details and examples of usage.

### Groups

- serverSummaries

### See Also

- [DSRequest.summaryFunctions](DSRequest.md#attr-dsrequestsummaryfunctions)

**Flags**: IR

---
