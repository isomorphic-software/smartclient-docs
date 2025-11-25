# Integration with Spring

[← Back to API Index](../main.md)

---

## KB Topic: Integration with Spring

### Description
**Overview**

The Spring framework has many different parts, from integration with Object Relational Mapping (ORM) and transaction management systems, to a Model View Controller (MVC) architecture.

If you are building a new application from scratch and/or you are trying to modernize the presentation layer of an existing application, most of Spring MVC is inapplicable in the [SmartClient architecture](smartArchitecture.md#kb-topic-smartclient-architecture). Specifically, SmartClient renders **all** HTML on the client, and the server is responsible only for retrieving data and enforcing business rules. This means that Spring's ModelAndView and all functionality related to retrieving and rendering Views is unnecessary in SmartClient. SmartClient only needs the Model, and provides methods to deliver that Model to SmartClient components (the server side method DSResponse.setData()).

However, Spring's DispatchServlet, Handler chain, and Controller architecture is applicable to SmartClient. See "Using Spring Controllers" below.

**Existing Spring Application**

As discussed under the general [server integration](clientServerIntegration.md#kb-topic-client-server-integration) topic, integrating SmartClient into your application involves finding a way to provide data that fulfills the [DataSource requests](../main_2.md#object-dsrequest) sent by SmartClient components.

There are 2 approaches for integrating SmartClient into an existing Spring application:

*   **call Spring beans via SmartClient DMI or custom DataSources** \[Recommended\]: use SmartClient Direct Method Invocation (DMI) to map [DataSource requests](../main_2.md#object-dsrequest) to beans managed by Spring, via [ServerObject.lookupStyle](../classes/ServerObject.md#attr-serverobjectlookupstyle):"spring". Return data to the browser by either simply returning it from your method, or via creating a DSResponse and calling DSResponse.setData() (server-side method). Or, use a similar approach based on custom DataSource implementations where the [serverConstructor](../classes/DataSource.md#attr-datasourceserverconstructor) is of the pattern **"spring:{bean\_name}"**
    
    This is the easiest method and produces the best result. A Collection of Java Beans, such as EJB or Hibernate-managed beans, can be directly returned to SmartClient as the result of a DMI method, without the need to create an intervening [Data Transfer Object](http://en.wikipedia.org/wiki/Data_transfer_object) to express which fields should be delivered to the browser - instead, only the fields declared on the DataSource are returned to the browser (see [dropExtraFields](../classes/DataSource.md#attr-datasourcedropextrafields). In this integration scenario, the majority of the features of the SmartClient Server framework still apply - see this [overview](featuresCustomPersistence.md#kb-topic-server-features-and-custom-persistence).
    
    Note, there are special scoping considerations to bear in mind when using Spring-injected DataSources or DMIs - see [this discussion](serverDataSourceImplementation.md#kb-topic-notes-on-server-side-datasource-implementations) of caching and thread-safety issues.
    
*   **configure Spring to return XML or JSON responses**: create variants on existing Spring workflows that use a different type of View in order to output XML or JSON data instead of complete HTML pages. The SmartClient [RestDataSource](../classes/RestDataSource.md#class-restdatasource) provides a standard "REST" XML or JSON-based protocol you can implement, or you can adapt generic [DataSources](../classes/DataSource.md#class-datasource) to existing formats.
    
    In some Spring applications, all existing Spring workflows can be made callable by SmartClient with a generic View class capable of serializing the Model to XML or JSON, combined with a Controller that always uses this View. Consider the following Java anonymous class, which uses the SmartClient JSTranslater class to dump the entire Spring Model as a JSON response.
    
    ```
      new View() {
            public void render(Map model, HttpServletRequest request,
                               HttpServletResponse response) throws IOException {
                    final ServletOutputStream outputStream = response.getOutputStream();
                    response.setContentType("application/x-javascript");
                    outputStream.println(JSTranslater.get().toJS(model));
                    outputStream.close();
            }
            public String getContentType() {
                    return "application/x-javascript";
            }
      }
     
    ```
    
    If you use this approach, you do not need to install the SmartClient server, and can [deploy](iscInstall.md#kb-topic-installing-the-smartclient-runtime) SmartClient as simple web content (JS/media/HTML files). If you are already familiar with how to generate XML from objects that typically appear in your Spring Models, this may be the easiest path.
    

#### **Using Spring Controllers with SmartClient DMI**

You can create a Controller that invokes standard SmartClient server request processing, including DMI, like so:

```
 public class SmartClientRPCController extends AbstractController
 {
     public ModelAndView handleRequest(HttpServletRequest request, 
                                       HttpServletResponse response)
         throws Exception
     {
         // invoke SmartClient server standard request processing
         com.isomorphic.rpc.RPCManager.processRequest(request, response);
         return null; // avoid default rendering
     }
 }
 
```
This lets you use Spring's DispatchServlet, Handler chain and Controller architecture as a pre- and post-processing model wrapped around SmartClient DMI.

#### **Using Spring Transactions with SmartClient DMI**

You can make DMI's participate in Spring's transaction management scheme by setting the [useSpringTransaction](../classes/DataSource.md#attr-datasourceusespringtransaction) flag on your DataSources or [OperationBinding](../classes/OperationBinding.md#class-operationbinding)s. This makes your DMI method(s) transactional, and ensures that any DSRequests and Spring DAO operations executed within that DMI use the same Spring-managed transaction. See the documentation for `useSpringTransaction` for more details.

In Power Edition and above, SmartClient Server has its own transaction management system. This allows you to send [queues](../classes/RPCManager.md#classmethod-rpcmanagerstartqueue) of [DSRequest](../main_2.md#object-dsrequest)s to the server, and the entire queue will be treated as a single database transaction. This is **not** the same thing as Spring transaction integration: SmartClient's built-in transaction management works across an entire queue of DSRequests, whereas Spring transactions are specific to a Java method that has been marked `@Transactional` - the transaction starts and ends when the method starts and ends.

It is possible to have an entire SmartClient queue - including any `@Transactional` DMIs that contain both Spring DAO operations and DSRequests - use the same Spring-managed transaction. To do this:

*   Create a new Spring service bean with a `@Transactional` method like this (note, the isolation level can vary as you please, but the propagation type must be REQUIRED to enable proper sharing of the transaction):
    ```
        @Transactional(isolation=Isolation.READ_COMMITTED, propagation=Propagation.REQUIRED)
        public class MyServiceBean {
     
            // invoke SmartClient server standard request processing
            public void processQueue(RPCManager rpc) throws Exception {
                rpc.processRPCTransaction();
            }
        }
    ```
    
*   **Either:** Subclass the `com.isomorphic.servlet.IDACall` servlet and override its `processRPCTransaction` method to inject the service bean you just created and invoke its transactional method. You will also have to change your `web.xml` file to point at this new servlet rather than `IDACall`
*   **Or:** Use a Spring Controller, as described in the section **Using Spring Controllers with SmartClient DMI**, above. Just follow the instructions for using a Spring Controller, but have your `handleRequest()` implementation inject your service bean and invoke its transactional method, as described for the `IDACall` subclass approach

Whether you choose the IDACall or Spring Controller approach, the important thing is that the call to `RPCManager.processRPCTransaction()` takes place from within a `@Transactional` method of a Spring service bean. This will place the processing of the entire SmartClient queue inside the transaction that is created by Spring to service that transactional method.

#### **Using Spring DataSources with SmartClient SQLDataSource**

Smartclient [SQL DataSources](sqlDataSource.md#kb-topic-sql-datasources) may be configured to obtain JDBC connections from the `javax.sql.DataSource` implementation provided by Spring context. Search for `sql.MyDatabase.interface.type` in [SQL settings](sqlSettings.md#kb-topic-sql-database-settings-in-serverproperties) overview for the configuration details.

#### **Spring Compatibility**
[Spring](https://spring.io/projects/spring-framework#learn) & [Hibernate](https://hibernate.org/) have gone through reworks recently in which backwards compatibility was lost, creating complexity and difficult tradeoffs for consumers of these libraries, where there may be conflicting requirements to use different, incompatible versions of those frameworks. We have tried to do the best we can in terms of supporting many possible combinations of versions, where feasible.

The [Spring](https://spring.io/projects/spring-framework#learn) 5 framework integrated with SmartClient is only compatible with [Java](https://www.oracle.com/java/technologies/downloads/) 8+, so you can't use older version of Java together with ${isc.DocUtils.linkForRef('group:springIntegration','SmartClient\\'s built-in Spring support')}, such as the "spring:" DMI target. **If you have to use a Java version less than 8**, please see the "Using Java version less than 8" section at the end of this document.

#### Using Hibernate 3 or 4 with Spring 5

The [Spring](https://spring.io/projects/spring-framework#learn) 5 ships with [Hibernate](https://hibernate.org/) 5 support only, i.e. without built-in Hibernate 3 and 4 support it used to have.

SmartClient provides "bridges" that allow Spring 5 to be used with Hibernate 3 or 4. To use this combination, include either `isomorphic_spring_hibernate-core-6.5.3.Final.jar` for Hibernate 3 support or `isomorphic_spring_hibernate4.jar` for Hibernate 4 support.

Smartclient bridge classes are based on Spring 4.3.26 `org.springframework.orm.hibernate3` and `org.springframework.orm.hibernate4` packages and are placed in corresponding packages: `com.isomorphic.springhibernate3` and `com.isomorphic.springhibernate4`. So, for example, to configure managed Hibernate SessionFactory `**com.isomorphic.springhibernate3**.LocalSessionFactoryBean` class should be used instead of `org.springframework.orm.hibernate3.LocalSessionFactoryBean` class:

```
 <bean id="hbSpringSessionFactory"
       className="com.isomorphic.springhibernate3.LocalSessionFactoryBean">
     <property name="configLocation" value="classpath:hibernate.cfg.xml"/>
 </bean>
 
```
Other than that the usage is the same.
#### Using Hibernate 5
Hibernate 5 is not yet supported by Smartclient, but it still may be used via custom DataSource implementation, as is demonstrated in [ORM DataSource](https://www.smartclient.com/smartclient/showcase/?id=ormDataSource) and [Resusable ORM DataSource](https://www.smartclient.com/smartclient/showcase/?id=reusableORMDataSource) Showcase samples. Note that in this case Smartclient built-in Hibernate support would be lost and features like data pagination, server-side sorting and filtering, server summaries etc would also have to be implemented manually in custom DataSource if you need them.

#### Using Java version less than 8

With pre JDK8, you cannot use Spring 5 (according to [Spring docs](https://github.com/spring-projects/spring-framework/wiki/Upgrading-to-Spring-Framework-5.x#upgrading-to-version-50)), so, you have to remove all Spring 5 related jars. Then, you could use Spring 4 or earlier, but without any of our framework support for Spring which, as of release 13.0, requires Spring 5+ (older releases work with Spring 4).

To remove Spring from the SmartClient server all Spring JARs must be removed from your WEB-INF/lib server directory:

*   spring-aop-6.1.15.jar
*   spring-beans-6.1.15.jar
*   spring-context-6.1.15.jar
*   spring-context-support-5.3.9.jar
*   spring-core-6.1.15.jar
*   spring-expression-6.1.15.jar
*   spring-jdbc-6.1.15.jar
*   spring-orm-6.1.15.jar
*   spring-tx-6.1.15.jar
*   spring-web-6.1.15.jar
*   spring-webmvc-6.1.15.jar
*   isomorphic\_spring.jar
*   isomorphic\_spring\_hibernate-core-6.5.3.Final.jar
*   isomorphic\_spring\_hibernate4.jar

and Spring configuration must be removed from your WEB-INF/web.xml:

```
 <!-- standard spring configuration -->
 <context-param>
     <param-name>contextConfigLocation</param-name>
     <param-value>/WEB-INF/applicationContext.xml</param-value>
 </context-param>
 <listener>
     <listener-class>com.isomorphic.spring.ContextLoaderListener</listener-class>
 </listener>
```

---
