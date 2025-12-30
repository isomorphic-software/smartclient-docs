# Server Features and Custom Persistence

[← Back to API Index](../reference.md)

---

## KB Topic: Server Features and Custom Persistence

### Description
The vast majority of the SmartClient Server framework's key features are not specific to the built-in SQL and Hibernate connectors, and still apply even when using a custom persistence mechanism.

See the listing below of major features and how to apply them with custom persistence:

**Server Data Binding:** Using the SmartClient Server framework means that the starting point for connecting to custom persistence logic is a clean Java API. SmartClient provides Java `DSRequest` and `DSResponse` objects with all of the methods necessary to handle data paging, sorting, validation error reporting, and other features. In most cases, you can fulfill a DSResponse by simply returning one of your Java business objects rather than worrying about how to encode objects to XML or JSON. Communication with the browser is automatically handled with an efficient, compressed protocol. *Custom DataSource example*, *DMI example*

**Data Selection (No DTOs):** When using a DataSource, Java data you return in your `DSResponse` is automatically trimmed to just the fields declared in the DataSource before delivery to the browser (see [dropExtraFields](../classes/DataSource.md#attr-datasourcedropextrafields)). This eliminates the need to create redundant [Data Transfer Objects](http://en.wikipedia.org/wiki/Data_transfer_object) to express the list of fields that need to be delivered to the UI - the DataSource already has this information, and can serve two purposes by both configuring UI components and trimming relevant data, from a single definition.

Furthermore, DataSources can extract specific fields from complex nested object graphs via XPath expressions, for both loading and saving of data. *XPath Binding example*

**Server Validation:** Both client and server validation are driven from declarations in a single DataSource definition. You already have a need to declare validators to drive SmartClient's client-side validation; when you use the SmartClient Server framework you get automatic server-side enforcement of the same validation rules, without the need to write any additional code. *Server Validation example*

**Queuing:** Queuing allows multiple data load or save requests from different UI components to be transparently combined into a single HTTP request with guaranteed in-order execution. The type of DataSource handling each request is not important, so queuing will work with your custom DataSource; in fact, a single queue could contain operations to be handled by many different types of DataSource. *Queuing examples*

**Declarative security:** The server framework provides robust authentication and authorization integration, to allow you to secure both DataSource operations (data fetch and update requests) and individual DataSource fields at various granularities. The declarative security rules are expressed directly in the `.ds.xml` file, and allow you declare rules as simple as "all operations on this DataSource require an authenticated user", or as complex as "a user can only update this field if he has role 'admin' and a call to the `isAuthorized()` method on a security checking object we have stored in the `HttpSession` returns true". Security rules are applied by the framework before and after a DSRequest is executed, so they are applied even to operations on completely custom DataSources. See [OperationBinding.requiresRole](../classes/OperationBinding.md#attr-operationbindingrequiresrole) and the properties it links to for more details on operation-level security, and [DataSourceField.viewRequiresAuthentication](../classes/DataSourceField.md#attr-datasourcefieldviewrequiresauthentication) and the properties it links to for more details on field-level security.

**Transaction Chaining:** allows one request in a queue of operations to incorporate values from previously executed requests in the same queue. This allows a series of dependent operations - such as fetching a value from one DataSource to be used in a query on another - to be defined with simple declarations right in the DataSource definition, with no need to write a custom Java class to manually pass data between the different operations. Since Transaction Chaining works strictly in terms of DataSource requests and responses and knows nothing about the underlying persistence mechanism, it works with any persistence strategy. See the [Transaction Chaining overview](transactionChaining.md#kb-topic-transaction-chaining).

**Java / JS Reflection:** Any Java object can be delivered to the browser as a JavaScript object, and vice versa. As a developer of a custom DataSource, you do not need to concern yourself with dealing with translations to and from JSON or XML; you work directly with native Java objects. For example, a method you write to fulfill a "fetch" operation can simply return a `Collection` of Java beans; the SmartClient Server framework would transparently handle converting this into a matching Javascript structure. *Saving nested objects example*

**Visual Builder:** The DataSource Wizards in Visual Builder are pluggable; we provide wizards for SQL and Hibernate DataSources, and it is easy to write a new wizard to integrate your custom DataSource into Visual Builder. *SQL Wizard screenshots*, *Hibernate Wizard screenshots*

**Batch DataSource Generator:** If the persistence scheme you are implementing your custom DataSource for is based on collections of Javabeans, the Batch DataSource Generator can generate DataSource definition files for instances of your custom DataSource. This is out of the box behavior, but you can also alter and extend the DataSource Generator to suit your exact needs - we supply the source and it has been specifically designed to be easy to modify.

**Batch Uploader:** A user interface for end-to-end batch upload of data as a pre-built, customizable component. This component - like any SmartClient databound component - only cares that a DataSource is a DataSource, so custom DataSources will work just like built-in ones. *Batch Uploader example*

**File Upload:** Single and multiple file uploads can be handled as a normal DataSource operation, including normal handling of validation errors. Optional automatic storage to SQL (no server code required) means you can upload to SQL tables for holding files, which can be related to Java Objects by id (eg, a User's uploaded files). *File Upload example*

**Export:** Allows any grid component to export its current dataset in CSV, XML or JSON format. This feature works by issuing the DataSource with an ordinary "fetch", and then changing the `DSResponse` to send back an import file rather than a resultset. Accordingly, this just works with custom DataSources. *Export example*

**HTTP Proxy:** The HTTP Proxy allows an application to access web services hosted on remote servers which are not normally accessible to web applications due to the ["same origin policy"](http://www.google.com/search?q=same+origin+policy)). This is a general feature of the SmartClient Server framework that does not directly apply to DataSources. *HTTP Proxy example*

**Lightweight Persistence / Reporting:** Even while using a custom DataSource to connect to a custom ORM system, you can still make use of the SQL DataSource for simple storage-only entities where an object-based representation is a waste of time. You can also do this for reporting scenarios that don't correspond to the object model.

---
