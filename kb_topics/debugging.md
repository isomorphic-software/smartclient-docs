# Debugging

[← Back to API Index](../reference.md)

---

## KB Topic: Debugging

### Description
#### Built-in Diagnostics

The SmartClient Developer Console is a suite of development tools implemented in SmartClient itself. The Console runs in its own browser window, parallel to your running application, so it is always available in every browser, and in every deployment environment.

The Developer Console can be opened by calling `isc.showConsole()` on any page in which SmartClient has been loaded. You can create a bookmark in your browser to quickly show the Console on any SmartClient application, without any changes to the application code:

1\. Create a new bookmark in your browser.  
2\. Enter url "javascript:isc.showConsole()".  
3\. Label the bookmark as "Show Console".  
4\. Consider adding this to the Bookmarks Toolbar. This allows one-click access to the Console from any SmartClient application.

Note: For most browsers you can evaluate javascript directly from the browser URL bar by entering `javascript:_string to evaluate_` directly in the URL bar, so setting up a bookmark is not strictly necessary. For Firefox 6 and above, this feature has been disallowed, but the bookmark approach will still work. Alternatively developers could use [Firefox Scratchpad](http://blog.mozilla.com/devtools/2011/08/15/introducing-scratchpad/) to launch the console.

Basic information on the features of the Developer Console can be found in the QuickStart Guide. For information about the "RPC" tab of the Developer Console and the request profiling information it can provide, see [the Developer Console RPC tab](devConsoleRPCTab.md#kb-topic-the-developer-console-rpc-tab). The Develper Console also supports debugging of remote pages (very useful for mobile devices) - see [remoteDebugging](remoteDebugging.md#kb-topic-remote-debugging) for more information. The remainder of this topic focuses on use of the log system and related debugging facilities.

The Developer Console contains a "Results" pane that displays a list of diagnostic messages logged by the SmartClient framework. The "Logging Preferences" menu lets you enable and disable SmartClient's built-in diagnostics in several categories. Because important diagnostic messages may be logged at any time, you should have the Developer Console open whenever you are working with SmartClient (and you should bookmark the "javascript:" expression above to make this easier).

Log messages are of the format:

   _timestamp_:_priority_:_category_:_message_

For example, the following log message:

```
     11:59:25:806:INFO:Page:Page loading complete.
```
Occurred at 11:59:25 local time and 806 milliseconds. It's priority was `INFO`, it occurred in the category _Page_, and the message is "Page loading complete.".

Each logging _category_ has a _priority_ associated with it. If a message's priority is lower than the current priority for the category it is logged in, the message will be suppressed (will not appear in the "Results" pane).

It is critical to be familiar with the diagnostic categories built-in to SmartClient - you will use them in most debugging sessions. Open the Logging Preferences menu and select "More.." to see a list of diagnostic log categories. Hover over each category name to see a description of what kind of messages are logged in the category.

#### Debugging JavaScript Errors

Javascript errors will typically be reported in the Developer Console. Wherever possible a stack trace will be included which can help determine the cause of the error. In addition to this, recent versions of the Firefox browser (versions 6.0 and above) ship with some useful development tools including the Error Console for reporting errors. We also recommend Console2 and Firebug for debugging in Firefox.

When JavaScript errors occur, SmartClient is usually able to report full stack traces in the Developer Console. This can be invaluable when your code triggers a JavaScript error in the SmartClient libraries themselves, or when it is unclear how your code is being called. Stack traces from the Developer Console Explorer should _always_ be included in issue reports sent to Isomorphic Software, if at all possible.

#### Avoiding JavaScript Validation Errors from the Framework

In Eclipse, you may find that you're getting a bunch of spurious validation errors from the SmartClient Framework JavaScript code. This can be distracting and slow down interactions with Eclipse. If you encounter this problem, you can try to apply the following fixes (verified in Eclipse 4.3 "Kepler"):

*   For each affected project, in _Properties => JavaScript => Include Path => Source_, exclude the SmartClient Framework files that are triggering the errors.
*   If errors are still being reported, you can switch off validation entirely:
    *   In _Window => Preferences => JavaScript => Validator => Errors/Warnings_, uncheck "Enable JavaScript Semantic Validation".
    *   For each affected project, in _Properties => Builders_, uncheck "JavaScript Validator" underneath where it says "Configure the builders for the project," and make sure that the "Enable project-specific settings" checkboxes are unchecked at both levels (second one in parens): _Properties => JavaScript => Validation (=> Errors/Warnings)_.

A more in-depth discussion can be found at [http://stackoverflow.com/questions/17329028/eclipse-kepler-disable-javascript-validation](http://stackoverflow.com/questions/17329028/eclipse-kepler-disable-javascript-validation).

#### Inspecting application state

The "Evaluate JS Expression" area of the Results Pane in the Developer Console can be used to inspect the current state of a SmartClient application by running JavaScript code. The result of any expression you evaluate will be intelligently summarized (via [Log.echo](../classes/Log.md#classmethod-logecho)). For example, simply typing a component's ID and pressing the "Eval JS" button will give you a dump of it's current property values.

Many, many component APIs can be usefully called while troubleshooting, eg, [ListGrid.data](../classes/ListGrid_1.md#attr-listgriddata) is a [ResultSet](../classes/ResultSet.md#class-resultset) when a grid is DataBound and [ResultSet.get](../classes/ResultSet.md#method-resultsetget) can be called to inspect the current values on records. In addition, new application code can be tried out, for example, you might repeatedly instantiate a new component, trying variants on the properties you could give it.

**Inspecting transient application state with logs**

Transient state, such as the values of local variables in a method that is crashing, can be sent to the Developer Console via using the [Log](../classes/Log.md#class-log) class. For example, to dump the value of the local variable "request":

```
     isc.logWarn("request is: " + isc.echo(request));
```
It's a good idea to dump the values of local variables in any method that is crashing or behaving unexpectedly.

Note the use of [logWarn()](../classes/isc.md#staticmethod-isclogwarn) above: in typical debugging sessions, it's best to simply use the `logWarn` method to output diagnostics to ensure your message will not be suppressed by log priority settings.

NOTE: never use the native `alert()` method to output diagnostics. Among other issues, `alert()` can affect timing, masking or altering the behavior you were trying to debug. SmartClient's logging system doesn't suffer from these problems and provides much more control.

#### Issues with the SmartClient Server
The [SmartClient Server](iscServer.md#kb-topic-smartclient-server-summary) has extensive diagnostic logging capabilities. See the [Server Logging topic](serverLogging.md#kb-topic-server-logging) for details on how to configure logging.  
Developers experiencing java thread deadlocks on the server should also consult the troubleshooting steps documented [here](troubleshootingServerDeadlocks.md#kb-topic-troubleshooting-thread-deadlocks-on-the-server).
#### Issue Reports

If you believe you've discovered a bug in SmartClient or you are having trouble using SmartClient APIs, you can report it in [the SmartClient Forums](http://forums.smartclient.com/).

**How quickly your issue is resolved is entirely up to you**. If you follow the steps below and submit an appropriate issue report, you will generally receive a rapid solution from Isomorphic Support, regardless of what support level you have, because Isomorphic aggressively corrects bugs and legitimate usage issues. If you skip steps you are likely to be directed back to this document and asked to submit a more complete issue report.

Before reporting an issue, ensure that you:

*   Have read the *QuickStart Guide* cover to cover. Later chapters cover more advanced topics and provide links to further examples and reference.
*   Have searched the *Feature Explorer* for examples that show what you are trying to do
*   Have searched this reference, trying multiple searches using different, common and related terms for what you are trying to do (eg for search, try "search", "filter", "criteria", "find", "match", etc)
*   Have searched the public [forums](http://forums.smartclient.com)

Always include:

*   A description of what you are trying to accomplish **from an end user's perspective**. The best answers often point out a simpler approach.
*   The browser(s), operating system(s) and SmartClient version(s) you experience the error on (SmartClient version is available in the lower-left handle corner of the Developer Console)

Then, include **either** a standalone test case (see below), **or**:

*   For JS errors, Stack traces from Firebug (for Firefox) or the Developer Console (for IE), as covered under "Debugging JavaScript Errors" above
*   What server platform and [databinding approach](clientServerIntegration.md#kb-topic-client-server-integration) you are using, if applicable
*   contents of the SmartClient Developer Console "Log messages" area, with appropriate diagnostic categories set the DEBUG or INFO level (see "Built-in Diagnostics" above)
*   for any problem involving server contact, the complete server-side log for the request that fails or produces unexpected results
*   Results of calling `echo()` on local variables or other application state you think is relevant (see "Inspecting Application State" above)
*   sample code and sample data

**Preparing a standalone test case**

A standalone test case is one of:

1.  a chunk of JavaScript code that can be executed from the "Eval JS" area of the Developer Console on some specified page within the unmodified SmartClient SDK, demonstrating your issue
2.  an .html or .jsp file that can be dropped at a specified location into an unmodified SmartClient SDK and will run without changes, demonstrating your issue.
3.  a .zip file that includes a standalone .html/.jsp file as above, as well as dependencies required to make the test case runnable, such as XML datasets

Submitting a standalone test case removes any ambiguity as to whether there is a bug in SmartClient or a bug in your code, and eliminates the possibility of Isomorphic Support responding with a "works for me" result due to incomplete information. Issues with verified test cases are routed directly to the engineer that authored the relevant SmartClient subsystem, often as the new highest priority task. In addition, the process of preparing a test case very often allows you to solve the issue yourself, if the underlying issue is not actually a framework bug.

There are two approaches to test case preparation:

1.  Add code to an existing SmartClient example until you can reproduce the problem
2.  Remove code from your application until it minimally shows the problem and runs standalone

For approach #1, find the nearest match to your use case in the *FeatureExplorer* examples or in the other examples accessible from the Examples folder of the SDK, then try to minimally modify that example to demonstrate your issue. Feature Explorer examples are a particularly good starting point because you can simply copy the code from the Feature Explorer to the Eval JS area of the Developer Console and begin changing it, and if successful this yields a type #1 test case, the easiest for you to submit and most efficient for Isomorphic to work with.

For approach #2,

1.  If a server is involved in initial page generation (eg a .jsp file), in most cases you can eliminate many server dependencies **and** create an easily modifiable starting point by using the browser's "View Source" feature to save a copy of the generated HTML output as an .html file in the same directory as the .jsp file that generated it. Such a file will generally continue to function (all relative paths are still correct), and can be modified freely without the need to later revert changes to a .jsp.
2.  Eliminate any code that isn't involved in the interaction. Keep running the test case as you eliminate code to ensure you are still seeing the issue (you may solve it this way, or find key preconditions that you can report to Isomorphic)
3.  For any issue that isn't cosmetic, revert to a default SmartClient skin
4.  For any necessary RPC/DataSource interactions, spoof the interaction with one of these approaches:
    *   switch any DataSources to one of the sample DataSources from the SDK (eg "supplyItem") if your issue can still be reproduced in this case.
    *   create a small sample dataset in JavaScript directly in the .html file, and use a [clientOnly DataSource](../classes/DataSource.md#attr-datasourceclientonly) with that dataset.
    *   capture server responses verbatim by setting the RPCManager log category to DEBUG, save the responses as flat files, and set [DataSource.dataURL](../classes/DataSource.md#attr-datasourcedataurl) to point at them.
    *   for RPCs, instead of calling the RPCManager, directly call your own callback function, passing a spoofed RPCResponse that includes just the fields your code depends upon
5.  Finally, move your .html file into the stock SmartClient SDK along with any remaining dependencies and verify the problem can still be reproduced

Having prepared the test case, combine it with the other required issue report information covered above, and submit it to the [forums](http://forums.smartclient.com/), or, if you have Enterprise Support, at the [Customer Support Extranet](http://support.isomorphic.com/).

#### Using the Debug Modules (Advanced)

See [Using the Debug Modules](debugModules.md#kb-topic-using-the-debug-modules).

#### Adding your own diagnostic categories

Calling `logWarn()` is fine for a log statement you plan to delete at the end of the debugging session. However, many log statements have lasting value if you could enable or disable them only when you need the relevant diagnostics, like SmartClient's built-in diagnostic categories. To do this, pick a priority level less than `WARN` (`INFO` or `DEBUG`), and call the corresponding method on the Log class (`logInfo()` or `logDebug()`), passing the category name as a second parameter. For example:

```
     isc.Log.logInfo("first record is: " + isc.Log.echo(myGrid.data.get(0)),
                     "myGridLoading");
 
```
This message will no longer appear in the Results Pane by default, because its priority (`INFO`) is less than the default of `WARN`. To see this message, open the Logging Preferences menu and pick "More..", then click the "Add" button, enter "myGridLoading" as the category name and set the priority to `INFO`. The message will now appear next time it is logged.

Now you have a custom log category that you and other developers can use to debug your application, subsystem by subsystem. These diagnostics will be available to you both in development and production environments.

As with SmartClient's built-in diagnostics, you may choose to log certain messages in your custom category at the `DEBUG` level and a lesser number of messages at the `INFO` level, to create different depths of diagnostic output.

#### Logging refinements

The core log methods (`logDebug()`, `logInfo()`, `logWarn()`) and the "echo" facilities (`echo()` and `echoAll()`) are available on every SmartClient component and Class. Hence, in many cases, the special JavaScript value "this" will refer to an object that supports `logWarn()` et al. For example:

```
     isc.Canvas.create({
        ID:"canvasExample",
        contents:"Hello World!",
        click:"this.logWarn('the Canvas is: ' + this.echo(this))"
     });
 
```
The special value "this" is not always set to a SmartClient component, for example, in some kinds of callbacks (eg [fetchData()](../classes/ListGrid_1.md#method-listgridfetchdata)). When in doubt, use these methods via the Log class as `isc.Log.logWarn()`.

**Find the source of logs** Sometimes, you will see a log message with a warning, usage error or other unusual condition, and it won't be clear how your code is causing the log to appear. In these situations, you can use [Log.traceLogMessage](../classes/Log.md#classmethod-logtracelogmessage) to request that a stack trace is logged whether that specific message appears. **Logging performance**

Because the log message is actually formed _before_ the call to the log system, logs that are suppressed can still carry a performance penalty. This is particularly true of logs that output a lot of data or occur frequently. To avoid this penalty, you can check in advance whether a message will be suppressed using [isc.Log.logIsDebugEnabled()](../classes/Class.md#classmethod-classlogisdebugenabled) and [isc.Log.logIsInfoEnabled()](../classes/Class.md#classmethod-classlogisinfoenabled). For example:

```
     if (isc.Log.logIsInfoEnabled("myGridLoading")) {
        isc.Log.logInfo("first record is: " + isc.Log.echo(myGrid.data.get(0)),
                        "myGridLoading");
     }
 
```
Generally, it is only important to do this for logs that will occur multiple times during a given user interaction (eg a mousedown or keypress) and/or that call `echo()` on objects with many properties.

### See Also

- [serverLogging](serverLogging.md#kb-topic-server-logging)
- [remoteDebugging](remoteDebugging.md#kb-topic-remote-debugging)

---
