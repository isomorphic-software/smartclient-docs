# Integrating SmartClient with Playwright

[← Back to API Index](../reference.md)

---

## KB Topic: Integrating SmartClient with Playwright

### Description
Playwright is a modern automated testing platform that can be used to test web applications. SmartClient supports a number of features to easily integrate with Playwright, making it extremely straightforward to start creating effective automated tests for SmartClient applications.

_For an overview of Automated Testing in SmartClient, see the documentation [here](automatedTesting.md#kb-topic-automated-testing)._

The Playwright website contains very helpful guides to walk you through how to install Playwright, how to run Playwright tests, and how to create test suites. If you're new to Playwright, we'd recommend you start [here](https://playwright.dev/docs/intro). You should be able to rapidly learn how to install Playwright and how to create and run e2e (end-to-end) tests.

**Custom Playwright commands for SmartClient applications**

The SmartClient SDK ships with a sample `commands.js` file, available under:

```
smartclientSDK/tools/playwright/commands.js
 
```
This file contains custom helper methods which simplify interacting with a running SmartClient application as Playwright runs your tests. See below for more details.

**Using _locators_ to interact with SmartClient User Interface components**

The [AutoTestLocator](../reference_2.md#type-autotestlocator) subsystem is used to reliably identify DOM elements generated within a SmartClient application.

For general concepts, see [obtainingLocators](../reference.md#kb-topic-obtaining-locators). The following is Playwright-specific guidance.

The sample `commands.js` file includes a `getSC()` method that uses [AutoTest.waitForElement](../classes/AutoTest.md#classmethod-autotestwaitforelement) to wait for any pending system actions, resolve an AutoTestLocator to a DOM element, and yield it back as a Playwright ElementHandle. You can make use of this method in your test code as follows:

```
 const element = await page.getSC(locator);
 await element.click();
 
```
or directly:
```
 await page.clickSC(locator);
 
```
`clickSC()` calls `getSC()` and handles the click interaction in just one call.

**Scroll behavior in Playwright**

For general concepts, see [scrollingBehavior](../reference.md#kb-topic-understanding-scroll-behavior). The following is Playwright-specific guidance.

Playwright actions like [click](https://playwright.dev/docs/api/class-elementhandle#element-handle-click) may scroll the target element into view. If SmartClient components redraw synchronously on scroll, this can interfere with Playwright actions. To avoid issues, ensure the element is in view before interacting.

For SmartClient skins that use [custom scrollbars](../classes/Canvas.md#attr-canvasshowcustomscrollbars), the Playwright [mouse.wheel](https://playwright.dev/docs/api/class-page#page-mouse-wheel) method may not see the component as a valid target for scrolling. For this reason the sample `commands.js` file includes a `scrollSC()` method. This method takes a locator plus target left and top position as arguments. Note that you can specify left and top as an explicit pixel position, or use a percentage string like "50%". For example, to scroll some component to its mid point vertically while leaving the horizontal scroll position unchanged you could invoke:

```
 await page.scrollSC(locator, null, "50%");
 
```

**Interacting with FormItems in Playwright**

SmartClient's SelectItem, ComboBoxItem and CheckboxItem are based on custom HTML rather than built-in browser controls, because this is required to provide advanced functionality such as multi-column dropdowns. Because of this, the _check()_ and _uncheck()_ functions for CheckboxItem and the _select()_ function for SelectItem and ComboBoxItem are not applicable.

Instead, the "click()" function is the way to interact with these controls, for example:

```
      await page.goto('https://smartclient.com/smartclient-latest/showcase/?id=updateOperation');

      // Click to start editing the grid
      await page.clickSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]' +
              '/member[index=1||length=4||Class=ListGrid||classIndex=0||classLength=1]/body/row[1]/col[2]');

      // Type a value into the 'description' item
      await page.typeSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]/' +
              'member[index=2||length=4||Class=DynamicForm||classIndex=0||classLength=1]/item[name=description]/element',
              'Glue Pelikan Roll-fix Refill Permanent #955');

      // Click the 'units' item to show the pickList
      await page.clickSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]/' +
              'member[index=2||length=4||Class=DynamicForm||classIndex=0||classLength=1]/item[name=units]/textbox');

      // Click a value in the pickList drop down
      await page.clickSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]/' + 
              'member[index=2||length=4||Class=DynamicForm||classIndex=0||classLength=1]/item[name=units]/pickList/body/row[3]/col[0]');

      // Click to toggle the value of the 'inStock' checkbox'
      await page.clickSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]/' +
              'member[index=2||length=4||Class=DynamicForm||classIndex=0||classLength=1]/item[name=inStock]/valueicon');

      // Click the Save button
      await page.clickSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]/' +
              'member[title=Save]/');

      // Verify the value has been updated
      const element = await page.getSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]/' +
              'member[index=1||length=4||Class=ListGrid||classIndex=0||classLength=1]/body/row[1]/col[2]');
      const text = await element.textContent();
      expect(text.trim()).toBe('Glue Pelikan Roll-fix Refill Permanent #955');
 
```
**Using force-click to dismiss [click masks](../classes/Canvas.md#method-canvasshowclickmask)**

In some cases you may need to dismiss a SmartClient click-mask by clicking. Examples include certain styles of drop-down, grid editing interactions, etc. - that are dismissed via an outside-click. Playwright will reject attempts to send a `click()` to some element under the click-mask by default as the target element will be obscured by the click mask in the DOM, and so is not directly "visible" as far as Playwright is aware. You can handle this by specifying [force:true](https://playwright.dev/docs/api/class-elementhandle#element-handle-click) on your click method.

For example if you have a _multiple:true_ SelectItem, a clickMask is used to watch for the user clicking outside the SelectItem drop-down. To dismiss the drop-down from a Playwright test, we recommend sending a `{force: true}` click() method to some other element on the page:

```
     await page.getSC(locator).click({force: true}) / await page.clickSC(locator, {force: true})
 
```
In this case _locator_ refers to the target component that we click on the app to dismiss the dropdown. Note that depending on how the application is configured, this click may dismiss the dropdown and prevent the click action from firing for the target that was actually clicked. You can handle this by invoking a second click to mimic the user interaction. For example:
```
     await page.getSC(locator).click({force: true});
     await page.getSC(locator).click();
 
```

**Waiting for asynchronous actions in Playwright**

Because the `getSC()` method uses [AutoTest.waitForElement](../classes/AutoTest.md#classmethod-autotestwaitforelement), which will not resolve until all [outstanding asynchronous system actions have completed](../classes/AutoTest.md#classmethod-autotestissystemdone), it is not usually necessary to write test code that explicitly waits for actions to complete (using `page.waitForTimeout()` calls, for example).  
In other words: if an action in a test kicks off a SmartClient DataSource operation and the next action is using `getSC()` to interact with another SmartClient component, the test will automatically wait for the asynchronous operation from the first action to complete before proceeding with the second action.

This alone may not be sufficient to handle every asynchronous behavior in an application. In some cases you may want to explicitly wait for the SmartClient framework to complete some action without having a subsequent `getSC()` call in your test. The [AutoTest.waitForSystemDone](../classes/AutoTest.md#classmethod-autotestwaitforsystemdone) method can be used to handle this. The `commands.js` sample file includes a custom method `"waitForSCDone"` which wraps this method in a Playwright helper.

To explicitly wait for all asynchronous SmartClient actions to complete, call the method in your test code as follows:

```
  await page.waitForSCDone();
 
```
For more details on explicitly handling asynchronous actions without using `getSC()`, see the [waitingForAsyncActions](waitingForAsyncActions.md#kb-topic-waiting-for-asynchronous-actions) section.

Additionally you may have asynchronous behaviors that are unrelated to SmartClient interactions, such as network activity that does not go through the SmartClient [RPCManager](../classes/RPCManager.md#class-rpcmanager), asynchronous rendering of third party widgets, etc. In these cases [AutoTest.isSystemDone](../classes/AutoTest.md#classmethod-autotestissystemdone) may return true even though the application is not ready for further input.

The `options` parameter for `getSC()` can be used to change the [waitStyle](../reference.md#attr-elementwaitconfigwaitstyle) passed to [AutoTest.waitForElement](../classes/AutoTest.md#classmethod-autotestwaitforelement). If you request `"element"` rather than `"system"`, instead of relying on [AutoTest.isSystemDone](../classes/AutoTest.md#classmethod-autotestissystemdone), the framework will continue trying to resolve the locator to an element until the command times out. This gives you an easy way to instruct the test case to keep trying to resolve a locator even after [AutoTest.isSystemDone](../classes/AutoTest.md#classmethod-autotestissystemdone) returns true.

Both `waitForSCDone()` and `getSC()` support being passed an explicit timeout on the `options` parameter. This governs how long the methods will wait for system quiescence / for the locator to be resolved. If no explicit timeout was specified, the default wait time for these methods is 30 seconds, but this can be customized by setting `"scCommandTimeout"` in your SmartClientCommands configuration.

Note that as long as `waitStyle` is set to `"system"`, it is very rare for `getSC()` methods to time out as the application will wait for [AutoTest.isSystemDone](../classes/AutoTest.md#classmethod-autotestissystemdone) and then attempt to resolve the locator. If it fails to resolve the locator to an element it will return `null` immediately rather than continue attempting to resolve the locator until the command times out.

If `getSC()` or `waitForSCDone()` does time out the Playwright test will fail.

**RPC timing logs in Playwright**

For general concepts, see [usingRPCTimingLogs](../reference.md#kb-topic-rpc-timing-logs). The following is Playwright-specific guidance.

The sample `commands.js` file includes a method `"enableSC_RPCTimeout"` which makes use of console logging in Playwright to take advantage of these APIs and log timing information for slow requests.

`enableSC_RPCTimeout` should typically be called only once, at the beginning of your test. It will remain active as long as the page is loaded. The method takes the following arguments:

*   `logThreshold` Any RPCs whose duration exceeds this threshold will log timing information via a console.log() call.
*   `timeoutThreshold` Any RPCs whose duration exceeds this threshold will cause the test to fail.
*   `options` This parameter in an object where you can set various attributes to configure logging behavior. These include:
    *   `logDetail`: one of `"none"`, `"summary"`, `"detailed"` or `"all"`
    *   `logSuccess`: If true, log a 'success' type notification for RPC transactions that do not exceed the specified timing threshold. This log will not include any explicit timing data
    *   `includeClientTimings`: Should detailed timing for client-processing be included?
    *   `includeServerTimings`: Should detailed timing for server-processing be included?

See the implementation in `commands.js` for more details.

Here's an example of how this might be used in a test file:

```
 // If the turnaround takes more than this many millis, log the timing information
 const LOG_TIMEOUT = 1000;
 // If the turnaround takes longer than this many millis, the test fails
 const FAILURE_TIMEOUT = 5000;
 
 test('Test Suite', async ({ page }) => { 
     await page.goto(targetUrl); 
     await page.enableSC_RPCTimeout(LOG_TIMEOUT, FAILURE_TIMEOUT, {logDetail:"detailed"});
     
     // test code goes here
 });
 
```
Note: `enableSC_RPCTimeout()` is effectively "invisible" to the flow of your test unless a transaction is encountered which exceeds the timeoutThreshold. If you want to explicitly wait for all pending actions to complete at any point, including waiting for active RPCRequests to be resolved, you can use the `waitForSCDone` method described above.

**Drag and drop in Playwright**

Playwright provides built-in support for drag and drop operations through the [dragAndDrop](https://playwright.dev/docs/api/class-page#page-drag-and-drop) method. The sample `commands.js` file includes a `dragAndDropSC()` method that handles complex drag and drop operations in SmartClient grids and lists, including logic for empty grids, row positioning, and drop position adjustments.

Here's an example of how to use drag and drop in Playwright:

```
     await page.dragAndDropSC(sourceLocator, targetLocator);
 
```
where _sourceLocator_ and _targetLocator_ are AutoTest locators for the source and target elements.

**Final Note**

In addition to the custom methods and approaches described above, developers can also always use the [page.evaluate()](https://playwright.dev/docs/api/class-page#page-evaluate) method to execute arbitrary JavaScript with access to the application scope.

**Playwright configuration for custom SmartClient commands**

The custom methods shipped in the SmartClient SDK will respect the following settings if present in the SmartClientCommands configuration:

*   _scLogCommands_: Boolean - if true each command will be logged via console.log()
*   _scCommandTimeout_: Number - default timeout for getSC() and waitForSCDone() in ms

---
