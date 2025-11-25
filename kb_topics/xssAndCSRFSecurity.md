# XSS and CSRF Security

[← Back to API Index](../main.md)

---

## KB Topic: XSS and CSRF Security

### Description
Cross-site scripting (XSS) and Cross-site request forgery (CSRF, sometimes XSRF) are two separate exploits that can be used to attack a vulnerable web application:

*   XSS allows an attacker to execute arbitrary Javascript in the user's browser. [Wikipedia](https://en.wikipedia.org/wiki/Cross-site_scripting)
*   CSRF allows an attacker to mislead the user into carrying out an action they did not intend. [Wikipedia](https://en.wikipedia.org/wiki/Cross-site_request_forgery)

#### Cross-site scripting
XSS attacks are made possible when values sent from the client are accepted as data values without first sanitizing them. Here, _sanitizing_ means checking values to ensure that they do not contain structures that would be interpreted as executable code if placed into an HTML document. An example of this in a SmartClient application would be a text field into which the user is supposed to enter their name. If an attacker instead enters into that field
```
    <script>alert("Hacked!")</script>
 
```
then inserting that field value into an HTML document will cause the script to execute.

The way to prevent this kind of attack is [DataSourceField.escapeHTML](../classes/DataSourceField.md#attr-datasourcefieldescapehtml). Setting that flag on your fields will ensure that script embedded in field values won't execute; because it is escaped, the value will be treated as literal text.

#### Cross-site request forgery
CSRF attacks occur when a malicious website sends a legitimate-looking request to a web application that the user is already logged into. Such attacks rely on the use of session cookies as the sole mechanism for identifying and authenticating the user, so the best way to prevent such an attack is to introduce an additional means of identifying the user: this is usually known as a CSRF token.

A CSRF token is a unique string of text that you generate on the server on session creation, and then expect to be passed as a parameter with all future requests. By storing the CSRF token in the session and comparing it to the passed token parameter, you can be sure that the request came from a source that is privy to the CSRF token, and thus that the request is not forged.

implementing a CSRF token strategy is really easy with SmartClient, especially if you are using the SmartClient server framework. Since all data-related requests go to a single URL, specified with [RPCManager.actionURL](../classes/RPCManager.md#classattr-rpcmanageractionurl), you can just add your CSRF token to that URL in your bootstrap file. Alternatively, you could use [RPCManager.transformRequest](../classes/RPCManager.md#classmethod-rpcmanagertransformrequest) to add your token, if your authentication system requires the CSRF token in another part of the request (for example, in an HTTP header). Using a CSRF token is a **highly recommended** security practice.

#### Domain synchronization
SmartClient implements a technique called _domain synchronization_ to ensure that server communications using the "hiddenFrame" protocol work reliably.

The "hiddenFrame" protocol uses an iframe to load content from the server. If your page sets `document.domain` at all, an iframe must have a matching `document.domain` setting or it can't contact the main page to report results. Due to proxying and other commonly-used techniques, there is no reliable way for the server to know what `document.domain` setting must be used. Therefore, SmartClient passes the setting to the server with each "hiddenFrame" request, in a parameter called `isc_dd`, and the server echoes that setting back down to the client.

Domain synchronization opens up the potential for an obscure hybrid XSS/CSRF attack on a SmartClient application, where it shares a domain with another, non-SmartClient application that is vulnerable to XSS attacks - for example, a SmartClient app at `payments.example.com` and a non-SmartClient app at `enquiry.example.com`. This attack would work by injecting an XSS payload into the vulnerable, non-SmartClient app at `enquiry.example.com`; this injected code would set the domain to "example.com", and then create an iframe that targets the SmartClient app at "payments.example.com", passing `isc_dd` as "example.com". The return function from that CSRF call would be able to access data from "payments.example.com", as a result of exploiting an XSS vulnerability in the app at "enquiry.example.com".

*   This exploit is only possible in these exact circumstances: ie, where a SmartClient app is deployed to the same domain as a non-SmartClient app that is vulnerable to XSS attacks
*   The attack is only meaningful if you have multiple separate apps deployed at different subdomains, with separate sets of users for each app
*   The attack is impossible if CSRF tokens are employed in the SmartClient app, since the forged request to "payments.example.com" would be rejected as lacking a CSRF token
*   If your page does not set `document.domain`, there is no need for domain synchronization, and you can simply switch it off by specifying `domainSync.disabled: true` in your `server.properties` file
*   If your page _does_ set `document.domain`, you can prevent this kind of exploit by providing a comma-separated list of valid base domains in `server.properties` setting `domainSync.baseDomains`. For example, the following setting would have prevented the above attack: `domainSync.baseDomains: payments.example.com`

Note that if you leave domain synchronization switched on and do not constrain it by providing a `baseDomains` setting as described above, the system will log a warning every time it echoes a client-provided domain name in a response.

---
