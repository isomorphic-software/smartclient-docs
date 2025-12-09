# RPCResponse Documentation

[← Back to API Index](../reference.md)

---

## Class: RPCResponse

### Description
Encapsulates an RPC response from the server. Instances of this class are automatically created and optionally passed to you in the callback you specify as part of your RPCRequest.

### See Also

- [RPCRequest](../reference.md#object-rpcrequest)
- [Callbacks.RPCCallback](Callbacks.md#method-callbacksrpccallback)

---
## ClassAttr: RPCResponse.STATUS_LOGIN_SUCCESS

### Description
Indicates that the login succeeded.

### Groups

- statusCodes
- constant

### See Also

- [RPCRequest](../reference.md#object-rpcrequest)

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_MAX_FILE_SIZE_EXCEEDED

### Description
Indicates that an uploaded file's size exceeded the maximum file size allowed.

### Groups

- statusCodes
- constant

### See Also

- [RPCResponse.STATUS_FILE_REQUIRED_ERROR](#classattr-rpcresponsestatus_file_required_error)
- [RPCRequest](../reference.md#object-rpcrequest)

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_MAX_LOGIN_ATTEMPTS_EXCEEDED

### Description
Indicates that too many authentication attempts have been made and the server refuses to accept any more login attempts.

### Groups

- statusCodes
- constant

### See Also

- [RPCRequest](../reference.md#object-rpcrequest)

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_AUTHORIZATION_FAILURE

### Description
Indicates a [Declarative Security](../kb_topics/declarativeSecurity.md#kb-topic-declarative-security) failure on the server. See the error handling section in [RPCManager documentation](RPCManager.md#class-rpcmanager) for more information.

### Groups

- statusCodes
- constant

### See Also

- [RPCRequest](../reference.md#object-rpcrequest)

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_REQUIRED_CRITERIA_MISSING

### Description
Indicates that an operation binding configured to require [OperationBinding.requiredCriterion](OperationBinding.md#attr-operationbindingrequiredcriterion) has received none.

### Groups

- statusCodes
- constant

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_UPDATE_WITHOUT_PK_ERROR

### Description
Indicates that the client attempted an update or remove operation without providing primary key field(s)

### Groups

- statusCodes
- constant

### See Also

- [RPCRequest](../reference.md#object-rpcrequest)

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_MAX_POST_SIZE_EXCEEDED

### Description
Indicates that the total size of the data sent to the server was more than the server is configured to allow. Most servers limit the post size to prevent out of memory style attack vectors that push a bunch of data at the server. Apache Tomcat, for example, is pre-configured to limit post size to 2mb, where the default max post-size in Jetty, used by default in Eclipse, is just 200k.

On internal networks, these limits can typically be safely raised or removed. With Tomcat, for example, you can remove the post limit by specifying the following attribute on the `<Connector>` element in conf/server.xml:  

```
 maxPostSize="-1"
 
```

In Jetty, you can update or create war/WEB-INF/jetty-web.xml, adding a section like this

```
 <Configure class="org.eclipse.jetty.webapp.WebAppContext"/>
     <Set name="maxFormContentSize">2000000</Set>
 </Configure>
 
```
**NOTE**: this status code is used whenever the server framework receives a request where the POST data has been removed, however, there are other possible causes, including:

*   security software installed on the server or network that erroneously detects some kind of exploit attempt, if its behavior is to just strip the POST data but allow the rest of the request through (SiteMinder is one product known to do this)
*   incorrectly written filter servlets that drop POST'd data

### Groups

- statusCodes
- constant

### See Also

- [RPCRequest](../reference.md#object-rpcrequest)

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_CRITERIA_REQUIRED_ERROR

### Description
—

### Groups

- statusCodes
- constant

**Deprecated**

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_UNKNOWN_HOST_ERROR

### Description
This response code only occurs when using the HTTP proxy. It is issued by the proxy servlet when the target host is unknown (ie, cannot be resolved through DNS). This response probably indicates that you are attempting to contact a nonexistent server (though it might mean that you have DNS problems).

### Groups

- statusCodes
- constant

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_LOGIN_INCORRECT

### Description
Indicates that the RPC has been intercepted by an authenticator that requires the user to log in.

### Groups

- statusCodes
- constant

### See Also

- [RPCRequest](../reference.md#object-rpcrequest)

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_OFFLINE

### Description
Indicates that the browser is currently offline, and that we do not hold a cached response for the request.

### Groups

- statusCodes
- constant
- offlineGroup

### See Also

- [RPCRequest](../reference.md#object-rpcrequest)

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_SUCCESS

### Description
Indicates successful completion of the request. This is the default status and is automatically used by the RPCResponse on the server unless you override it with setStatus().  
  
See the error handling section in [RPCManager documentation](RPCManager.md#class-rpcmanager) for more information.

### Groups

- statusCodes
- constant

### See Also

- [RPCRequest](../reference.md#object-rpcrequest)

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_FAILURE

### Description
Indicates a generic failure on the server. See the error handling section in [RPCManager documentation](RPCManager.md#class-rpcmanager) for more information.

### Groups

- statusCodes
- constant

### See Also

- [RPCRequest](../reference.md#object-rpcrequest)

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_TRANSPORT_ERROR

### Description
This response code is usable only with the XMLHttpRequest transport and indicates that the server returned an HTTP response code outside the range 200-299 (all of these statuses indicate success, but ordinarily only 200 is used). To get the actual response code, you can query rpcResponse.httpResponseCode in your callback.

Note that currently this error code will never occur for the `hiddenFrame` transport - instead, use [RPCResponse.STATUS_SERVER_TIMEOUT](#classattr-rpcresponsestatus_server_timeout) to detect `hiddenFrame` transport errors.

### Groups

- statusCodes
- constant

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_FILE_REQUIRED_ERROR

### Description
Indicates that an empty file was uploaded for a required 'binary' field.

### Groups

- statusCodes
- constant

### See Also

- [RPCResponse.STATUS_MAX_FILE_SIZE_EXCEEDED](#classattr-rpcresponsestatus_max_file_size_exceeded)

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_TRANSACTION_FAILED

### Description
Indicates that the request was either never attempted or was rolled back, because automatic or user transactions are in force and another request in the same transaction failed. Note that the request(s) that actually failed will have a code specific to the failure; it is only the requests that would otherwise have succeeded that are marked with this failure code.

### Groups

- statusCodes
- constant

### See Also

- [RPCRequest](../reference.md#object-rpcrequest)

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_SERVER_TIMEOUT

### Description
Indicates a request timed out with no server response.

This is a client-only error code - never sent by the server (since it's the server that times out).

NOTE that if using `hiddenFrame` as the transport (not the default), a malformed response such as a "500 Server Error" or 404 errors will be reported as a timeout.

### Groups

- statusCodes
- constant

**Flags**: R

---
## ClassAttr: RPCResponse.INVALID_RESPONSE_FORMAT

### Description
Indicates that a response with invalid format has been received from server. If the datasource is using "iscServer" dataFormat, this means that the response is not recognized as a valid ISC frame.

One possible cause for this error can be the reception of a RestDataSource JSON response that lacks a valid [RestDataSource.jsonPrefix](RestDataSource.md#attr-restdatasourcejsonprefix) and/or [RestDataSource.jsonSuffix](RestDataSource.md#attr-restdatasourcejsonsuffix)

If it is using "xml" or "json" dataFormat, the response could not be parsed as XML or JSON.

### Groups

- statusCodes
- constant

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_CONNECTION_RESET_ERROR

### Description
This response code only occurs when using the HTTP proxy. It is issued by the proxy servlet when the attempt to contact the target server results in a Java SocketException. This response probably indicates that the target server is currently down.

### Groups

- statusCodes
- constant

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_VALIDATION_ERROR

### Description
Indicates a validation failure on the server. See the error handling section in [RPCManager documentation](RPCManager.md#class-rpcmanager) for more information.

### Groups

- statusCodes
- constant

### See Also

- [RPCRequest](../reference.md#object-rpcrequest)

**Flags**: R

---
## ClassAttr: RPCResponse.STATUS_LOGIN_REQUIRED

### Description
Indicates that a login is required before this RPCRequest can proceed.

Applications do not directly set this status code, instead, to trigger the relogin flow, return the loginRequiredMarker in the response sent by your server when login is required. See the [Relogin Overview](../kb_topics/relogin.md#kb-topic-relogin) for details.

### Groups

- statusCodes
- constant

### See Also

- [RPCRequest](../reference.md#object-rpcrequest)

**Flags**: R

---
## Attr: RPCResponse.clientContext

### Description
The [RPCRequest.clientContext](RPCRequest.md#attr-rpcrequestclientcontext) object as set on the [RPCRequest](../reference.md#object-rpcrequest).

### See Also

- [RPCRequest.clientContext](RPCRequest.md#attr-rpcrequestclientcontext)

**Flags**: R

---
## Attr: RPCResponse.httpResponseText

### Description
The actual text of the HTTP response. Only available when the default [RPCTransport](../reference.md#type-rpctransport) "xmlHttpRequest" transport is in use,

**Flags**: R

---
## Attr: RPCResponse.status

### Description
Status code for this response. Status codes less than zero are considered errors by the RPCManager, those greater than or equal to zero are considered successes. Please see the error handling section the [RPCManager docs](RPCManager.md#class-rpcmanager) for more information on what the RPCManager does with the status code and how you can override this behavior.

When using the SmartClient server you can set the rpcResponse.status by calling the server-side method RPCResponse.setStatus().

When not using the SmartClient server, the RPCManager makes no assumptions about the structure of the response, so the status code just reflects the [RPCResponse.httpResponseCode](#attr-rpcresponsehttpresponsecode): status will be [STATUS\_TRANSPORT\_ERROR](#classattr-rpcresponsestatus_transport_error) if an HTTP-level error occurred such as "500 server error". If you have a status code you need to transmit you can simply embed it in the response (as part of [RPCResponse.data](#attr-rpcresponsedata)) and interpret it from the callback.

With or without the SmartClient server, the [relogin](../kb_topics/relogin.md#kb-topic-relogin) status codes (such as [RPCResponse.STATUS_LOGIN_REQUIRED](#classattr-rpcresponsestatus_login_required)) are triggered whenever special markers, such as the loginRequiredMarker, appear in the body of the response. See the [Relogin\\n Overview](../kb_topics/relogin.md#kb-topic-relogin) for details.

### See Also

- [RPCRequest.reportDownloadErrorsAsDocuments](RPCRequest.md#attr-rpcrequestreportdownloaderrorsasdocuments)

**Flags**: IR

---
## Attr: RPCResponse.httpHeaders

### Description
HTTP headers returned by the server as a map from header name to header value.

Headers are available only when the default [RPCTransport](../reference.md#type-rpctransport) "xmlHttpRequest" is in use, and browsers may limit access to headers for cross-domain requests or in other security-sensitive scenarios.

**Flags**: R

---
## Attr: RPCResponse.data

### Description
The data sent by the server.

When communicating with the SmartClient server, rpcResponse.data is the data passed to the server-side method RPCResponse.setData() by your Java code. This data is translated into JavaScript objects by the rules described under [RPCRequest.data](RPCRequest.md#attr-rpcrequestdata).

When not communicating with the SmartClient server rpcResponse.data contains the raw HTTP response body. See [RPCRequest.useSimpleHttp](RPCRequest.md#attr-rpcrequestusesimplehttp), [RPCRequest.serverOutputAsString](RPCRequest.md#attr-rpcrequestserveroutputasstring), [RPCRequest.evalResult](RPCRequest.md#attr-rpcrequestevalresult) for details.

**Flags**: R

---
## Attr: RPCResponse.httpResponseCode

### Description
This attribute (available when using the the `xmlHttpRequest` transport) contains the HTTP response code sent by the server.

Note that this is different from [RPCResponse.status](#attr-rpcresponsestatus) - that attribute is used to indicate a status code for the RPC itself whereas httpResponseCode is the raw HTTP response code for the HTTP request that contained the RPCRequest.

This feature relies on the XMLHttpRequest object which can be disabled by end-users in some supported browsers. See [platformDependencies](../kb_topics/platformDependencies.md#kb-topic-platform-dependencies) for more information.

If you're using this attribute, you'll typically want to avoid the default error handling response of RPCManager. To do so, set [RPCRequest.willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror) to `true`.

**Flags**: R

---
## Attr: RPCResponse.transactionNum

### Description
ID of the transaction sent to the server via [RPCManager.sendQueue](RPCManager.md#classmethod-rpcmanagersendqueue) containing the [RPCRequest](../reference.md#object-rpcrequest) associated with this response.

**Flags**: R

---
## ClassMethod: RPCResponse.create

### Description
RPCResponses shouldn't be created directly. Instances of this class are automatically created and optionally passed to you in the callback you specify as part of your [RPCRequest](../reference.md#object-rpcrequest).

---
