# Server-side REST Connector

[← Back to API Index](../reference.md)

---

## KB Topic: Server-side REST Connector

### Description
_**NOTE:** This article discusses SmartClient's server-side REST client implementation. It should not be confused with the client-side [RestDataSource](../classes/RestDataSource.md#class-restdatasource) implementation; the client-side dataSource is intended for cases where you are creating the server API and thus have control over the format and protocols used, but you do not wish to use the SmartClient Server for some reason. The server-side implementation, which is documented below, is intended for cases where you need to connect to existing third-party REST APIs (which, despite the impression that "REST" is a standardized approach, vary significantly from one to the other in their details)_

RestConnector is a built-in server-side [DataSource](../classes/DataSource.md#class-datasource) implementation. It is able to convert a standard client-submitted or server-created [DSRequest](../reference_2.md#object-dsrequest) into an arbitrary REST webservice call, and convert the REST service response into a standard [DSResponse](../classes/DSResponse.md#class-dsresponse). These conversions are highly configurable, making use of any or all of the following:

*   [Record-level](../classes/DataSource.md#attr-datasourcerecordxpath) and [field-level](../classes/DataSourceField.md#attr-datasourcefieldvaluexpath) XPath processing
*   [Velocity-based](velocitySupport.md#kb-topic-velocity-context-variables) templates providing powerful declarative data templating and conversion for both [requests](../classes/DataSource.md#attr-datasourcerequesttemplate) and [responses](../classes/DataSource.md#attr-datasourceresponsetemplate). These templates are evaluated at request/response execution time, so can include dynamic elements such as the criteria sent from the client
*   Where declarative conversion is not sufficient, inline scripts written in Groovy, Javascript or other JSR-223 languages can add conversion of arbitrary complexity. Again, we support scripts for converting both [requests](../classes/DataSource.md#attr-datasourcetransformrequestscript) and [responses](../classes/DataSource.md#attr-datasourcetransformresponsescript) at the record-level, and for response data at the [field-level](../classes/DataSourceField.md#attr-datasourcefieldfieldvaluescript)

#### Pervasive Velocity support
`RestController` was designed to be as flexible and configurable as possible. One of the ways we achieve this is with pervasive support for Velocity templating. In the descriptor (`*.ds.xml` file) of a RestController dataSource, you can use Velocity expressions in any element, and they will be replaced at execution time. This means that you can embed references to `server.properties` items, elements from the values and criteria of this operation, elements of other useful context objects, and arbitrary values that your code has set up in the Velocity template context (see the [Velocity overview](velocitySupport.md#kb-topic-velocity-context-variables) for details of these latter two). See the sample config below for examples of how this feature can be used. Additional examples are also shown in the docs of individual config properties ([headers](../classes/DataSource.md#attr-datasourceheaders), for example)

**Important:** Because we allow references to `$criteria` and `$values` in `RestConnector` config, it follows that we re-evaluate Velocity expressions on every `DSRequest`; in fact, as the following section discusses, when there are multiple valueSets, we evaluate Velocity expressions multiple times per `DSRequest`. However, we do **not** evaluate `$config` references per-`DSRequest`: `$config` references are evaluated during `DataSource` initialization, and are fixed thereafter. The main implication of this is, if you are pooling and reusing `DataSource` instances (which is the default), `$config` references will be fixed after initial evaluation for the life of the JVM, so you should not expect to be able to change a config setting and have it picked up in `RestConnector` Velocity templates.

#### Multiple ValueSets
`RestController` has a general ability to handle multiple valueSets, but only for REST services where both the [requestFormat](../classes/DataSource.md#attr-datasourcerequestformat) and the [responseFormat](../classes/DataSource.md#attr-datasourceresponseformat) are "json". For example, if we receive a [dsRequest](../reference_2.md#object-dsrequest) with two valueSets, like this:
```
    [
        {name:"Smith", ID:72},
        {name:"Jones", ID:1044}
    ]
 
```
We will combine those two records into a single JSON block to send to the remote REST server:
```
   [{"name":"Smith","ID": 72},{"name":"Jones","ID":1044}]
 
```
`RestConnector` is also able to wrap singular records in a list, for remote services that want to treat all input as a list - see [wrapInList](../classes/DataSource.md#attr-datasourcewrapinlist)

[Request templates](../classes/DataSource.md#attr-datasourcerequesttemplate) are also able to handle multiple valueSets. If there are multiple valueSets in the `DSRequest`, or if `wrapInList` is in force, we will apply each valueSet to the template, constructing a list of templated JSON blocks to send to the REST server.

#### Authentication
RestConnector provides the following standard authentication methods:

*   Basic Authorization with a username and password or API token
*   Bearer Authorization with an API token
*   Bearer Authorization with a refresh/access token scheme, such as JSON Web Tokens (JWT)
*   Manually-constructed Authorization header
*   Ad-hoc, informal auth schemes, like embedding an API token in the body of the request

The supported authentication methods are all secure as long as you are using HTTPS connections, but the refresh/access token approach adds an additional layer of security by using frequently-changed, short-lived tokens instead of credentials that remain valid for an extended period. For this reason, we recommend using that approach if you have the choice.

As noted, `RestConnector` is flexible enough that it is able to connect with REST APIs that use non-standard authentication techniques, such as embedding a token or username/password credentials in the request body. These non-standard authentication approaches are found more often than might be thought, and although they are non-standard, they are not any less secure than the standard approaches as long as you are using HTTPS.

See the [auth block](../classes/DataSource.md#attr-datasourceauth) documentation for full details.

#### Example configuration
RestConnector configuration is typically expressed in the [serverConfig](../classes/DataSource.md#attr-datasourceserverconfig) block of a DataSource descriptor (`.ds.xml` file) - the client has no need to know about this configuration, and generally should not be able to see it - although `serverConfig` is optional in nearly every cases; see the `serverConfig` documentation for details of this.

An example configuration is shown below.

```
   <DataSource
       ID="SomeRestDataSource"
       serverType="rest"
   >
     <serverConfig>
       <requestFormat>params</requestFormat>
       <responseFormat>json</responseFormat>
       <recordXPath>items</recordXPath>

       <!-- This is the default URL to send REST requests to, if not overridden at the 
               OperationBinding level.  Note, this MUST be declared inside the serverConfig
               block, otherwise client code in the browser will try to use it.  This example
               just uses plain, untemplated config but there are lots more options - see the
               operationBindings below -->
       <dataURL>https://somerestservice.com/api/search</dataURL>

       <auth>
         <type>basic</type>
         <username>$config['rest.somerestservice.apiUser']</username>
         <password>$config['rest.somerestservice.apiToken']</password>
       </auth>

       <operationBindings>
         <operationBinding operationType="fetch" operationId="customerFetch">
           <!-- You can use values defined in your server.properties file with the 
                   "$config" context variable -->
           <dataURL>$config['rest.somerestservice.baseURL']/customers</dataURL>
         </operationBinding>
       
         <operationBinding operationType="update" operationId="updateCustomer">
           <!-- And you can use values and criteria sent up from the client with "$values" 
                   and "$criteria" -->
           <dataURL>$config['rest.somerestservice.baseURL']/customer/$criteria['customerId']?name=$values['custName']</dataURL>
           <requestFormat>json</requestFormat>
         </operationBinding>
       
         <operationBinding operationType="remove">
           <!-- And you can use arbitrary values placed in the template context, as with 
                   "$deletePath" here --> 
           <dataURL>$config['rest.somerestservice.baseURL']/$deletePath/$values['itemKey']</dataURL>
         </operationBinding>
       </operationBindings>
     </serverConfig>
   </DataSource>
 
```

### Related

- [RESTRequestFormat](../reference.md#type-restrequestformat)
- [RESTResponseFormat](../reference.md#type-restresponseformat)
- [RESTAuthenticationType](../reference_2.md#type-restauthenticationtype)
- [RESTAuthentication](../reference.md#object-restauthentication)
- [DataSource.serverConfig](../classes/DataSource.md#attr-datasourceserverconfig)
- [DataSource.headers](../classes/DataSource.md#attr-datasourceheaders)
- [OperationBinding.headers](../classes/OperationBinding.md#attr-operationbindingheaders)
- [DataSource.params](../classes/DataSource.md#attr-datasourceparams)
- [OperationBinding.params](../classes/OperationBinding.md#attr-operationbindingparams)
- [DataSource.httpMethod](../classes/DataSource.md#attr-datasourcehttpmethod)
- [OperationBinding.httpMethod](../classes/OperationBinding.md#attr-operationbindinghttpmethod)
- [DataSource.requestFormat](../classes/DataSource.md#attr-datasourcerequestformat)
- [OperationBinding.requestFormat](../classes/OperationBinding.md#attr-operationbindingrequestformat)
- [DataSource.responseFormat](../classes/DataSource.md#attr-datasourceresponseformat)
- [OperationBinding.responseFormat](../classes/OperationBinding.md#attr-operationbindingresponseformat)
- [DataSource.wrapInList](../classes/DataSource.md#attr-datasourcewrapinlist)
- [OperationBinding.wrapInList](../classes/OperationBinding.md#attr-operationbindingwrapinlist)
- [DataSource.xmlTag](../classes/DataSource.md#attr-datasourcexmltag)
- [OperationBinding.xmlTag](../classes/OperationBinding.md#attr-operationbindingxmltag)
- [DataSource.csvDelimiter](../classes/DataSource.md#attr-datasourcecsvdelimiter)
- [OperationBinding.csvDelimiter](../classes/OperationBinding.md#attr-operationbindingcsvdelimiter)
- [DataSource.csvQuoteCharacter](../classes/DataSource.md#attr-datasourcecsvquotecharacter)
- [OperationBinding.csvQuoteCharacter](../classes/OperationBinding.md#attr-operationbindingcsvquotecharacter)
- [DataSource.suppressAutoMappings](../classes/DataSource.md#attr-datasourcesuppressautomappings)
- [OperationBinding.suppressAutoMappings](../classes/OperationBinding.md#attr-operationbindingsuppressautomappings)
- [DataSource.requestTemplate](../classes/DataSource.md#attr-datasourcerequesttemplate)
- [OperationBinding.requestTemplate](../classes/OperationBinding.md#attr-operationbindingrequesttemplate)
- [DataSource.responseTemplate](../classes/DataSource.md#attr-datasourceresponsetemplate)
- [OperationBinding.responseTemplate](../classes/OperationBinding.md#attr-operationbindingresponsetemplate)
- [DataSource.requiresCompleteRESTResponse](../classes/DataSource.md#attr-datasourcerequirescompleterestresponse)
- [OperationBinding.requiresCompleteRESTResponse](../classes/OperationBinding.md#attr-operationbindingrequirescompleterestresponse)
- [DataSource.auth](../classes/DataSource.md#attr-datasourceauth)
- [RESTAuthentication.type](../classes/RESTAuthentication.md#attr-restauthenticationtype)
- [RESTAuthentication.username](../classes/RESTAuthentication.md#attr-restauthenticationusername)
- [RESTAuthentication.password](../classes/RESTAuthentication.md#attr-restauthenticationpassword)
- [RESTAuthentication.authToken](../classes/RESTAuthentication.md#attr-restauthenticationauthtoken)
- [RESTAuthentication.authHeader](../classes/RESTAuthentication.md#attr-restauthenticationauthheader)
- [RESTAuthentication.dataSource](../classes/RESTAuthentication.md#attr-restauthenticationdatasource)

---
