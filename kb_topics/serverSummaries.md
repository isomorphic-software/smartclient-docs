# Server Summaries

[← Back to API Index](../reference.md)

---

## KB Topic: Server Summaries

### Description
In SmartClient, "summarization" refers to applying functions to DataSource fields to obtain _summary records_ calculated from the values of multiple DataSource records.

For example, by applying an "average" function to a DataSourceField representing the dollar value of an order, you can calculate the average dollar amount of a set of orders.

Server Summaries is a feature of the SmartClient Server allowing similar summaries to be computed server-side, generally by the database engine itself, or client-side for [clientOnly DataSources](clientOnlyDataSources.md#kb-topic-client-only-datasources). Client-side calculation of summary records is also supported on ListGrids via the [showGridSummary feature](../classes/ListGrid_1.md#attr-listgridshowgridsummary).

**Server-side calculation is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

See also the related feature which allows a single field to receive a value summarized from several related records, [DataSourceField.includeSummaryFunction](../classes/DataSourceField.md#attr-datasourcefieldincludesummaryfunction).

Summarization can be statically configured directly in a .ds.xml file, or can be dynamically configured when sending a [DSRequest](../reference.md#object-dsrequest), either client-side or server-side. The following examples all assume a DataSource with fields like this:

```
 <DataSource ID="dsOrders" ...>
      <fields>
          <field name="customerName" type="text" />
          <field name="orderDate" type="date" />
          <field name="deliveryStatus" type="string" />
          ...
      </fields>
 </DataSource>
 
```

#### Summaries in DataSource .ds.xml files

You can declare summarization directly on an [operationBinding](../classes/OperationBinding.md#class-operationbinding) in a .ds.xml file, using [OperationBinding.summaryFunctions](../classes/OperationBinding.md#attr-operationbindingsummaryfunctions) and [OperationBinding.groupBy](../classes/OperationBinding.md#attr-operationbindinggroupby). For example:

```
  <DataSource ID="dsOrders" ...>
      ...
      <operationBindings>
          <operationBinding operationType="fetch" operationId="lastOrderDateByCustomer">
              <summaryFunctions>
                  <orderDate>max</orderDate>
              </summaryFunctions>
              <groupBy>customerName</groupBy>
          </operationBinding>
      </operationBindings>
  </DataSource>
 
```
This would return summary records representing the most recent order per customer. Represented in JSON, the returned records would look like:
```
   { customerName: "JBar Struts", orderDate:"2012/02/05" },
   { customerName: "KFoo Widgets", orderDate:"2012/03/01" },
   ...
 
```
This is analogous to the result of a SQL query like:
```
	SELECT
		max(order.orderDate)
		order.customerName
	FROM
		order
	GROUP BY
		order.customerName
 
```
Note that, as with SQL, the returned records will _only_ include the fields where summary functions were applied or which were used for grouping - "deliveryDate" and other fields are not included because in general, summary records may represent data from more than one record (there may be more than one record with the "max" value, and consider also "sum" or "avg" functions), so it's ambiguous which record's values should be returned for non-grouped, non-summarized fields.

#### Dynamically Requested Summaries

[DSRequest.summaryFunctions](../classes/DSRequest.md#attr-dsrequestsummaryfunctions) and [DSRequest.groupBy](../classes/DSRequest.md#attr-dsrequestgroupby) allow you to dynamically request a server summary from client-side code. For example:

```
	dsOrders.fetchData(null, callback, {
		summaryFunctions:{"orderDate": "max"}
		groupBy:["customerName"],
	});
 
```
By default such requests are allowed, but such requests can be disallowed on a per-DataSource or system-wide level if you have concerns - see [DataSource.allowClientRequestedSummaries](../classes/DataSource.md#attr-datasourceallowclientrequestedsummaries).

You can also dynamically request summaries from server-side code (for example, in a [DMI](../classes/DMI.md#class-dmi) method):

```
   DSRequest dsRequest = new DSRequest("dsOrders", "fetch");
   dsRequest.setSummaryFunctions(new HashMap() {{
	    put("orderDate", SummaryFunctionType.MAX);
   }});
   dsRequest.setGroupBy("customerName");
   DSResponse dsResponse = dsRequest.execute();
 
```

#### Sort & Data Paging

Sort directions are supported for queries that involve server summarization although may only target fields that are returned by the query (only those fields included in `groupBy` or where a `summaryFunction` was applied).

Data paging is also supported, however, consider that for aggregated queries, when asked for a second page of data, the database is likely to have to repeat all the work of calculating aggregated values. Turning paging off or setting a generous [ListGrid.dataPageSize](../classes/ListGrid_1.md#attr-listgriddatapagesize) is advised.

#### Criteria

#### SQL & clientOnly DataSource

Criteria is automatically split into pre and post summarization parts:

*   Fields that are not summarized will have criteria applied to them before summarization. This includes [group by](../classes/DSRequest.md#attr-dsrequestgroupby) fields and fields that are there just for filtering purposes, i.e. might not be fetched at all. For example if a "price" field would be a regular field in a fetch, i.e. not summarized, criteria like "price < 5" will eliminate records where price is less than 5, so such records would not affect the average or total computed.
*   Fields that are summarized will have criteria applied to them after summarization. For example if the "avg" summary function is being applied to a "price" field would, same criteria "price < 5" would eliminate records where summarized value "avg(price)" is less than 5.

This post-summarization server filtering matches client-side filtering, since it is always post-summarization on the client-side. Disabling filter for summarized fields on the client-side is no longer necessary to get the same results, as it was in previous versions.

Previous versions applied criteria on the server for all fields **before** summarization. You can get that behavior back via [OperationBinding.applyCriteriaBeforeAggregation](../classes/OperationBinding.md#attr-operationbindingapplycriteriabeforeaggregation) setting. Note that in that case you need to turn off client-side filtering for aggregated fields, because client-side filtering cannot replicate pre-summarization filtering, as client sees only the final computed aggregates. See [OperationBinding.applyCriteriaBeforeAggregation](../classes/OperationBinding.md#attr-operationbindingapplycriteriabeforeaggregation) docs for more details.

#### HB and JPA DataSources

Criteria apply to record **before** summaries are applied. For example, if the "avg" function is being applied to a "price" field, criteria like "price < 5" will eliminate records where price is less than 5 _before_ the average price is calculated. This means that client-side filtering may not work as expected with summarized results: client-side filter criteria are necessarily applied _after_ summary functions have been applied, so may not match the server's behavior. You can set [ResultSet.useClientFiltering](../classes/ResultSet.md#attr-resultsetuseclientfiltering) to disable client-side filtering on a grid via [ListGrid.dataProperties](../classes/ListGrid_1.md#attr-listgriddataproperties). Or individual fields can be marked [canFilter:false](../classes/ListGridField.md#attr-listgridfieldcanfilter).

#### SQL Templating & Aggregation

With the [SQL Templating](customQuerying.md#kb-topic-custom-querying-overview) feature you can customize portions of the query without ever having to re-create portions that the framework knows how to generate. This allows to create partially or entirely custom complex aggregation queries to use in a regular "fetch" operation. The SQL Templating feature supports aggregated queries just as regular ones with some additions, see below.

In clause-by-clause substitution there are two additional aggregation specific clauses: [groupClause](../classes/OperationBinding.md#attr-operationbindinggroupclause) providing "group by" part of aggregated query and [groupWhereClause](../classes/OperationBinding.md#attr-operationbindinggroupwhereclause) providing "having" part of aggregated query (or outer "where" part if sub-select approach is used, see [OperationBinding.useHavingClause](../classes/OperationBinding.md#attr-operationbindingusehavingclause) for more details). The automatically generated `groupClause` and `groupWhereClause` clauses are also available as [$defaultGroupClause](../reference.md#type-defaultqueryclause) and [$defaultGroupWhereClause](../reference.md#type-defaultqueryclause) SQL templating variables. Note that if [OperationBinding.applyCriteriaBeforeAggregation](../classes/OperationBinding.md#attr-operationbindingapplycriteriabeforeaggregation) is set to `true`, `groupWhereClause` is not generated.

`SQLDataSource.getSQLClause()` server-side API can generate the entire query, in case you wanted to use an aggregated query as just part of a larger query (perhaps a sub-select), or different parts of a query, including `groupClause` and `groupWhereClause` aggregated query clauses.

Also note `SQLDataSource.getPartialHaving()` and `SQLDataSource.getHavingWithout()` server-side APIs which generate partial SQL condition expressions to be used as a complete or partial "having" or outer "where" clause. This is also can be accessed via `$sql.partialHaving` and `$sql.havingWithout` functions in SQL templates, see `$sql` variable description in [velocitySupport](velocitySupport.md#kb-topic-velocity-context-variables).

To see an example of wrapping the main query as a sub-select to achieve additional aggregation level and splitting provided criteria into different chunks of condition expressions to apply them to specific parts of a completely customized aggregation query, see the [Custom Aggregation Query](https://www.smartclient.com/smartclient-latest/showcase/?id=summariesCustomSQL2) sample.

#### Fields with customSelectExpression

Fields with [customSelectExpression](../classes/DataSourceField.md#attr-datasourcefieldcustomselectexpression) can be used with server summaries as both `groupBy` fields or fields with `summaryFunction`. In case of `summaryFunction` requested on field with `customSelectExpression` we will wrap SQL function around the expression, which may or may not be correct.

#### Summarizing without Grouping

Declaring just `<summaryFunctions>` without declaring `<groupBy>` is allowed. This will always give you exactly one summary record in the result, which will represent the summary functions as applied to all records that match the criteria in the DSRequest.

#### Grouping without Summarizing

Declaring just `<groupBy>` without `<summaryFunctions>` is also allowed. This gives results similar to a SQL "select distinct": one record per distinct set of values for the grouped fields. This kind of result can be used in various ways; one common use case is populating a ComboBoxItem with a list of existing values for a field that already appear in DataSource records.

Check out [this example](https://www.smartclient.com/smartclient-latest/showcase/?id=loadedValues) of grouping without summarizing being used to determine all unique values of a field.

#### Custom Aggregation

You can implement your own custom aggregation functions in addition to the built-in ones by providing custom DMI implementation for the "fetch" operation. To see the example of using custom function see [Custom Aggregation](https://www.smartclient.com/smartclient-latest/showcase/?id=summariesCustom) sample. Note, that in order to access custom summary function on the server-side you need to use `DSRequest.getRawSummaryFunctions()` API.

#### Extra fields in the [DSRequest.outputs](../classes/DSRequest.md#attr-dsrequestoutputs)

Aggregated data fetches cannot include additional fields that are not aggregated or grouped by. Therefore, if [DSRequest.outputs](../classes/DSRequest.md#attr-dsrequestoutputs) includes fields that are not part of the aggregation request, we apply the ${isc.DocUtils.linkForRef('type:SummaryFunction','\\'MIN\\' summary function')} to those fields to ensure they are fetched.

### Related

- [SummaryFunction](../reference.md#type-summaryfunction)
- [DSRequest.summaryFunctions](../classes/DSRequest.md#attr-dsrequestsummaryfunctions)
- [DSRequest.groupBy](../classes/DSRequest.md#attr-dsrequestgroupby)
- [OperationBinding.summaryFunctions](../classes/OperationBinding.md#attr-operationbindingsummaryfunctions)
- [OperationBinding.groupBy](../classes/OperationBinding.md#attr-operationbindinggroupby)
- [DataSourceField.includeSummaryFunction](../classes/DataSourceField.md#attr-datasourcefieldincludesummaryfunction)
- [DataSourceField.joinPrefix](../classes/DataSourceField.md#attr-datasourcefieldjoinprefix)
- [DataSourceField.joinString](../classes/DataSourceField.md#attr-datasourcefieldjoinstring)
- [DataSourceField.joinSuffix](../classes/DataSourceField.md#attr-datasourcefieldjoinsuffix)
- [DataSource.allowClientRequestedSummaries](../classes/DataSource.md#attr-datasourceallowclientrequestedsummaries)
- [DataSourceField.allowClientRequestedSummaries](../classes/DataSourceField.md#attr-datasourcefieldallowclientrequestedsummaries)
- [OperationBinding.groupWhereClause](../classes/OperationBinding.md#attr-operationbindinggroupwhereclause)

---
