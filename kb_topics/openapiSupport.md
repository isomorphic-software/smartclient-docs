# OpenAPI Specification (OAS) Support

[← Back to API Index](../reference.md)

---

## KB Topic: OpenAPI Specification (OAS) Support

### Description
If you allow access to your server-side DataSources via the [RESTHandler servlet](servletDetails.md#kb-topic-the-core-and-optional-smartclient-servlets), the SmartClient server can also generate a standard [OpenAPI specification](https://github.com/OAI/OpenAPI-Specification) of the REST interface supported by `RestHandler`. This allows any client system that supports OpenAPI to access the operations supported by your DataSources. Because details like [field types](../reference_2.md#type-fieldtype) and [validators](../classes/Validator.md#class-validator)) are automatically translated to OpenAPI, the OpenAPI specification (OAS) of your DataSource operations is much more specific and detailed than the general [RestDataSource](../classes/RestDataSource.md#class-restdatasource) protocol spec, and can allow automatically generated UIs or automatically generated communication stubs to be much richer and easier to use.

Very often, a reasonably simple DataSource expresses more than can be easily translated to the current OpenAPI specification. In such cases, efforts are made to use the OpenAPI [extensions](https://swagger.io/docs/specification/openapi-extensions/) mechanism to provide that level of detail. Validators are one common area of interest. It is worthwhile to inspect the raw YAML output at least once before relying solely on visual tooling, unless said tooling supports vendor extensions. [ReDoc](https://github.com/Redocly/redoc), for example, is able to render the generated spec well, and in fact powers the example specification (see link below), but leaves out important details found in the extensions, like the RESTHandler's JSON [prefix](../classes/RestDataSource.md#attr-restdatasourcejsonprefix) and [suffix](../classes/RestDataSource.md#attr-restdatasourcejsonsuffix).

#### Tooling
The generated specification makes extensive use of [remote references](https://swagger.io/docs/specification/using-ref/) to make the spec more readable without tooling. Unfortunately, a number of popular tools do not yet support the use of this OAS feature. Postman, for example, has at least one [issue](https://github.com/postmanlabs/openapi-to-postman/issues/38) that you can watch for progress. In the meantime, we've found that the hosted [Swagger](http://editor.swagger.io/) tools seem to work well, if you make allowances for [Cross-Origin Resource Sharing](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS). One very simple way of doing so with Swagger Editor, for example, is to enable a CORS filter (perhaps temporarily) like the one provided by [Jetty](https://www.eclipse.org/jetty/javadoc/jetty-9/org/eclipse/jetty/servlets/CrossOriginFilter.html):
```
     <filter>
         <filter-name>cross-origin</filter-name>
         <filter-class>org.eclipse.jetty.servlets.CrossOriginFilter</filter-class>
     </filter>
     <filter-mapping>
         <filter-name>cross-origin</filter-name>
         <url-pattern>/restapi/*</url-pattern>
     </filter-mapping>
 
```
allowing the Swagger Editor to access the YAML generated for you by SmartClient, through the use of its `url` query parameter. e.g., [http://editor.swagger.io/?url=http://localhost:8080/api/Customer.yaml](http://editor.swagger.io/?url=http://localhost:8080/api/Customer.yaml)
#### Usage
Configure the RESTHandler endpoint as usual (refer to server [javadoc](server/javadoc/com/isomorphic/servlet/RESTHandler.html) for details), and submit a GET request there for the `openapi.yaml` resource. For example, if your servlet is configured to respond to requests at `/restapi`
```
   <servlet-mapping>
       <servlet-name>RESTHandler</servlet-name>
       <url-pattern>/restapi/</url-pattern>
   </servlet-mapping>
 
```
then a GET request to `/restapi/openapi.yaml` will yield the automatically generated documentation, based on your application's DataSource (ds.xml) configurations. This specification is generated dynamically, so that each new request for the specification includes any changes made to new or updated DataSources since the last request. Alternatively, save the file to disk, with modifications if desired, and serve it statically from another location if that's more in line with your requirement.
#### Structure
By design, `openapi.yaml` by default includes a reference to every path exposed by every DataSource.ds.xml file found in your project. The paths exposed by your DataSource are determined by the rules documented in the ${isc.DocUtils.linkForRef('group:servletDetails','RESTHandler servlet\\'s')} SimplifiedREST protocol. For an Order DataSource with only default operationBindings, these references would look something like the following:
```
 paths:
   /:
     post:
       summary: DataSource-agnostic POSTMessage protocol
       # and so on... remainder clipped for brevity

   /RESTDataSource/Order/fetch:
     $ref: Order.yaml#/paths/~1RESTDataSource~1Order~1fetch
   /RESTDataSource/Order/add:
     $ref: Order.yaml#/paths/~1RESTDataSource~1Order~1add
   /RESTDataSource/Order/update:
     $ref: Order.yaml#/paths/~1RESTDataSource~1Order~1update
   /RESTDataSource/Order/remove:
     $ref: Order.yaml#/paths/~1RESTDataSource~1Order~1remove
   /RESTDataSource/Order/batch:
     $ref: Order.yaml#/paths/~1RESTDataSource~1Order~1batch
   /Order:
     $ref: Order.yaml#/paths/~1Order
   /Order/{orderId}:
     $ref: Order.yaml#/paths/~1Order~1%7BorderId%7D
 
```
The first path in the above listing documents RESTHandler's singular AdvancedREST endpoint, described by the ${isc.DocUtils.linkForRef('class:RestDataSource','RESTDataSource\\'s')} postMessage protocol and found in our example configuration at `/restapi/`. As documented elsewhere, this should normally be the endpoint preferred by all but the simplest of integrations.

On the other hand, it is also the endpoint most difficult to document effectively, due in part to a handful of restrictions found in the OAS 3.x specification. One such restriction is documented in an open issue around [request/response correlation](https://github.com/OAI/OpenAPI-Specification/issues/2031), which in short points out that there is no good way to correlate a variation of some request to the matching variation on the response. In the case of the AdvancedREST endpoint, of course, request and response formats both depend entirely on the values provided in `dataSource`, `operationType`, and `operationId` arguments. Ideally, we could document the inputs and outputs of a resource like `/restapi/?dataSource=Order&operationType=fetch&operationId=fetchByCustomer` separately from one like `/restapi/?dataSource=Order&operationType=fetch&operationId=fetchByUser`, but this is expressly [disallowed](https://swagger.io/docs/specification/paths-and-operations/).

In the absence of any spec-compliant mechanism like [supporting interdependencies between query parameters](https://github.com/OAI/OpenAPI-Specification/issues/256#issuecomment-583476857) then, we also provide simplified variations of the AdvancedREST endpoint on each DataSource's specification, seen alongside the other SimplifiedREST endpoints with the `RESTDataSource` path. These 'SimplifiedPOST' endpoints do allow for Criteria & AdvancedCriteria, as well as batching of multiple operations against the same DataSource.

You can easily view all of the operations for a single DataSource by making the request to `{id}.yaml` instead of openapi.yaml, where `{id}` is the ID of any DataSource in your project. Building on the examples above, a request for `/restapi/Order.yaml`would include every path except '/'. Again, prefer the RestHandler's AdvancedREST endpoint to SimplifiedREST, with the caveat that SimplifiedREST documentation my be more explicit until a future version of the OAS spec addresses some of the issues discussed here.

A full example specification is too lengthy to include in documentation, so it is left to the reader to experiment with their own DataSources (sample DataSources are included with the SDK and in [Maven archetypes](mavenSupport.md#kb-topic-maven-support) or with the example specification bundled in the SDK (link below), using this documentation as guidance. Most of what is generated for you can be pretty easily traced back to your DataSource - [description](../classes/DataSource.md#attr-datasourcedescription), field names, required/optional attributes, and type mappings are all pretty straightforward, and the rest of it really should work the way you might expect it to. A few specific examples include:

*   A field's valueMaps are expressed as an enum and appended to the [description](../classes/DataSourceField.md#attr-datasourcefielddescription), complete with [i18n translations](dataSourceLocalization.md#kb-topic-datasource-and-component-xml-localization) as applicable, when a locale can be derived from the servlet request or is specified explicitly with a 'locale' query parameter (e.g., ?locale=es).
*   A note about authorization constraints is also appended, when any [Declarative Security](../classes/DataSource.md#attr-datasourcerequiresauthentication) rules are found (rules themselves are not disclosed, by design).
*   Any operationBinding with an explicit operationId is exposed on its own path, where its binding-specific [criteria](../classes/OperationBinding.md#attr-operationbindingcriteria), [description](../classes/OperationBinding.md#attr-operationbindingdescription), [outputs](../classes/OperationBinding.md#attr-operationbindingoutputs), etc. are respected.

Note that multiple operations of the same operationType are supported. The example below illustrates the same DataSource with multiple add operations:

##### DataSource

```
 <DataSource serverType="sql" schema="PUBLIC" dbName="ClassicModels"
   ID="Order"
   tableName="orders">

   <serverObject className="com.example.classicmodels.OrderOperations" />

   <fields>
     <field name="orderNumber" type="sequence" primaryKey="true" />
     <field name="orderDate" type="date" required="true" />
     <field name="requiredDate" type="date" required="true" />
     <field name="shippedDate" type="date" />
     <field name="status" type="enum" length="15" required="true">
       <valueMap>
         <value>In Process</value>
         <value>Shipped</value>
         <value>Cancelled</value>
         <value>Disputed</value>
         <value>Resolved</value>
         <value>On Hold</value>
       </valueMap>
     </field>
     <field name="comments" type="text" length="16777216" />
     <field name="customerNumber" title="Customer" type="integer" required="true"
          foreignKey="Customer.customerNumber"
          displayField="customerName" />
     <field name="customerName" includeFrom="Customer.customerName" hidden="true" />
   </fields>
   <operationBindings>
     <binding operationType="add" operationId="addWithDiscountCode" serverMethod="addWithDiscountCode" />
     <binding operationType="add" operationId="addWithManualAdjustment" serverMethod="addWithManualAdjustment" />
   </operationBindings>
 </DataSource>
 
```

##### Paths

```
   /Order:
     $ref: Order.yaml#/paths/~1Order
   /Order/{orderId}:
     $ref: Order.yaml#/paths/~1Order~1%7BorderId%7D
   /Order/add/addWithDiscountCode:
     $ref: Order.yaml#/paths/~1Order~1add~1addWithDiscountCode
   /Order/add/addWithManualAdjustment:
     $ref: Order.yaml#/paths/~1Order~1add~1addWithManualAdjustment
 
```
#### Customization
A complete specification will normally require at least some content that cannot be derived, so most users will at minimum want to replace default values for things like application title, description, and version number attributes.

The simplest means for this kind of minimal customization is through [server.properties](server_properties.md#kb-topic-serverproperties-file) configuration. Example values for supported properties include:

```
   openapi.info.version: 1.0.0
   openapi.info.title: New Application
   openapi.info.description: A short description of New Application

   ## default value derived from servlet context & httpRequest
   openapi.servers.servletUrl: http://localhost:8080/restapi
 
```
You may also use configuration to control which DataSources are exposed to your specification. Three strategies are supported:

*   Exclusion: Set an 'apidoc' attribute value to false on any DataSource definition to exclude it from the list of documented DataSource operations.
    ```
    <DataSource ID="Order" tableName="orders" apidoc="false">
    ```
    
*   Blacklisting: Exclude a (comma-separated) list of DataSources through server.properties configuration:
    ```
    openapi.ds.blacklisted: Order, OrderDetail
    ```
    
*   Whitelisting: Exclude everything **but** a (comma-separated) list of DataSources, also through server.properties configuration:
    ```
    openapi.ds.whitelisted: Order, OrderDetail
    ```
    

No matter which strategy you use, [Dynamic DataSources](server/javadoc/com/isomorphic/datasource/DynamicDSGenerator.html) must always be allowed explicitly, and are added to the list after whitelisting / blacklisting rules are applied. Your DynamicDSGenerator must be able to resolve the given names, which may be supplied either through server.properties configuration or via an HttpServletRequest attribute, usually set by a filter that intercepts requests for the RESTHandler servlet. The mechanism you use will depend on your requirement - DynamicDSGenerators registered using a simple [prefix](server/javadoc/com/isomorphic/datasource/DataSource.html#addDynamicDSGenerator-com.isomorphic.datasource.DynamicDSGenerator-java.lang.String-) may be easily configured using the former, while those registered using [patterns](server/javadoc/com/isomorphic/datasource/DataSource.html#addDynamicDSGenerator-com.isomorphic.datasource.DynamicDSGenerator-java.util.regex.Pattern) may need to be a little more dynamic, and better suited to the latter approach. The following are examples of both approaches, which work equally well:
```
openapi.ds.dynamics: DYN_Environment, DYN_Status
```
```
request.setAttribute("openapi.ds.dynamics", "DynamicOrder$Foo_0123, DynamicOrderItem$Foo_0123,");
```
Finally, a DataSource is automatically excluded from the specification under the following circumstances:

*   It is marked with serverOnly="true"
*   It is marked with requires="false"
*   It is marked with its type="component"
*   It has no fields (and inherits no fields)

Similarly, an explicitly defined operationBinding may also be excluded from the specification, if one or more of the following conditions are true:

*   It is configured for exclusion with an 'apidoc' attribute value of false.
    ```
    <binding apidoc="false" operationType="add" operationId="addWithDiscountCode" serverMethod="addWithDiscountCode" />
    ```
    
*   The operationType is 'update' or 'remove' and (neither of these are common scenarios):
    *   No primaryKeys have been defined AND the binding is not configured to [allowMultiUpdate](../classes/OperationBinding.md#attr-operationbindingallowmultiupdate)
    *   OR there are no non-key fields at all

For very advanced customizations, a handful of [Freemarker](https://freemarker.apache.org/) templates are bundled with the server runtime, and can be found in the `com.isomorphic.openapi` package of the isomorphic-core-rpc module. Any of these templates may be overridden by placing a copy in a location known to the RESTHandler servlet (again, refer to server javadoc), but this kind of thing should normally be considered the last course of action.

#### FAQ
As always, the SmartClient [forums](https://forums.smartclient.com/) are an appropriate place to seek guidance in unusual circumstances.
#### Examples

*   [Example OpenAPI Specification](../../../docs/resources/openapi.html)

---
