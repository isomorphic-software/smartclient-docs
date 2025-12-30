# The Core and Optional SmartClient servlets

[← Back to API Index](../reference.md)

---

## KB Topic: The Core and Optional SmartClient servlets

### Description
The following is a description of the servlets and filters you'll find in the web.xml file contained in the smartclientRuntime and what they do:

_Core Functionality_

*   Init servlet - see the article on [SmartClient Server Initialization](serverInit.md#kb-topic-server-framework-initialization)
*   IDACall servlet - **required** for [DMI](dmiOverview.md#kb-topic-direct-method-invocation), built-in RPC operations and built-in DataSource operations to work. All databound examples in the SDK use this servlet. If you're planning on using a custom actionURL for all your RPC requests, then you don't need this servlet.
*   FileDownload servlet - required for serving the Isomorphic framework code compressed and with caching headers as well as for serving skin images with caching headers. It is highly recommended that you use this for production but is not required.
*   PreCache servlet - loads resources into memory on container startup. Not required, but if you exclude this servlet there may be a slow response to the very first request.
*   jsp-config section - the iscTaglib registration block is required to use `<isomorphic>` tags, and the \*.isc and \*.rpc mappings. These are optional, if you want to use these as handy development tools.

_Optional Functionality_

*   RESTHandler servlet - handles SmartClient Server DataSource operations issued by REST clients: it's like IDACall, but for the REST protocol. Typically, the clients of this servlet would not be ordinary SmartClient/SmartGWT applications (though they could be), but other client technologies that need to access SmartClient DataSource operations as reusable services. If you do not plan to connect to the server using the REST protocol, then you don't need this servlet.
*   AxisServlet - exposes all DataSource operations via a WSDL service described by SmartClientOperations.wsdl. This is effectively the same as the RESTHandler servlet, but for SOAP clients. If you do not plan to connect to the server using webservice protocols, then you don't need this servlet.
*   HttpProxy - used by the RPCManager when sending AJAX RPCs to a server other than the server that serves the main application page. You need to install this servlet if, for example, your application will be querying web services exposed by servers other than the server that is serving the rest of the application. See the javadoc for this servlet for various configuration options, such as how to restrict the URLs that are allowed to be proxied.
*   MessagingServlet - used by the realtime messaging system. If you're planning on using this subsystem, you'll need this servlet.
*   CompressionFilter - required if you want to use dynamic compression of html and js files.
*   JSSyntaxScannerFilter - development tool that looks for trailing commas in JS source (scans html files for `<script>` tags and scans .js files in their entirety). This is a useful development tool, but should not be included in production.
*   NoCacheFilter - development tool that makes any content it intercepts non-cacheable in order to ensure developers are looking at the latest version of a file when modifying examples. Not for production use.
*   DataSourceLoader - a servlet that returns the definition of one or more DataSources in JavaScript notation. This servlet is provided as an alternative to using the `<isomorphic:loadDS>` JSP tag, and is particularly suitable in environments where JSP tags can't be used for some reason (such as with SmartGWT). See [Creating DataSources](dataSourceDeclaration.md#kb-topic-creating-datasources) for more details.
*   ScreenLoaderServlet - a servlet that returns the definition of one or more screens in JavaScript notation. Can be invoked using a traditional HTTP GET, the [loadUI JSP tag](loadUITag.md#kb-topic-isomorphicloadui), or the [RPCManager.loadScreen](../classes/RPCManager.md#classmethod-rpcmanagerloadscreen) function.
*   ProjectLoaderServlet - returns a JavaScript fragment that when executed loads a named project and [caches](../classes/RPCManager.md#classmethod-rpcmanagercachescreens) all (or a specified subset) of its screens up-front. Can be invoked using a traditional HTTP GET, or the [RPCManager.loadProject](../classes/RPCManager.md#classmethod-rpcmanagerloadproject) function. Refer to [javadoc](server/javadoc/com.isomorphic.servlet.ProjectLoaderServlet) for parameter names and their meanings.

Note that not all of the servlets and filters listed under _Optional Functionality_ above are present in the web.xml that ships with the smartclientRuntime - if you need to use any of these, copy their configuration from the web.xml available under the WEB-INF directory of smartclientSDK. Other servlets, filters and configuration files from the smartclientSDK should not be copied to your deployment, simply because the SDK includes many developer tools that are not extensively audited from a security standpoint.

---
