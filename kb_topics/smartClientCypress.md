# Integrating SmartClient with Cypress

[← Back to API Index](../reference.md)

---

## KB Topic: Integrating SmartClient with Cypress

### Description
Cypress is an automated testing platform that can be used to test web applications. SmartClient supports a number of features to easily integrate with Cypress, making it extremely straightforward to start creating effective automated tests for SmartClient applications.

_For an overview of Automated Testing in SmartClient, see the documentation [here](automatedTesting.md#kb-topic-automated-testing)._

The Cypress website contains very helpful guides to walk you through how to install Cypress, how to run the Cypress application, and how to create tests. If you're new to Cypress, we'd recommend you start [here](https://docs.cypress.io/guides/getting-started/installing-cypress). You should be able to rapidly learn how to install cypress and how to create and run e2e (end-to-end) tests.

**Custom cypress commands for SmartClient Applications**

The SmartClient SDK ships with a sample `commands.js` file, available under `smartclientSDK/tools/cypress/commands.js` .

This file contains some [custom commands](https://docs.cypress.io/api/cypress-api/custom-commands) which simplify interacting with a running SmartClient application as cypress runs your tests. See below for more details.

**Using _locators_ to interact with SmartClient User Interface components**

The [AutoTestLocator](../reference_2.md#type-autotestlocator) subsystem is used to reliably identify DOM elements generated within a SmartClient application.

You have two options for obtaining locators from your app:

**1.-** The Developer Console.

Open the Developer Console and, in the first tab titled "Results", click on the link near the middle of the page, titled "Show AutoTest Locators." Now as you click on elements within the application, the locator for the element will be displayed in the Developer Console. Double-click the locator (or select and use `Ctrl+C`) to copy it to the clipboard.

**2.-** Via the [AutoTest.installLocatorShortcut](../classes/AutoTest.md#classmethod-autotestinstalllocatorshortcut) script. After running the scriptlet to install the locator shortcut, you can simply click on the target element while holding down the appropriate modifier keys and the appropriate locator string will be copied to the clipboard.

**Resolving locators back to DOM elements in Cypress**

A stored locator string can be resolved back to a DOM element via [AutoTest.getElement](../classes/AutoTest.md#classmethod-autotestgetelement) or [AutoTest.waitForElement](../classes/AutoTest.md#classmethod-autotestwaitforelement). Using `waitForElement()` is preferable as this will not resolve until any active, asynchronous operations within an application have completed.

The sample `commands.js` file includes a command `"getSC"` which uses `waitForElement()` to wait for any pending system actions, then resolve an AutoTestLocator to its target DOM element and yield it back. You can make use of this command in your test code as follows:

```
  cy.getSC(<locator>).click();
 
```

**Cypress actions native scroll behavior**

By default Cypress actions such as [click](https://docs.cypress.io/api/commands/click) can cause the target element to be scrolled on the page. See the `scrollBehavior` option described [here](https://docs.cypress.io/guides/references/configuration#Actionability).

In some cases SmartClient components may redraw synchronously on scroll which may interfere with your Cypress test's execution. For example if a listGrid is [incrementally rendering](../classes/ListGrid_1.md#attr-listgridshowallrecords) its records, a scroll may require a redraw to ensure the user doesn't see unrendered cells that were previously outside the viewport. If this happens while a Cypress click action is in progress, Cypress will throw an error as the target element will have been replaced in the DOM while the action was still in progress. Developers may avoid this problem by ensuring the target element is already scrolled into view, and specifying `scrollBehavior:false` on Cypress' click command options.

**Scrolling SmartClient components**

In some cases a Cypress test may need to explicitly change the scroll position of a SmartClient component.

For SmartClient skins that use [custom scrollbars](../classes/Canvas.md#attr-canvasshowcustomscrollbars), the Cypress [scrollTo](https://docs.cypress.io/api/commands/scrollto) command may not see the component as a valid target for scrolling. For this reason the sample `commands.js` file includes a `scrollSC()` command. This command takes a locator plus target left and top position as arguments. Note that you can specify left and top as an explicit pixel position, or use a percentage string like "50%". For example, to scroll some component to its mid point vertically while leaving the horizontal scroll position unchanged you could invoke:

```
  cy.scrollSC(<locator>, null, "50%");
 
```
**Interacting with SmartClient FormItems**

SmartClient's SelectItem, ComboBoxItem and CheckboxItem are based on custom HTML rather than built-in browser controls, because this is required to provide advanced functionality such as multi-column dropdowns. Because of this, the _check()_ and _uncheck()_ functions for CheckboxItem and the _select()_ function for SelectItem and ComboBoxItem are not applicable.

Instead, the "click()" function is the way to interact with these controls, for example:

```
      cy.visit('https://smartclient.com/smartclient-latest/showcase/?id=updateOperation')

      // Click to start editing the grid
      cy.getSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]' +
              '/member[index=1||length=4||Class=ListGrid||classIndex=0||classLength=1]/body/row[1]/col[2]'
      ).click()

      // Type a value into the 'description' item
      cy.getSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]/' +
              'member[index=2||length=4||Class=DynamicForm||classIndex=0||classLength=1]/item[name=description]/element'
      ).type('Glue Pelikan Roll-fix Refill Permanent #955')

      // Click the 'units' item to show the pickList
      cy.getSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]/' +
              'member[index=2||length=4||Class=DynamicForm||classIndex=0||classLength=1]/item[name=units]/textbox'
      ).click()

      // Click a value in the pickList drop down
      cy.getSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]/' + 
              'member[index=2||length=4||Class=DynamicForm||classIndex=0||classLength=1]/item[name=units]/pickList/body/row[3]/col[0]'
      ).click()

      // Click to toggle the value of the 'inStock' checkbox'
      cy.getSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]/' +
              'member[index=2||length=4||Class=DynamicForm||classIndex=0||classLength=1]/item[name=inStock]/valueicon'
      ).click()

      // Click the Save button
      cy.getSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]/' +
              member[title=Save]/'
      ).click()

      // Verify the value has been updated
      cy.getSC('//testRoot[]/child[index=0||length=1||Class=VStack||classIndex=0||classLength=1]/' +
              'member[index=1||length=4||Class=ListGrid||classIndex=0||classLength=1]/body/row[1]/col[2]'
      ).invoke('text').then((text) => { 
          expect(text.trim()).to.equal('Glue Pelikan Roll-fix Refill Permanent #955')
      })
 
```
**Using force-click to dismiss [click masks](../classes/Canvas.md#method-canvasshowclickmask)**

In some cases you may need to dismiss a SmartClient click-mask by clicking. Examples include certain styles of drop-down, grid editing interactions, etc. - that are dismissed via an outside-click. Cypress will reject attempts to send a `click()` to some element under the click-mask by default as the target element will be obscured by the click mask in the DOM, and so is not directly "visible" as far as Cypress is aware. You can handle this by specifying [{force:true}](https://docs.cypress.io/api/commands/hover#Force-click) on your click command.

For example if you have a _multiple:true_ SelectItem, a clickMask is used to watch for the user clicking outside the SelectItem drop-down. To dismiss the drop-down from a Cypress test, we recommend sending a `{force: true}` click() command to some other element on the page:

```
     cy.getSC(<locator>).click({force: true})
 
```
In this case _`<locator>`_ refers to the target component that we click on the app to dismiss the dropdown. Note that depending on how the application is configured, this click may dismiss the dropdown and prevent the click action from firing for the target that was actually clicked. You can handle this by invoking a second click to mimic the user interaction. For example:
```
     cy.getSC(<locator>).click({force: true}).click()
 
```

**Waiting for Asynchronous application actions**

Because the `getSC()` command uses [AutoTest.waitForElement](../classes/AutoTest.md#classmethod-autotestwaitforelement), which will not resolve until all [outstanding asynchronous system actions have completed](../classes/AutoTest.md#classmethod-autotestissystemdone), it is not usually necessary to write test code that explicitly waits for actions to complete (using `cy.wait()` calls, for example).  
To put it another way: if an action in a test kicks off a SmartClient DataSource operation and the next action is using `getSC()` to interact with another SmartClient component, the test will automatically wait for the asynchronous operation from the first action to complete before proceeding with the second action.

This alone may not be sufficient to handle every asynchronous behavior in an application. In some cases you may want to explicitly wait for the SmartClient framework to complete some action without having a subsequent `getSC()` call in your test. The [AutoTest.waitForSystemDone](../classes/AutoTest.md#classmethod-autotestwaitforsystemdone) method can be used to handle this. The `commands.js` sample file includes a custom command `"waitForSCDone"` which wraps this method in a Cypress command.

To explicitly wait for all asynchronous SmartClient actions to complete, call the method in your test code as follows:

```
  cy.waitForSCDone();
 
```
Additionally you may have asynchronous behaviors that are unrelated to SmartClient interactions, such as network activity that does not go through the SmartClient [RPCManager](../classes/RPCManager.md#class-rpcmanager), asynchronous rendering of third party widgets, etc. In these cases [AutoTest.isSystemDone](../classes/AutoTest.md#classmethod-autotestissystemdone) may return true even though the application is not ready for further input.

The `options` parameter for `getSC()` can be used to change the [waitStyle](../reference.md#attr-elementwaitconfigwaitstyle) passed to [AutoTest.waitForElement](../classes/AutoTest.md#classmethod-autotestwaitforelement). If you request `"element"` rather than `"system"`, instead of relying on [AutoTest.isSystemDone](../classes/AutoTest.md#classmethod-autotestissystemdone), the framework will continue trying to resolve the locator to an element until the command times out. This gives you an easy way to instruct the test case to keep trying to resolve a locator even after [AutoTest.isSystemDone](../classes/AutoTest.md#classmethod-autotestissystemdone) returns true.

Both `waitForSCDone()` and `getSC()` support being passed an explicit timeout on the `options` parameter. This governs how long the commands will wait for system quiescense / for the locator to be resolved. If no explicit timeout was specified, the default wait time for these commands is 30 seconds, but this can be customized by setting `"scCommandTimeout"` in your Cypress config.

Note that as long as `waitStyle` is set to `"system"`, it is very rare for `getSC()` commands to time out as the application will wait for [AutoTest.isSystemDone](../classes/AutoTest.md#classmethod-autotestissystemdone) and then attempt to resolve the locator. If it fails to resolve the locator to an element it will return `null` immediately rather than continue attempting to resolve the locator until the command times out.

If `getSC()` or `waitForSCDone()` does time out the Cypress test will fail.

**Logging Timing information for [RPC](../reference.md#object-rpcrequest) and [DataSource](../reference.md#object-dsrequest) transactions**

SmartClient provides a number of helpful APIs which allow developers to intercept slow client-server requests and get timing data, indicating how much time was elapsed in the various processing steps.

Cypress tests can make use of these capabilities to log timing information for slow requests, and optionally cause the test to fail.

The primary APIs for this are as follows:

*   [RPCManager.setTimingDataEnabled](../classes/RPCManager.md#classmethod-rpcmanagersettimingdataenabled) - this method turns on logic to record detailed timing data (client and server side) on every SmartClient RPC transaction
*   [RPCManager.addProcessingCompleteCallback](../classes/RPCManager.md#classmethod-rpcmanageraddprocessingcompletecallback) - this allows you to register a callback function to fire after every SmartClient RPC transaction completes
*   [RPCManager.getTransactionDescription](../classes/RPCManager.md#classmethod-rpcmanagergettransactiondescription) - this method returns a brief description of a transaction
*   [RPCManager.getTimingData](../classes/RPCManager.md#classmethod-rpcmanagergettimingdata) - returns the timing data for a transaction as a [Tree](../classes/Tree.md#class-tree)
*   [RPCManager.getFormattedTimingData](../classes/RPCManager.md#classmethod-rpcmanagergetformattedtimingdata) - this formats the timing data as a string for logging purposes

The sample `commands.js` file includes a command `"enableSC_RPCTimeout"` which makes use of [Event emitters](https://nodejs.org/api/events.html#class-eventemitter) in Cypress to take advantage of these APIs and log timing information for slow requests.

`enableSC_RPCTimeout` should typicaly be called only once, at the beginning of your test. It will remain active as long as the page is loaded. The command takes the following arguments:

*   `logThreshold` Any RPCs whose duration exceeds this threshold will log timing information via a `cy.log()` call.
*   `timeoutThreshold` Any RPCs whose duration exceeds this threshold will cause the test to fail.
*   `options` This parameter in an object where you can set various attributes to configure logging behavior. These include:
    *   `logDetail`: one of `"none"`, `"summary"`, `"detailed"` or `"all"`
    *   `logSuccess`: If true, log a 'success' type notification for RPC transactions that do not exceed the specified timing threshold. This log will not include any explicit timing data
    *   `includeClientTimings`: Should detailed timing for client-processing be included?
    *   `includeServerTimings`: Should detailed timing for server-processing be included?

See the implementation in `commands.js` for more details.

Here's an example of how this might be used in a `.cy.js` file:

```
 // If the turnaround takes more than this many millis, log the timing information
 const LOG_TIMEOUT = 1000;
 // If the turnaround takes longer than this many millis, the test fails
 const FAILURE_TIMEOUT = 5000;
 
 describe('Test Suite', () => { 

     beforeEach(() => {
         cy.visit(<target url>); 
         cy.enableSC_RPCTimeout(LOG_TIMEOUT, FAILURE_TIMEOUT, {logDetail:"detailed"});
     });
   
     it('Perform some test', () => {
         ... // test code goes here
     });

 });
 
```
Note: `enableSC_RPCTimeout()` is effectively "invisible" to the flow of your test unless a transaction is encountered which exceeds the timeoutThreshold. If you want to explicitly wait for all pending actions to complete at any point, including waiting for active RPCRequests to be resolved, you can use the `waitForSCDone` command described above.

**Drag and Drop Interaction**

To achieve this goal, the easiest way is to use a specialized plugin for Cypress, where you only need to run the following command:

```
     npm install --save-dev @4tw/cypress-drag-drop
 
```
Finally, you need to add the following code to the commands.js file:
```
     require("@4tw/cypress-drag-drop");
 
```
This way, you can perform drag and drop interactions by simply running the following command:
```
     cy.get('@source').drag('@target')
 
```
where '@source' is obtained via _cy.get()/getSC(`<locator>`).as('source')_ and '@target' via _cy.get()/getSC(`<locator>`).as('target')._

**Final Note**

In addition to the custom commands and approaches described above, developers can also always use the [cy.window()](https://docs.cypress.io/api/commands/window) command to execute arbitrary JavaScript with access to the application scope.

**Cypress configuration for custom SmartClient commands**

The custom commands shipped in the SmartClient SDK will respect the following settings if present in the Cypress configuration:

*   _scLogCommands_: Boolean - if true each command will be logged via cy.log()
*   _scCommandTimeout_: Number - default timeout for getSC() and waitForSCDone() in ms

---
