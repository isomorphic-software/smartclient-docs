# Remote Debugging

[← Back to API Index](../main.md)

---

## KB Topic: Remote Debugging

### Description
In Pro and better builds (and also the Eval build), the SmartClient [Developer Console](debugging.md#kb-topic-debugging) supports debugging remote pages, including those running on mobile devices. With remote debugging, you can use all of the powerful debugging features of the [Developer Console](debugging.md#kb-topic-debugging) - the component hierarchy (Watch tab), client/server requests (RPC tab), logs and log categories - using the large screen and physical keyboard of a desktop machine.

#### Using Remote Debugging

To enable remote debugging on a page, just add `isc_remoteDebug=true` to the page URL. For example:

[http://localhost:8080/isomorphic/system/reference/SmartClient\_Explorer.html?isc\_remoteDebug=true](http://localhost:8080/isomorphic/system/reference/SmartClient_Explorer.html?isc_remoteDebug=true)

Note in the URL above, set localhost to the actual hostname or IP address of the machine running the SDK.

You'll also need to be sure that your [isomorphicDir](../classes/Page.md#classmethod-pagesetisomorphicdir) has been set up correctly and that messaging is enabled on your server as noted below.

Then direct your _desktop_ browser to the Developer Console in the `system/helpers/` subdirectory of your isomorphic dir - typically:

[http://localhost:8080/isomorphic/system/helpers/Log.html](http://localhost:8080/isomorphic/system/helpers/Log.html)

At top right of the page, you will see a "Remote" dropdown that lists the devices and URLs that have registered for remote debugging (by passing the `isc_remoteDebug` parameter). As you roll over the available remote targets in this dropdown, the target page will glow blue to make it easy to tell which page you will be selecting for debugging - this is particularly handy when you have a lot of devices. Pick the page to debug and just starting using the [Developer Console](debugging.md#kb-topic-debugging) as normal.

If you reload the page on your mobile device, the remote Developer Console automatically re-establishes the connection. And any settings - such as Logging Preferences or Watch tab settings - automatically persist as they normally would.

#### Licensing

Anyone with a Pro or better license can use the Remote Debugging feature. Under the covers, the Remote Debugging feature actually uses the Real-time Messaging module, which is not a Pro feature. However we've rearranged things so that Pro users can use Real-time Messaging _just for Remote Debugging_. This does mean that, if you are upgrading your environment to the current release and you don't already have Real-time Messaging, you will need to follow the installation steps normally required for Real-time Messaging before the Remote Debugging feature will work. See the [messaging](messaging.md#kb-topic-real-time-messaging) documentation for details.

### See Also

- [debugging](debugging.md#kb-topic-debugging)

---
