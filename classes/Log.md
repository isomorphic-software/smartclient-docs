# Log Documentation

[← Back to API Index](../reference.md)

---

## Class: Log

### Description
A logging system similar to the Java log4j package: messages are logged with a "category" and "priority", and developers can dynamically set which log messages are being displayed.

5 log priorities are available, with the following general meaning:

*   "debug": diagnostic info which is only likely to be understood by a developer with source access, or would occur too frequently for normal usage
*   "info": reports of significant events in the normal operation of the subsystem
*   "warn": some kind of problem is likely to occur, an API appears is apparently being misused or will yield a partial or very slow result
*   "error": a definite error has occurred which may be recoverable
*   "fatal": total failure with no possibility of recovery

Log categories do not need to be declared in advance - you can simply make up a category name and start logging to it, and control whether that category's messages will be displayed via `setPriority()`.

**NOTE:** to open the Developer Console in any page that loads ISC, type javascript:isc.Log.show() in the URL bar - this URL is bookmarkable.

The Developer Console should **always** be open while developing any ISC-enabled application, because ISC logs many important errors and warnings to the Developer Console.

NOTE: if you have the Microsoft JavaScript Debugger installed, ISC will be unable to log stack traces on JS errors until you go to Tools->Internet Options->Advanced Tab and check "Disable script debugging". The ability to see stack traces in the Developer Console is generally much more useful for debugging ISC-based applications than the generic Javascript Debugging facilities.

### Groups

- debug

### See Also

