# Union DataSources

[← Back to API Index](../reference.md)

---

## KB Topic: Union DataSources

### Description
The UnionDataSource assimilates records from multiple member dataSources, matching fields by name and data type, or by explicit configuration. Different types of member dataSource are allowed, so you can union SQL data with Hibernate data and generic data from a legacy system, for example. For efficiency, SmartClient will use the SQL UNION keyword to achieve the data union for any members dataSources that are [SQL DataSource](sqlDataSource.md#kb-topic-sql-datasources)s; data from any non-SQL members is combined in Java code as a post-process.

Like other dataSource types, unionDataSources can filter, sort and page their bonded data sets, and other dataSource features like [declarative security](../classes/DataSourceField.md#attr-datasourcefieldviewrequires) and [included fields](../classes/DataSourceField.md#attr-datasourcefieldincludefrom) work as you would expect. However, [Server Summaries](serverSummaries.md#kb-topic-server-summaries) and grouping do not currently work with UnionDS.

**Example usage**  
UnionDataSource is useful when you need a unified view of data entities that, for whatever reason, you ordinarily keep separate. A plausible example is Customers and Suppliers; those are two distinct entities, and would typically be implmented as separate database tables or Hibernate persistent classes, or whatever. This makes sense: there are lots of things you want to know about a Customer that are not relevant for a Supplier, and vice versa. In most ways, these are not similar things.

However, from a Customs point of view, Customers and Suppliers _are_ similar - they are both Trading Partners. As mentioned above, you probably store lots of things about Customers that you don't store about Suppliers and vice versa, but there will be a set of fields common to both - name, address, country, and financial details like total amount sold or purchased this year. You can use UnionDataSource to provide a "Trading Partners" view of this data.

**Configuration**  
If your member dataSources are very similar, unionDataSource can work in an auto-config mode where all you specify is the list of member dataSource in the unionDataSource's [unionOf](../classes/DataSource.md#attr-datasourceunionof) property, and we derive a set of common fields amongst the members where the names and data types match (there is flexibility in this auto-derivation process - see [defaultUnionFieldsStrategy](../classes/DataSource.md#attr-datasourcedefaultunionfieldsstrategy)). You can trim this by specifying the list of fields you want to union (again, assuming they have the same name in each member dataSource) using the [unionFields](../classes/DataSource.md#attr-datasourceunionfields) property. You can also refine the auto-derived configuration by specifying field definitions in the unionDataSource, using field-level [unionOf](../classes/DataSourceField.md#attr-datasourcefieldunionof) definitions to explicitly declare which member fields should be unioned. You can also use unionDataSource field definitions to optionally rename the unioned field, and do more mundane things, like change the title. Eg,

```
    <field name="tradingPartnerId" unionOf="customerDS.custId,vendorDS.vendorCode" title="Partner ID"/>
 
```
**Performance note**  
Ordering and paging with a UnionDataSource only makes sense when applied to the bonded dataset; in order to ensure that we can sort and page the overall dataset correctly, we must fetch every matching record from each member dataSource. For this reason, you should not rely on the paging feature to keep the number of records in the working dataset small; always provide criteria for that purpose. This is a good practice, and one we recommend for any type of dataSource, but it is particularly important with unionDataSource, to avoid situations where we have to fetch thousands or millions of rows from multiple member dataSources, in order to find out which of those rows are in positions 100 to 150 with the current sort settings.

### Related

- [DataSource.unionOf](../classes/DataSource.md#attr-datasourceunionof)
- [DataSource.unionFields](../classes/DataSource.md#attr-datasourceunionfields)
- [DataSource.defaultUnionFieldsStrategy](../classes/DataSource.md#attr-datasourcedefaultunionfieldsstrategy)
- [OperationBinding.unionFields](../classes/OperationBinding.md#attr-operationbindingunionfields)
- [DataSourceField.unionOf](../classes/DataSourceField.md#attr-datasourcefieldunionof)

---
