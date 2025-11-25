# Messaging Documentation

[← Back to API Index](../main.md)

---

## Class: Messaging

### Description
The Real-Time Messaging module creates a channel for messages to be sent from the server to the client (a.k.a. "server push") in real-time (as opposed to periodically polling the server for updates).

See [Messaging overview](../kb_topics/messaging.md#kb-topic-real-time-messaging) for information.

---
## ClassAttr: Messaging.websocketURL

### Description
URL where the WebSocket endpoint is registered. On the server, the URI of the endpoint is controled by the server.properties configuration setting `messaging.websocket.URI` and defaults to `/isomorphic/websocket`

This URL must ultimately start with ws:// or wss://, but you may specify this value as starting with http:// or https:// and it will be automatically converted to ws(s)://

**Flags**: IR

---
## ClassAttr: Messaging.fallBackToComet

### Description
Whether or not to fall back to Comet if [WebSocket](#classattr-messagingusewebsocket) communication fails, and has never succeeded since page load. Once WebSocket communication succeeds, we never fall back.

If we're not falling back to Comet, we'll reattempt connecting via WebSockets if we time out trying to open a WebSocket connection, or an open WebSocket reports an error.

**Flags**: IR

---
## ClassAttr: Messaging.messagingURL

### Description
URL where the MessagingServlet has been installed. See the server-side JavaDoc for details on the MessagingServlet.

**Flags**: IR

---
## ClassAttr: Messaging.useWebSocket

### Description
Whether to attempt to use the WebSocket protocol for Realtime Messaging. Enabled by default. When enabled, the webSocket protocol is preferred and tried first, but a failure to initially connect using webSockets causes the client to fall back to http push.

See [Messaging overview](../kb_topics/messaging.md#kb-topic-real-time-messaging) for more detail on messaging protocols.

Note that once a successful connection using the webSocket protocol is established, the protocol is marked as available and will be used until the client browser page is reloaded (at which point it will again be preferred, but backed off if the initial connection fails).

**Flags**: IR

---
## ClassAttr: Messaging.connectTimeout

### Description
Number of milliseconds to wait when initiating a server connection before dropping the attempt and trying again.

**Flags**: IR

---
## ClassAttr: Messaging.websocketConnectTimeout

### Description
Number of milliseconds to wait when initiating a server connection before dropping the attempt and trying again.

**Flags**: IR

---
## ClassMethod: Messaging.subscribe

### Description
Subscribes the client to the messaging channel identified by channel.

When the server or another connected browser sends a message on this channel, the callback will be invoked with a single 'data' parameter containing the data that was just sent to the channel.

Calling subscribe() again for a channel you are already subscribed to will result in the new callback replacing the old, and will cause the server connection to be re-established.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| channel | [String](#type-string) | false | — | — |
| callback | [MessagingCallback](#type-messagingcallback) | false | — | callback fired whenever data is sent to this channel |
| subscribeCallback | [Callback](../main.md#type-callback) | false | — | callback fired when the subscription is established |
| selector | [String](#type-string) | true | — | JMS selector used with Queues to filter the messages that arrive to the channel (optional). |

### Groups

- messaging

---
## ClassMethod: Messaging.unsubscribe

### Description
Unsubscribes the client from the messaging channel identified by channel.

This will cause a reconnect to the server - for this reason we defer the actual reconnect to allow for multiple unsubscribe() calls in sequence.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| channel | [String](#type-string) | false | — | — |

### Groups

- messaging

---
## ClassMethod: Messaging.disconnect

### Description
Sever the connection to the server and stop receiving messages.

### Groups

- messaging

---
## ClassMethod: Messaging.getSubscribedChannels

### Description
Returns an array of identifiers for all currently subscribed channels on this client

### Returns

`[Array of String](#type-array-of-string)` — —

### Groups

- messaging

---
## ClassMethod: Messaging.send

### Description
Send data to one or more channels, by sending the data to the server, where it is expected to be delivered to any other browser subscribed to the same channel.

Data can be any nested structure of primitive types (String, Date, Number) or compound data structure consisting of Arrays and Objects containing primitive types. The optional callback fires when the message has been successfully sent, or if an error occurs.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| channels | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | — |
| data | [Any](#type-any) | false | — | — |
| callback | [RPCCallback](#type-rpccallback) | false | — | — |

### Groups

- messaging

---
## ClassMethod: Messaging.connectionUp

### Description
Called when the messaging connection allowing the server to send messages to the client is established - whether that's the result of an initial connect() or a re-establishment after it is severed.

---
## ClassMethod: Messaging.connectionDown

### Description
Called when the messaging connection allowing the server to send messages to the client is disconnected. This can occur either when you explicitly disconnect the connection or if a keepalive packet from the server does not arrive on time. This latter is defined as the `messaging.keepaliveInterval` plus the `messaging.keepaliveReestablishDelay`. With default settings, a maximum of 4 seconds will elapse between the connection actually going down and you receiving this callback.

---
## ClassMethod: Messaging.connected

### Description
Returns whether the Messaging system currently has a connection to the server.

This is not perfectly authoritative since the server may crash at any given instant. This method will return true if we have opened a connection to the server and the connection has been successfully acknowledged by the server.

### Returns

`[boolean](../main.md#type-boolean)` — whether we are currently connected

### Groups

- messaging

---
