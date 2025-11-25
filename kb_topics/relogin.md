# Relogin

[← Back to API Index](../main.md)

---

## KB Topic: Relogin

### Description
When a user's session has expired and the user tries to navigate to a protected resource, typical authentication systems will redirect the user to a login page. With Ajax systems such as SmartClient, this attempted redirect may happen in response to background data operations such as a form trying to save. In this case, the form perceives the login page as a malformed response and displays a warning, and the login page is never displayed to the user.

The ideal handling of this scenario is that the form's attempt to save is "suspended" while the user re-authenticates, then is completed normally. SmartClient makes it easy to implement this ideal handling _without_ having to implement session timeout handling in every codepath that contacts the server, by providing central notification of session timeout, and the ability to re-send a transaction that encountered session timeout.

#### Detecting session timeout

To enable SmartClient to detect that session timeout has occurred, a special marker needs to be added to the HTTP response that is sent when a user's session has timed out. This is called the `loginRequiredMarker`.

If your authentication system will redirect to a login page when a user's session is timed out, it's sufficient to simply embed the `loginRequiredMarker` in the login page. The `loginRequiredMarker` is valid HTML and will have no effect on the behavior or appearance of the page. The `loginRequiredMarker` is found in smartclientSDK/isomorphic/login/loginRequiredMarker.html in your SDK. Simply copy the contents of this file verbatim into your login page anywhere inside the `<body>` tag; it does not need to be customized in any way for your application.

The HTML snippet in loginRequiredMarker.html consists of two parts:

*   It includes the [RPCManager.loginRequiredMarker](../classes/RPCManager.md#classattr-rpcmanagerloginrequiredmarker). Responses to standard [xmlHttpRequest transport](../classes/RPCRequest.md#attr-rpcrequesttransport) RPC requests will be scanned for this marker and kick off the [loginRequired flow](../classes/RPCManager.md#classmethod-rpcmanagerloginrequired) automatically.
*   For [hiddenFrame transport](../classes/RPCRequest.md#attr-rpcrequesttransport) request, it also includes some JavaScript to explicitly notify the RPCManager in the SmartClient app running in the parent frame or opener window that login is required.

If it's a problem to modify the login page (even with a marker that has no effect on appearance or behavior), see if you can configure your authentication system to return a special response specifically for background requests for data. By default, when using the SmartClient Server Framework, all such requests go to the [RPCManager.actionURL](../classes/RPCManager.md#classattr-rpcmanageractionurl) and include an HTTP query parameter "isc\_rpc=1"; various authentication systems can be configured to detect these requests and handle them separately. One approach is to simply copy loginRequiredMarker.html into your application in an area not protected by authentication and redirect to it when a background data request with an expired session is detected.

#### Handling session timeout

When SmartClient detects the `loginRequiredMarker`, the transaction that encountered session timeout is put on hold, and [RPCManager.loginRequired](../classes/RPCManager.md#classmethod-rpcmanagerloginrequired) is called. At this point you have a few options:

1.  Leave the SmartClient application and take the user to the login page, by simply doing a `window.location.replace(_myLoginURL_)`, the simplest but least user friendly option.
2.  Open a new browser window that goes to your plain HTML login form (or offer a link that opens such a browser window), using a modal dialog in the application page that prompts the user to login before continuing, then re-send the intercepted transaction ([RPCManager.resendTransaction](../classes/RPCManager.md#classmethod-rpcmanagerresendtransaction) when the user indicates he has logged in. This is simple, does not drop context, but is not seamless.
3.  Use a SmartClient interface, typically a DynamicForm in a Window, to collect credentials, perform login as a background RPC, and on success re-send the intercepted transaction ([RPCManager.resendTransaction](../classes/RPCManager.md#classmethod-rpcmanagerresendtransaction). A complete example of this, which assumes an authentication system that can take credentials as HTTP POST params, is included in the SDK as isomorphic/login/reloginFlow.js.

**Authentication via background RPC form POST**

The approach shown in reloginFlow.js posts the credentials gathered from the user to [RPCManager.credentialsURL](../classes/RPCManager.md#classattr-rpcmanagercredentialsurl). To make this work with an authentication system that can accept credentials via HTTP POST:

1.  set the RPCManager.credentialsURL to the URL where credentials should be POST'd
2.  include reloginFlow.js in your page, modified, if necessary, so that the names of the USERNAME and PASSWORD params match what your authentication system uses
3.  configure your authentication system to send back the loginSuccessMarker as part of a successful login response, and the loginRequiredMarker as part of a failed login response

If your authentication system can accept POST'd credentials at any URL it protects, the last step may be as simple as configuring the loginSuccessMarker file itself as a protected resource (`isomorphic/login/loginSuccessMarker.html`).

**Authentication via background SmartClient server RPC/DMI**

If you are using the SmartClient Java server and your authentication system allows you to mark a user as authenticated from Java, you can perform a normal RPC or DMI with the credentials gathered from the user and send back success or failure indications as normal RPC or DMI responses. This can be useful if, in addition to logging in, you want to send back additional data.

**Advanced: concurrency**

If, after loginRequired() has fired and before the user has re-authenticated, you send additional RPCs to protected URLs, you will get additional loginRequired() notifications. This may happen to applications that poll for data or periodically save without user action. You may wish to avoid this by setting an application-specific flag to avoid firing requests during the relogin process. However, you must ultimately either [resend](../classes/RPCManager.md#classmethod-rpcmanagerresendtransaction) or [discard](../classes/RPCManager.md#classmethod-rpcmanagercleartransaction) every transaction for which loginRequired() fires, or you will have a memory leak due to suspended transactions.

Note also that there is no requirement that the relogin process blocks user interaction. Applications that access multiple services may choose to simply show an unobtrusive error indication such that the user can log back in at his leisure, or even log the user back in automatically.

### Related

- [RPCManager.loginRequired](../classes/RPCManager.md#classmethod-rpcmanagerloginrequired)
- [RPCManager.credentialsURL](../classes/RPCManager.md#classattr-rpcmanagercredentialsurl)
- [RPCManager.loginStatusCodeMarker](../classes/RPCManager.md#classattr-rpcmanagerloginstatuscodemarker)
- [RPCManager.loginRequiredMarker](../classes/RPCManager.md#classattr-rpcmanagerloginrequiredmarker)
- [RPCManager.loginSuccessMarker](../classes/RPCManager.md#classattr-rpcmanagerloginsuccessmarker)
- [RPCManager.maxLoginAttemptsExceededMarker](../classes/RPCManager.md#classattr-rpcmanagermaxloginattemptsexceededmarker)
- [RPCManager.reloginCommFailureMessage](../classes/RPCManager.md#classattr-rpcmanagerrelogincommfailuremessage)
- [RPCRequest.containsCredentials](../classes/RPCRequest.md#attr-rpcrequestcontainscredentials)

---
