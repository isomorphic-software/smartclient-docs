# Integration with JPA

[← Back to API Index](../reference.md)

---

## KB Topic: Integration with JPA

### Description
To use JPA, set serverType="jpa" in your .ds.xml file, then set [beanClassName](../classes/DataSource.md#attr-datasourcebeanclassname) to the fully qualified class name of the JPA entity. For example:
```
 <DataSource
     ID="countryDS"
     serverType="jpa"
     beanClassName="com.smartgwt.sample.showcase.server.jpa.Country"
 >
     <fields>
 <!-- ... Fields definition ... -->
     </fields>
 </DataSource>
 
```
[DataSource.autoDeriveSchema](../classes/DataSource.md#attr-datasourceautoderiveschema) is supported for deriving DataSource fields from JPA entities automatically (except with JPA 1.0; see below).

Full support is provided for executing simple [Criteria](../reference_2.md#type-criteria), with [AdvancedCriteria](../reference.md#object-advancedcriteria) supported if you have Power Edition or above. However, note that there are limitations with case sensitive search in MySQL since MySQL automatically uses the 'like' operator in a case-insensitive manner and JPA does not correct this. See [MySQL Reference Manual :: C.5.5.1 Case Sensitivity in String Searches](http://dev.mysql.com/doc/refman/5.5/en/case-sensitivity.html) for more information.

If create a custom DataSource based on the built-in JPA functionality, subclass `com.isomorphic.jpa.JPA2DataSource`.

#### Beans and the DSRequest / DSResponse

In case of "pre-existing beans" approach, see [hbBeans](hbBeans.md#kb-topic-beans-and-the-dsrequest--dsresponse) for the information how incoming DSRequest data is used and what to expect in DSResponse.

#### JPA relations

For JPA integration where Java beans have been explicitly declared, JPADataSource supports automatic handling of JPA relations that don't declare a concrete field to hold ID values - see [jpaHibernateRelations](jpaHibernateRelations.md#kb-topic-jpa--hibernate-relations).

#### JPA configuration

JPA configuration should be specified in the `persistence.xml` file as usual, and placed in the `/WEB-INF/classes/META-INF` directory. For JPA 2.0 make sure you correctly declare its usage in `persistence.xml`:

```
 <persistence
     version="2.0"
     xmlns="http://java.sun.com/xml/ns/persistence"
     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xsi:schemaLocation="http://java.sun.com/xml/ns/persistence 
                         http://java.sun.com/xml/ns/persistence/persistence_2_0.xsd"
 >
 ...
 </persistence>
```
  

JPADataSource supports operations with composite primary keys. Setting data source level property [idClassName](../classes/DataSource.md#attr-datasourceidclassname) to fully qualified class name indicates, that entity uses composite primary key.

JPADataSource supports automatic handling of JPA relations that don't declare a concrete field to hold ID values - see [jpaHibernateRelations](jpaHibernateRelations.md#kb-topic-jpa--hibernate-relations).

#### JPA 1.0 compatibility

To use JPA 1.0, set serverType="jpa1" instead. JPA 1.0 does not support [DataSource.autoDeriveSchema](../classes/DataSource.md#attr-datasourceautoderiveschema). For JPA 1.0, the concrete implementation class (for subclassing to create a custom DataSource) is `com.isomorphic.jpa.JPADataSource`.

#### JPA transactions

JPA provides three mechanisms for transactions: for JEE applications JPA provides integration with JTA (Bean Managed Transactions and Container Managed Transactions); for JSE applications JPA has a native `EntityTransaction` implementation (Locally Managed Transactions). Spring framework is another popular way for declaring transactions in application. The transaction mechanism should be configured in the [server.properties](server_properties.md#kb-topic-serverproperties-file) file by setting property **`jpa.emfProvider`** to the fully qualified class name of the provider (implementation of `com.isomorphic.jpa.EMFProviderInterface`). SmartClient comes with five implementations:

*   **`com.isomorphic.jpa.EMFProviderLMT`** - for Locally Managed Transactions. Every fetch or DML operation starts a new transaction and commits after successful execution.  
    This implementation reads the **`jpa.persistenceUnitName`** property from the [server.properties](server_properties.md#kb-topic-serverproperties-file) file. The value of this property needs to be set to the name of the persistence unit configured in `persistence.xml` file. For example:
    ```
     jpa.persistenceUnitName: PERSISTENCE_UNIT_NAME
          
    ```
    
*   **`com.isomorphic.jpa.EMFProviderBMT`** - for Bean Managed Transactions. Every fetch or DML operation acquires the transaction object from the container and starts it.  
    This implementation reads two properties from the [server.properties](server_properties.md#kb-topic-serverproperties-file) file: **`jpa.entityManager`** and **`jpa.entityManagerFactory`** containing appropriate resource name references configured in `/WEB-INF/web.xml`. Configuration example:
    ```
     <!-- EntityManager resource reference name declaration -->
     <persistence-context-ref>
        <persistence-context-ref-name>persistence/em</persistence-context-ref-name>
        <persistence-unit-name>PERSISTENCE_UNIT_NAME</persistence-unit-name>
     </persistence-context-ref>
    
     <!-- EntityManagerFactory resource reference name declaration -->
      <persistence-unit-ref>
          <persistence-unit-ref-name>persistence/emf</persistence-unit-ref-name>
          <persistence-unit-name>PERSISTENCE_UNIT_NAME</persistence-unit-name>
      </persistence-unit-ref>
    
     #Property values for sample references:
     jpa.entityManager: persistence/em
     jpa.entityManagerFactory: persistence/emf
          
    ```
    
*   **`com.isomorphic.jpa.EMFProviderCMT`** - for Container Managed Transactions. Every fetch or DML operation acquires the transaction object from the JEE container. After successful method execution the container commits the transaction. In case of execution failure `tx.setRollbackOnly()` is used to notify container to rollback the transaction.  
    This implementation reads two properties from the [server.properties](server_properties.md#kb-topic-serverproperties-file) file: **`jpa.entityManager`** and **`jpa.entityManagerFactory`** containing appropriate resource name references configured in `/META-INF/ejb-jar.xml`. Configuration example:
    ```
     <?xml version="1.0" encoding="UTF-8"?>
     <ejb-jar
          version = "3.0"
          xmlns = "http://java.sun.com/xml/ns/javaee"
          xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation = "http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/ejb-jar_3_0.xsd">
          <enterprise-beans>
              <session>
                  <ejb-name>TestEJB</ejb-name>
                  <persistence-context-ref>
                      <persistence-context-ref-name>persistence/em</persistence-context-ref-name>
                      <persistence-unit-name>PERSISTENCE_UNIT_NAME</persistence-unit-name>
                  </persistence-context-ref>
                  <persistence-unit-ref>
                      <persistence-unit-ref-name>persistence/emf</persistence-unit-ref-name>
                      <persistence-unit-name>PERSISTENCE_UNIT_NAME</persistence-unit-name>
                  </persistence-unit-ref>
             </session>
         </enterprise-beans>
     </ejb-jar>
    
     #Property values for sample references:
     jpa.entityManager: persistence/em
     jpa.entityManagerFactory: persistence/emf
          
    ```
    
*   **`com.isomorphic.jpa.EMFProviderNoTransactions`** - transactions are not used.  
    From the [server.properties](server_properties.md#kb-topic-serverproperties-file) file this implementation reads the **`jpa.persistenceUnitName`** property which must containt the name of persistence unit configured in `persistence.xml` file. For example:
    ```
     jpa.persistenceUnitName: PERSISTENCE_UNIT_NAME
          
    ```
    
*   **`com.isomorphic.jpa.EMFProviderSpring`** - for Spring Framework managed Transactions. Every fetch or DML operation acquires the transaction object from the Spring Application Context.  
    This implementation reads two properties from the [server.properties](server_properties.md#kb-topic-serverproperties-file) file: **`jpa.entityManagerFactory`** and **`jpa.transaction`** containing appropriate bean names configured in Spring Application Context. You have to declare additional bean in your Spring Application Context to allow SmartClient to acquire reference to context. Configuration example:
    ```
     <!-- SpringApplicationContextProvider bean definition required to get access to application context. -->
     <bean id="springApplicationContextProvider" class="com.isomorphic.spring.SpringApplicationContextProvider" />
    
     <!-- Connection to data base -->
     <bean id="dataSource"
          class="org.springframework.jdbc.datasource.DriverManagerDataSource"
          p:driverClassName="DRIVER_CLASS"
          p:url="CONNECTION_URL"
          p:username="DB_USER_NAME"
          p:password="DB_USER_PASSWORD" />
    
     <!-- Reference to JPA EntityManagerFactory -->
     <bean id="entityManagerFactory" class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
         <property name="dataSource" ref="dataSource" />
         <property name="jpaVendorAdapter">
            <bean class="org.springframework.orm.jpa.vendor.HibernateJpaVendorAdapter">
                <property name="database" value="DB_TYPE" />
            </bean>
         </property>
         <property name="persistenceUnitName" value="PERSISTENCE_UNIT_NAME" />
     </bean>
    
     <!-- Reference to JpaTransactionManager -->
     <bean id="transactionManager" class="org.springframework.orm.jpa.JpaTransactionManager">
         <property name="entityManagerFactory" ref="entityManagerFactory" />
     </bean>
    
     #Property values for sample bean names:
     jpa.entityManagerFactory: entityManagerFactory
     jpa.transaction: transactionManager
          
    ```
    

You can set **`jpa.emfProvider`** to your own implementation of `com.isomorphic.jpa.EMFProviderInterface` if you have specific requirements for transaction handling. `EMF` will instantiate provided implementation on initialization (static) and will use same instance every time. By using own implementation you can have complete control over creating/using `EntityManagerFactory` and `EntityManager` instances.

**Additional configurations:**

In case you have several persistence units defined in your `persistence.xml` you can have additional configurations in [server.properties](server_properties.md#kb-topic-serverproperties-file) file. Additional configurations (prefixed with **`jpa.`**) should have name, **`emfProvider`** property and other properties required by specified EMF provider implementation. For example:

```
 jpa.configName.emfProvider: com.isomorphic.jpa.EMFProviderLMT
 jpa.configName.persistenceUnitName: ANOTHER_PERSISTENCE_UNIT_NAME
```
To use additional JPA configuration you have to set **`jpaConfig`** property in data source definition:
```
 <DataSource
     ID="countryDS"
     serverType="jpa"
     beanClassName="com.smartgwt.sample.showcase.server.jpa.Country"
     jpaConfig="configName"
 >
```
**Transaction management:**

*   Operating under [RPCManager](../classes/RPCManager.md#class-rpcmanager) (`[DSRequest](../reference_2.md#object-dsrequest)` has reference to `[RPCManager](../classes/RPCManager.md#class-rpcmanager)`):
    
    *   If participating in automatic transactions:
        *   retrieves existing transaction from `[RPCManager](../classes/RPCManager.md#class-rpcmanager)` (if available);
        *   starts new transaction (if not found in `[RPCManager](../classes/RPCManager.md#class-rpcmanager)`);
    *   If one transaction per operation is used - starts new transaction;
    *   Registers itself to `DSRequest.registerCallback()` for `onSuccess()`/ `onFailure()` execution to commit/roll back transaction;
    *   Sets `DSRequest.setFreeOnExecute()` to `false` to postpone releasing of `EntityManager` avoiding lazy loading exceptions when creating JS response and traversing through persistent object tree;
    *   Registers itself to `RPCManager.registerFreeResourcesHandler()` for `freeResources()` execution to release `EntityManager`.
    
      
    If you want to use same `EntityManager` and transaction in your custom data source implementation you can acquire it by
    ```
    JPAConnectionHolder holder = DataSource.getTransactionObject(req, EMF.TRANSACTION_ATTR);
    ```
    `JPAConnectionHolder` instance contains references to entity manager and transaction object used by `JPADataSource`. You should never commit/rollback automatic transaction. Overall commit/rollback will be issued by `RPCManager` and will be handled by `JPADataSource` object which started transaction.
*   Operating without [RPCManager](../classes/RPCManager.md#class-rpcmanager):
    *   starts new transaction;
    *   commits/rolls back transaction and releases `EntityManager` if `DSRequest.setFreeOnExecute()` is set to `true` (defalut);
    *   relies on calling code to call `onSuccess()`/`onFailure()` to commit/roll back transaction and to call `freeResources()` to release `EntityManager`.  
        Example code for data source operation execution with manual transaction handling:
        ```
                      DSRequest req = new DSRequest("myDS", "fetch");
                      req.setFreeOnExecute(false);
                      DSResponse resp = req.execute();
                      List dataList = resp.getDataList();
                      //... traverse through persistent object tree
                      // Commit current transaction.
                      ((JPADataSource) r.getDataSource()).onSuccess();
                      // Release entity manager.
                      ((JPADataSource) r.getDataSource()).freeResources(req);
                  
        ```
        

#### Inbound DSRequest data will use numeric field types from your bean

For fields with numeric types, the [record data](../classes/DSRequest.md#attr-dsrequestdata) in DSRequests will automatically be converted to the type of the target field, before the request is received in a [DMI](../classes/DMI.md#class-dmi). For details, see [dsRequestBeanTypes](dsRequestBeanTypes.md#kb-topic-dsrequest-data-auto-converted-to-bean-types).

#### Manual JPA Integration

In some cases you may not be able to immediately use the built-in JPADataSource - in this case take a look at [manual Hibernate integration](manualJpaHibernate.md#kb-topic-manual-jpa--hibernate-integration).

### See Also

- [sqlConnectionPooling](sqlConnectionPooling.md#kb-topic-sql-connection-pooling)

---
