# Error Handling Overview

[← Back to API Index](../reference.md)

---

## KB Topic: Error Handling Overview

### Description
[RPCResponse](../classes/RPCResponse.md#class-rpcresponse) and [DSResponse](../classes/DSResponse.md#class-dsresponse) objects have an integer status field that the RPCManager inspects when the response is received from the server. If the value of this field is less than zero, the request is considered to have failed. Otherwise it is considered to have succeeded. This value is settable via the setStatus() method call on the server-side DSResponse and RPCResponse objects.

Errors in a SmartClient application fall into two main categories:

*   Validation errors, which arise as a result of rules in the application's business logic being broken. These are part of the normal operation of the system. A response with validation errors has a status of [RPCResponse.STATUS_VALIDATION_ERROR](../classes/RPCResponse.md#classattr-rpcresponsestatus_validation_error)
*   Unrecoverable errors, which are errors with the system itself. These are not part of the normal operation of the system

**Validation errors** occur when an [add](../classes/DataSource.md#method-datasourceadddata), or [update](../classes/DataSource.md#method-datasourceupdatedata) operation contains values that do not conform to [specified validation rules](../classes/DataSourceField.md#attr-datasourcefieldvalidators). When a user is [saving](../classes/DynamicForm.md#method-dynamicformsavedata) or [validating](../classes/DynamicForm.md#method-dynamicformvalidate) edits in a databound component such as a [DynamicForm](../classes/DynamicForm.md#class-dynamicform) or [canEdit:true ListGrid](../classes/ListGrid_1.md#attr-listgridcanedit), validation errors are handled by redrawing the component to display those errors to the user.

How the user sees those errors is completely configurable - for example, see the DynamicForm properties [showErrorIcons](../classes/DynamicForm.md#attr-dynamicformshowerroricons), [showErrorText](../classes/DynamicForm.md#attr-dynamicformshowerrortext), [showInlineErrors](../classes/DynamicForm.md#attr-dynamicformshowinlineerrors), and indeed most DynamicForm properties that contain the word "Error" - but the default in most skins is to highlight the field with some kind of error icon, and provide the actual error text message in a floating box when the user hovers over the field.

Note that the centralized [RPCManager.handleError](../classes/RPCManager.md#classmethod-rpcmanagerhandleerror) method (see below) will not be invoked for validation errors that occurred while editing data in a component.

Validation errors can also occur when application code directly invokes dataSource APIs to save data instead of calling [saveData()](../classes/DynamicForm.md#method-dynamicformsavedata) on an edit component. (See [DataSource.addData](../classes/DataSource.md#method-datasourceadddata), [DataSource.updateData](../classes/DataSource.md#method-datasourceupdatedata)). In this case, since there is no component in which validation errors can be displayed, [centralized error handling](../classes/RPCManager.md#classmethod-rpcmanagerhandleerror) **will** be invoked by default.

In addition to validation errors, RPCRequests and DSRequests can fail due to errors with the system itself. For example:

*   A network transport problem
*   A server-side crash
*   An update failed because a transaction was rolled back

Errors like this can either be handled centrally, or you can choose to handle them in your regular callback code. The [RPCRequest.willHandleError](../classes/RPCRequest.md#attr-rpcrequestwillhandleerror) attribute determines whether or not central error handling will be invoked.

**Centralized Error Handling**  
If the status field for a request shows a failure, and `willHandleError` has not been set to true for, [RPCManager.handleError](../classes/RPCManager.md#classmethod-rpcmanagerhandleerror) will be invoked, (unless the error was a validation error occurring while editing data in a DataBoundComponent, as discussed above).

By default, `RPCManager.handleError()` logs a warning and shows a dialog with the contents of the response's [data](../classes/RPCResponse.md#attr-rpcresponsedata) field (which is assumed to contain a meaningful description of the error that occurred). If you specified a callback in your request, it will **not** be called.

This default behavior means that any SmartClient application has a basic handling mechanism for unrecoverable errors, without any code to write.

You can customize centralized error handling at two levels:

*   Override [RPCManager.handleError](../classes/RPCManager.md#classmethod-rpcmanagerhandleerror) to provide your own error handling logic (note that customization takes place at the static class level, not per-instance)
*   Override [RPCManager.handleTransportError](../classes/RPCManager.md#classmethod-rpcmanagerhandletransporterror). This logic is called earlier than handleError, and it is called even when you are using custom error handling (discussed below). It is intended to allow your code to inspect the failed response early in the handling flow, to see if it is really unrecoverable. For example, a failure might have happened because of a temporary network problem, so resubmitting the request may be a valid thing to do to try to resolve the error. Note, as with handleError, this is a static class-level customization

**Custom Error Handling**  
As an alternative to handling errors centrally, you can handle them in your regular callback methods. To do this, specify [willHandleError](../classes/RPCRequest.md#attr-rpcrequestwillhandleerror) as a request property. When you do this, [RPCManager.handleError](../classes/RPCManager.md#classmethod-rpcmanagerhandleerror) is bypassed, and your callback is invoked as normal. If you want to invoke the default error handling logic in your callback, you can use [RPCManager.runDefaultErrorHandling](../classes/RPCManager.md#classmethod-rpcmanagerrundefaulterrorhandling)

_Note: if `handleTransportError()` was configured it **will** be called for error codes indicating a transport error even if `willHandleError` is true._

For `willHandleError:true` requests, your callback code can determine that it is in error state by inspecting the status property on the response. Any value less than zero indicates an error. See the documented status codes such as [RPCResponse.STATUS_FAILURE](../classes/RPCResponse.md#classattr-rpcresponsestatus_failure) for more information on specific error codes that may be returned by the SmartClient server.

Note that if validation failed for a save request on an edit component, setting `willHandleError` to true will cause your callback to be invoked, but the normal behavior of populating the field errors onto the form and redrawing it **also** takes place.

Note, when you are handling errors in user callbacks, an error status other than [RPCResponse.STATUS_VALIDATION_ERROR](../classes/RPCResponse.md#classattr-rpcresponsestatus_validation_error) typically indicates some sort of serious, unrecoverable error. Therefore, ensure that your error handling code does not assume that the response will be properly formed or contain particular elements.

You can specify `willHandleError` (or any other DSRequest/RPCRequest property) on a component request by providing the DSRequest Properties parameter. For example, on a [ListGrid.fetchData](../classes/ListGrid_2.md#method-listgridfetchdata):

```
     listGrid.fetchData({}, function(dsResponse, data, dsRequest) {
         if (dsResponse.status < 0) {
             // Error handling here...
         } else {
             // Normal processing here
         }
     }, {willHandleError: true});
 
```
**Error Status Codes**  
The error status codes used by the framework are documented as class variables of the [RPCResponse class](../classes/RPCResponse.md#class-rpcresponse). Status codes in the range -1 to -100 are reserved for use by the framework; if you wish to introduce new custom error statuses for your own use, avoid this range.

**Errors indicating login is required**  
Some of the framework error statuses indicate that login is required, typically because a user's HTTP session has timed out. The best way to handle this situation is to use the built-in [re-login flow](relogin.md#kb-topic-relogin) to automatically prompt users to log back in as required, and then resubmit the requests that triggered the login required response.

**Errors during a file download**

If the server responds to a [file download request](../classes/RPCRequest.md#attr-rpcrequestdownloadresult) with an error status code, standard error handling will be invoked.

This includes:

*   export operations such as [exportData()](../classes/ListGrid_2.md#method-listgridexportdata), [exportClientData()](../classes/ListGrid_2.md#method-listgridexportclientdata), or [exportContent()](../classes/RPCManager.md#classmethod-rpcmanagerexportcontent).
*   downloading of binary field values via [DataSource.downloadFile](../classes/DataSource.md#method-datasourcedownloadfile)
*   custom download operations where the [RPCRequest.downloadResult](../classes/RPCRequest.md#attr-rpcrequestdownloadresult) flag is set

However if a server encounters an error while [streaming a response](../classes/DSRequest.md#attr-dsrequeststreamresults) to the browser this will not trigger [RPCManager.handleError](../classes/RPCManager.md#classmethod-rpcmanagerhandleerror) and the centralized error handling pathway.

Therefore if you have an error condition that could arise in the middle of a file download, best practice is to:

*   _pre-validate the request_: do an ordinary, non-download request to check all common error conditions, before the request that actually initiates a download. This can avoid problems like a user who tries to download after their session has timed out, or tries to download a file that another user has deleted
*   _return a valid file containing a user-friendly error message_: for example, if the download is for an Excel spreadsheet but the database was unexpectedly unavailable, return a valid spreadsheet containing just the error message.

**Unrecoverable server error handling**  
Unrecoverable server `Exception` will be written to HTTP response as a warning containing the exception message. Depending on framework setting `servlet.sendStackTraceToClient` (boolean) exception stacktrace can also be included.

### Related

- [DataSource.getSimpleErrors](../classes/DataSource.md#classmethod-datasourcegetsimpleerrors)
- [RPCManager.handleError](../classes/RPCManager.md#classmethod-rpcmanagerhandleerror)
- [RPCManager.runDefaultErrorHandling](../classes/RPCManager.md#classmethod-rpcmanagerrundefaulterrorhandling)
- [RPCManager.handleTransportError](../classes/RPCManager.md#classmethod-rpcmanagerhandletransporterror)
- [DataSource.handleError](../classes/DataSource.md#method-datasourcehandleerror)
- [FormItem.clearErrors](../classes/FormItem.md#method-formitemclearerrors)
- [FormItem.setErrors](../classes/FormItem.md#method-formitemseterrors)
- [FormItem.hasErrors](../classes/FormItem.md#method-formitemhaserrors)
- [DSResponse.status](../classes/DSResponse.md#attr-dsresponsestatus)
- [DSResponse.queueStatus](../classes/DSResponse.md#attr-dsresponsequeuestatus)
- [DSResponse.errors](../classes/DSResponse.md#attr-dsresponseerrors)
- [DSRequest.callback](../classes/DSRequest.md#attr-dsrequestcallback)
- [RPCRequest.callback](../classes/RPCRequest.md#attr-rpcrequestcallback)
- [RPCRequest.willHandleError](../classes/RPCRequest.md#attr-rpcrequestwillhandleerror)

---
