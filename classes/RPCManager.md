# RPCManager Documentation

[← Back to API Index](../reference.md)

---

## Class: RPCManager

### Description
RPCManager is a static singleton class that manages transparent client/server RPC (remote procedure call). This class provides a generic, low-level client/server communication integration point.

SmartClient's powerful databinding subsystem (see [DataSource](DataSource.md#class-datasource), [DataBoundComponents](../reference.md#interface-databoundcomponent)) automatically make use of this class to issue RPCs as necessary, based on the [DataSource protocol](../kb_topics/dataSourceOperations.md#kb-topic-datasource-operations). To integrate DataBoundComponents with your server, [start here](../kb_topics/clientServerIntegration.md#kb-topic-client-server-integration).

For arbitrary client/server interactions outside of the DataSource subsystem, the SmartClient server also provides the [Direct Method Invocation](../kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) feature.

The RPCManager class can also be used _directly_ to send data to a URL of your choosing and optionally be called back with server-returned data when the server replies.

The SmartClient [server code](../kb_topics/iscServer.md#kb-topic-smartclient-server-summary) has APIs for processing RPC requests providing features such as automatic Java <--> JavaScript object translation and handling of queued requests.  
The [IDACall servlet](../kb_topics/servletDetails.md#kb-topic-the-core-and-optional-smartclient-servlets) makes use of these features to handle standard [DataSource](DataSource.md#class-datasource) requests and [DMI](DMI.md#class-dmi) calls. Developers can also override the `actionURL` of specific requests and use these APIs directly in a JSP, Servlet or Filter.

Note: the client-side RPCManager class can also be used without the SmartClient server. For an overview of client/server interactions without the SmartClient server, see [this overview](../kb_topics/nonJavaBackend.md#kb-topic-net-php-serverless-integration).

Simple arbitrary Remote Procedure Call example (client code):

```
 var data = { here: "is some data", to: ["send to the server"]};
 isc.RPCManager.sendRequest({ data: data, callback: "myCallback(data)", actionURL: "/rpcHandler.jsp"});
 function myCallback(data) { alert("response from the server: " + data); }
 
```

Simple arbitrary Remote Procedure Call example (server code: /rpcHandler.jsp):  
  

```
 RPCManager rpc = new RPCManager(request, response, out);
 Object data = rpc.getData();
 System.out.println("client sent: " + data.toString());
 rpc.send("here's a response");
 
```

**Queuing**  
Because of browser limitations on the total number of simultaneous HTTP connections to a given server, batching multiple RPC requests into a single HTTP request is highly advisable whenever possible. The RPCManager provides a queuing mechanism that allows this.  
  
Queuing example (client code):

```
 var wasQueuing = isc.RPCManager.startQueue();
 isc.RPCManager.send("a string of data", "myCallback(data)", {actionURL: "/rpcHandler.jsp"});
 isc.RPCManager.sendRequest({ data: ["some", "more data", 2], callback: "myCallback(data)", actionURL: "/rpcHandler.jsp"});
 isc.RPCManager.sendRequest({ data: "different callback", callback: "myCallback2(data)", actionURL: "/rpcHandler.jsp"});
 if (!wasQueuing) isc.RPCManager.sendQueue();
 
 function myCallback(data) { alert("response from the server: " + data); }
 function myCallback2(data) { alert("response from the server (other callback): " + data); }
 
```

Queuing example (server code: /rpcHandler.jsp):  
  

```
 RPCManager rpc = new RPCManager(request, response, out);

 for(Iterator i = rpc.getRequests().iterator(); i.hasNext();) {
     RPCRequest rpcRequest = (RPCRequest)i.next();
     Object data = rpcRequest.getData();
     System.out.println("client sent:" + data.toString());

     //send back the data sent to us by the client
     rpc.send(rpcRequest, new RPCResponse(data));
 }
 
```
  
  
**Error Handling**  
  
Please see this [separate article](../kb_topics/errorHandling.md#kb-topic-error-handling-overview) on error handling.

---
## ClassAttr: RPCManager.keepParentsOnFilterMaxNodesExceededMessage

### Description
Default message displayed to the user when a databound [load-on-demand](ResultTree.md#attr-resulttreeloaddataondemand) [TreeGrid](TreeGrid.md#class-treegrid) is filtered while [keepParentsOnFilter](ResultTree.md#attr-resulttreekeepparentsonfilter) is in force, and the number of tree nodes matching the filter exceeds [keepParentsOnFilterMaxNodes](ResultTree.md#attr-resulttreekeepparentsonfiltermaxnodes)

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: RPCManager.timeoutErrorMessage

### Description
Default message displayed to user when an operation fails to return from the server within the timeout period specified by [RPCManager.defaultTimeout](#classattr-rpcmanagerdefaulttimeout).

### Groups

- i18nMessages

### See Also

- [RPCManager.defaultTimeout](#classattr-rpcmanagerdefaulttimeout)

**Flags**: IRW

---
## ClassAttr: RPCManager.defaultTimeout

### Description
In milliseconds, how long the RPCManager waits for an RPC request to complete before returning an error.

Default of 240000 milliseconds is four minutes. If set to zero, the RPCManager will not enforce a timeout, however, see [RPCRequest.timeout](RPCRequest.md#attr-rpcrequesttimeout) for a discussion of default timeouts that are built into browsers.

**Flags**: RW

---
## ClassAttr: RPCManager.allowCrossDomainCalls

### Description
By default SmartClient will show a warning message on attempted requests to another domain as this is usually not supported at the browser level by default due to security considerations.

Some browsers now do support cross domain requests through the use of Http Access Control headers (See the [W3C Cross-Origin Resource Sharing recommendation](https://fetch.spec.whatwg.org/#http-cors-protocol)). If your application intends to rely on this behavior to perform cross-domain requests, you can set `allowCrossDomainCalls` to true to disable the standard SmartClient warning when such calls occur.

Note also that this is typically not an issue if you are using the SmartClient server (part of Pro, Power and Enterprise editions of SmartClient), as this includes the [HTTPProxy servlet](#classmethod-rpcmanagersendproxied).

**Flags**: IRWA

---
## ClassAttr: RPCManager.loginSuccessMarker

### Description
Marker the system will look for in order to detect when login was successful.

The default loginSuccessMarker is the following string:  
`"`<SCRIPT>`//'\"]]>>isc_loginSuccess"`

### Groups

- relogin

### See Also

- [RPCManager.loginRequiredMarker](#classattr-rpcmanagerloginrequiredmarker)

**Flags**: IRWA

---
## ClassAttr: RPCManager.defaultPrompt

### Description
If showPrompt is enabled for a given transaction, this is the defaultPrompt to be shown to the user in a modal dialog while the transaction occurs. May be overridden at the request level via [RPCRequest.prompt](RPCRequest.md#attr-rpcrequestprompt).  
More targetted default prompts are also supported for certain code-paths. See the following set of properties for details:

*   [RPCManager.removeDataPrompt](#classattr-rpcmanagerremovedataprompt)
*   [RPCManager.saveDataPrompt](#classattr-rpcmanagersavedataprompt)
*   [RPCManager.fetchDataPrompt](#classattr-rpcmanagerfetchdataprompt)

### Groups

- rpcPrompt
- i18nMessages

### See Also

- [RPCManager.showPrompt](#classattr-rpcmanagershowprompt)
- [RPCManager.promptStyle](#classattr-rpcmanagerpromptstyle)
- [RPCManager.promptCursor](#classattr-rpcmanagerpromptcursor)
- [RPCRequest.showPrompt](RPCRequest.md#attr-rpcrequestshowprompt)
- [RPCRequest.prompt](RPCRequest.md#attr-rpcrequestprompt)
- [RPCRequest.promptStyle](RPCRequest.md#attr-rpcrequestpromptstyle)
- [RPCRequest.promptCursor](RPCRequest.md#attr-rpcrequestpromptcursor)

**Flags**: IRW

---
## ClassAttr: RPCManager.promptStyle

### Description
Controls the default prompt style. Overrideable by [RPCRequest.promptStyle](RPCRequest.md#attr-rpcrequestpromptstyle).

### Groups

- rpcPrompt

### See Also

- [RPCRequest.promptStyle](RPCRequest.md#attr-rpcrequestpromptstyle)

**Flags**: IRW

---
## ClassAttr: RPCManager.maxLoginAttemptsExceededMarker

### Description
Marker the system will look for in order to detect when the number of maximum logins was exceeded.

The default maxLoginAttemptsExceededMarker is the following string: `"`<SCRIPT>`//'\"]]>>isc_maxLoginAttemptsExceeded"`

### Groups

- relogin

### See Also

- [RPCManager.loginRequiredMarker](#classattr-rpcmanagerloginrequiredmarker)

**Flags**: IRWA

---
## ClassAttr: RPCManager.screenLoaderURL

### Description
The screenLoaderURL specifies the URL where ScreenLoaderServlet is installed.

**Flags**: RW

---
## ClassAttr: RPCManager.verifyAsError

### Description
When true, any problems found by either [verifyComponents](LoadProjectSettings.md#attr-loadprojectsettingsverifycomponents) or [verifyDataSources](LoadProjectSettings.md#attr-loadprojectsettingsverifydatasources) are shown together in a dialog presented to the end user. Provides default values for [LoadProjectSettings.verifyAsError](LoadProjectSettings.md#attr-loadprojectsettingsverifyaserror), [LoadScreenSettings.verifyAsError](LoadScreenSettings.md#attr-loadscreensettingsverifyaserror), and [CreateScreenSettings.verifyAsError](CreateScreenSettings.md#attr-createscreensettingsverifyaserror).

### See Also

- [CreateScreenSettings.verifyAsError](CreateScreenSettings.md#attr-createscreensettingsverifyaserror)
- [LoadScreenSettings.verifyAsError](LoadScreenSettings.md#attr-loadscreensettingsverifyaserror)
- [LoadProjectSettings.verifyAsError](LoadProjectSettings.md#attr-loadprojectsettingsverifyaserror)

**Flags**: IRW

---
## ClassAttr: RPCManager.showPrompt

### Description
If set to `true`, the RPCManager will block the UI with a modal dialog containing the text from RPCManager.defaultPrompt (or the per-RPCRequest override) until the RPC to the server completes.

If set to `false`, the RPC happens transparently, allowing the user to continue interacting with the UI.

DataSource requests, which are a particular type of RPCRequest, are controlled by the more-specific DataSource-level setting [DataSource.showPrompt](DataSource.md#attr-datasourceshowprompt).

### Groups

- rpcPrompt

### See Also

- [RPCManager.defaultPrompt](#classattr-rpcmanagerdefaultprompt)
- [RPCManager.promptStyle](#classattr-rpcmanagerpromptstyle)
- [RPCRequest.showPrompt](RPCRequest.md#attr-rpcrequestshowprompt)

**Flags**: RW

---
## ClassAttr: RPCManager.useXmlHttpRequest

### Description
Selects the default http transport for all RPC requests. If set to true, RPCManager will use XMLHttp for requests to the server. If set to false, it will use hidden frames. Overrideable on a per-request basis via [RPCRequest.useXmlHttpRequest](RPCRequest.md#attr-rpcrequestusexmlhttprequest).

Note that if the end user disables ActiveX controls in Internet Explorer, the XMLHttpRequest object will not be available and SmartClient will automatically fall back on frames communication.

### See Also

- [RPCRequest.useXmlHttpRequest](RPCRequest.md#attr-rpcrequestusexmlhttprequest)

**Deprecated**

**Flags**: RW

---
## ClassAttr: RPCManager.validateDataPrompt

### Description
Default prompt displayed to the user while a server validation is pending.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: RPCManager.credentialsURL

### Description
Specifies URL where credentials should be submitted to attempt relogin when session timeout is encountered during a background RPC. See [Relogin](../kb_topics/relogin.md#kb-topic-relogin)

### Groups

- relogin

**Flags**: RWA

---
## ClassAttr: RPCManager.reportDownloadErrorsAsDocuments

### Description
Whether errors during download should be reported inside the document, rather than through the [normal mechanism](RPCResponse.md#attr-rpcresponsestatus). Establishes a default for [RPCRequest.reportDownloadErrorsAsDocuments](RPCRequest.md#attr-rpcrequestreportdownloaderrorsasdocuments).

**Flags**: IRW

---
## ClassAttr: RPCManager.useHttpProxy

### Description
Whether the [HttpProxyServlet](../kb_topics/servletDetails.md#kb-topic-the-core-and-optional-smartclient-servlets) should be used in order to get around the "same origin policy" that prevents web pages from contacting other sites.

Default behavior is to use the HttpProxyServlet whenever a URL appears to be pointing to another site. Set [RPCRequest.useHttpProxy](RPCRequest.md#attr-rpcrequestusehttpproxy) false to have a particular request avoid using the HttpProxyServlet even when it appears to be necessary, or set `RPCManager.useHttpProxy` to false to avoid ever attempting to use the HttpProxyServlet.

**Flags**: IR

---
## ClassAttr: RPCManager.projectLoaderURL

### Description
The projectLoaderURL specifies the URL where ProjectLoaderServlet is installed.

**Flags**: RW

---
## ClassAttr: RPCManager.loginStatusCodeMarker

### Description
String sequence which marks the response as a one which contains login status information.

The default loginStatusCodeMarker is the following string: `"`<SCRIPT>`//'\"]]>>isc_"`

### Groups

- relogin

### See Also

- [RPCManager.loginRequiredMarker](#classattr-rpcmanagerloginrequiredmarker)

**Flags**: IRWA

---
## ClassAttr: RPCManager.fetchDataPrompt

### Description
Default prompt displayed to the user while an operation is running to fetch data from the server.  
Displayed as a result of [ListGrid.filterData](ListGrid_2.md#method-listgridfilterdata), [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata) and [ListGrid.clearCriteria](ListGrid_2.md#method-listgridclearcriteria) code paths.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: RPCManager.ALL_GLOBALS

### Description
Passing this special value to [loadScreen](#classmethod-rpcmanagerloadscreen) indicates that all global names should be preserved when evaluating loaded screen.

### See Also

- [RPCManager.loadScreen](#classmethod-rpcmanagerloadscreen)

**Flags**: R

---
## ClassAttr: RPCManager.removeDataPrompt

### Description
Default prompt displayed to user while an operation is running to remove data from the server.  
Displayed as a result of the [ListGrid.removeSelectedData](ListGrid_2.md#method-listgridremoveselecteddata) code path.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: RPCManager.loginRequiredMarker

### Description
Marker the system will look for in XHTP responses in order to detect when login is required. The default loginRequiredMarker is the following string:  
`"`<SCRIPT>`//'\"]]>>isc_loginRequired"`

As described in [relogin](../kb_topics/relogin.md#kb-topic-relogin), if this snippet is encountered in the response to a SmartClient RPC request (with standard transport `"xmlHttpRequest"`), the RPCManager will suspend the current transaction and fire the [RPCManager.loginRequired](#classmethod-rpcmanagerloginrequired) notification.

The default loginRequired marker should generally **not** be customized. It is designed to be safe to insert into any HTML page or other server response without affecting display or functionality, for example, within an HTML comment. You should \*only\* customize the `loginRequiredMarker` if you have absolutely no ability to change the response that the server will send when login is required.

If you do customize the `loginRequiredMarker`, then the loginRequiredMarker, [RPCManager.loginSuccessMarker](#classattr-rpcmanagerloginsuccessmarker) and [RPCManager.maxLoginAttemptsExceededMarker](#classattr-rpcmanagermaxloginattemptsexceededmarker) should all start with the [RPCManager.loginStatusCodeMarker](#classattr-rpcmanagerloginstatuscodemarker). If they do not, there will be a small impact on performance as every response must be separately scanned for each marker, instead of just scanning once for the [RPCManager.loginStatusCodeMarker](#classattr-rpcmanagerloginstatuscodemarker).

In addition, the [RPCManager.loginStatusCodeMarker](#classattr-rpcmanagerloginstatuscodemarker) should ideally contain text that could not possibly validly appear as a data value in a normal response, since if that were possible, end users could enter the loginRequiredMarker as a data value and cause SmartClient to falsely detect session timeout when handling an ordinary data response. This is why the default marker has characters that make it impossible for it to be validly interpreted as a JavaScript String, XML document or HTML content - there is no way that an end user could enter this as a data value in an application and have it appear verbatim in a server response.

### Groups

- relogin

**Flags**: IRWA

---
## ClassAttr: RPCManager.promptCursor

### Description
Controls the default cursor shown when [RPCManager.promptStyle](#classattr-rpcmanagerpromptstyle) is set to `"cursor"`. Overrideable by [RPCRequest.promptCursor](RPCRequest.md#attr-rpcrequestpromptcursor).

### Groups

- rpcPrompt

### See Also

- [RPCRequest.promptCursor](RPCRequest.md#attr-rpcrequestpromptcursor)

**Flags**: IRW

---
## ClassAttr: RPCManager.reloginCommFailureMessage

### Description
Message that will be reported in the relogin window if relogin fails due to communication problems.

### Groups

- relogin
- i18nMessages

**Flags**: IRW

---
## ClassAttr: RPCManager.defaultTransport

### Description
Selects the transport use for RPC requests by default. You can override this setting on a per-request basis by setting [RPCRequest.transport](RPCRequest.md#attr-rpcrequesttransport).

### See Also

- [RPCRequest.transport](RPCRequest.md#attr-rpcrequesttransport)

**Flags**: IRW

---
## ClassAttr: RPCManager.actionURL

### Description
Specifies the default URL for RPCRequests and DSRequests that do not specify a URL.

URLs can be set on a per-request basis via [RPCRequest.actionURL](RPCRequest.md#attr-rpcrequestactionurl), or on a per-DataSource or per-operationType basis via [DataSource.dataURL](DataSource.md#attr-datasourcedataurl) and [OperationBinding.dataURL](OperationBinding.md#attr-operationbindingdataurl) respectively. However, note that in order to be able to make use of [queuing](#classmethod-rpcmanagerstartqueue), you should have all data loading and saving requests go to a single URL unless you are forced to use distinct URLs by legacy services.

The primary use case for setting the default `actionURL` is to add a CSRF / XSRF ([Cross-site Request Forgery](http://en.wikipedia.org/wiki/Cross-site_request_forgery)) token. Assuming you are using a single URL for all data requests as covered above, adding a CSRF token to the default `actionURL` as a simple HTTP parameter will cause the CSRF token to be included in all RPCRequests and DSRequests from all DataSources without further effort.

If the `actionURL` is changed while transactions are suspended, any suspended transactions whose `actionURL` was defaulted to this property (e.g. because [RPCRequest.actionURL](RPCRequest.md#attr-rpcrequestactionurl) wasn't set) will be updated to have the new `actionURL`.

**Flags**: RW

---
## ClassAttr: RPCManager.saveDataPrompt

### Description
Default prompt displayed to the user while an operation is running to save data to the server.  
Displayed as a result of the [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata) code path.

### Groups

- i18nMessages

**Flags**: IRW

---
## ClassAttr: RPCManager.useCursorTracker

### Description
If true, an image is shown to the right of the cursor when [RPCRequest.promptStyle](RPCRequest.md#attr-rpcrequestpromptstyle) is set to "cursor", otherwise the cursor itself is modified via css to the value of [RPCRequest.promptCursor](RPCRequest.md#attr-rpcrequestpromptcursor).

This value can be overridden on a per-request basis via [RPCRequest.useCursorTracker](RPCRequest.md#attr-rpcrequestusecursortracker).

### Groups

- rpcPrompt

### See Also

- [RPCRequest.useCursorTracker](RPCRequest.md#attr-rpcrequestusecursortracker)

**Flags**: IRW

---
## ClassAttr: RPCManager.allowIE9Leak

### Description
In Internet Explorer 9, when a string of JavaScript is evaluated via the native `eval()` function, objects created within that evaluation are not released from browser memory until the page is reloaded.

SmartClient uses the `eval()` function to evaluate JSON formatted responses to RPCRequests by default, making long running applications potentially susceptible to memory leaks over time.

Note that this does not apply to DataSources which use [DataSource.useStrictJSON](DataSource.md#attr-datasourceusestrictjson) formatted responses as the framework avoids calling eval() altogether and makes use of the native browser `JSON.parse()` method which does not have this issue. By default we also use strict json formatted responses for all [dataFormat:"iscServer"](DataSource.md#attr-datasourcedataformat) dataSources in IE9, so these leaks are mainly a concern only for dataSources with [DataSource.dataFormat](DataSource.md#attr-datasourcedataformat) set to "json".

Setting this property to `false` enables a workaround suggested on the [Microsoft Knowledge Base](http://support.microsoft.com/kb/2572253) to avoid such memory leaks by evaluating script in a hidden iframe and periodically refresh that frame. However developers should be aware of the following limitation with this setting: attempting to access certain object types including `Date` or `function` objects generated from such an evaluation can subsequently lead to a JavaScript error with the message `"Can't execute code from a freed script"`.

This workaround therefore may not be suitable for all transactions or dataSources within a given application.

This property may also be specified for specific [RPCRequests](RPCRequest.md#attr-rpcrequestallowie9leak).

This issue is discussed further in the online [SmartClient FAQ](http://forums.smartclient.com/showthread.php?t=8159).

**Flags**: IRWA

---
## ClassAttr: RPCManager.promptDelay

### Description
If the request is configured to block user interactivity ([RPCRequest.showPrompt](RPCRequest.md#attr-rpcrequestshowprompt)), this property controls the delay in milliseconds before a visual indication is shown to the user that interactivity is blocked.

Studies have shown that users will perceive a short operation as occurring faster if they are not shown a wait cursor, throbber or other busy indicator, but that a busy indicator _must_ appear after a briefy delay or the user will perceive the system as broken or hung.

Note that, regardless of this setting, interactivity is immediately blocked if showPrompt is true, since the purpose of blocking is to prevent duplicate requests or prevent interacting with components while they are in transition. This setting controls only how fast a visual indication of blocking is shown.

### Groups

- rpcPrompt

### See Also

- [RPCManager.showPrompt](#classattr-rpcmanagershowprompt)
- [RPCRequest.promptDelay](RPCRequest.md#attr-rpcrequestpromptdelay)

**Flags**: IRWA

---
## ClassAttr: RPCManager.httpProxyURL

### Description
The URL to use for proxied requests. This is a global system-wide setting.

### See Also

- [RPCRequest.httpProxyURL](RPCRequest.md#attr-rpcrequesthttpproxyurl)

**Flags**: IR

---
## ClassMethod: RPCManager.isScreenCached

### Description
Returns true if a screen with the given name has already been cached by a call to [RPCManager.cacheScreens](#classmethod-rpcmanagercachescreens) or similar (e.g. [RPCManager.loadProject](#classmethod-rpcmanagerloadproject)), false otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| screenName | [String](#type-string) | false | — | name of the screen |

### See Also

- [LoadScreenSettings.cacheScreen](LoadScreenSettings.md#attr-loadscreensettingscachescreen)

---
## ClassMethod: RPCManager.getTransactionDescription

### Description
Returns a brief description of the transaction in the following format for logging purposes: `"Transaction with _n_ operation(s). [dsName1.operationType; dsName2.operationType; ...]"`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| transactionNum | [Integer](../reference_2.md#type-integer) | false | — | The number of the transaction to return timing data for |

### Returns

`[String](#type-string)` — transaction description

---
## ClassMethod: RPCManager.addProcessingCompleteCallback

### Description
This method will register a callback to fire every time the processing of an RPC transaction is fully complete, including any [request-level](DSRequest.md#attr-dsrequestcallback) or [queue-level](#classmethod-rpcmanagersendqueue) user callbacks.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | false | — | Callback to fire when processing is complete. This takes a single parameter "transactionNum" |

### Returns

`[Integer](../reference_2.md#type-integer)` — Identifier for the registered callback. May be passed to [RPCManager.removeProcessingCompleteCallback](#classmethod-rpcmanagerremoveprocessingcompletecallback) to unregister this callback.

### See Also

- [RPCManager.removeProcessingCompleteCallback](#classmethod-rpcmanagerremoveprocessingcompletecallback)
- [RPCManager.getTimingData](#classmethod-rpcmanagergettimingdata)

---
## ClassMethod: RPCManager.handleError

### Description
`handleError()` will be called if [RPCResponse.status](RPCResponse.md#attr-rpcresponsestatus) is negative and [RPCRequest.willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror) was not set. It is called for both [DSResponse](DSResponse.md#class-dsresponse)s and [RPCResponse](RPCResponse.md#class-rpcresponse)s that have a non-success status. You can check whether the response is a DSResponse by checking `response.isDSResponse`.

By default `handleError()` always logs a warning. In addition, if [response.data](RPCResponse.md#attr-rpcresponsedata) was set to a String, a warning dialog will be shown to the user with response.data as the message, which allows the server to send user error messages back without writing custom client-side error handling.

To do custom error handling that is specific to a particular component or type of request, set [RPCRequest.willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror) and deal with errors in the rpcRequest.callback. To change the default system-wide error handling, override this method. Note that since `handleError()` is a class method, to override it you will call [addClassProperties()](Class.md#classmethod-classaddclassproperties) rather than addProperties(), like so:

```
     isc.RPCManager.addClassProperties({
         handleError : function (response, request) { .. custom handling .. }
     })
 
```
To invoke the default error handling in your new handler, you can simply call the method [RPCManager.runDefaultErrorHandling](#classmethod-rpcmanagerrundefaulterrorhandling).

If you're using the xmlHttpRequest [RPCRequest.transport](RPCRequest.md#attr-rpcrequesttransport), you can access the [HTTP status code](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) of the response (eg 404 Not Found or 500 Server Error) as [RPCResponse.httpResponseCode](RPCResponse.md#attr-rpcresponsehttpresponsecode).

For very advanced usage, the response.xmlHttpRequest contains the native XMLHttpRequest object used to make the request. Accessing this object is subject to possible cross-platform bugs and inconsistencies, and Isomorphic recommends that you wrap any access to the XMLHttpRequest object in a try/catch block because some browsers may throw exceptions when certain attributes of this object are accessed. For example, if you try to access XMLHttpRequest.status (for the HTTP status code) when the network cable is unpluged in Windows, you'll get an Exception in Firefox.

See the [overview of error handling](../kb_topics/errorHandling.md#kb-topic-error-handling-overview) for additional guidance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| response | [Response](#type-response) | false | — | the RPCResponse or DSResponse object returned from the server |
| request | [Request](#type-request) | false | — | the RPCRequest or DSRequest that was sent to the server |

### Groups

- errorHandling
- operations

### See Also

- [DataSource.handleError](DataSource.md#method-datasourcehandleerror)
- [RPCManager.handleTransportError](#classmethod-rpcmanagerhandletransporterror)
- [RPCManager.runDefaultErrorHandling](#classmethod-rpcmanagerrundefaulterrorhandling)

---
## ClassMethod: RPCManager.cancelQueue

### Description
Cancel a queue of requests (also called a transaction).

If a transactionId is passed, that transaction will be cancelled, otherwise, the current (not yet sent) transaction is cancelled. You can retrieve the id of the current transaction, if there is one, by calling [getQueueTransactionId()](#classmethod-rpcmanagergetqueuetransactionid) before the transaction has been sent.

Note that cancelQueue() calls [clearTransaction()](#classmethod-rpcmanagercleartransaction) and attempts to abort the request. However, note also that whilst cancelling a transaction that has already been sent will not necessarily stop the HTTP request that has been issued - this is only possible on some browsers and with some transports - it will reliably cause SmartClient to ignore any response returned by the server and not fire any callbacks that have been passed in.

Also, take into account that this method removes all queued requests from the current queue, but queueing is still active, so if you also want to disable queuing you should call [startQueue(false)](#classmethod-rpcmanagerstartqueue).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| transactionNum | [int](../reference.md#type-int) | true | — | transactionId of the queue. |

---
## ClassMethod: RPCManager.setActionURL

### Description
Setter for [RPCManager.actionURL](#classattr-rpcmanageractionurl).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| actionURL | [URL](../reference_2.md#type-url) | false | — | new actionURL |

---
## ClassMethod: RPCManager.transformRequest

### Description
Returns the data that should be sent to the [RPCManager.actionURL](#classattr-rpcmanageractionurl).

In a manner analogous to [DataSource.transformRequest](DataSource.md#method-datasourcetransformrequest), this method allows you to transform an [RPCRequest](../reference.md#object-rpcrequest), such as by adding [HTTP headers](RPCRequest.md#attr-rpcrequesthttpheaders), to ensure proper handling on the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rpcRequest | [RPCRequest](#type-rpcrequest) | false | — | the RPCRequest being processed |

### Returns

`[Any](#type-any)` — data to be sent to the actionURL

---
## ClassMethod: RPCManager.suspendTransaction

### Description
Suspends the current transaction, such that all processing of the transaction is halted, any remaining [callbacks](RPCRequest.md#attr-rpcrequestcallback) in the transaction won't fire, and the transaction can never [timeout](RPCRequest.md#attr-rpcrequesttimeout).

`suspendTransaction()` is typically used to handle total failures for an entire transaction, such as HTTP status 500, or session timeout resulting in [loginRequired()](#classmethod-rpcmanagerloginrequired) being called. In both cases the intent is to put the transaction on hold so that a transient problem can be resolved, and then the transaction can be re-sent successfully. By using suspendTransaction(), components that submitted requests never realize there was a transient failure, and so error handling logic does not have to be implemented in every component.

Generally you can only validly suspend a transaction from either [RPCManager.loginRequired](#classmethod-rpcmanagerloginrequired) or [RPCManager.handleError](#classmethod-rpcmanagerhandleerror), and in the case of `handleError()`, only when the first response in the transaction has an error. Suspending and re-sending a partially processed transaction means that some responses will be processed twice, with undefined results for requests issued automatically by UI components.

A suspended transaction must ultimately be either cleared via [RPCManager.clearTransaction](#classmethod-rpcmanagercleartransaction) or re-sent via [RPCManager.resendTransaction](#classmethod-rpcmanagerresendtransaction) or memory will be leaked.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| transaction | [Transaction Object](#type-transaction-object)|[ID](#type-id) | true | — | transaction to delay. Defaults to the current transaction if there is one |

### See Also

- [RPCManager.resendTransaction](#classmethod-rpcmanagerresendtransaction)

**Flags**: A

---
## ClassMethod: RPCManager.queueSent

### Description
This method is called by the RPCManager every time it sends a queue of requests to the server (note that if you are not using queuing, the system simply sends queues containing just one request, so this API is valid regardless).

There is no default implementation of this method; it is simply an override point. It is intended to be used by user code that needs to be notified when SmartClient sends requests to the server. Note that the list of [RPCRequest](../reference.md#object-rpcrequest)s passed to this method is strictly **read-only**.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| requests | [List of RPCRequest](#type-list-of-rpcrequest) | false | — | The queue of [RPCRequest](../reference.md#object-rpcrequest)s that was sent |

---
## ClassMethod: RPCManager.send

### Description
This method is a convenience wrapper on `RPCManager.sendRequest()` - it calls through to sendRequest().

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Any](#type-any) | false | — | data to be passed to the server |
| callback | [RPCCallback](#type-rpccallback) | true | — | method to call on RPC completion |
| requestParams | [Object](../reference.md#type-object) | true | — | object literal containing any additional properties you want to set - these will be applied to the RPCRequest object that will be auto-created for you. |

### See Also

- [RPCManager.sendRequest](#classmethod-rpcmanagersendrequest)
- [RPCRequest](../reference.md#object-rpcrequest)

---
## ClassMethod: RPCManager.getFormattedTimingData

### Description
Returns formatted text visualising the tree of timing data available from the [RPCManager.getTimingData](#classmethod-rpcmanagergettimingdata) API. Intended for use in log messages and other non-interactive, information-only settings. For more advanced usages, call `getTimingData()` and work directly with the tree structure that API returns.

Please read the `getTimingData()` documentation for some important remarks about the availability of timing data, depending on where you are calling it from. These remarks apply equally to `getFormattedTimingData()`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| transactionNum | [Integer](../reference_2.md#type-integer) | false | — | The number of the transaction to return timing data for |
| callback | [FormattedTimingDataCallback](#type-formattedtimingdatacallback) | true | — | A callback to invoke, passing the formatted timing data. This parameter is optional, but it is necessary if timing data cannot be obtained synchronously, as described in the `getTimingData()` documentation |
| operationNo | [Integer](../reference_2.md#type-integer) | true | — | Optionally, the index of a specific operation in the overall transaction. Only pass this parameter if you want to limit the returned data to a single request |
| includeClient | [boolean](../reference.md#type-boolean) | true | — | Whether to include client-side timing data. Optional defaults to true |
| includeServer | [boolean](../reference.md#type-boolean) | true | — | Whether to include server-side timing data. Optional, defaults to true |
| maxDepth | [Integer](../reference_2.md#type-integer) | true | — | The maximum depth to descend into the tree. The lowest meaningful value for this parameter is 1 - anything less will simply cause the API to return an empty string. This parameter is optional; if it not passed, we default to "no limit" |

### Returns

`[String](#type-string)` — Formatted text visualising the tree of timing data, if the timing data can be retrieved synchronously

---
## ClassMethod: RPCManager.sendProxied

### Description
Send an HTTP request to a remote host, potentially through the HttpProxy servlet installed on the SmartClient Server.

This API allows contacting services which are hosted on servers other than the origin server if the HttpProxy servlet is enabled on the SmartClient Server.

The HttpProxy will be used if the [RPCRequest.actionURL](RPCRequest.md#attr-rpcrequestactionurl) starts with "http" and uses a hostname other than "localhost" or `window.location.hostname`, or if the port number differs, or if `request.useHttpProxy` is explicitly set. Otherwise the request goes to the origin server (the server that returned the current page).

The [RPCRequest](../reference.md#object-rpcrequest) properties that will be respected when relaying requests via the HttpProxy are: [actionURL](RPCRequest.md#attr-rpcrequestactionurl), [httpMethod](RPCRequest.md#attr-rpcrequesthttpmethod), [params](RPCRequest.md#attr-rpcrequestparams), [contentType](RPCRequest.md#attr-rpcrequestcontenttype), [httpHeaders](RPCRequest.md#attr-rpcrequesthttpheaders), and [data](RPCRequest.md#attr-rpcrequestdata). In this case "data", if set, will be used as the request body for an HTTP POST.

Higher-level APIs like [DataSource](DataSource.md#class-datasource) or [WebService](WebService.md#class-webservice) call through this API, and so automatically use the HttpProxy if [DataSource.dataURL](DataSource.md#attr-datasourcedataurl) or [webService.location](WebService.md#method-webservicesetlocation) is set to a foreign server.

This API is only suitable for direct use when loading unstructured data that will not be shown in a [DataBoundComponent](../reference.md#interface-databoundcomponent). For a WSDL-described web service, use [XMLTools.loadWSDL](XMLTools.md#classmethod-xmltoolsloadwsdl) instead. For other web services, use a [DataSource](DataSource.md#class-datasource) with [dataURL](DataSource.md#attr-datasourcedataurl), and use [DataSource.transformRequest](DataSource.md#method-datasourcetransformrequest) and [DataSource.transformResponse](DataSource.md#method-datasourcetransformresponse) as necessary to form requests for the service and transform responses for display.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| request | [RPCRequest Properties](#type-rpcrequest-properties) | false | — | rpcRequest to be routed through the HttpProxy |

---
## ClassMethod: RPCManager.runDefaultErrorHandling

### Description
Runs the default error handling normally performed by [RPCManager.handleError](#classmethod-rpcmanagerhandleerror). May be called from a custom handler to achieve the default behavior if one has been installed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| response | [DSResponse](#type-dsresponse) | false | — | response the response |
| request | [DSRequest](#type-dsrequest) | false | — | request the request |

### Groups

- errorHandling
- operations

### See Also

- [RPCManager.handleError](#classmethod-rpcmanagerhandleerror)

---
## ClassMethod: RPCManager.removeProcessingCompleteCallback

### Description
Unregister the [processingComplete](#classmethod-rpcmanageraddprocessingcompletecallback) callback associated with the parameter index

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [Integer](../reference_2.md#type-integer) | false | — | The identifying index returned from [RPCManager.addProcessingCompleteCallback](#classmethod-rpcmanageraddprocessingcompletecallback) |

---
## ClassMethod: RPCManager.sendRequest

### Description
Send the passed `RPCRequest` to the server. If queuing is in effect, this queues the request instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rpcRequest | [RPCRequest Properties](#type-rpcrequest-properties) | false | — | RPCRequest to send to the server |

---
## ClassMethod: RPCManager.xmlHttpRequestAvailable

### Description
Returns true if the XMLHttpRequest object is available, false otherwise. See [platformDependencies](../kb_topics/platformDependencies.md#kb-topic-platform-dependencies) for more information on when XMLHttpRequest parser may not available and what features are impacted as a result.

### Returns

`[Boolean](#type-boolean)` — true if XMLHttpRequest is available, false otherwise.

---
## ClassMethod: RPCManager.getCurrentTransactionId

### Description
Synonym of [RPCManager.getQueueTransactionId](#classmethod-rpcmanagergetqueuetransactionid).

### Returns

`[Integer](../reference_2.md#type-integer)` — the transactionNum of the current transaction, or null

---
## ClassMethod: RPCManager.sendQueue

### Description
Send all currently queued requests to the server. You need only call this method if you are using queuing otherwise your requests are synchronously submitted to the server.

This method will do nothing and the callback will not be called if no requests have actually been queued. You can detect whether the queue is empty by calling [getQueueTransactionId()](#classmethod-rpcmanagergetqueuetransactionid).

NOTE: if you aren't the caller who first enables queuing (startQueue() returns true), you should in general avoid calling sendQueue(), because whoever was first to enable queuing may have more requests to add to the same queue.

See [RPCManager.startQueue](#classmethod-rpcmanagerstartqueue) for more information about queuing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RPCQueueCallback](#type-rpcqueuecallback) | true | — | Callback to fire when the queued operations complete. Callback will be fired with 1 parameter: `responses` an array of [DSResponse](DSResponse.md#class-dsresponse) or [RPCResponse](RPCResponse.md#class-rpcresponse) objects that were part of the transaction fired by this method. |

### See Also

- [RPCManager.send](#classmethod-rpcmanagersend)
- [RPCManager.sendRequest](#classmethod-rpcmanagersendrequest)
- [RPCManager.startQueue](#classmethod-rpcmanagerstartqueue)

---
## ClassMethod: RPCManager.getLoadProjectErrorStatus

### Description
Convenience method that returns the error status for a failed call to [RPCManager.loadProject](#classmethod-rpcmanagerloadproject). Applies the following rules:

*   reports "badCredentials" if the [RPCResponse.status](RPCResponse.md#attr-rpcresponsestatus) is `STATUS_LOGIN_REQUIRED` or `STATUS_LOGIN_INCORRECT`
*   reports "timeout" if the [RPCResponse.status](RPCResponse.md#attr-rpcresponsestatus) is `STATUS_SERVER_TIMEOUT`
*   reports "noResponseFromURL" if the [RPCResponse.httpResponseCode](RPCResponse.md#attr-rpcresponsehttpresponsecode) is 0
*   reports "badReifyServerURL" if the [RPCResponse.httpResponseCode](RPCResponse.md#attr-rpcresponsehttpresponsecode) is 404 or another code representing a transport error, such as 408 or 503
*   reports "projectNotFound" if the [RPCResponse.httpResponseCode](RPCResponse.md#attr-rpcresponsehttpresponsecode) is 500 and the [RPCResponse.httpResponseText](RPCResponse.md#attr-rpcresponsehttpresponsetext) contains the string "Unable to load any of the projects"
*   otherwise reports "servletError"

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rpcResponse | [RPCResponse](#type-rpcresponse) | false | — | server response |

### Returns

`[String](#type-string)` — the error status (null if no error)

---
## ClassMethod: RPCManager.setTimingDataEnabled

### Description
Pass `true` or `false` to switch the gathering of timing metrics on and off programmatically. The timing data thus gathered can be viewed in the "Timing" section of the [Developer Console RPC tab](../kb_topics/devConsoleRPCTab.md#kb-topic-the-developer-console-rpc-tab), or retrieved by your own code by use of the [RPCManager.getTimingData](#classmethod-rpcmanagergettimingdata) API.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| enabled | [boolean](../reference.md#type-boolean) | false | — | Whether to switch timing data on or off |

---
## ClassMethod: RPCManager.exportContent

### Description
Exports the printable representation of a set of widgets as a .pdf that is then downloaded to the user (triggering the "Save As.." dialog).

As with other exports, the resulting file can be [saved to the server filesystem](DSRequest.md#attr-dsrequestexporttofilesystem) instead of, or in addition to being downloaded to the user. See server-side docs for com.isomorphic.contentexport.PdfExport for more details on server-side processing and code samples for redirecting PDF output to a file or in-memory buffer, as well as instructions for adding additional stylesheets.

You can either pass any `Canvas` to `exportContent`, or you can pass HTML that you have retrieved by calling [Canvas.getPrintHTML](Canvas.md#method-canvasgetprinthtml). When calling `getPrintHTML()` to retrieve HTML for use with `exportContent()`, you must pass the [PrintProperties.printForExport](PrintProperties.md#attr-printpropertiesprintforexport) or [DrawPane](DrawPane.md#class-drawpane) and [FacetChart](FacetChart.md#class-facetchart) instances will not export properly.

You can use a custom skin when exporting your HTML content. To use a custom skin, add a line to [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file):

```
   skin.{skinName}.location: custom/skin
 
```
Where {skinName} is the name of your custom skin, and the value is the path to your skin resources from the application webroot.

Also, you can set the filename of the export via [DSRequest.exportFilename](DSRequest.md#attr-dsrequestexportfilename). For example:

```
 var settings = {
     exportFilename: "export" // without .pdf
     // ... other DSRequest properties
 };
 
```

In case you do not provide a filename for your export, the system will assign the default filename "export".

Requires the SmartClient server framework, but does not require use of server-based databinding - no .ds.xml files need to exist.

You can also inject a small amount of CSS from the browser via [DSRequest.exportCSS](DSRequest.md#attr-dsrequestexportcss) - this is intended primarily for switching the page size on the fly, for exceptionally wide or tall exports.

_**Note**_ that theoretically, it is possible to send custom HTML to the Smartclient server that attempts to include resources from the local server filesystem (predominantly images) and export them to PDF. To prevent this, there is a setting in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) named `contentExport.allowedResourceLocations` which lists URL/path segments used to determine what is allowed.  
It is a semicolon-separated list of path segments that identify allowed resource locations for PDF exports. If a resource is not allowed, it will not be loaded into the PDF, and a warning will be logged in the server logs. The full path of the resource is checked to contain at least one of the allowed path segments listed here. This check is performed using a crude substring search, meaning if any string in this list is a substring of the provided URL, it is allowed. There is a special placeholder "{webRoot}" that represents the web root of the application. It will be replaced with the actual web root directory at runtime. Additionally, if this setting is entirely omitted, access to the local filesystem outside of the web root directory will not be allowed. For example:

`contentExport.allowedResourceLocations:{webRoot}/skins/Tahoe/;localhost:8080/otherApp/;http://www.foo.bar`

This would allow resources from anywhere inside the "Tahoe" skin directory, any URL from "otherApp" on localhost:8080, and any URL from the specified external HTTP address.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canvas | [Canvas](#type-canvas)|[Array of Canvas[]](#type-array-of-canvas)|[HTMLString](../reference.md#type-htmlstring) | false | — | Canvas or canvas list that has exportable widgets, or an HTML fragment derived from [getPrintHTML()](Canvas.md#method-canvasgetprinthtml) |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Request properties for the export to pdf object |

---
## ClassMethod: RPCManager.createScreen

### Description
Creates a screen previously cached by a call to [RPCManager.cacheScreens](#classmethod-rpcmanagercachescreens). (Compare with [Project.createScreen](Project.md#method-projectcreatescreen) for [reify](../kb_topics/reify.md#kb-topic-reify-overview) projects.)

As with [RPCManager.loadScreen](#classmethod-rpcmanagerloadscreen), the default behavior is to prevent any global widget IDs from being established, the returned Canvas will be the outermost component of the screen, and that Canvas will provide access to other widgets in the screen via [getByLocalId()](Canvas.md#method-canvasgetbylocalid)

Alternatively, as with [RPCManager.loadScreen](#classmethod-rpcmanagerloadscreen), a list of IDs that should be allowed to become globals can be passed, allowing those widgets to be retrieved via a call to [Canvas.getById](Canvas.md#classmethod-canvasgetbyid) after the screen has been created.

If you do not pass `globals` and avoid depending on global IDs within the screen definition itself (for example, by embedding JavaScript event handlers in the screen definition that use global IDs), you can create the same screen multiple times.

Creating a screen may or may not cause it to draw, depending on current global autoDraw setting ([isc.setAutoDraw](isc.md#staticmethod-iscsetautodraw)) and any `autoDraw` settings in the screen itself.

Instead of `globals`, you may instead pass a [substitution configuration](../reference.md#object-createscreensettings) to change what classes are used to construct widgets, or subsitute existing widgets for those to be constructed, by widget ID.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| screenName | [String](#type-string) | false | — | name of the screen to create |
| settings | [CreateScreenSettings](#type-createscreensettings)|[Array of String](#type-array-of-string) | true | — | widgets to allow to take their global IDs, or a widget remap config |

### Returns

`[Canvas](#type-canvas)` — last top-level widget in the screen definition

---
## ClassMethod: RPCManager.hasCurrentTransactionQueued

### Description
Returns true if there is a current transaction (queue of requests)

This method will return false if no requests are currently queued, even if [RPCManager.startQueue](#classmethod-rpcmanagerstartqueue) has been called.

### Returns

`[Boolean](#type-boolean)` — true if there is a current transaction

---
## ClassMethod: RPCManager.resendTransaction

### Description
Resend a suspended transaction to the server. See [RPCManager.suspendTransaction](#classmethod-rpcmanagersuspendtransaction) for context.

Note that the transaction must have been previously suspended, and in particular suspended validly according to the rules described in the docs for [RPCManager.suspendTransaction](#classmethod-rpcmanagersuspendtransaction), or undefined results will occur.

You can resend **all** suspended transactions by calling [RPCManager.resendTransaction](#classmethod-rpcmanagerresendtransaction) with no arguments.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| transactionNum | [int](../reference.md#type-int) | true | — | id of the transaction to be re-sent, or null to resend all suspended transactions |

### See Also

- [relogin](../kb_topics/relogin.md#kb-topic-relogin)

**Flags**: A

---
## ClassMethod: RPCManager.exportImage

### Description
Converts an [SVG string](DrawPane.md#method-drawpanegetsvgstring) to one of several possible image formats, and can either initiate a download or return the base64-encoded image data.

Control the image format via [DSRequest.exportImageFormat](DSRequest.md#attr-dsrequestexportimageformat).

Default is to download the image (triggering the browser's save dialog). [DSRequest.exportFilename](DSRequest.md#attr-dsrequestexportfilename) can be used to control the default filename provided in the save dialog.

To instead return the data as a normal DSResponse, set [DSRequest.exportDisplay](DSRequest.md#attr-dsrequestexportdisplay) to "return". In this case the data is always base64 encoded.

Requires the SmartClient server framework, with the same set of [required .jars](../kb_topics/javaModuleDependencies.md#kb-topic-java-module-dependencies) as are required for PDF export of charts in legacy IE.

See also [DrawPane.getSvgString](DrawPane.md#method-drawpanegetsvgstring) and [DrawPane.getDataURL](DrawPane.md#method-drawpanegetdataurl).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| svgString | [String](#type-string) | false | — | XML string containing SVG data |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | request properties controlling options for export |
| callback | [ExportImageCallback](#type-exportimagecallback) | true | — | optional callback when using `exportDisplay`:"return". **Does not fire** for other `exportDisplay` modes |

---
## ClassMethod: RPCManager.loadProject

### Description
Loads projects using the [ProjectLoaderServlet](../kb_topics/servletDetails.md#kb-topic-the-core-and-optional-smartclient-servlets), reachable at [RPCManager.projectLoaderURL](#classattr-rpcmanagerprojectloaderurl), and fires the given callback after the project has been cached. When a project is loaded, all of its DataSources and screens (except where explicitly overridden by settings) are also cached in the project.

Loading of a project merely caches DataSources and screens. No screens are created automatically. To create a screen, you must call [Project.createScreen](Project.md#method-projectcreatescreen) or [Project.createStartScreen](Project.md#method-projectcreatestartscreen), which will automatically create any DataSource needed by the screen that's not already globally bound. You can also manually instantiate and globally bind (if not already bound) a screen DataSource without creating the screen, by calling [Project.getDataSource](Project.md#method-projectgetdatasource).

Note that any screen cached in a loaded project will also be bound in the global cache if no screen of that name is present there. You can create a screen from the global cache using [RPCManager.createScreen](#classmethod-rpcmanagercreatescreen).

When projects are cached, they're made available via [Project.get](Project.md#classmethod-projectget). To remove a cached project, and release storage for its cached screens and DataSources, simply call [Project.destroy](Project.md#method-projectdestroy).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| projectNames | [String](#type-string) | false | — | Comma-separated string containing the names of project(s) to load. |
| callback | [LoadProjectCallback](#type-loadprojectcallback) | false | — | Callback for notification of completion of project(s) loaded and screens cached. |
| settings | [LoadProjectSettings](#type-loadprojectsettings) | false | — | Settings applicable to the loadProject operation. |

---
## ClassMethod: RPCManager.getTimingData

### Description
Returns timing data gathered for the transaction number passed in. The timing data is an instance of [the SmartClient Tree class](Tree.md#class-tree), where parent nodes encapsulate the timings of their descendants. This timing data is what drives the "Timing" view of the [Developer Console RPC tab](../kb_topics/devConsoleRPCTab.md#kb-topic-the-developer-console-rpc-tab). Note, the returned `Tree` has [modelType](Tree.md#attr-treemodeltype) "children", so it can easily be traversed manually by simply following the nodes' "children" property recursively from the tree's "root" element.

Each node in the tree contains the following properties:

| name | A descriptive name |
|---|---|
| start | The start time, in milliseconds since the epoch, recorded by either the client or the server, depending on where this data was gathered. See the important notes at the bottom of the [Developer Console RPC](../kb_topics/devConsoleRPCTab.md#kb-topic-the-developer-console-rpc-tab) article regarding the relevance of the start and end time properties |
| end | The end time, in milliseconds since the epoch. See start, above |
| elapsed | The elapsed time in milliseconds for this operation |
| children | The list of this node's direct children, if it has any |

Note, if you call `getTimingData()` directly from a [DSRequest callback](DSRequest.md#attr-dsrequestcallback) or [queue callback](#classmethod-rpcmanagersendqueue), the timing data will be incomplete, because the queue at that point is incomplete (user callback processing is part of the processing that is being measured). To get around this, you can either move your `getTimingData()` call to thread-end by calling it on a 0ms delay:

```
    isc.RPCManager.sendQueue(function(data) {
        // Don't call getTimingData() directly - hang it on a timer
        isc.Timer.setTimeout(function() {
            var timingData = isc.RPCManager.getTimingData(data[0].transactionNum);
            // Process data here...
        }, 0);
    }); 
```

Alternatively, you can move your `getTimingData()` call into a "processing complete" callback, and register it with the [RPCManager.addProcessingCompleteCallback](#classmethod-rpcmanageraddprocessingcompletecallback) API. Processing complete callbacks fire when the transaction is fully complete, including any user callbacks.

Also note, if you are using the [Developer Console](../kb_topics/debugging.md#kb-topic-debugging), timing data may not be available synchronously from your application code, so you will have to implement a callback function and pass it as the second parameter. This is inconvenient, but it is a browser restriction that we have no control over.

If you call `getTimingData()` from your queue callback on a 0ms delay, or using a processing complete callback, as described above, the synchronous call is likely to work. If you introduce any kind of delay, or call `getTimingData()` in a way that is not synchronized with the transaction - for example, periodically on a timer, or in response to some user action - the synchronous call is likely to return an error message stating that the timing data is unavailable synchronously, and you should provide a callback. Again, all of this applies only if you have the SmartClient Developer Console open (and it applies equally to [getFormattedTimingData()](#classmethod-rpcmanagergetformattedtimingdata)).

Here is an example of how to provide a callback to the function:

```
    isc.RPCManager.getTimingData(myTransactionNum, function(retval) {
        var root = retval.root;
        // Whatever processing of the timing data is required...
    }, ... optional params if required ...);
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| transactionNum | [Integer](../reference_2.md#type-integer) | false | — | The number of the transaction to return timing data for |
| callback | [TimingDataCallback](#type-timingdatacallback) | true | — | A callback to invoke, passing the timing data object tree. This parameter is optional, but it is necessary if timing data cannot be obtained synchronously, as described above |
| operationNo | [Integer](../reference_2.md#type-integer) | true | — | Optionally, the index of a specific operation in the overall transaction. Only pass this parameter if you want to limit the returned data to a single request |
| includeClient | [boolean](../reference.md#type-boolean) | true | — | Whether to include client-side timing data. Optional defaults to true |
| includeServer | [boolean](../reference.md#type-boolean) | true | — | Whether to include server-side timing data. Optional, defaults to true |

### Returns

`[Object](../reference.md#type-object)` — the tree of timing data, as described in the above documentation

### See Also

- [RPCManager.getFormattedTimingData](#classmethod-rpcmanagergetformattedtimingdata)

---
## ClassMethod: RPCManager.getQueueTransactionId

### Description
Returns the id of the current transaction (a queue of requests).

This method will return null if no requests are currently queued, even if [RPCManager.startQueue](#classmethod-rpcmanagerstartqueue) has been called.

### Returns

`[Integer](../reference_2.md#type-integer)` — the transactionNum of the current transaction, or null

---
## ClassMethod: RPCManager.cacheScreens

### Description
Loads the definitions of a set of screens saved in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) format, using the [ScreenLoaderServlet](../kb_topics/servletDetails.md#kb-topic-the-core-and-optional-smartclient-servlets).

Unlike [RPCManager.loadScreen](#classmethod-rpcmanagerloadscreen), `cacheScreens()` does not cause any UI components to be created or drawn, it just loads the definitions of the screens. This allows a subsequent, synchronous call to [RPCManager.createScreen](#classmethod-rpcmanagercreatescreen) to create the actual screen, rather than contacting the `ScreenLoader` servlet and showing a loading message.

If you're using [reify](../kb_topics/reify.md#kb-topic-reify-overview), and the screens are part of a [Project](Project.md#class-project), you should use [Reify.loadProject](#method-reifyloadproject) to cache the screens instead of this method. See help topic [Reify For Developers](../kb_topics/reifyForDevelopers.md#kb-topic-reify-for-developers) for an overview of how you can integrate Reify into your development process.

See [RPCManager.loadScreen](#classmethod-rpcmanagerloadscreen) for the meaning of the `locale` parameter.

Calling `cacheScreens` twice with the same screenName will re-load the definition of that screen from the server such that subsequent calls to `createScreen()` will use the new definition.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| screenName | [Array of String](#type-array-of-string) | false | — | name of the screens to cache |
| callback | [Function](#type-function) | false | — | callback for notification of screens being successfully cached |
| locale | [String](#type-string) | true | — | The name of a locale to use for resolving i18n tags in the component XML of the screen |
| requestProperties | [RPCRequest Properties](#type-rpcrequest-properties) | true | — | optional properties for the request |

### See Also

- [reify](../kb_topics/reify.md#kb-topic-reify-overview)
- [Project](Project.md#class-project)

---
## ClassMethod: RPCManager.requestsArePending

### Description
Returns whether there are any pending RPC requests.

### Returns

`[Boolean](#type-boolean)` — true if one or more RPC requests are pending, false otherwise.

---
## ClassMethod: RPCManager.loadScreen

### Description
Loads a screen saved in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) format, using the [ScreenLoaderServlet](../kb_topics/servletDetails.md#kb-topic-the-core-and-optional-smartclient-servlets).

The ScreenLoaderServlet will look for a file named _screenName_.ui.xml in the directory given by the "project.ui" setting, which defaults _webroot_/shared/ui and can be configured in [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file).

The `screen` provided by the callback will be the outermost component if your loaded screen consists of a hierarchy of widgets all contained under one parent (which is true of any screens created in Reify).

If you have multiple widget hierarchies in your screen, the `screen` returned will be the last top-level component created.

By default, components in the loaded screens that have [global IDs](Canvas.md#attr-canvasid) will not actually be allowed to take those global IDs - instead, only widgets that have one of the global IDs passed as the `globals` parameter will actually receive their global IDs. To override this behavior, pass the special value [RPCManager.ALL_GLOBALS](#classattr-rpcmanagerall_globals) for the `globals` parameter.

When globals are being suppressed, the `screen` available in the callback will provide access to widgets that did not receive their global IDs via [Canvas.getByLocalId](Canvas.md#method-canvasgetbylocalid), and the `suppressedGlobals` available in the callback will be a mapping from suppressed global ID to the widget or other component that would have used that global ID if globals were not suppressed. In addition, any other `Canvas` loaded with the screen also provides access to any suppressed globals from the screen via `getByLocalId()`.

To load multiple screens at once, use [Reify.loadProject](#method-reifyloadproject) if the screens are part of a [Project](Project.md#class-project), otherwise use [RPCManager.cacheScreens](#classmethod-rpcmanagercachescreens).

Components in the screen will default to having [Canvas.autoDraw](Canvas.md#attr-canvasautodraw) set to false. This may be overridden by setting the [RPCRequest.suppressAutoDraw](RPCRequest.md#attr-rpcrequestsuppressautodraw) attribute explicitly to `false` on the request properties object.

You can optionally provide a locale name to use when resolving any i18n tags in the screen's component XML. If you do not supply this, the locale will be derived from the servlet API, and so will generally be a locale appropriate to the client's operating system settings. Only provide a locale manually if you have a special requirement that requires the user's operating system locale to be overridden in your application. If you provide a locale name, it should be of the form "xx" or "xx\_YY", where "xx" is a valid language code and "YY" is a valid country code. For example, "fr" or "en\_GB".

This API assumes the ScreenLoaderServlet is installed at the default location - to use a different location, use the `requestProperties` parameter to specify a different URL via [RPCRequest.actionURL](RPCRequest.md#attr-rpcrequestactionurl). The `requestProperties` parameter can also be used to pass additional params to a custom ScreenLoaderServlet - see the "Dynamic Component XML" section of the [Component XML overview](../kb_topics/componentXML.md#kb-topic-component-xml).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| screenName | [String](#type-string) | false | — | name of the screen to load |
| callback | [LoadScreenCallback](#type-loadscreencallback) | false | — | callback for notification of screen being loaded |
| settings | [Array of String](#type-array-of-string)|[LoadScreenSettings](#type-loadscreensettings) | true | — | widgets to allow to take their global IDs, or load settings |
| locale | [String](#type-string) | true | — | The name of a locale to use for resolving i18n tags in the component XML of the screen |
| requestProperties | [RPCRequest Properties](#type-rpcrequest-properties) | true | — | optional properties for the request |
| missingDSIsNotFatal | [Boolean](#type-boolean) | true | — | If true, server logic does not crash out if it cannot load a DataSource specified in the screen definition. Instead, a stub DataSource is returned, which consists of nothing except the ID and an `unableToLoad` flag, which client-side code can use to determine that the DataSource could not be loaded on the server. Optional, defaults to false (ie, a missing DataSource causes a crash by default) |

### See Also

- [Project](Project.md#class-project)
- [reify](../kb_topics/reify.md#kb-topic-reify-overview)

---
## ClassMethod: RPCManager.startQueue

### Description
Start queuing [DSRequests](../reference_2.md#object-dsrequest) and [RPCRequests](../reference.md#object-rpcrequest) system-wide, for later sending when RPCManager.sendQueue() is called, at which time all queued requests will be sent as a single, combined HTTP request.

Combining requests via queuing:

*   allows the server to implement transactional saving when multiple records are affected by actions in the UI
*   can reduce overhead by combining related requests, avoiding the use of multiple network connections, redundant authentication checks, and other redundant resource allocations that would otherwise happen if requests were processed separately
*   can simplify application logic that otherwise has to deal with multiple outstanding server requests that might complete in any order

Queuing is used automatically by many, many framework features, including multi-row grid editing ([Grid Mass Editing](ListGrid_1.md#attr-listgridautosaveedits)), *multi-row drag & drop*, [data paging for large trees](ResultTree.md#attr-resulttreefetchmode), ["serverCustom" validators](../reference.md#type-validatortype), *Master-Detail saves*, [OLAP / datacube functionalty](CubeGrid.md#class-cubegrid), and many others.

Queuing also has subtler architectural benefits in terms of building reusable services - see the QuickStart Guide sections on Queuing for details.

For all the reasons given above, it's extremely important to use DataSources that can support queuing. Queuing is automatically supported when using server-based DataSources with the SmartClient Server Framework, and is supported by [RestDataSource](RestDataSource.md#class-restdatasource).

**Order of Execution**

When the SmartClient Server framework receives a queued request, it will process all requests, in order, in a single thread, before any response is sent to the client. All client-side actions related to queued requests, such as [callbacks firing](ListGrid_2.md#method-listgridfetchdata) on completion, likewise happen in queue order, after all server-side processing has taken place.

Therefore when using queuing you can use the callback argument of [RPCManager.sendQueue](#classmethod-rpcmanagersendqueue) to detect that all operations have completed, which is much simpler than the logic needed to track multiple asynchronous operations and wait for all to complete.

**Nested Queuing**

In some cases you may wish to combine requests being sent by application logic with queued requests automatically sent by components. For example, you may want to call [ListGrid.saveAllEdits](ListGrid_2.md#method-listgridsavealledits) but also add an additional request to the same queue.

To do this, just call `startQueue()` before `saveAllEdits()` (or whatever other API would also normally perform a queued request), then call `sendQueue()`. Framework features that use queuing will automatically notice that you have already started a queue, and will not automatically call `sendQueue()` in this case. You can implement the same behavior in your own reusable components by checking the return value of `startQueue()`, which tells you whether queuing is already active.

**Requests that can't be queued**

When using queuing, all requests in a given queue must go to the same [RPCRequest.actionURL](RPCRequest.md#attr-rpcrequestactionurl) and use the same transport (XMLHttp or frames). If a request specifies a different actionURL or transport than that of the requests currently on the queue, it will be sent to the server separately, ahead of the queue, and a warning will be logged to the Developer Console.

Due to browser security restrictions, at most one request with a [file\\n upload](../kb_topics/upload.md#kb-topic-uploading-files) can be sent in a queue. If you attempt to add another, the existing queue will be sent immediately, logging a warning, and queueing restarted for the new request.

Note that whenever requests are not sent in a single queue, order is not guaranteed, and the callback provided to [RPCManager.sendQueue](#classmethod-rpcmanagersendqueue) at the end of your transaction may fire before requests not sent in the final queue have completed.

**Implementing your own Queuing**

If you are in the rare situation that:

*   you can't use the SmartClient Server framework
*   the server you are integrating with some pre-existing support for combining operations in a flexible way, similar to queuing
*   you are totally unable to implement the RestDataSource protocol for this server, even through approaches such as adding it as an additional service while leaving the original services unchanged, or going through an intermediate server

.. then you can implement a crude version of the built-in queuing feature by using [dataProtocol:"clientCustom"](DataSource.md#attr-datasourcedataprotocol) to avoid HTTP requests being immediately sent when a DataSource executes. In outline:

*   create an API similar to `startQueue()` for managing a global setting reflecting whether your special queuing system is active. Your DataSources should check for this global setting in [DataSource.transformRequest](DataSource.md#method-datasourcetransformrequest), and, if queuing is active, store the request you received in [DataSource.transformRequest](DataSource.md#method-datasourcetransformrequest) in memory, for example in an Array
*   implement your own equivalent of `RPCManager.sendQueue()` which sends an HTTP request representing your combined requests, then once you receive your combined response, call [DataSource.processResponse](DataSource.md#method-datasourceprocessresponse) for each request.

Note that attempting to integrate with `RPCManager`'s queuing system doesn't really make sense - `RPCManager` won't be aware of your separate, special queue of requests, so will reject calls to `sendQueue()` since RPCManager's queue is empty. Similarly, enabling queuing on `RPCManager` may cause inadvertent queuing of unrelated requests you did not intend to queue. Maintaining your own separate notion of whether queuing is active is simpler and less error prone.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| shouldQueue | [boolean](../reference.md#type-boolean) | true | — | whether queuing should be enabled, default true. Passing false will disable queuing but not send the queue yet, so that any queued requests will be sent along with the next send()/sendRequest() |

### Returns

`[boolean](../reference.md#type-boolean)` — whether queuing was already enabled before we called.

### See Also

- [RPCManager.sendQueue](#classmethod-rpcmanagersendqueue)

---
## ClassMethod: RPCManager.clearTransaction

### Description
Erase all client-side record of a transaction, such that any response from the server will be ignored.

A transaction means a batch of one or more RPCRequests that have already been sent to the server via [RPCManager.sendQueue](#classmethod-rpcmanagersendqueue).

You can retrieve the id of the current transaction, if there is one, by [getQueueTransactionId()](#classmethod-rpcmanagergetqueuetransactionid) before the transaction is sent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| transactionNum | [int](../reference.md#type-int) | false | — | id of the transaction to be cleared |

### See Also

- [relogin](../kb_topics/relogin.md#kb-topic-relogin)

**Flags**: A

---
## ClassMethod: RPCManager.handleTransportError

### Description
`handleTransportError()` handles server error responses for submitted transactions. When the server responds to a submitted transaction with an HTTP error code this method will be called before any individual response callbacks are fired, regardless of whether [RPCRequest.willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror) was specified on the submitted request\[s\].

This provides the developer with an opportunity to handle a server error by (for example) suspending and resubmitting the transaction before any other handling occurs.

The default implementation takes no action - by default transport errors are handled via [RPCManager.handleError](#classmethod-rpcmanagerhandleerror), or by the standard request callback methods, depending on request.willHandleError. To perform custom handing for transport errors this classMethod may be overridden as follows

```
     isc.RPCManager.addClassProperties({
         handleTransportError : function (transactionNum, status, httpResponseCode, httpResponseText) 
         {
                .. custom handling .. 
         }
     })
 
```

Return an explicit `false` from this method to cancel default error handling, so that [RPCManager.handleError](#classmethod-rpcmanagerhandleerror) is not called for any [DSResponse](DSResponse.md#class-dsresponse) in this transaction.

Note: This method only applies to operations submitted via [XMLHttpRequest](../reference.md#type-rpctransport) - it is not possible to provide similar error handling for other transports.

See the [overview of error handling](../kb_topics/errorHandling.md#kb-topic-error-handling-overview) for additional guidance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| transactionNum | [int](../reference.md#type-int) | false | — | The submitted client-server transaction number |
| status | [Integer](../reference_2.md#type-integer) | false | — | The RPCResponse status code |
| httpResponseCode | [Integer](../reference_2.md#type-integer) | false | — | The HTTP Response code reported by the server |
| httpResponseText | [String](#type-string) | false | — | The raw HTTP Response text |

### Returns

`[Boolean](#type-boolean)` — false to cancel default error handling

### Groups

- errorHandling

### See Also

- [RPCManager.handleError](#classmethod-rpcmanagerhandleerror)

---
## ClassMethod: RPCManager.loginRequired

### Description
Called when a session timeout is encountered while trying to do a background RPC. See [Relogin](../kb_topics/relogin.md#kb-topic-relogin).

The transaction with the passed `transactionId` is suspended, and should either be [cleared](#classmethod-rpcmanagercleartransaction) or [resent](#classmethod-rpcmanagerresendtransaction) after the user has been re-authenticated.

The `rpcRequest` parameter can be used to determine whether the suspended transaction can simply be dropped (eg, it's periodic polling request).

The `rpcResponse` parameter has rpcResponse.data set to the raw text of the response that triggered `loginRequired()`. Some very advanced relogin strategies may need to inspect the raw response to get information needed for re-authentication.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| transactionNum | [int](../reference.md#type-int) | false | — | id of the transaction |
| rpcRequest | [RPCRequest](#type-rpcrequest) | false | — | first RPCRequest of the transaction |
| rpcResponse | [RPCResponse](#type-rpcresponse) | false | — | RPCResponse containing the session timeout response that caused loginRequired() to be invoked |

### Groups

- relogin

---
## ClassMethod: RPCManager.getLoadProjectErrorMessage

### Description
Convenience method that returns a message describing the error for a failed call to [RPCManager.loadProject](#classmethod-rpcmanagerloadproject). Calls [RPCManager.getLoadProjectErrorStatus](#classmethod-rpcmanagergetloadprojecterrorstatus).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rpcResponse | [RPCResponse](#type-rpcresponse) | false | — | server response |

### Returns

`[String](#type-string)` — the error message (null if no error)

---
