# Integration with Hibernate

[← Back to API Index](../reference.md)

---

## KB Topic: Integration with Hibernate

### Description
SmartClient can integrate with Hibernate in two main ways, both of which are enabled by creating a DataSource descriptor (.ds.xml file) with [serverType="hibernate"](../classes/DataSource.md#attr-datasourceservertype):

*   Pre-existing beans: a SmartClient DataSource can be automatically derived from either a Hibernate-managed bean or the Hibernate mapping. Use [schemaBean](../classes/DataSource.md#attr-datasourceschemabean) to derive from the bean or [DataSource.autoDeriveSchema](../classes/DataSource.md#attr-datasourceautoderiveschema) to derive from the mapping. In this case you will initially have a very short .ds.xml per bean - no `<fields>` are required unless and until you want to override the automatically derived fields.
*   "Beanless" mode: SmartClient can drive Hibernate as a storage layer only, automatically generating Hibernate configuration from a SmartClient DataSource file (_dataSourceID_.ds.xml). In this case, you do not write a Java bean or create Hibernate mappings; Hibernate's beanless ["dynamic model"](http://docs.jboss.org/hibernate/orm/3.3/reference/en-US/html/persistent-classes.html#persistent-classes-dynamicmodels) mode is used.

Which mode to use is primarily a matter of preference and pre-existing code. However, if you do not have pre-existing code or other special circumstances, the following approach is the most productive:

1.  use "beanless" mode, specifying fields in SmartClient's .ds.xml format (far more compact than a Java bean with a getter and setter for each field)
2.  add business logic as needed via DMI, Server Scripting, custom server validators, and other approaches covered in the QuickStart Guide
3.  call any reusable DMI methods both via your SmartClient UI and via other, non-UI related Java logic (the DMI methods are now a reusable "data services tier")
4.  only create an actual Java bean if you discover re-usable, bean-specific business logic that cannot be encapsulated as a data service (rare)

Note that the [Admin Console](adminConsole.md#kb-topic-admin-console)'s "Import DataSources" section can be used to import test data into serverType:"hibernate" DataSources in the same manner as SQLDataSources.

HibernateDataSource supports operations with composite primary keys. Setting data source level property [idClassName](../classes/DataSource.md#attr-datasourceidclassname) to fully qualified class name indicates, that entity uses composite primary key.

#### Beans and the DSRequest / DSResponse

In case of "pre-existing beans" approach, see [hbBeans](hbBeans.md#kb-topic-beans-and-the-dsrequest--dsresponse) for the information how incoming DSRequest data is used and what to expect in DSResponse.

#### Hibernate relations

For Hibernate integration where Java beans have been explicitly declared, HibernateDataSource supports automatic handling of Hibernate relations that don't declare a concrete field to hold ID values - see [jpaHibernateRelations](jpaHibernateRelations.md#kb-topic-jpa--hibernate-relations).

#### Hibernate Configuration

You can provide Hibernate configuration to the SmartClient server in three ways:

*   You can place a traditional `hibernate.cfg.xml` file somewhere on the classpath
*   You can have SmartClient look up a Hibernate `Configuration` to use. This works in the same way as a [ServerObject](../reference_2.md#object-serverobject), and in fact makes use of the ServerObject code, though note that lookupStyle "attribute" is not supported. To look up a configuration, add ServerObject-compliant properties to your [server.properties](../reference.md#kb-topic-serverproperties-file) file, prefixed with `hibernate.config`. For example:
    ```
            hibernate.config.lookupStyle: spring
            hibernate.config.bean: mySessionFactory
     
    ```
    
*   You can provide a Hibernate configuration at the level of individual DataSources, by specifying a [configBean](../classes/DataSource.md#attr-datasourceconfigbean) on the dataSource (this is only applicable if you are using Spring; see below)

If you choose to have SmartClient lookup the Hibernate configuration, and you specify a [lookupStyle](../classes/ServerObject.md#attr-serverobjectlookupstyle) of "spring", SmartClient will make use of a Hibernate `SessionFactory` configured by Spring. It is possible to set up multiple Hibernate configurations in Spring, and to map individual DataSources to different configurations by making use of the `dataSource.configBean` property mentioned above. Please note the following caveats:

*   DataSource-level Hibernate configuration is intended for unusual cases, such as when the physical data store for one DataSource is actually a different database. Hibernate relations between entities with different configurations do not work
*   If you choose to configure Hibernate via Spring, "beanless" on-the-fly mappings are not supported; all entities must be hand-mapped to a bean, either in the properties of the Spring bean providing the configuration, in a `.cfg.xml` file named in the Spring bean's `configLocation` property, or by use of persistence annotations in the actual mapped beans themselves

#### Inbound DSRequest data will use numeric field types from your bean

For fields with numeric types, the [record data](../classes/DSRequest.md#attr-dsrequestdata) in DSRequests will automatically be converted to the type of the target field, before the request is received in a [DMI](../classes/DMI.md#class-dmi). For details, see [dsRequestBeanTypes](dsRequestBeanTypes.md#kb-topic-dsrequest-data-auto-converted-to-bean-types).

#### Manual Hibernate Integration

In some cases you may not be able to immediately use the built-in HibernateDataSource - in this case take a look at [manual Hibernate integration](manualJpaHibernate.md#kb-topic-manual-jpa--hibernate-integration).

### See Also

- [DataSource.beanClassName](../classes/DataSource.md#attr-datasourcebeanclassname)
- [sqlConnectionPooling](sqlConnectionPooling.md#kb-topic-sql-connection-pooling)

---
