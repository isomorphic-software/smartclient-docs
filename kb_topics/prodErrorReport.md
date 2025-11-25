# Production Error Reporting

[← Back to API Index](../main.md)

---

## KB Topic: Production Error Reporting

### Description
SmartClient provides a comprehensive set of APIs for capturing rich diagnostic information when JavaScript errors occur in production systems. These APIs enable developers to gather detailed context about errors, making it significantly easier to troubleshoot issues that occur in deployed applications.

This information can be captured by saving it to a [DataSource](../classes/DataSource.md#class-datasource) for later analysis, or by integrating with third-party error monitoring tools such as [Datadog](https://www.datadoghq.com/) or [Sentry](https://sentry.io/). These tools can automatically aggregate errors, track trends, and alert developers when issues occur.

**Automated AI Analysis**

It's particularly effective to automate feeding error reports to AI systems for analysis. At [Reify.com](https://www.reify.com/), we use an end-to-end approach where novel errors are automatically reported via email to developers, with AI adding analysis and suggested remedies inline. This dramatically reduces the time needed to diagnose and fix production issues.

**Available Telemetry**

SmartClient's error reporting APIs can capture:

*   **Rich Stack Traces** - Browser-specific stack trace with function names, arguments, and line numbers via [Class.getStackTrace](../classes/Class.md#method-classgetstacktrace)
*   **Timer Origin Traces** - When an error occurs in a [timer callback](../classes/Timer.md#classmethod-timersettimeout), the stack trace leading up to the setTimeout() call is automatically included, showing where the timer was originally set
*   **Event Stream History** - Complete record of user interactions leading up to the error via [EventStream](../classes/EventStream.md#class-eventstream), including mouse clicks, key presses, and other events
*   **UI Component State** - Full snapshot of visible UI components and their states via [Canvas.getTopLevelComponents](../classes/Canvas.md#classmethod-canvasgettoplevelcomponents) and [Canvas.getUISummary](../classes/Canvas.md#method-canvasgetuisummary)
*   **Framework and Browser Info** - SmartClient version, build date, browser type and version

**Example: Capturing Error Context**

The following code demonstrates how to capture comprehensive error information when a JavaScript error occurs. This example shows the key APIs and how they work together:

```
  // Set up EventStream to capture user interactions
  var eventStream = isc.EventStream.create({
      autoStart: true,
      captureEventErrors: true,
      captureClickEvents: true,
      captureKeyEvents: true
  });

  // Enable timer trace logging for setTimeout() origin tracking
  isc.Log.setPriority("timerTrace", "DEBUG");

  // Set up error listener to capture full context
  eventStream.setEventErrorListener(function(eventStreamData) {
      // Capture full stack trace
      var errorEvent = eventStreamData.events ? eventStreamData.events.last() : null;
      var stackTrace = errorEvent ? errorEvent.errorTrace : "No error trace available";

      // Get timer trace if error occurred in setTimeout callback
      var timerTrace = isc.Timer.getTimerTrace();

      // Get visible top-level components
      var topLevelComponents = isc.Canvas.getTopLevelComponents();

      // Capture UI summary for each visible component
      var componentSummaries = topLevelComponents.map(function(canvas) {
          return canvas.getUISummary();
      });

      // Assemble complete error report
      var report = {
          timestamp: new Date().toISOString(),
          errorMessage: stackTrace.split('\n')[0],

          // Stack traces
          stackTrace: stackTrace,
          timerTrace: timerTrace,

          // User interaction history
          eventStream: {
              startTime: eventStreamData.startTime,
              endTime: eventStreamData.endTime,
              nEvents: eventStreamData.nEvents,
              events: eventStreamData.events
          },

          // UI state at time of error
          visibleComponents: componentSummaries,
          topLevelComponentsCount: topLevelComponents.length,

          // Environment info
          browser: {
              name: isc.Browser.appCodeName || isc.Browser.appName,
              version: isc.Browser.version,
              platform: isc.Browser.OS || isc.Browser.platform
          },
          framework: {
              version: isc.version,
              buildDate: isc.buildDate
          }
      };

      // Verify data is JSON serializable
      var reportJSON = JSON.stringify(report, null, 2);

      // Send to your error tracking system (DataSource, Datadog, Sentry, etc.)
      // myErrorTrackingDS.addData(report);
  });
 
```

**Example Error Report Data**

Here's an abridged sample of what the captured error data looks like:

```
 {
   "timestamp": "2025-10-16T00:42:59.912Z",
   "errorMessage": "Error: Test error triggered from setTimeout callback",
   "stackTrace": "Error: Test error triggered from setTimeout callback
     null.eval(<no args: exited>) @ [no file]:167:23
     [c]Class.fireCallback(...) on [Class Timer] @ ISC_Core.js:3500:34
     [c]Timer._fireTimeout(...) on [Class Timer] @ ISC_Core.js:31803:10
   Stack trace for setTimeout() call:
     isc_Button.click() on [Button ID:isc_Button_2] @ [no file]:161:32
     ...",
   "timerTrace": "
     isc_Button.click() on [Button ID:isc_Button_2] @ [no file]:161:32
     ...",
   "eventStream": {
     "startTime": "2025-10-16T00:42:58.958Z",
     "nEvents": 1,
     "events": [
       {
         "eventType": "mouseout",
         "timeOffset": 948,
         "locator": "//:Label[title=\"Header Section\"]/",
         "targetID": "isc_Label_0",
         "targetClass": "Label",
         "errorTrace": "...",
         "threadCode": "TMR0"
       }
     ]
   },
   "visibleComponents": [
     {
       "id": "testModalWindow",
       "smartClientComponentType": "Window",
       "members": [
         {
           "id": "isc_DynamicForm_0",
           "smartClientComponentType": "DynamicForm",
           "values": {},
           "fields": [...]
         }
       ]
     },
     {
       "id": "testMainLayout",
       "smartClientComponentType": "VLayout",
       "members": [...]
     }
   ],
   "topLevelComponentsCount": 2,
   "browser": {
     "name": "Chrome",
     "version": 140,
     "platform": "MacOS"
   },
   "framework": {
     "version": "v15.0d_2025-10-16",
     "buildDate": "2025-10-16"
   }
 }
 
```

This comprehensive error context makes it much easier to reproduce and fix issues that occur in production, especially when combined with AI analysis tools.

### Related

- [Class.getStackTrace](../classes/Class.md#classmethod-classgetstacktrace)
- [Log.getStackTrace](../classes/Log.md#classmethod-loggetstacktrace)
- [Timer.getTimerTrace](../classes/Timer.md#classmethod-timergettimertrace)
- [Canvas.getTopLevelComponents](../classes/Canvas.md#classmethod-canvasgettoplevelcomponents)
- [Class.getStackTrace](../classes/Class.md#method-classgetstacktrace)
- [EventStream.setEventErrorListener](../classes/EventStream.md#method-eventstreamseteventerrorlistener)
- [Canvas.getUISummary](../classes/Canvas.md#method-canvasgetuisummary)

---
