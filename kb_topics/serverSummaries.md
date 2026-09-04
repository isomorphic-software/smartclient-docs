# Server Summaries

[← Back to API Index](../reference.md)

---

## KB Topic: Server Summaries

### Description
In SmartClient, "summarization" refers to applying functions to DataSource fields to obtain _summary records_ calculated from the values of multiple DataSource records.

For example, by applying an "average" function to a DataSourceField representing the dollar value of an order, you can calculate the average dollar amount of a set of orders.

Client-side calculation of summary records is a [listGrid feature](../classes/ListGrid_1.md#attr-listgridshowgridsummary). Server Summaries is a feature of the SmartClient Server allowing similar summaries to be computed server-side, generally by the database engine itself.

See also the related feature which allows a single field to receive a value summarized from several related records, [DataSourceField.includeSummaryFunction](../classes/DataSourceField.md#attr-datasourcefieldincludesummaryfunction).

**The Server Summaries feature is available with Power or better licenses only.** See [smartclient.com/product](http://smartclient.com/product) for details.

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

#### Criteria, Sort & Data Paging

Criteria and sort directions are supported for queries that involve server summarization.

Criteria apply to record **before** summaries are applied. For example, if the "avg" function is being applied to a "price" field, criteria like "price < 5" will eliminate records where price is less than 5 _before_ the average price is calculated. This means that client-side filtering may not work as expected with summarized results: client-side filter criteria are necessarily applied _after_ summary functions have been applied, so may not match the server's behavior. You can set [ResultSet.useClientFiltering](../classes/ResultSet.md#attr-resultsetuseclientfiltering) to disable client-side filtering on a grid via [ListGrid.dataProperties](../classes/ListGrid_1.md#attr-listgriddataproperties). Or individual fields can be marked [canFilter:false](../classes/ListGridField.md#attr-listgridfieldcanfilter).

Sort directions may only target fields that are returned by the query (only those fields included in `groupBy` or where a `summaryFunction` was applied).

Data paging is also supported, however, consider that for aggregated queries, when asked for a second page of data, the database is likely to have to repeat all the work of calculating aggregated values. Turning paging off or setting a generous [ListGrid.dataPageSize](../classes/ListGrid_1.md#attr-listgriddatapagesize) is advised.

#### SQL Templating

[SQL Templating](#kb-topic-customquerying) is also supported with server summaries. Clause-by-clause substitution works normally.

#### Fields with customSelectExpression

Fields with [customSelectExpression](#attr-datasourcefieldcustomselectexpression) can be used with server summaries as both `groupBy` fields or fields with `summaryFunction`. In case of `summaryFunction` requested on field with `customSelectExpression` we will wrap SQL function around the expression, which may or may not be correct.

#### Summarizing without Grouping

Declaring just `<summaryFunctions>` without declaring `<groupBy>` is allowed. This will always give you exactly one summary record in the result, which will represent the summary functions as applied to all records that match the criteria in the DSRequest.

#### Grouping without Summarizing

Declaring just `<groupBy>` without `<summaryFunctions>` is also allowed. This gives results similar to a SQL "select distinct": one record per distinct set of values for the grouped fields. This kind of result can be used in various ways; one common use case is populating a ComboBoxItem with a list of existing values for a field that already appear in DataSource records.

Check out [this example](https://www.smartclient.com/smartclient-latest/showcase/?id=loadedValues) of grouping without summarizing being used to determine all unique values of a field.

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

---
