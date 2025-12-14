# Real-Time Messaging

[← Back to API Index](../reference.md)

---

## KB Topic: Real-Time Messaging

### Description
The optional Real-Time Messaging (RTM) module for SmartClient allows browser-based web applications to:

*   publish and subscribe to client-server messaging channels
*   send and receive messages via server push, for "real-time" updates without polling

For examples of publish and subscribe messaging, see: *Portfolio Grid* and *Stock Chart*

This functionality is currently supported for deployment on Java server platforms only, and requires a Power license or better as well as purchase of the Real-Time Messaging module. See [http://smartclient.com/product](http://smartclient.com/product) for details, and see [loadingOptionalModules](loadingOptionalModules.md#kb-topic-loading-optional-modules) for instructions on setting up the Messaging module.

#### Usage Summary

Messaging works in terms of _channels_. A _channel_ is an abitrary identifier for a destination for a message. When messages are sent to a channel, anyone subscribed to that channel receives the message.

The same concept appears in JMS (Java Message Service), where the equivalent term to channel is "topic" (for JMS, queues are supported as well).

Messages can be sent to a channel from either the client-side ([Messaging.send](../classes/Messaging.md#classmethod-messagingsend)) or server-side (ISCMessageDispatcher.send(), or equivalent JMS APIs to send a message to a Topic).

You can subscribe to a channel from either the client-side ([Messaging.subscribe](../classes/Messaging.md#classmethod-messagingsubscribe)) or server-side (ISCMessageDispatcher.register() and ISCMessageDispatcher.subscribe(), or equivalent JMS APIs to subscribe to a Topic).

Channels can be used in any way the application needs. For example, a chat application similar to IRC would typically create a new channel every time 2 or more people want to talk to one another.

#### Server API summary

Server-side RTM interfaces are provided by the following classes in com.isomorphic.messaging:

| ISCMessageDispatcherAbstract class; use to obtain a concrete message dispatcher class.instance()returns a concrete ISCMessageDispatcher class capable of delivering responses within the JVM or JMS (based on configuration)send(ISCMessage msg)send a messageregister(ISubscriber subscriber)register this subscriberunregister(ISubscriber subscriber)unregister this subscribersubscribe(ISubscriber subscriber, String channel)subscribe a given subscriber to a given channelunsubscribe(ISubscriber subscriber, String channel)unsubscribe a given subscriber from a given channelboolean isSubscribed(ISubscriber subscriber, String channel)check to see if a given subscriber is subscribed to a given channel | Abstract class; use to obtain a concrete message dispatcher class. | instance()returns a concrete ISCMessageDispatcher class capable of delivering responses within the JVM or JMS (based on configuration) | send(ISCMessage msg)send a message | register(ISubscriber subscriber)register this subscriber | unregister(ISubscriber subscriber)unregister this subscriber | subscribe(ISubscriber subscriber, String channel)subscribe a given subscriber to a given channel | unsubscribe(ISubscriber subscriber, String channel)unsubscribe a given subscriber from a given channel | boolean isSubscribed(ISubscriber subscriber, String channel)check to see if a given subscriber is subscribed to a given channel |
|---|---|---|---|---|---|---|---|---|
| Abstract class; use to obtain a concrete message dispatcher class. |
| instance()returns a concrete ISCMessageDispatcher class capable of delivering responses within the JVM or JMS (based on configuration) |
| send(ISCMessage msg)send a message |
| register(ISubscriber subscriber)register this subscriber |
| unregister(ISubscriber subscriber)unregister this subscriber |
| subscribe(ISubscriber subscriber, String channel)subscribe a given subscriber to a given channel |
| unsubscribe(ISubscriber subscriber, String channel)unsubscribe a given subscriber from a given channel |
| boolean isSubscribed(ISubscriber subscriber, String channel)check to see if a given subscriber is subscribed to a given channel |
| ISCMessageMessage object.ISCMessage(String channel, Object data)ISCMessage(List channels, Object data)create a message bound for the specified channel(s) with the specified data payload | Message object. | ISCMessage(String channel, Object data) | ISCMessage(List channels, Object data)create a message bound for the specified channel(s) with the specified data payload |
| Message object. |
| ISCMessage(String channel, Object data) |
| ISCMessage(List channels, Object data)create a message bound for the specified channel(s) with the specified data payload |
| ISubscriberSimple interface for a message subscriber. Required methods are:public void send(ISCMessage msg) throws Exception;public ISCMessage nextMessage(long timeout) throws Exception; | Simple interface for a message subscriber. Required methods are: | public void send(ISCMessage msg) throws Exception; | public ISCMessage nextMessage(long timeout) throws Exception; |
| Simple interface for a message subscriber. Required methods are: |
| public void send(ISCMessage msg) throws Exception; |
| public ISCMessage nextMessage(long timeout) throws Exception; |
| ISCSubscriberSimple concrete implementation of ISubscriber. send() adds message to a queue and nextMessage() retrieves them. |

#### Data Protocols
The Realtime Messaging subsystem supports real-time communication between client and server using either [WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) or [Comet \[HTTP Server Push\]](https://en.wikipedia.org/wiki/Comet_\(programming\)).

WebSockets is preferred as the non-websockets implementation requires a persistent connection to the server, and browsers are mandated by the HTTP protocol spec to limit connections to a single host to 6. This becomes significant if an application with Messaging connections is opened in multiple browser windows or tabs. The application can be significantly slowed down as as connections are used up by messaging, meaning the app's non-messaging operations will start slowing down and blocking as fewer connections are available for parallel operations.

Both client and server are configured to [use WebSockets by default](../classes/Messaging.md#classattr-messagingusewebsocket) if supported. If the server does not respond correctly to WebSocket requests, the framework will automatically detect this and silently back off to using Comet. The Messaging APIs are not impacted in any way by the protocol being used, so this process is invisible to end users and to application code.

Some cases that may cause WebSockets to be unavailable include:

*   Firewalls configured to block the webSocket connnections
*   Proxies / reverse proxies that haven't been configured to handle the webSocket (wss://) protocol
*   Older servlet engines that don't support websockets

If you're unsure which protocol is being used by a running application, you can use the native browser developer tools to watch for network requests against the [Messaging.websocketURL](../classes/Messaging.md#classattr-messagingwebsocketurl) and [Messaging.messagingURL](../classes/Messaging.md#classattr-messagingmessagingurl).  
If you're unsure _why_ Web Sockets are not being used in your application we'd recommend enabling DEBUG level server-side logging for com.isomorphic.messaging. This should report details on the framework's attempts to set up a websocket listener during server startup.
#### Server Configuration

The SmartClient message dispatcher can operate in simple mode or enterprise mode:

*   Simple mode uses an in-memory messaging delivery system with no message persistence, and can operate only in the context of a single JVM
*   Enterprise mode uses Java Message Service (JMS) as the messaging backend, and can operate in a clustered environment

The default settings will use the Simple Mode (no JMS). To use JMS, set the following in [server.properties](server_properties.md#kb-topic-serverproperties-file):
```
 # Use com.isomorphic.messaging.JMSMessageDispatcher for JMS-backed messaging
 messaging.dispatcherImplementer: com.isomorphic.messaging.JMSMessageDispatcher 
 
```

#### JMS configuration: setting JNDI properties

There are two styles of configuring JNDI and configuring SmartClient Messaging to find a JMS Topic or Queue Connection Factory:

**1\. Configure JNDI in your servlet engine**

In this case, you would set JNDI properties (java.naming.\* properties) via your application's [jndi.properties](http://docs.oracle.com/javase/jndi/tutorial/beyond/env/source.html) file.

**2\. Configure JNDI via server.properties**

If you set `messaging.jms.context` to a string such as "mySettings", it tells SmartClient to refer to several other properties in the `server.properties` file, prefixed with "jndi" + the value of `messaging.jms.context`. For example:

```
 messaging.jms.context: mySettings
 jndi.mySettings.java.naming.factory.initial: org.jboss.naming.remote.client.InitialContextFactory
 jndi.mySettings.java.naming.provider.url: remote://localhost:4447
 jndi.mySettings.java.naming.factory.url.pkgs: org.jboss.naming:org.jnp.interfaces
 jndi.mySettings.java.naming.security.authentication: simple
 jndi.mySettings.java.naming.security.principal: admin
 jndi.mySettings.java.naming.security.credentials: admin
 
```
The configuration above means that, when the Messaging system uses JNDI to look up ConnectionFactory instances, the Hashtable of environment information passed to `new InitialContext()` will contain entries such as `java.naming.provider.url = remote://localhost:4447` and the various other `java.naming.*` JNDI properties shown above.

This is an alternative to using `jndi.properties` or other means provided by your servlet engine for JNDI setup. If you use this mechanism, the JNDI properties shown above will be used only when Messaging looks up JMS resources, and not for any other JNDI lookups.

#### JMS configuration: JNDI path to find ConnectionFactory instances

When using JNDI "lookup()" calls to find your JMS ConnectionFactory instances, SmartClient using the following properties from server.properties (shown below with their default values):

```
        messaging.jms.jndiPrefix: jms
        messaging.jms.topicConnectionFactory: TopicConnectionFactory
        messaging.jms.queueConnectionFactory: QueueConnectionFactory
 
```
SmartClient will first call the JNDI API `context.lookup()` with the `jndiPrefix` property shown above, then with either the `topicConnectionFactory` or `queueConnectionFactory` property depending on whether a topic or queue is being looked up.

Note that _there is horrible confusion and inconsistency across servlet engines_ as to how JNDI paths are handled when looking up JMS resources:

*   you _may_ need to specify the prefix "java:comp/env" as part of the `messaging.jms.jndiPrefix` property, or it may be considered implicit
*   when defining the "name" attribute on the JNDI `<Resource>` tag for your ConnectionFactory or a specific Topic or Queue, you _may_ need to use the prefix "jms/" in the "name" attribute, and if you don't, your Resource may be unable to be found. So for example, if you meant to name a Topic "MyTopic" the name may need to be "jms/MyTopic". Alternatively, adding the "jms/" prefix may mean that the path to lookup the resource is now "jms/jms/MyTopic" or that it cannot be found at all.
*   whether or not you used the prefix "jms" in the "name" attribute of your `<Resource>`, it may be required as part of the `messaging.jms.jndiPrefix` property.

So for example, if you have Topic ConnectionFactory named either "jms/MyFactory" or just "MyFactory", any of the following settings may work:
```
        messaging.jms.jndiPrefix: java:comp/env
        messaging.jms.topicConnectionFactory: jms/MyFactory
 
```
```
        messaging.jms.jndiPrefix: 
        messaging.jms.topicConnectionFactory: jms/MyFactory
 
```
```
        messaging.jms.jndiPrefix: 
        messaging.jms.topicConnectionFactory: MyFactory
 
```
```
        messaging.jms.jndiPrefix: java:comp/env
        messaging.jms.topicConnectionFactory: MyFactory
 
```
Example configurations for various popular JMS engines (ActiveMQ, JBoss, etc) can be found on the [Isomorphic Public Wiki](http://wiki.smartclient.com/). Try searching for ["messaging"](http://wiki.smartclient.com/dosearchsite.action?queryString=messaging) or ["jms"](http://wiki.smartclient.com/dosearchsite.action?queryString=jms) or the name of the engine you are trying to configure.

#### Other Messaging properties

The following properties that control Messaging can also be set via server.properties. Generally, do not adjust these properties unless you are extremely familiar with how web-based streaming works and with the specific details of your network topology.

```
 
 # how often do we send keepalives to the client (ms) 
        messaging.keepaliveInterval: 3000

 # how long the client waits after the keepaliveInterval before re-establishing
 # the connection (ms)
        messaging.keepaliveReestablishDelay: 1000

 # how long the client waits for the connect handshake to complete before 
 # retrying (ms)
        messaging.connectTimeout: 4000

 # connection time to live - the maximum amount of time a persistent connection
 # is allowed to stay open before being re-established (ms).  Connections are re-created
 # every 2 minutes by default because intervening firewalls or web proxies will often sever
 # connections that have been open too long, as will the browser itself.
        messaging.connectionTTL: 120000

 # total response size to pad out to in order to defeat bufferring by intervening proxies
 # (in bytes).  Set higher if you see data leaving the server, but it never arrives at the
 # client machine.  With older legacy proxies, values as high as 256k may be required.
        messaging.flushBufferSize: 8096

 # dispatcher to use for user registration/message queueing
 # com.isomorphic.messaging.LocalMessageDispatcher for simple one-jvm messaging
 # com.isomorphic.messaging.JMSMessageDispatcher for JMS-backed messaging
        messaging.dispatcherImplementer: com.isomorphic.messaging.LocalMessageDispatcher

 # jms configuration - for JMSMessageDispatcher only
        messaging.jms.context: _container_
        messaging.jms.jndiPrefix: jms
        messaging.jms.topicConnectionFactory: TopicConnectionFactory
        messaging.jms.queueConnectionFactory: QueueConnectionFactory
```

#### Servlet Container WebSocket Configuration

Some websocket configuration must be done at the level of the servlet container, such as Tomcat (included in our SDK), Jetty, etc. This includes the setting of the maximum supported text and binary message sizes.

For this, we've added a section to the file `WEB-INF/web-tomcat.xml` included in the SDK:

```
 <!-- maximum text message size -->
 <context-param>
     <param-name>org.apache.tomcat.websocket.textBufferSize</param-name>
     <param-value>262144</param-value>
 </context-param>

 <!-- maximum binary message size -->
 <context-param>
     <param-name>org.apache.tomcat.websocket.binaryBufferSize</param-name>
     <param-value>262144</param-value>
 </context-param>
```
If you're not using our stock Embedded Tomcat and web-tomcat.xml file you'll need to apply equivalent changes to your own servlet container.

Note that this not something configurable from the familiar server properties file because our server properties are not accessible from the servlet container's initialization code.

#### Tips

*   For best performance on legacy browsers (Internet Explorer pre-8.0), we recommend forwarding the messaging connections to an HTTP 1.0 server. Otherwise, because older Internet Explorer browsers use no more than 2 concurrent connections to the same web server, with the Messaging connection open, all other connections will execute serially. This means that something like a data fetch might be held up until all images on the page have finished loading.

### Related

- [Messaging.send](../classes/Messaging.md#classmethod-messagingsend)
- [Messaging.getSubscribedChannels](../classes/Messaging.md#classmethod-messaginggetsubscribedchannels)
- [Messaging.subscribe](../classes/Messaging.md#classmethod-messagingsubscribe)
- [Messaging.unsubscribe](../classes/Messaging.md#classmethod-messagingunsubscribe)
- [Messaging.connected](../classes/Messaging.md#classmethod-messagingconnected)
- [Messaging.disconnect](../classes/Messaging.md#classmethod-messagingdisconnect)

---
