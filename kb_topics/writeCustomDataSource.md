# Custom Server DataSources

[← Back to API Index](../main.md)

---

## KB Topic: Custom Server DataSources

### Description
Out of the box, and with no code to write, SmartClient supports SQL, JPA and Hibernate for persistence, which includes EJB 3.0, EclipseLink and other Java persistence systems accessible via JPA. For other Java-based persistence systems, such as legacy EJBs or systems proprietary to your company, you write a custom DataSource class in Java. In most cases, it is possible to write a single, generic DataSource class that provides access to all data that is a available from a given persistence mechanism; for example, a single DataSource class can typically be written for accessing all data accessible via legacy EJB.

Note that a majority of the features of the SmartClient Server framework apply even when using your own persistence mechanism. As with the features supported by SmartClient's browser-based visual components, SmartClient's server-side features rely only on the concept of a DataSource and not on the details of the ultimate persistence mechanism. Hence they are usable with a custom DataSource regardless of the final data provider.

We provide a complete working example of a custom DataSource in the SmartClient Feature Explorer; you can see it in action *here*. This example "ormDataSource" is an adaptor for Hibernate which supports the 4 CRUD operations, data paging, server-side sort and filter, and which participates correctly in [cache synchronization](../classes/ResultSet.md#class-resultset). The code required is minimal, and the approaches taken generalize to any ORM system. Studying the Java source code for this DataSource - which is available in the "ORMDataSource.java" tab in the example linked to above - is the best way to get a start on implementing your own custom DataSource.

*   `ORMDataSource` extends `BasicDataSource`.
*   `ORMDataSource` is primarily an implementation of four key methods: `executeFetch`, `executeAdd`, `executeUpdate` and `executeRemove`. All the logic related to the actual CRUD data operation takes place in one of these methods. This is the recommended approach.
*   The class also implements the `execute` method. This is an override of the method that is actually called by the framework, and as such is an appropriate place to set up shared objects that will be used in more than one CRUD operation, and to perform shared pre- and post-processing. As you can see, the example is setting up a Hibernate session and transaction, and then calling `super.execute` - this calls back into the framework and ultimately leads to the appropriate data operation method being called.
*   Note how each of the `executeXxx` methods conforms to the [DataSource protocol](dataSourceOperations.md#kb-topic-datasource-operations). To take `executeFetch` as an example, note how it:
    
    *   Retrieves the criteria for the fetch from the supplied `DSRequest`
    *   Implements logic to obey the `startRow`, `endRow` and `batchSize` values. This is only necessary for a DataSource that intends to support automatic data paging.
    *   Retrieves `sortByFields` from the supplied `DSrequest`, and uses that value to change the order of the resultset. This is only necessary for a DataSource that intends to support server-side sorting.
    *   Populates `startRow`, `endRow` and `totalRows` on the `DSResponse`.
    *   Populates the `DSResponse`'s `data` member with the list of objects retrieved by the Hibernate call.
    
      
    These are the only parts of this method that are of significance as far as SmartClient is concerned - the rest of the method is concerned with communicating with the data provider, which is of no interest to SmartClient as long as the method conforms to the DataSource protocol for a "fetch" operation.

  
**The DataSource descriptor**

Once your custom DataSource is implemented, you need to to create a descriptor for each instance of the DataSource. As noted above, it is generally possible to write one custom DataSource class that is capable of handling all data access for a particular persistence mechanism. DataSource descriptors, on the other hand, are written per entity.

A DataSource descriptor is an XML file with the special suffix `.ds.xml`. The descriptor for a custom DataSource is, for the most part, identical to the descriptor for a built-in DataSource: it is the central place where you describe the DataSource instance to the system - its fields, validations, security constraints, special data operations, transaction chaining expressions and so on (see the [DataSource docs](../classes/DataSource.md#class-datasource) for full details).

One property that is always required for a custom DataSource is [serverConstructor](../classes/DataSource.md#attr-datasourceserverconstructor). This fully-qualified class name tells SmartClient what to instantiate when data operations for this DataSource arrive on the server - in other words, it is how you tell SmartClient to use your custom class. In the *ORM DataSource example*, on the `ormDataSource_country` tab, you will see how we use this property to tie the `ormDataSource_country` DataSource _instance_ to the `ormDataSource` DataSource _implementation_.

Finally, if your data model is based on Javabeans, or on POJOs that broadly follow the Javabean conventions (basically, if they have private state variables accessible via public getters and setters), SmartClient can automatically generate basic DataSource definitions for your beans that will only need minimal change (ie, specifying a `serverConstructor`) to be fully operational. Both the *Reify Javabean Wizard* and the Batch DataSource Generator can create DataSource descriptors from existing beans.

**Server framework features relevant to custom DataSources**

The vast majority of the SmartClient Server framework's key features are not specific to the built-in SQL and Hibernate connectors, and still apply even when using a custom persistence mechanism. See [this overview](featuresCustomPersistence.md#kb-topic-server-features-and-custom-persistence) of which features apply when using a custom persistence mechanism and how best to leverage those features.

---
