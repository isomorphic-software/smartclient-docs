# .NET, PHP, Serverless Integration

[← Back to API Index](../reference.md)

---

## KB Topic: .NET, PHP, Serverless Integration

### Description
While SmartClient's extensive server features are lost if you cannot install the Java-based server framework, SmartClient UI components can be integrated with any server technology. This topic provides pointers to documentation that is most relevant for this type of integration.

#### Installation

As described in [_Deploying SmartClient_](iscInstall.md#kb-topic-installing-the-smartclient-runtime), for a client-only integration, installation consists of just copying a directory of JavaScript and media files to your webserver.

#### Creating Components

SmartClient components can be included in any .html page, including dynamically generated pages produced by .php or .asp files. The standard SmartClient libraries can be included in the page as follows, and [optional modules](loadingOptionalModules.md#kb-topic-loading-optional-modules) can be loaded in the same way:

```
 <HTML><HEAD>
 <SCRIPT>var isomorphicDir="../isomorphic/";</SCRIPT>
 <SCRIPT SRC=../isomorphic/system/modules/ISC_Core.js></SCRIPT>
 <SCRIPT SRC=../isomorphic/system/modules/ISC_Foundation.js></SCRIPT>
 <SCRIPT SRC=../isomorphic/system/modules/ISC_Containers.js></SCRIPT>
 <SCRIPT SRC=../isomorphic/system/modules/ISC_Grids.js></SCRIPT>
 <SCRIPT SRC=../isomorphic/system/modules/ISC_Forms.js></SCRIPT>
 <SCRIPT SRC=../isomorphic/system/modules/ISC_RichTextEditor.js></SCRIPT>
 <SCRIPT SRC=../isomorphic/system/modules/ISC_Drawing.js></SCRIPT>
 <SCRIPT SRC=../isomorphic/system/modules/ISC_DataBinding.js></SCRIPT>
 <SCRIPT SRC=../isomorphic/system/modules/ISC_Calendar.js></SCRIPT>
 <SCRIPT SRC=../isomorphic/skins/SmartClient/load_skin.js></SCRIPT>
 </HEAD><BODY>
 ...
```
SmartClient components can then be created via normal JavaScript:
```
 <SCRIPT>
 isc.Button.create({
     title:"Button",
     click:"isc.say('Hello World')"
 });
 </SCRIPT>
 
```
This approach is discussed in more detail in the [QuickStart Guide](/smartclient-release/docs/SmartClient_Quick_Start_Guide.pdf), Chapter 4, _Coding_. Note that JavaScript-based component instantiation is currently the recommended approach, and most examples are provided in the JavaScript format.

#### Data Loading / Data Binding

The primary focus of SmartClient integration is connecting DataSource operations to your server. The [Client-side Data Integration](clientDataIntegration.md#kb-topic-client-side-data-integration) chapter covers the key approaches, including cookbook approaches for REST-based integration with any server that can return XML or JSON over HTTP.

#### Simple RPCs (non-DataSource requests)

You can implement simple RPCs by having your server output [JSON](http://www.json.org/) (JavaScript Object Notation) and using [RPCRequest.evalResult](../classes/RPCRequest.md#attr-rpcrequestevalresult) to directly turn JSON results into live JavaScript objects. [RPCRequest.serverOutputAsString](../classes/RPCRequest.md#attr-rpcrequestserveroutputasstring) lets you load arbitrary server results, including JSON results that need to be processed before they can be eval()'d.

Alternatively, if you are familiar with WSDL web services, you can implement simple RPCs as web service operations: use [XMLTools.loadWSDL](../classes/XMLTools.md#classmethod-xmltoolsloadwsdl) to load the service definition, and then use [WebService.callOperation](../classes/WebService.md#method-webservicecalloperation) to call the operations. We don't generally recommend this approach unless you are already deeply familiar with WSDL - it's far more complicated that producing and consuming JSON.

#### HTTPProxy: Cross-site or cross-port data loading

If you develop a prototype using the SmartClient SDK and SmartClient Java Server, and then you migrate the prototype to another server technology, you need to be aware that the SmartClient Java Server includes an HTTPProxy servlet that allows SmartClient interfaces to contact servers other than the origin server (bypassing what is called the ["same origin policy"](http://www.google.com/search?q=same+origin+policy)).

SmartClient uses the HttpProxy automatically when needed, so it may not be obvious that the HTTPProxy is in use. Then, your migrated application will encounter errors attempting to contact the HTTPProxy servlet.

To avoid these errors, ensure that all services that your application uses are accessed using the same hostname and port as the page was loaded from. In particular, watch for WSDL files, which contain the service URL - you may need to use [WebService.setLocation](../classes/WebService.md#method-webservicesetlocation) to ensure that the web service URL and page URL match.

If your production application really does need to access services or content hosted on other servers, typical practice is to pursue normal SmartClient integration with your server, then write server-side code that contacts other hosts on behalf of your SmartClient interface.

---
