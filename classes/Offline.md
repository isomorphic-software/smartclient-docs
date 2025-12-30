# Offline Documentation

[← Back to API Index](../reference.md)

---

## Class: Offline

### Description
The Offline class provides features for storing and retrieving values in persistent browser storage. Because this storage is both persistent (ie, it remains available after the browser is closed and re-opened) and local to the browser, it allows applications to operate when the client is not connected to a network, albeit with some obvious limitations.

As well as providing straightforward APIs for storing, retrieving and removing values, Offline support is integrated into the normal request/response cycle. You can configure the framework so that server responses are automatically cached in Offline storage. Then, at some future point when the client is offline, responses for known requests are returned from the Offline cache.

SmartClient makes use of various underlying storage techniques, depending on what the browser supports, but the API to a SmartClient program is the same regardless of the underlying storage - simple key/value pairs. Currently, we provide Offline support for all HTML5-compliant browsers, plus earlier versions of Internet Explorer (6 and 7). The amount of storage available is dictated by the browser, and varies from approximately 500KB to approximately 5MB.

### Groups

- offlineGroup

---
## ClassMethod: Offline.goOnline

### Description
Explicitly sets this session into online mode. This setting will override whatever state the browser reports. This allows users to manually set an application into offline or online state.

### See Also

- [Offline.goOffline](#classmethod-offlinegooffline)
- [Offline.useNativeOfflineDetection](#classmethod-offlineusenativeofflinedetection)

---
## ClassMethod: Offline.useNativeOfflineDetection

### Description
Tells the Offline system to query the browser for the current online/offline state. Calling this method switches off the explicit offline mode setting switched on by calling [Offline.goOnline](#classmethod-offlinegoonline) or [Offline.goOffline](#classmethod-offlinegooffline).

It is important to note that browsers vary quite considerably in their ability to detect that they are offline. Many older browsers simply can't do it; HTML5 browsers expose the `navigator.onLine` property, but each browser's implementation is different. Some browsers have a manual "Work Offline" mode which allows the user to make the decision, and SmartClient provides an equivalent mechanism with the `goOffline` and `goOnline` methods. Generally speaking, these methods are more reliable than allowing the browser to decide whether your application is offline.

### See Also

- [Offline.goOnline](#classmethod-offlinegoonline)
- [Offline.goOffline](#classmethod-offlinegooffline)

---
## ClassMethod: Offline.remove

### Description
Removes the key/value pair mapped by the passed-in key from browser-local storage

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| key | [String](#type-string) | false | — | The key to remove |

### See Also

- [Offline.put](#classmethod-offlineput)
- [Offline.get](#classmethod-offlineget)

---
## ClassMethod: Offline.get

### Description
Returns the value mapped to the passed-in key from browser-local storage, or null if no such key exists.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| key | [String](#type-string) | false | — | The key to retrieve a value for |

### Returns

`[Any](#type-any)` — The value mapped to the passed in key, or null if no such key exists

### See Also

- [Offline.put](#classmethod-offlineput)

---
## ClassMethod: Offline.goOffline

### Description
Explicitly sets this session into offline mode. This setting will override whatever state the browser reports. This allows users to manually set an application into offline or online state.

### See Also

- [Offline.goOnline](#classmethod-offlinegoonline)
- [Offline.useNativeOfflineDetection](#classmethod-offlineusenativeofflinedetection)

---
## ClassMethod: Offline.isOffline

### Description
Returns true if the current browser session is offline (ie, not connected to a network). If an online/offline state has been set explicitly (see [Offline.goOffline](#classmethod-offlinegooffline) and [Offline.goOnline](#classmethod-offlinegoonline)), the explicitly-set state will be returned. Otherwise, the offline state as reported by the browser will be returned. See [useNativeOfflineDetection](#classmethod-offlineusenativeofflinedetection) for important notes on browser detection of offline state.

### Returns

`[Boolean](#type-boolean)` — true if the current browser session is offline

### See Also

- [Offline.goOffline](#classmethod-offlinegooffline)
- [Offline.goOnline](#classmethod-offlinegoonline)
- [Offline.useNativeOfflineDetection](#classmethod-offlineusenativeofflinedetection)

---
## ClassMethod: Offline.put

### Description
Stores the passed-in value in browser-local storage, mapped to the passed-in key. If there is no room left to store the value, we discard values from the offline store, oldest first, until there is room to store the value. If you don't want this behavior, explicitly pass false in the `recycleEntries` parameter.

Note that limitations in the underlying storage engines mean that only primitive values - Strings, numbers and booleans - can be stored. If you wish to store an Array or Object, you will have to serialize it to JSON first, and then `eval` it after retrieval to turn it back into an object.

**Note:** This method throws an exception if it could not store the value (either because storage is full and recycleEntries was false, or because the value to store is simply too large)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| key | [String](#type-string) | false | — | The key to use when storing the value |
| value | [Any](#type-any) | false | — | The value to store |
| recycleEntries | [boolean](../reference.md#type-boolean) | true | — | If false, suppresses the default behavior of repeatedly discarding the oldest entry if there is insufficient space to store the value |

### See Also

- [Offline.get](#classmethod-offlineget)

---
