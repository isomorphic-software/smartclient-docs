# Integration with Hibernate

[← Back to API Index](../reference.md)

---

## KB Topic: Integration with Hibernate

### Description
SmartClient integrates with Hibernate via DataSource descriptors (.ds.xml files) with [serverType="hibernate"](../classes/DataSource_1.md#attr-datasourceservertype). A JPA entity bean class is required, specified via [beanClassName](../classes/DataSource_1.md#attr-datasourcebeanclassname) or [schemaBean](../classes/DataSource_1.md#attr-datasourceschemabean) (which doubles as beanClassName when the latter is not set). SmartClient can automatically derive DataSource fields from the bean using [DataSource.autoDeriveSchema](../classes/DataSource_1.md#attr-datasourceautoderiveschema) — in this case the .ds.xml only needs to declare overrides for fields where the derived defaults are insufficient.

If you do not need Hibernate-specific features (named queries, Hibernate relations, Spring transaction integration), consider using [serverType="sql"](../classes/DataSource_1.md#attr-datasourceservertype) (SQLDataSource) instead. SQLDataSource requires no entity beans and provides equivalent CRUD, filtering, paging and export capabilities with simpler configuration.

Note that the [Admin Console](adminConsole.md#kb-topic-admin-console)'s "Import DataSources" section can be used to import test data into serverType:"hibernate" DataSources in the same manner as SQLDataSources.

HibernateDataSource supports operations with composite primary keys. Setting data source level property [idClassName](../classes/DataSource_1.md#attr-datasourceidclassname) to fully qualified class name indicates, that entity uses composite primary key.

#### Beans and the DSRequest / DSResponse

In case of "pre-existing beans" approach, see [hbBeans](hbBeans.md#kb-topic-beans-and-the-dsrequest--dsresponse) for the information how incoming DSRequest data is used and what to expect in DSResponse.

#### Hibernate relations

For Hibernate integration where Java beans have been explicitly declared, HibernateDataSource supports automatic handling of Hibernate relations that don't declare a concrete field to hold ID values - see [jpaHibernateRelations](jpaHibernateRelations.md#kb-topic-jpa--hibernate-relations).

#### Hibernate Configuration

You can provide Hibernate configuration to the SmartClient server in three ways:

*   You can place a traditional `hibernate.cfg.xml` file somewhere on the classpath
*   You can have SmartClient look up a Hibernate `Configuration` to use. This works in the same way as a [ServerObject](../reference_2.md#object-serverobject), and in fact makes use of the ServerObject code, though note that lookupStyle "attribute" is not supported. To look up a configuration, add ServerObject-compliant properties to your [server.properties](server_properties.md#kb-topic-serverproperties-file) file, prefixed with `hibernate.config`. For example:
    ```
            hibernate.config.lookupStyle: spring
            hibernate.config.bean: mySessionFactory
     
    ```
    
*   You can provide a Hibernate configuration at the level of individual DataSources, by specifying a [configBean](../classes/DataSource_1.md#attr-datasourceconfigbean) on the dataSource (this is only applicable if you are using Spring; see below)

If you choose to have SmartClient lookup the Hibernate configuration, and you specify a [lookupStyle](../classes/ServerObject.md#attr-serverobjectlookupstyle) of "spring", SmartClient will make use of a Hibernate `SessionFactory` configured by Spring. It is possible to set up multiple Hibernate configurations in Spring, and to map individual DataSources to different configurations by making use of the `dataSource.configBean` property mentioned above. Please note the following caveats:

*   DataSource-level Hibernate configuration is intended for unusual cases, such as when the physical data store for one DataSource is actually a different database. Hibernate relations between entities with different configurations do not work
*   A Spring-managed `SessionFactory` does not support adding entity mappings at runtime. All entity beans must be pre-registered in the Spring configuration (via annotated class scanning, `.cfg.xml` mappings referenced by the `configLocation` property, or Spring bean properties)

#### Inbound DSRequest data will use numeric field types from your bean

For fields with numeric types, the [record data](../classes/DSRequest.md#attr-dsrequestdata) in DSRequests will automatically be converted to the type of the target field, before the request is received in a [DMI](../classes/DMI.md#class-dmi). For details, see [dsRequestBeanTypes](dsRequestBeanTypes.md#kb-topic-dsrequest-data-auto-converted-to-bean-types).

#### Manual Hibernate Integration

In some cases you may not be able to immediately use the built-in HibernateDataSource - in this case take a look at [manual Hibernate integration](manualJpaHibernate.md#kb-topic-manual-jpa--hibernate-integration).

### See Also

- [DataSource.beanClassName](../classes/DataSource_1.md#attr-datasourcebeanclassname)
- [sqlConnectionPooling](sqlConnectionPooling.md#kb-topic-sql-connection-pooling)

---
