# SmartClient Server Summary

[← Back to API Index](../reference.md)

---

## KB Topic: SmartClient Server Summary

### Description
The SmartClient Server is a set of Java libraries, servlets and tools that provide the key server-side components needed to build a complete application in the modern web architecture.

The SmartClient Server can be [integrated](iscInstall.md#kb-topic-installing-the-smartclient-runtime) into any pre-existing Java application, and is designed to rapidly connect SmartClient visual components to pre-existing Java business logic or persistence engines. SmartClient's Ajax request processing facilities can be easily integrated into [Spring controllers](springIntegration.md#kb-topic-integration-with-spring) or custom servlets and JSPs.

Alternatively, the SmartClient Server provides a complete SQL and Hibernate-based persistence engine for new applications, with out-of-the-box servlets for processing Ajax data requests.

The SmartClient Server is optional, and SmartClient's client-side Ajax engine can be integrated with any server that provides HTTP access, using XML, JSON, SOAP or proprietary data protocols. However any server in a modern web application will be required to provide most or all of the features of the SmartClient Server (described below), and the SmartClient Server represents a best-of-breed implementation of these facilities with a long history of high-volume production deployments.

#### Server enforcement of [Validators](../classes/Validator.md#class-validator)

Data passed from the browser can be automatically validated by the SmartClient Server. In contrast, when using [client-side integration](clientDataIntegration.md#kb-topic-client-side-data-integration), data arrives as HTTP params or XML messages, and you must parse values into the correct types (eg java.util.Date) and validate them, or use a server framework that does so.

#### High Speed Data Delivery / Data Compression

The SmartClient Server delivers data to and from the browser using a proprietary, maximally efficient protocol, providing simple Java APIs for sending and receiving data.

SmartClient's data protocol is:

*   automatically compressed: provides 6-8x improvement in bandwidth utilization
*   efficient on the server: high speed data serialization for any Java Object
*   efficient in the browser: faster than ordinary XML or JSON data delivery
*   minimal: facilities for [trimming](../classes/DataSource.md#attr-datasourcedropextrafields) and [extracting](../classes/DataSourceField.md#attr-datasourcefieldvaluexpath) only the data you want the browser to see

#### Transparent upload support

SmartClient provides special client and server-side support for [file\\n upload](upload.md#kb-topic-uploading-files), which allows single and multiple-file HTTP uploads to be performed as a background Ajax request without reloading the page or launching sub-windows.

Uploaded files arrive at the SmartClient server as Java InputStreams accessible from the DSRequest object, and can optionally be automatically stored via SmartClient's SQL subsystem.

#### Transparent Queuing / "Batch" Operations

Any request transmitted to the SmartClient Server can be combined into a "queue" transmitted as a single HTTP request, with in-order execution for all queued operations. [startQueue()](../classes/RPCManager.md#classmethod-rpcmanagerstartqueue) starts a queue and [sendQueue()](../classes/RPCManager.md#classmethod-rpcmanagersendqueue) transmits it; queuing is transparent to the code that initiates the individual requests. This enables:

*   re-use of data access operations across different screens
*   easy implementation of transaction boundaries
*   simplified saving and loading of screens with complex, master-detail views
*   guaranteed in-order processing of operations
*   more efficient network usage

#### Reify

[Reify](reify.md#kb-topic-reify-overview) is included with the SmartClient Server, and uses server features such as automatic SQL binding to provide a rapid prototyping environment.

#### Automatic Bi-directional Java < - > JavaScript serialization and translation

Provides a powerful, type-safe [data transmission mechanism](../classes/RPCRequest.md#attr-rpcrequestdata) for moving data between a Java server and the browser.

Any Java objects, including Java Beans, POJOs, Java Collections, XML DOMs and all Java primitives, with any level of nesting, can be automatically serialized and delivered as JavaScript Objects to the SmartClient client-side components.

JavaScript Objects existing in the browser can likewise be automatically transmitted to a Java Server and translated to Java Objects, with any level of nesting and automatic preservation of primitive types.

#### SQL and Hibernate connectors

DataSources of serverType:"sql" or serverType:"hibernate" can generate and execute queries against popular SQL engines or against the Hibernate ORM system, providing SmartClient's [DataBoundComponent](../reference.md#interface-databoundcomponent)s with the four standard CRUD operations (create, retrieve, update, delete) without writing any server-side code. For rapid prototyping, these DataSources can even generate SQL tables based on the DataSource declaration, using the [Admin Console](adminConsole.md#kb-topic-admin-console) visual tool.

Server-side APIs allow server-side modification of the request before it is executed (for example, to enforce security) and post-processing of the request after execution (for example, to provide calculated values).

Both serverType:"sql" and serverType:"hibernate" support the field-operator-value queries that can be generated by using the [FilterBuilder](../classes/FilterBuilder.md#class-filterbuilder) component (see *example*).

#### Rich, Standardized Request / Response protocol

The SmartClient Server provides a standardized request and response protocol designed for data-oriented "CRUD" operations (create, retrieve, update, delete).

This standardized protocol automatically handles [request metadata](../reference.md#object-dsrequest) (paging parameters, requested sort order, original values of data being modified) and [response metadata](../classes/DSResponse.md#class-dsresponse) (error handling, cache management, session expiration etc).

This standardized protocol avoids developers in different groups inventing their own incompatible and redundant request/response protocols, and allows developers to more easily learn code they didn't author.

#### Bi-directional XPath binding to Java Objects

Most UI designs do not directly reflect the underlying Object model and so some degree of translation is necessary in order to populate UI components with data and apply user changes to the Java Object model. This is often accomplished with brittle, difficult to understand data translation code sprinkled throughout the system, done in a different way for every screen or component.

SmartClient provides a standard, [XPath-based approach](../classes/DataSourceField.md#attr-datasourcefieldvaluexpath) to adapting any Java-based Object model to the requirements of the UI design. Data relevant to the application UI is centrally extracted in the server-side [DataSource](../classes/DataSource.md#class-datasource) layer, so that all UI components have a consistent, unified view of the data model for both loading **and** saving data.

#### Broadest possible browser support

The SmartClient Server can compensate for facilities [missing or disabled in certain browsers](platformDependencies.md#kb-topic-platform-dependencies), including ActiveX being disabled in IE6 and missing XML support in some versions of Apple's Safari browser.

#### Transparent Proxying

[Proxying](../classes/RPCManager.md#classmethod-rpcmanagersendproxied) allows SmartClient applications to access web services, RSS feeds, HTML content and other data services in a secure manner regardless of where they are located: across the enterprise or publicly available.

#### Optional [Network Performance](networkPerformance.md#kb-topic-network-performance) Module

Provides:

*   compressed delivery of SmartClient runtime, application logic and other assets such as CSS
*   [background download](../reference_2.md#object-fileloader) of SmartClient and other assets for zero user-perceived load time
*   on-the-fly stripping and combining of JavaScript (application code and data)
*   browser cache control

#### Optional Messaging Module (aka server push)

The [Messaging](messaging.md#kb-topic-real-time-messaging) module allows the server to "push" messages to the client, without client polling, for real-time monitoring/dashboarding applications.

---
