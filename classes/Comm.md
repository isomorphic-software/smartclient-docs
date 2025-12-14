# Comm Documentation

[← Back to API Index](../reference.md)

---

## Class: Comm

### Description
Provides background communication with an HTTP server

---
## ClassAttr: Comm.concurrentXHRErrorMessage

### Description
The message to show the user if [concurrentXHRsInIE](#classattr-commconcurrentxhrsinie) is in force and an error occurs on the concurrent worker thread. If this attribute is left at its default null value, the user is shown the error message reported by the browser, along with the URL and line number where the error occurred (this information is also logged to the developer console, regardless of the message shown to the user)

### Groups

- i18n

**Flags**: IRW

---
## ClassAttr: Comm.concurrentXHRsInIE

### Description
If true, SmartClient will use a [web worker](https://html.spec.whatwg.org/multipage/workers.html) to send [RPCRequest](../reference.md#object-rpcrequest)s and [DSRequest](../reference.md#object-dsrequest)s concurrent with the main Javascript thread, if:

*   The [transport](RPCRequest.md#attr-rpcrequesttransport) is "xmlHttpRequest"
*   The browser is Internet Explorer 10 or greater

We do this because Internet Explorer sometimes queues the sending of data with other, timer-delayed tasks on the single Javascript thread. With a busy application, this can lead to an xmlHttpRequest seeming to block; the HTTP connection is made to the server, and the server then goes into a wait state while the browser completes other timer-delayed tasks. If there are expensive timer-delayed tasks in the way, such as a reflow of the UI, completing the send to the server can block for a significant length of time, leading in turn to server turnaround times that are significantly longer than they need to be.

Internet Explorer is the only browser that behaves like this, so this option does not apply to other browsers.

**Flags**: IRWA

---