- [Log.setPriority](#classmethod-logsetpriority)

---
## ClassAttr: Log.WARN

### Description
A declared value of the enum type [LogPriority](../reference.md#type-logpriority).

**Flags**: R

---
## ClassAttr: Log.DEBUG

### Description
A declared value of the enum type [LogPriority](../reference.md#type-logpriority).

**Flags**: R

---
## ClassAttr: Log.FATAL

### Description
A declared value of the enum type [LogPriority](../reference.md#type-logpriority).

**Flags**: R

---
## ClassAttr: Log.stackTracePriority

### Description
At this priority and above, a stack trace will be included automatically along with the log message itself.

**Flags**: IRWA

---
## ClassAttr: Log.INFO

### Description
A declared value of the enum type [LogPriority](../reference.md#type-logpriority).

**Flags**: R

---
## ClassAttr: Log.defaultPriority

### Description
Any logs below this priority will be suppressed, unless a more specific setting exists for the category.

### See Also

- [Log.setPriority](#classmethod-logsetpriority)

**Flags**: IRWA

---
## ClassAttr: Log.messageCount

### Description
Maximum number of logged messages to retain in memory.

Note that if the Developer Console is open, it will accumulate an unbounded number of messages in the "Log Messages" area. `messageCount` only affects the number of messages held in memory in the main application's browser window or tab.

**Flags**: IR

---
## ClassAttr: Log.ERROR

### Description
A declared value of the enum type [LogPriority](../reference.md#type-logpriority).

**Flags**: R

---
## ClassMethod: Log.getDefaultLogPriority

### Description
A common usage of [Class.getDefaultLogPriority](Class.md#classmethod-classgetdefaultlogpriority) is to call the method directly on the Log class.

### Returns

`[LogPriority](../reference.md#type-logpriority)` — default priority for logging messages on this object.

---
## ClassMethod: Log.setDefaultPriority

### Description
Set the default priority of messages that will be visible.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| priority | [LogPriority](../reference.md#type-logpriority) | false | — | priority level to set |
| object | [Class](#type-class)|[Instance Object](#type-instance-object) | true | — | Optional ISC class or instance - if passed the default priority will be set for logging occurring on the class or instance only. |

---
## ClassMethod: Log.getCallTrace

### Description
Returns a one-line summary of the current method call, showing method name and passed arguments. This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.getCallTrace(arguments)" whenever "this" is an instance, or call the static classMethod on the [Log](#class-log) class otherwise.

Note the `arguments` object is required in most cases for this method to function. In some browsers, it can be derived automatically, but developers looking to debug on multiple platforms should not rely on this.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| args | [Arguments](#type-arguments) | true | — | arguments object from the call to trace. If ommitted, where supported, arguments will be derived from the calling function, or if this is not supported, the method will not function. |

### Groups

- debug

---
## ClassMethod: Log.logFatal

### Description
A common usage of [Class.logFatal](Class.md#classmethod-classlogfatal) is to call the method directly on the Log class.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.logDebug](#classmethod-loglogdebug)

---
## ClassMethod: Log.echoLeaf

### Description
Return a very short (generally less than 40 characters) string representation of any object, suitable for viewing by a developer for debugging purposes. This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.echoLeaf" whenever "this" is an instance, or call the static classMethod on the [Log](#class-log) class otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to echo |

### Returns

`[String](#type-string)` — a short string representation of the object

### Groups

- debug

### See Also

- [Class.echo](Class.md#method-classecho)

---
## ClassMethod: Log.isEnabledFor

### Description
Would a message logged to the given category at the given priority appear in the Log?

NOTE: if there is no specific priority setting for a given category, the `Log.defaultPriority` is used.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | false | — | category name |
| priority | [LogPriority](../reference.md#type-logpriority) | false | — | priority level to check |

---
## ClassMethod: Log.getMessages

### Description
Return an Array of the most recently logged messages as an Array of Strings. Up to [Log.messageCount](#classattr-logmessagecount) messages may be returned.

### Returns

`[Array of String](#type-array-of-string)` — most recently logged messages

### Groups

- debug

---
## ClassMethod: Log.echo

### Description
Return a short string representation of any object, suitable for viewing by a developer for debugging purposes.

If passed an object containing other objects, echo will not recurse into subobjects, summarizing them instead via echoLeaf().

NOTE: echo() is used to generate the output shown in the Log window when evaluating an expression.

This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.echo()" whenever "this" is an instance, or call the static classMethod on the [Log](#class-log) class otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to echo |

### Returns

`[String](#type-string)` — a short string representation of the object

### Groups

- debug

### See Also

- [Log.echoAll](#classmethod-logechoall)
- [Log.echoLeaf](#classmethod-logecholeaf)

---
## ClassMethod: Log.timeMethod

### Description
Observe a method on an object, logging execution time whenever the method is called.

Call a second time with identical arguments to disable tracing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference_2.md#type-object) | false | — | object to observe |
| methodName | [String](#type-string) | false | — | name of the method to observe |

### Groups

- debug

---
## ClassMethod: Log.getPriority

### Description
Return the priority setting for a particular category.

If there is no priority setting specific to this category, `null` will be returned, NOT `Log.defaultPriority`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | false | — | category name |
| object | [Class](#type-class)|[Instance Object](#type-instance-object) | true | — | Optional class or instance to check for specific log priority overrides |

### Returns

`[LogPriority](../reference.md#type-logpriority)` — priority setting

---
## ClassMethod: Log.logInfo

### Description
A common usage of [Class.logInfo](Class.md#classmethod-classloginfo) is to call the method directly on the Log class.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.logDebug](#classmethod-loglogdebug)

---
## ClassMethod: Log.echoAll

### Description
Like echo(), except that if passed an Array, echoAll() will echo() every element of the Array. This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.echo()" whenever "this" is an instance, or call the static classMethod on the [Log](#class-log) class otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to echo |

### Returns

`[String](#type-string)` — a short string representation of the object

### Groups

- debug

### See Also

- [Log.echo](#classmethod-logecho)

---
## ClassMethod: Log.setLogPriority

### Description
A common usage of [Class.setLogPriority](Class.md#classmethod-classsetlogpriority) is to call the method directly on the Log class.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | false | — | Category for which the log priority will be updated. If not all logs on this canvas will be logged at the priority passed in. |
| priority | [LogPriority](../reference.md#type-logpriority) | false | — | priority level |

### See Also

- [Log.setPriority](#classmethod-logsetpriority)

---
## ClassMethod: Log.clear

### Description
Clear all currently displayed Log messages

---
## ClassMethod: Log.traceLogMessage

### Description
Causes a stack trace to be logged any time a message containing the provided pattern is logged. This can help figure out the origin of warnings or other mysterious logs in a large complex application.

The passed `messagePattern` is interpreted as a JavaScript regular expression.

Note: log messages that do not appear in the Developer Console because of [log priority settings](#classmethod-logsetlogpriority) will never trigger a stack trace.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| messagePattern | [String](#type-string) | false | — | — |
| prefix | [String](#type-string) | true | — | — |

### Groups

- debug

---
## ClassMethod: Log.logDebug

### Description
A common usage of [Class.logDebug](Class.md#classmethod-classlogdebug) is to call the method directly on the Log class.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.echo](#classmethod-logecho)
- [Log.setPriority](#classmethod-logsetpriority)

---
## ClassMethod: Log.clearPriority

### Description
Clear the priority setting for a particular category, so that the category's effective priority returns to `Log.defaultPriority`  
If the optional second parameter is passed, the specific priority setting for the category on that object will be cleared, so logs in that category on that object will be logged at the global priority level for the category.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | false | — | category name |
| object | [Class](#type-class)|[Instance Object](#type-instance-object) | true | — | Optional instance or class object - if passed clear logging priority for the appropriate category on that object. |

---
## ClassMethod: Log.logWarn

### Description
A common usage of [Class.logWarn](Class.md#classmethod-classlogwarn) is to call the method directly on the Log class.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.logDebug](#classmethod-loglogdebug)

---
## ClassMethod: Log.show

### Description
Open the Developer Console.

The Developer Console should **always** be open while developing any ISC-enabled application, because ISC logs many important errors and warnings to the Developer Console.

In Internet Explorer, the Developer Console is able to log a stack trace for every JS error, including errors that occur in non-ISC code.

NOTE: if you have the Microsoft JavaScript Debugger installed, ISC will be unable to log stack traces on JS errors until you go to Tools->Internet Options->Advanced Tab and check "Disable script debugging". The ability to see stack traces in the Developer Console is generally much more useful for debugging ISC-based applications than the generic Javascript Debugging facilities.

### Groups

- debug

---
## ClassMethod: Log.getDefaultPriority

### Description
Retrieves the default priority of messages that will be visible.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Class](#type-class)|[Instance Object](#type-instance-object) | true | — | Optional ISC class or instance - if passed the returns the default priority for the class or instance only. |

### Returns

`[LogPriority](../reference.md#type-logpriority)` — default priority for which messages will be logged.

---
## ClassMethod: Log.logError

### Description
A common usage of [Class.logError](Class.md#classmethod-classlogerror) is to call the method directly on the Log class.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| message | [String](#type-string) | false | — | message to log |
| category | [String](#type-string) | true | — | category to log in |

### See Also

- [Log.logDebug](#classmethod-loglogdebug)

---
## ClassMethod: Log.setDefaultLogPriority

### Description
A common usage of [Class.setDefaultLogPriority](Class.md#classmethod-classsetdefaultlogpriority) is to call the method directly on the Log class.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | false | — | Category for which the log priority will be updated. If not all logs on this canvas will be logged at the priority passed in. |
| priority | [LogPriority](../reference.md#type-logpriority) | false | — | priority level |

### See Also

- [Log.setPriority](#classmethod-logsetpriority)

---
## ClassMethod: Log.getStackTrace

### Description
Returns a "stack trace" - one line per method in the current call stack, showing the method name and any parameters passed. This function is available as a static on every ISC Class and as an instance method on every instance of an ISC Class.  
General best practice is to call the method as "this.getStackTrace" whenever "this" is an instance, or call the static classMethod on the [Log](#class-log) class otherwise.

Platform Notes: In Mozilla Firefox, if Firebug is enabled, a stack trace will be logged to the firebug console in addition to the standard stack trace string returned by this method.  
In browsers other than Internet Explorer a complete stack trace may not be available - this occurs when a function is re-entrant (meaning it calls itself). In this case the stack will terminate with text indicating where the recursive function call occurred.

See [debugging](../kb_topics/debugging.md#kb-topic-debugging) for further information information.

### Returns

`[String](#type-string)` — stack trace. Use eg [Class.logWarn](Class.md#method-classlogwarn) to log to the Developer Console.

### Groups

- debug

---
## ClassMethod: Log.applyLogPriorities

### Description
Apply a batch a batch of priority settings, as a object mapping category names to priority levels.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [Object](../reference_2.md#type-object) | false | — | priority settings for multiple categories |

---
## ClassMethod: Log.traceMethod

### Description
Observe a method on an object, logging a stack trace whenever the method is called.

Call a second time with identical arguments to disable tracing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference_2.md#type-object) | false | — | object to observe |
| methodName | [String](#type-string) | false | — | name of the method to observe |

### Groups

- debug

---
## ClassMethod: Log.setPriority

### Description
Set the priority of messages that will be visible for this log category.

After calling setPriority, any messages logged to the given category whose priority is below the specified priority will not appear in the Log.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| category | [String](#type-string) | false | — | category name |
| priority | [LogPriority](../reference.md#type-logpriority) | false | — | priority level to set |
| object | [Class](#type-class)|[Instance Object](#type-instance-object) | true | — | Optional ISC class or instance - if passed the priority will be set for logging occurring on the class or instance only. |

### See Also

- [Log.isEnabledFor](#classmethod-logisenabledfor)

---
## ClassMethod: Log.getLogPriorities

### Description
Get all priority settings as an object mapping category names to priority levels.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Class](#type-class)|[Instance Object](#type-instance-object) | true | — | Optional param to get priorities specific to some ISC class or instance. |
| overridesOnly | [boolean](../reference.md#type-boolean) | true | — | If this method is retrieving the priorities specific to logging for some class or instance, this parameter can be used to view only the overrides to the default log priorities on this object. |

### Returns

`[Object](../reference_2.md#type-object)` — priority settings

---
