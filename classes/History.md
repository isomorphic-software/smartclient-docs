# History Documentation

[← Back to API Index](../reference.md)

---

## StaticMethod: History.setHistoryTitle

### Description
Sets the title associated with all history entries. This is the string that appears in the history drop-down. If left unset, this default to the history id that is passed into [History.addHistoryEntry](#staticmethod-historyaddhistoryentry).

Note: Currently, this works in IE only. You may call this method in all other browsers, but it will not change what's displayed in the history drop-down.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| title | [String](#type-string) | false | — | The title to show in the history drop-down. |

---
## StaticMethod: History.getCurrentHistoryId

### Description
Returns the current history id as reflected by the current URL.

### Returns

`[String](#type-string)` — The current history id as reflected by the current URL.

---
## StaticMethod: History.addHistoryEntry

### Description
Call this method to add a synthetic history entry. The new history entry is added in the history stack after the currently visible page - in exactly the same way as the browser would treat a new page transition at this point. In other words, if the user has navigated ten pages using, say, a mixture of synthetic and real history entries, then presses back five times and then triggers a call to this method, the history entry will be created at the 6th position in the history stack and any history entries forward of that will be discarded.

**NOTE:** Browsers including Chrome and Firefox require a delay, even a minimal 1 millisecond timeout, between additions to the browser's history stack or else only the last addition will have an effect. The History module does not allow two different (by id) history entries to be added in the same thread of execution. To check whether another history entry can be added by the current thread, call [History.readyForAnotherHistoryEntry](#staticmethod-historyreadyforanotherhistoryentry).

This method must be called with an id. This id can be any string - it will be URL-encoded and added to the current page URL as an anchor (e.g. #foo). This URL change allows the user to bookmark this particular application state. When the user next navigates to this history entry, the id you supplied here will be passed back to the callback you supplied via [History.registerCallback](#staticmethod-historyregistercallback).

You may also optionally supply some arbitrary data to associate with this history entry. If you do this, the data you passed in will be passed back to you as part of the callback you specified via [History.registerCallback](#staticmethod-historyregistercallback). This data object can be anything you want, but there are some caveats:

*   The data parameter is currently supported by all SmartClient-supported browsers except **Safari**
*   As long as the user has not navigated away from the top-level page (i.e. the user is navigating within synthetic history entries only), whatever data you pass in will be handed back to you.
*   When the user navigates away from the current page, SmartClient will attempt to serialize the data into a string so that when/if the user comes back to this history entry, it can be deserialized and passed back to your logic. To take advantage of this, you need to make sure that your data is serializeable. As long as your data is a native datatype (String, Number, Boolean) or a collection of such datatypes (collections meaning object literals and arrays), then it will serialize correctly. Things like pointers to the document object and functions cannot be serialized.
*   In order for the serialization to occur on a page transition, you must have the SmartClient Core module loaded on the page at the time of the transition. If it's not available, the data will be lost, but you will still get a callback with the id you specify if the user navigates back to this history entry later.
*   The data associated with this history entry will persist as long as at least one instance of the browser remains open on the user's machine. Once the user closes all browser instances, the data will be lost.
*   Also, the user can trigger a history callback at any time by navigating to a bookmarked history entry that may have been created in a past session, such that no data is associated with that id in the current session. How you choose to handle that situation is up to you.

You're always guaranteed to receive the id you associate with a history entry in the callback that you specify, but the data you associated may or may not be available, so be careful about how you use it. Note that by passing the `requiresData` parameter to [History.registerCallback](#staticmethod-historyregistercallback) you can suppress the callback from firing unless the stored data object is actually available.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [String](#type-string) | false | — | The id you want to associate with this history entry. This value will appear as an anchor reference at the end of the URL string. For example, if you pass in "foo" as the id, the URL will then have a #foo tacked on the end of it. This id will be passed back to the callback you specified in [History.registerCallback](#staticmethod-historyregistercallback) when the user navigates to this history entry in the future. |
| title | [String](#type-string) | true | — | The title to show in the history drop-down for this history entry. If not specified, the `id` is used, unless you've set an explicit history title via [History.setHistoryTitle](#staticmethod-historysethistorytitle). Note: this currently works in IE only. You may pass a title in any other browser, but it will not change what's displayed in the history drop-down. |
| data | [Any](#type-any) | true | — | Arbitrary data to associate with this history entry. When the user next navigates to this history entry, this data will be provided as an argument to your callback function. Note that the SmartClient Core module is also required to be loaded on the page for this particular feature to work. |

---
## StaticMethod: History.registerCallback

### Description
Registers a callback to be called when the user navigates to a synthetic history entry.

**NOTE:** Only one primary callback can be registered at a time. Unless `isAdditional` is true, then `registerCallback()` registers the primary callback. To register a callback that is called in addition to the primary callback, if set, pass `true` for `isAdditional`.

If the SmartClient Core module is loaded on the page where you're using the History module, you can use any format acceptable to [Class.fireCallback](Class.md#method-classfirecallback) as the callback. The parameters 'id' and 'data' will be passed to your callback, in that order.

If the SmartClient Core module is not loaded on the page, you can use one of the following formats:

*   A function that takes an id and a data argument, in that order.
*   An object literal with a property named 'method' whose value is a function that takes an id and a data argument, in that order; and a property named 'target' that specifies the object on which the callback function should be applied. So, e.g:
    ```
     {target: myObj, method: myObj.myFunction}
     
    ```
    

The user can navigate to a synthetic history entry (and trip this callback) in one of two ways:

*   When [History.addHistoryEntry](#staticmethod-historyaddhistoryentry) method is called, a new URL associated with the history entry is generated, and the browser's back/forward navigation buttons become active. The user can then navigate back to a stored history entry via standard browser history navigation, or by explicitly hitting the appropriate URL. In this case both the ID and data parameter passed to [History.addHistoryEntry](#staticmethod-historyaddhistoryentry) will be available when the callback fires.
*   Alternatively the user can store a generated history URL (for example in a browser bookmark) and navigate directly to it in a new browser session. In this case the 'addHistoryEntry()' may not have been fired within the browser session. This callback will still fire with the appropriate history ID but the data parameter will be null. You can disable this behavior by passing in the `requiresData` parameter.

If this method is called before the page has loaded, and the page initially has a URL with a history ID, the callback will be fired with the appropriate ID on page load. However if a history callback is registered after the page has loaded, it will not be fired until the user moves to a new synthetic history entry. If you wish to explicitly check the current URL for a history entry, you can use the [History.getCurrentHistoryId](#staticmethod-historygetcurrenthistoryid) method.

When the user transitions to the history entry immediately before the first synthetic history entry, the callback is fired with an id of null.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [String](#type-string)|[Object](../reference.md#type-object) | false | — | The callback to invoke when the user navigates to a synthetic history entry. |
| requiresData | [boolean](../reference.md#type-boolean) | false | — | If passed, this callback will only be fired if the user is navigating to a history entry that was explicitly generated in this browser session. |
| isAdditional | [boolean](../reference.md#type-boolean) | true | — | If false or unspecified, then the callback is considered to be the primary callback, replacing the previous primary callback if the primary callback was previously registered. If true, then the callback is an additive callback; that is, it is called in addition to the primary callback, and after the primary callback is called. |

### Returns

`[int](../reference.md#type-int)` — the ID of the callback. This can be passed to [History.unregisterCallback](#staticmethod-historyunregistercallback) to remove the callback.

---
## StaticMethod: History.getHistoryData

### Description
Returns the data associated with the specified history id.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [String](#type-string) | false | — | The id for which to fetch history data. |

### Returns

`[Any](#type-any)` — The data associated with the specified history id.

---
## StaticMethod: History.unregisterCallback

### Description
Unregisters a callback so that it will no longer be called when the user navigates to a synthetic history entry.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [int](../reference.md#type-int) | false | — | the ID of the callback that was returned by [History.registerCallback](#staticmethod-historyregistercallback). |

### Returns

`[boolean](../reference.md#type-boolean)` — `true` if the callback registration was located and removed; `false` otherwise.

---
## StaticMethod: History.readyForAnotherHistoryEntry

### Description
Can another history entry be added to the browser's history stack in the current thread?

Browsers including Chrome and Firefox require a delay, even a minimal 1 millisecond timeout, between additions to the browser's history stack or else only the last addition will have an effect. The History module does not allow two different (by id) history entries to be added in the same thread of execution.

### Returns

`[boolean](../reference.md#type-boolean)` — whether another history entry can be added via [History.addHistoryEntry](#staticmethod-historyaddhistoryentry).

---
