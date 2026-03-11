# RPCRequest Documentation

[← Back to API Index](../reference.md)

---

## Attr: RPCRequest.suppressAutoDraw

### Description
If [RPCRequest.evalResult](#attr-rpcrequestevalresult) is set, setting this property to true causes [Canvas.autoDraw](Canvas.md#attr-canvasautodraw) to be set to false for the duration of the result evaluation - which is generally what you want if you're returning new components from the server.

This also effects components loaded via the [RPCManager.loadScreen](RPCManager.md#classmethod-rpcmanagerloadscreen) API.

**Flags**: IRWA

---
## Attr: RPCRequest.isBackgroundRequest

### Description
Is this a background request?

This attribute may be set to true for requests that do not interfere with the normal flow of user interaction within an application.

Background requests are ignored by [AutoTest.waitForSystemDone](AutoTest.md#classmethod-autotestwaitforsystemdone), giving automated testing tools a way to identify specific operations that should not interfere with the flow of the test, without entirely disabling the ability to [wait for network operations](SystemWaitConfig.md#attr-systemwaitconfigincludenetworkoperations).

**Flags**: IRW

---
## Attr: RPCRequest.useSimpleHttp

### Description
When set to true, assume the request is not going to the SmartClient server, and hence send a simple HTTP request that does not use SmartClient-specific request encoding.

Values specified in [RPCRequest.params](#attr-rpcrequestparams) are sent to to the server as HTTP request parameters. If [RPCRequest.httpMethod](#attr-rpcrequesthttpmethod) is "GET", parameters appear in the request URL, otherwise if httpMethod is "POST", parameters are encoded in the request body (exactly like an HTML form does). These parameters are then accessible via typical server-side APIs for retrieving HTTP parameters, eg, servletRequest.getParameter(paramName) in Java Servlets.

Note that if [RPCRequest.httpMethod](#attr-rpcrequesthttpmethod) method is POST and [RPCRequest.data](#attr-rpcrequestdata) is supplied, [RPCRequest.data](#attr-rpcrequestdata) is assumed to be a string to post as the HTTP request body, and [RPCRequest.params](#attr-rpcrequestparams) are sent as URL parameters instead. This usage is for sending custom request bodies such as the XML payloads used for SOAP. In this case, [RPCRequest.contentType](#attr-rpcrequestcontenttype) is typically also set to indicate the content type of the request body.

Setting `useSimpleHttp` to true also automatically sets [RPCRequest.serverOutputAsString](#attr-rpcrequestserveroutputasstring) to true as well.

**Flags**: IRWA

---
## Attr: RPCRequest.downloadResult

### Description
If enabled, causes the RPCRequest to download the requested resource as a file, either showing the browser's Save dialog or displaying the file-content in [a new browser window](#attr-rpcrequestdownloadtonewwindow).

Download requests will use [transport](#attr-rpcrequesttransport): "hiddenFrame" by default.

In this mode, the download will be performed by a standard HTTP request issued by the browser. If [DSRequest.downloadToNewWindow](#attr-rpcrequestdownloadtonewwindow) is true, the request will be targeted against a new browser window, and if the resulting file can be displayed inline by the browser it will be. If [DSRequest.downloadToNewWindow](#attr-rpcrequestdownloadtonewwindow) is not true, or the browser cannot display the returned file inline, the browser will download the file and store it to the user's file system.

Download requests with [transport](#attr-rpcrequesttransport): "hiddenFrame" do not fire any callbacks.

If a developer explicitly sets `request.transport` to "xmlHttpRequest", the browser will instead use an XMLHttpRequest to download the data from the server. This mode differs from hiddenFrame downloads in various ways:

*   Explicit [RPCRequest.httpHeaders](#attr-rpcrequesthttpheaders) may be sent to the server in this mode
*   Instead of automatically downloading the response to the user's filesystem, the server response will be available as a [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob), and the [RPCRequest.downloadCallback](#method-rpcrequestdownloadcallback) will be invoked, if specified.  
    Returning `false` from the downloadCallback will suppress the default behavior of saving the file to the user's filesystem, giving developers an opportunity to take other actions, such as generating a data URL from the Blob.
*   xmlHttpRequest download does not have a built-in progress bar to indicate download progress. Developers may make use of the [RPCRequest.xhr_onProgress](#method-rpcrequestxhr_onprogress) event to indicate download progress if required.

**Flags**: IRWA

---
## Attr: RPCRequest.downloadToNewWindow

### Description
When [downloadResult](#attr-rpcrequestdownloadresult) is true, setting this attribute to true causes the content of the downloaded file to be displayed in a new browser window.

Note that this setting is currently incompatible with [transport:"xmlHttpRequest"](#attr-rpcrequesttransport). See the [downloadResult](#attr-rpcrequestdownloadresult) documentation for more details on xmlHttpRequest downloads

**Flags**: IRWA

---
## Attr: RPCRequest.serverOutputAsString

### Description
Setting this flag makes the body of the HTTP response available as a String in the [RPCRequest.callback](#attr-rpcrequestcallback) as [RPCResponse.data](RPCResponse.md#attr-rpcresponsedata). This is typically only useful if you are sending a request that will **not** be received by the SmartClient Java Server, however in that case, set [RPCRequest.useSimpleHttp](#attr-rpcrequestusesimplehttp):true instead, which implies `serverOutputAsString:true`.

`serverOutputAsString:true` allows you to, for example, load the contents of static files off your webserver into a string for processing on the client with no server support. The [RPCRequest.actionURL](#attr-rpcrequestactionurl) must be in the same domain as the current page for this to work.

This feature relies on the XMLHttpRequest object which can be disabled by end-users in some supported browsers. See [platformDependencies](../kb_topics/platformDependencies.md#kb-topic-platform-dependencies) for more information.

Generally this API is used for either [non-Java backends](../kb_topics/nonJavaBackend.md#kb-topic-net-php-serverless-integration) or for advanced usage such as content that requires processing before it can be used in SmartClient components (such as client-side web scraping). Note that SmartClient provides higher-level APIs for loading common types of data, see eg [HTMLFlow](HTMLFlow.md#class-htmlflow) for HTML content, [ViewLoader](ViewLoader.md#class-viewloader) for loading SmartClient components, [XMLTools.loadXML](XMLTools.md#classmethod-xmltoolsloadxml) for loading XML, [RPCRequest.evalResult](#attr-rpcrequestevalresult) for loading [JSON](http://www.json.org/), and [DataSource](DataSource.md#class-datasource) for loading structured data in various formats.

**Flags**: IRWA

---
## Attr: RPCRequest.useCursorTracker

### Description
If true, an image is shown to the right of the cursor when [RPCRequest.promptStyle](#attr-rpcrequestpromptstyle) is set to "cursor", otherwise the cursor itself is modified via css to the value of [RPCRequest.promptCursor](#attr-rpcrequestpromptcursor).

If left unspecified, the default value is set by [RPCManager.useCursorTracker](RPCManager.md#classattr-rpcmanagerusecursortracker).

### Groups

- rpcPrompt

### See Also

- [RPCManager.useCursorTracker](RPCManager.md#classattr-rpcmanagerusecursortracker)

**Flags**: IRW

---
## Attr: RPCRequest.httpHeaders

### Description
HTTP headers to send, as a Object mapping Header name -> Header value, eg  
{ "Content-Type" : "text/xml" }

Valid with the xmlHttpRequest [transport](#attr-rpcrequesttransport) only.

**Flags**: IRW

---
## Attr: RPCRequest.bypassCache

### Description
For xmlHttp transport + httpMethod: "GET" only, set to true to force a conditional GET request even if the browser thinks it has a current cached response.

**Flags**: IRWA

---
## Attr: RPCRequest.paramsOnly

### Description
When set to true, assume the request is not going to the SmartClient server, and hence send a simple HTTP request. Values specified in [RPCRequest.params](#attr-rpcrequestparams) are sent to to the server as HTTP request parameters. If [RPCRequest.httpMethod](#attr-rpcrequesthttpmethod) method is POST and [RPCRequest.data](#attr-rpcrequestdata) is supplied, it is assumed to be a string to post as the HTTP requestBody.

Setting this to true automatically defaults [RPCRequest.serverOutputAsString](#attr-rpcrequestserveroutputasstring) to true as well.

**Deprecated**

**Flags**: IRWA

---
## Attr: RPCRequest.httpProxyURL

### Description
The proxy URL to use for this request (if [RPCRequest.useHttpProxy](#attr-rpcrequestusehttpproxy) is set for this request). If unset, the value of [RPCManager.httpProxyURL](RPCManager.md#classattr-rpcmanagerhttpproxyurl) will be used instead.

### See Also

- [RPCManager.httpProxyURL](RPCManager.md#classattr-rpcmanagerhttpproxyurl)

**Flags**: IR

---
## Attr: RPCRequest.promptCursor

### Description
Controls the cursor shown when [RPCManager.promptStyle](RPCManager.md#classattr-rpcmanagerpromptstyle) is set to `"cursor"` for this request only. Defaults to [RPCManager.promptCursor](RPCManager.md#classattr-rpcmanagerpromptcursor).

### Groups

- rpcPrompt

### See Also

- [RPCManager.promptCursor](RPCManager.md#classattr-rpcmanagerpromptcursor)

**Flags**: IRW

---
## Attr: RPCRequest.ignoreTimeout

### Description
When set to true, no reply is expected from the server. However, if a reply is received, it will be processed.

Note: setting this to true, forces [RPCRequest.sendNoQueue](#attr-rpcrequestsendnoqueue) to `true` for this request.

**Flags**: IRWA

---
## Attr: RPCRequest.allowIE9Leak

### Description
Advanced flag to avoid a potential memory leak in Internet Explorer 9 for requests with JSON formatted responses.

This attribute may be set to `false` to explicitly enable the workaround described [here](RPCManager.md#classattr-rpcmanagerallowie9leak) for this request, avoiding a potential memory leak in Internet Explorer 9.

This workaround has a limitation in that if parsing the JSON response generates certain object types including JavaScript `Date` or `function` objects, attempts to interact with these objects can subsequently lead to a JavaScript error with the message `"Can't execute code from a freed script"`.

This workaround therefore may not be suitable for all transactions or dataSources within a given application.

This property may also be set globally within an application (via [RPCManager.allowIE9Leak](RPCManager.md#classattr-rpcmanagerallowie9leak))\_.

Note: This memory leak and workaround is discussed further in the online [SmartClient FAQ](http://forums.smartclient.com/showthread.php?t=8159).

**Flags**: IRA

---
## Attr: RPCRequest.sendNoQueue

### Description
When set to true, this request is sent to the server immediately, bypassing any current queue.

**Flags**: IRWA

---
## Attr: RPCRequest.contentType

### Description
Valid with the xmlHttpRequest transport only and only when [RPCRequest.httpMethod](#attr-rpcrequesthttpmethod) is set to "POST".

**Flags**: IRW

---
## Attr: RPCRequest.omitNullMapValuesInResponse

### Description
If enabled, the server omits any key/value pairs in map that have null values from the response. This can reduce the size of the response when many fields have null values.

To enable this globally for all responses you can set RPCManager.omitNullMapValuesInResponse in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file).

Note that [SQL DataSources](../kb_topics/sqlDataSource.md#kb-topic-sql-datasources) don't add nulls to results for null values so this flag does nothing in that case.

**Flags**: IRWA

---
## Attr: RPCRequest.useXmlHttpRequest

### Description
Selects the default http transport for this RPCRequest. If set to true, this request will use XMLHttpRequest for the transport to the server. If set to false it will use a hidden frame. If left unset, the transport mechanism is determined from the RPCManager default set in [RPCManager.useXmlHttpRequest](RPCManager.md#classattr-rpcmanagerusexmlhttprequest)

If you're using queueing, note that all requests in the queue must use the same transport. If you attempt to send a request via a different transport than those that are currently on the queue, it will be sent to the server separately, ahead of the queue, and a warning will be logged to the Developer Console.

If you specify `true` for this attribute and XMLHttp is not available, a warning will be logged to the Developer Console and RPCManager will attempt to use the frames transport for this request. Note that some features like [RPCRequest.serverOutputAsString](#attr-rpcrequestserveroutputasstring) require the XMLHttp transport and will not work if the XMLHttp transport is unavailable (this can happen if the end user is using Internet Explorer and has disabled ActiveX). You can query the availability of XMLHttp by calling [RPCManager.xmlHttpRequestAvailable](RPCManager.md#classmethod-rpcmanagerxmlhttprequestavailable)

### See Also

- [RPCManager.useXmlHttpRequest](RPCManager.md#classattr-rpcmanagerusexmlhttprequest)
- [RPCManager.xmlHttpRequestAvailable](RPCManager.md#classmethod-rpcmanagerxmlhttprequestavailable)

**Deprecated**

**Flags**: IRWA

---
## Attr: RPCRequest.willHandleError

### Description
With willHandleError:false, rpcResponses that indicate an error go through centralized handling in the RPCManager and rpcRequest.callback is never invoked.

Setting willHandleError:true means that your rpcRequest.callback will receive rpcResponses that have an error status and must handle them.

See also the error handling section in the [RPCManager](RPCManager.md#class-rpcmanager) docs.

### Groups

- errorHandling

### See Also

- [RPCManager](RPCManager.md#class-rpcmanager)

**Flags**: IRW

---
## Attr: RPCRequest.transport

### Description
Selects the transport used for this RPCRequest. If unset, the value of [RPCManager.defaultTransport](RPCManager.md#classattr-rpcmanagerdefaulttransport) will be used.

If you're using queueing, note that all requests in the queue must use the same transport. If you attempt to send a request via a different transport than those that are currently on the queue, it will be sent to the server separately, ahead of the queue, and a warning will be logged to the Developer Console.

If you specify an unknown transport, an error will be logged to the DeveloperConsole and [RPCManager.defaultTransport](RPCManager.md#classattr-rpcmanagerdefaulttransport) will be used instead.

If you specify the `xmlHttpRequest` transport and it is not available, a warning will be logged to the Developer Console and the RPCManager will attempt to use the `hiddenFrame` transport instead for this request. Note that some features like [RPCRequest.serverOutputAsString](#attr-rpcrequestserveroutputasstring) require the `xmlHttpRequest` transport and will not work if the `xmlHttpRequest` transport is unavailable (this can happen if the end user is using Internet Explorer and has disabled ActiveX). You can check whether or not the `xmlHttpRequest` transport is currently available by calling [RPCManager.xmlHttpRequestAvailable](RPCManager.md#classmethod-rpcmanagerxmlhttprequestavailable).

### See Also

- [RPCManager.defaultTransport](RPCManager.md#classattr-rpcmanagerdefaulttransport)

**Flags**: IRWA

---
## Attr: RPCRequest.actionURL

### Description
Overrides RPCManager.actionURL for this request only. If you're using queuing, note that queues as per-URL - in other words all RPCRequests in a queue must go to a single URL. If you attempt to send a request with an actionURL that is different from those already in the queue, it will be sent to the server separately, ahead of the queue, and a warning will be logged to the Developer Console.

### See Also

- [RPCManager.actionURL](RPCManager.md#classattr-rpcmanageractionurl)

**Flags**: IRW

---
## Attr: RPCRequest.promptStyle

### Description
Controls the prompt style for this request only. Defaults to [RPCManager.promptStyle](RPCManager.md#classattr-rpcmanagerpromptstyle).

### Groups

- rpcPrompt

### See Also

- [RPCManager.promptStyle](RPCManager.md#classattr-rpcmanagerpromptstyle)

**Flags**: IRW

---
## Attr: RPCRequest.promptDelay

### Description
Overrides RPCManager.promptDelay for this request only. Defaults to [RPCManager.promptDelay](RPCManager.md#classattr-rpcmanagerpromptdelay).

If you're using queuing, note that the promptDelay of the first request is used for the entire queue.

### Groups

- rpcPrompt

### See Also

- [RPCRequest.showPrompt](#attr-rpcrequestshowprompt)
- [RPCManager.promptDelay](RPCManager.md#classattr-rpcmanagerpromptdelay)

**Flags**: IRWA

---
## Attr: RPCRequest.callback

### Description
If you expect to receive a response to your RPC request, you can specify a callback that will be called with an instance or RPCResponse class as sent by the server. Queuing does not affect callbacks in any way - your specified callback will be invoked for each RPCRequest that contained a callback regardless of whether the request was sent as part of a queue or not.

Note that if the request encounters an error (such as 500 server error), by default the callback will **not** be fired, instead, [RPCManager.handleError](RPCManager.md#classmethod-rpcmanagerhandleerror) is called to invoke the default system-wide error handling. Set [RPCRequest.willHandleError](#attr-rpcrequestwillhandleerror):true to have your callback invoked regardless of whether there are errors, however, make sure your callback properly handles malformed responses when [RPCResponse.status](RPCResponse.md#attr-rpcresponsestatus) is non-zero. See the [error handling overview](../kb_topics/errorHandling.md#kb-topic-error-handling-overview) for more details.

This callback will not be invoked for [RPCRequest.downloadResult](#attr-rpcrequestdownloadresult) download requests.

### Groups

- errorHandling

**Flags**: IRW

---
## Attr: RPCRequest.showPrompt

### Description
Overrides `RPCManager.showPrompt` for this request only.

If you're using queuing, note that if any of the requests in the queue specify showPrompt:true, then a prompt will be shown for the entire queue with the prompt text of the first request in the queue to specify a custom prompt if promptStyle is set to "dialog".

If promptStyle is set to "cursor" for the request that specified showPrompt: true, then the entire queue uses the "cursor" style for the prompt.

### Groups

- rpcPrompt

### See Also

- [RPCManager.showPrompt](RPCManager.md#classattr-rpcmanagershowprompt)
- [RPCRequest.promptStyle](#attr-rpcrequestpromptstyle)

**Flags**: IRW

---
## Attr: RPCRequest.callbackParam

### Description
For use only with the [scriptInclude](../reference.md#type-rpctransport) transport, this attribute specifies the name of the URL parameter which is used to specify the callback function that the server is expected to call by writing out JavaScript code. The actual function to call is automatically generated and differs for every request (to allow concurrency).

For example, with `callbackParam` set to it's default value of "callback", the server might be contacted with a URL like:

```
    loadData?callback=isc_scriptIncludeCallback_5
 
```
.. then the server's response should look like:
```
    isc_scriptIncludeCallback_5({ .. data .. });
 
```
The name "isc\_scriptIncludeCallback\_5" is automatically generated and will differ each time the server is contacted.

SmartClient makes of this server-provided callback mechanism, then calls [RPCRequest.callback](#attr-rpcrequestcallback) normally.

`rpcRequest.callbackParam` is ignored by all transport other than `scriptInclude`.

**Flags**: IRW

---
## Attr: RPCRequest.containsCredentials

### Description
For use during [Relogin](../kb_topics/relogin.md#kb-topic-relogin), this property marks this request an attempt to login, therefore a response containing the `loginRequiredMarker` is a normal condition and should result in the status code [RPCResponse.STATUS_LOGIN_INCORRECT](RPCResponse.md#classattr-rpcresponsestatus_login_incorrect) rather than a call to [loginRequired()](RPCManager.md#classmethod-rpcmanagerloginrequired).

It is not required to set `containsCredentials`, however, it does typically simplify relogin logic by separating the handling of RPCs that are login attempts from RPCs that are not.

### Groups

- relogin

**Flags**: IRWA

---
## Attr: RPCRequest.useHttpProxy

### Description
Indicates whether this request should use the HttpProxyServlet in order to enable contacting hosts other than the origin server (available only in Pro Edition or better).

When various UI components issues requests automatically, or when a call to [RPCManager.sendProxied](RPCManager.md#classmethod-rpcmanagersendproxied) is made, the HttpProxy will automatically be used for a URL that starts with "http" and uses a hostname other than "localhost" or `window.location.hostname`, or if the port number differs.

`rpcRequest.useHttpProxy` should only be used to force requests to go through the HttpProxy when the above rules don't work, or to avoid using the HttpProxy when contacting hosts that allow cross-site calls via the [Http Access Control](http://www.google.com/search?q=http+access+control) standard.

You can also set [RPCManager.useHttpProxy](RPCManager.md#classattr-rpcmanagerusehttpproxy):false to avoid ever using the HttpProxyServlet.

**Flags**: IR

---
## Attr: RPCRequest.evalResult

### Description
This works similarly to [RPCRequest.serverOutputAsString](#attr-rpcrequestserveroutputasstring) except the resulting String is automatically evaluated as JavaScript. The result of the evaluation is then passed to any specified [RPCRequest.callback](#attr-rpcrequestcallback) as [RPCResponse.data](RPCResponse.md#attr-rpcresponsedata).

This feature can be used to dynamically load new application modules into a running application. An RPCRequest with `evalResult` enabled can be used to fetch a static .js file or JavaScript dynamically generated by the server. The returned JavaScript can contain anything that a JavaScript file loaded at init time can contain, including new views and new SmartClient class definitions.

_Example usage with [RPCManager.sendRequest](RPCManager.md#classmethod-rpcmanagersendrequest):_

```
 isc.RPCManager.sendRequest({
     evalResult:true,
     actionURL:"js/loadLabel.js",
     evalVars:{var1:"A Value"}
 });
 
```
This call would execute the code from `loadLabel.js`, and make the variable `var1` available to that code. Therefore if the .js file contained this code:
```
 isc.Label.create({
     contents:var1
 })
 
```
A label would be created with contents set to the value of `var1` - the string `"A Value"`.

This feature relies on the XMLHttpRequest object which can be disabled by end-users in some supported browsers. See [platformDependencies](../kb_topics/platformDependencies.md#kb-topic-platform-dependencies) for more information.

### Groups

- viewLoading

### See Also

- [ViewLoader](ViewLoader.md#class-viewloader)
- [RPCRequest.evalVars](#attr-rpcrequestevalvars)

**Flags**: IRWA

---
## Attr: RPCRequest.httpMethod

### Description
Selects the HTTP method that will be used for the request. Typical values are "POST" and "GET".

The more obscure "PUT", "DELETE" and "HEAD" methods are also valid, however, none of these are supported by the Safari browser previous to version 3.0.

**Flags**: IRW

---
## Attr: RPCRequest.params

### Description
Values to be sent as simple HTTP params, as a JavaScript Object where each property/value pair will become an HTTP parameter name and value. These parameters are then accessible on the server, for example, using servletRequest.getParameter(paramName) in Java Servlets.

Array-valued parameters will be submitted as multiple instances of the same parameter, similar to an HTML form with a multi-select (?paramName=value1&paramName=value2 ...), accessible as getParameterValues(paramName) in Java Servlets. Any non-atomic type, such as an Object, will be serialized to [JSON](http://www.json.org/) by the [JSONEncoder](JSONEncoder.md#class-jsonencoder). If this isn't desirable, serialize the data in advance so that the value provided in `rpcRequest.params` is a String.

Note that this API is primarily used in combination with [RPCRequest.useSimpleHttp](#attr-rpcrequestusesimplehttp) - when contacting the SmartClient Server, use [RPCRequest.data](#attr-rpcrequestdata) instead, which provides full JavaScript <-> Java translation of arbitrary structures. `rpcRequest.params` can also be used with the SmartClient Server, where it provides an an opportunity to send additional data aside from the main [RPCRequest.data](#attr-rpcrequestdata) payload. This is useful for adding data to DataSource requests which will be kept separate from the automatically sent DataSource data, or for making parts of the request visible in the URL for HTTP-level logging or layer 4 switches.

Note that in contrast to [RPCRequest.data](#attr-rpcrequestdata) object, the data in `rpcRequest.params` is not deserialized by the SmartClient server, and all values arrive on the server as String type (like HTTP parameters always do).

The params value can also be specified as a componentID or component instance that provides a method getValues() that returns an Object containing parameter names and values. SmartClient components [DynamicForm](DynamicForm.md#class-dynamicform), [ValuesManager](ValuesManager.md#class-valuesmanager) are two such classes. Lastly, you may specify the ID of a native form element (retrievable via getElementById()) and the params will be populated from there. If there is an error resolving your params directive, it will be logged to the Developer Console.

Note: The params are submitted once per http transaction. If you are using [request queuing](RPCManager.md#classmethod-rpcmanagerstartqueue) to bundle multiple RPCRequests or DSRequests into a single HTTP turnaround, the params from the various RPCRequests will be merged, with the later-queued transactions winning on parameter name collisions. A warning will be logged in the Developer Console if multiple RPCRequests specified params.

**Flags**: IRW

---
## Attr: RPCRequest.prompt

### Description
Overrides RPCManager.defaultPrompt for this request only. If you're using queuing, note that the prompt string from the first request in the queue is the one that is shown to the user.

### Groups

- rpcPrompt

### See Also

- [RPCManager.defaultPrompt](RPCManager.md#classattr-rpcmanagerdefaultprompt)
- [RPCManager.showPrompt](RPCManager.md#classattr-rpcmanagershowprompt)
- [RPCManager.promptStyle](RPCManager.md#classattr-rpcmanagerpromptstyle)
- [RPCManager.promptCursor](RPCManager.md#classattr-rpcmanagerpromptcursor)
- [RPCRequest.showPrompt](#attr-rpcrequestshowprompt)
- [RPCRequest.promptStyle](#attr-rpcrequestpromptstyle)
- [RPCRequest.promptCursor](#attr-rpcrequestpromptcursor)

**Flags**: IRW

---
## Attr: RPCRequest.data

### Description
This attribute specifies the payload of the RPCRequest. When using the [SmartClient server](../kb_topics/iscServer.md#kb-topic-smartclient-server-summary), any JavaScript simple type or arbitrarily nested set of Objects and Arrays can be sent to server and automatically translated to Java Objects.

Here are the mapping of JavaScript types to their corresponding server object types:  
  

| JS Type | Java Type |
|---|---|
| Object: {} | Map |
| Array: [] | List |
| String | String |
| Number | Long\|Double |
| Boolean | Boolean |
| Date | java.util.Date |
| String | com.smartgwt.client.types.ValueEnum |

  
  
Note that the order of keys/values in the Maps created on the server is not guaranteed because JavaScript Object literals do not guarantee order.

When using JPA or Hibernate Java value used can be affected by the Java Bean declaration. See [dsRequestBeanTypes](../kb_topics/dsRequestBeanTypes.md#kb-topic-dsrequest-data-auto-converted-to-bean-types) for details.

Server->client conversion follows this table as well, with some extras. See the toJS() method on JSTranslater in the server documentation for a description of additional behaviors.

When **not** communicating with the SmartClient server, `rpcRequest.data` becomes simple HTTP parameters or an HTTP request body - see [RPCRequest.useSimpleHttp](#attr-rpcrequestusesimplehttp) for details.

### See Also

- [RPCResponse.data](RPCResponse.md#attr-rpcresponsedata)

**Flags**: IRW

---
## Attr: RPCRequest.reportDownloadErrorsAsDocuments

### Description
Whether errors during download should be reported inside the document, rather than through the [normal mechanism](RPCResponse.md#attr-rpcresponsestatus). If unset, this will be defaulted from [RPCManager.reportDownloadErrorsAsDocuments](RPCManager.md#classattr-rpcmanagerreportdownloaderrorsasdocuments).

**Flags**: IRW

---
## Attr: RPCRequest.withCredentials

### Description
In browsers that support [Cross-Origin Resource Sharing](https://fetch.spec.whatwg.org/#http-cors-protocol) and [XMLHttpRequest 2](http://caniuse.com/#feat=xhr2), and where the service at the [actionURL](#attr-rpcrequestactionurl) allows the origin to send credentials (see `Access-Control-Allow-Credentials`), should user credentials such as cookies, HTTP authentication, and client-side SSL certificates be sent with the actual CORS request?

This setting only applies when the request [transport](#attr-rpcrequesttransport) is "xmlHttpRequest".

Note that Internet Explorer 10 and 11 do not send cookies as part of user credentials: [IE10 doesn't support cookies on cross origin XMLHttpRequest withCredentials=true](https://connect.microsoft.com/IE/Feedback/Details/759587/).

**Flags**: IRA

---
## Attr: RPCRequest.timeout

### Description
Sets the timeout on this request. Default is to use [RPCManager.defaultTimeout](RPCManager.md#classattr-rpcmanagerdefaulttimeout).

If you're using [queuing](RPCManager.md#classmethod-rpcmanagerstartqueue), note that the timeout setting derived from the last request in the queue is used for the entire queue. If you want to override the timeout for the queue, make sure to set your override at least on the last request in the queue.

For the "xmlHttpRequest" [transport](#attr-rpcrequesttransport), this timeout can only happen if the server actually fails to respond within the specified number of milliseconds. For the "hiddenFrame" transport, this timeout will occur for non-200 (HTTP\_OK) responses.

If `timeout` is set to zero, the RPCManager will not enforce a timeout for this request. However, note that all browsers enforce their own timeouts on HTTP requests, and may have different timeouts for different kinds of failures (no response at all from server, hung response after receiving headers, hung response after receiving partial data, etc). Also, intervening web proxies or firewalls may impose timeouts of their own.

As a rough rule of thumb, if your server response will have a lengthy pause before data begins to be sent, 1-2 minutes is the maximum allowable pause for a public site and still may not work for a minority of users, but up to 4 minutes may be allowable in a controlled environment (intranet or extranet with well-known user base).

Above these limits, your code should return some kind of immediate response to the browser, then kick off a server-side process to complete processing. The browser can then either poll for completion, or use a server-push notification system such as SmartClient Real-Time Messaging (see [http://smartclient.com/product](http://smartclient.com/product)).

### See Also

- [RPCManager.defaultTimeout](RPCManager.md#classattr-rpcmanagerdefaulttimeout)

**Flags**: IRWA

---
## Attr: RPCRequest.mockMode

### Description
If enabled and request is applied to [RPCManager.cacheScreens](RPCManager.md#classmethod-rpcmanagercachescreens) or [RPCManager.loadScreen](RPCManager.md#classmethod-rpcmanagerloadscreen) indicates that referenced DataSources should be loaded in mock mode.

**Flags**: IR

---
## Attr: RPCRequest.evalVars

### Description
If you've set [RPCRequest.evalResult](#attr-rpcrequestevalresult) : true, then the property values of this object will be available in the evaluation scope of the result under the variable names specified by the property names.

So e.g. if evalVars is: `{foo: "bar"}` then a reference to the variable `foo` in the result will evaluate to `"bar"`.

### Groups

- viewLoading

**Flags**: IRWA

---
## Attr: RPCRequest.clientContext

### Description
An object to be held onto for the duration of the RPC turnaround to track application-specific context.  
When an RPC turnaround completes, the `clientContext` is available in the [RPCCallback](Callbacks.md#method-callbacksrpccallback) as `rpcResponse.clientContext`. The `clientContext` is never sent to the server.  
The `clientContext` is useful for holding onto state that will be used when the [RPCCallback](Callbacks.md#method-callbacksrpccallback) fires, such as the name of a component that will receive the returned data.

### See Also

- [RPCResponse.clientContext](RPCResponse.md#attr-rpcresponseclientcontext)

**Flags**: IRW

---
## Attr: RPCRequest.useStrictJSON

### Description
If set true, tells the server to use strict JSON format when serializing the response data. If set false, tells the server to use a more permissive encoding that is still valid JS, but is not technically valid JSON. The default value of null tells the server to use the default global setting (see below).

To enable this globally for all responses you can set `RPCManager.useStrictJSON` in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file). If the global flag is not set either way in `server.properties`, it defaults to false.

### See Also

- [DSRequest.useStrictJSON](DSRequest.md#attr-dsrequestusestrictjson)

**Flags**: IRWA

---
## Method: RPCRequest.xhr_onProgress

### Description
Progress event notification fired repeatedly during requests with [RPCRequest.transport](#attr-rpcrequesttransport) set to `"xmlHttpRequest"`.

This callback will be invoked from the native [XMLHttpRequest progress event](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/progress_event).

This is typically useful to provide visual feedback to the user when a lengthy download is in progress.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| progressEvent | [Object](../reference.md#type-object) | false | — | The native [ProgressEvent](https://developer.mozilla.org/en-US/docs/Web/API/ProgressEvent) with attributes indicating the `loaded` content so far, and, if `Content-Length` headers were set on the response, the `total` download size. Note that this is a native event produced by the browser and SmartClient does not guarantee consistency for the event object, or the timing of the `onprogress` event notifications across browsers. |
| request | [RPCRequest](#type-rpcrequest) | false | — | the request that initiated the download |

---
## Method: RPCRequest.downloadCallback

### Description
Callback for [download requests](#attr-rpcrequestdownloadresult) with [RPCRequest.transport](#attr-rpcrequesttransport) set to `"xmlHttpRequest"`.

This method will fire when a download request completes. If [DSRequest.willHandleError](#attr-rpcrequestwillhandleerror) is true it will fire on both successful completion or failure as reflected by the [DSResponse.status](DSResponse.md#attr-dsresponsestatus).

By default, successful download requests will save the returned file to the filesystem. To suppress this behavior, return false from this callback. This allows you to take some other action such as generating a [data url](https://developer.mozilla.org/en-US/docs/web/http/basics_of_http/data_urls) to display media, etc.

Note that for a successful download request, the `data` parameter will be a [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob). For an unsuccessful download attempt, the data parameter typically contains the error message from the server. To invoke standard error handling, [RPCManager.runDefaultErrorHandling](RPCManager.md#classmethod-rpcmanagerrundefaulterrorhandling) may be called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| response | [RPCResponse](#type-rpcresponse) | false | — | the response to the request |
| data | [Object](../reference.md#type-object) | false | — | The Blob returned by the server, or error message if the download was unsuccessful |
| fileName | [String](#type-string) | false | — | The file name for the downloaded file, derived from the [content-disposition header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition). |
| type | [String](#type-string) | false | — | the content type for the downloaded file, as specified by the [content-type header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type). |
| request | [RPCRequest](#type-rpcrequest) | false | — | the request that initiated the download |

### Returns

`[Boolean](#type-boolean)` — return false to suppress default behavior of saving the download file to the user's filesystem.

---
