# Memory Leaks

[← Back to API Index](../reference.md)

---

## KB Topic: Memory Leaks

### Description
Care must be taken to avoid memory leaks in your application:

*   Any [Canvas](../classes/Canvas.md#class-canvas) (including subclasses) that you're done using should be destroy()d to avoid memory leaks. Since [destroy()](../classes/Canvas.md#method-canvasdestroy) is recursive, you only need to call destroy() on the topmost component in any hierarchy of widgets you don't need. This includes [DynamicForm](../classes/DynamicForm.md#class-dynamicform) automatically destroying [FormItem](../classes/FormItem.md#class-formitem)s and [DrawPane](../classes/DrawPane.md#class-drawpane) automatically destroying [DrawItem](../classes/DrawItem.md#class-drawitem)s.
*   Any [ValuesManager](../classes/ValuesManager.md#class-valuesmanager)s that you are done using should be destroy()d to avoid memory leaks, and will never be automatically destroyed as a consequence of destroying any related Canvas.
*   [ResultSet](../classes/ResultSet.md#class-resultset) and [ResultTree](../classes/ResultTree.md#class-resulttree) instances that you **manually** create need to be destroy()d to avoid leaks. ResultSet and ResultTree instances automatically created by [ListGrid](../classes/ListGrid_1.md#class-listgrid)s and [TreeGrid](../classes/TreeGrid.md#class-treegrid)s (see [ListGrid.fetchData](../classes/ListGrid_2.md#method-listgridfetchdata)) do not need to be destroy()d as they are automatically destroyed with the creating ListGrid or TreeGrid.
*   If your application creates an unbounded number of DataSources while it is running (this is very rare), DataSources that are given a [DataSource.ID](../classes/DataSource.md#attr-datasourceid) need to be destroy()d to avoid leaks. Most applications do not need to worry about this, as they create a fixed set of DataSources, and [DataSource.get](../classes/DataSource.md#classmethod-datasourceget) will never cause a leak.
*   Any other kinds of SmartClient objects you create will be garbage collected normally.

#### Testing for memory leaks

Seeing the browser's memory use rise dramatically after a given operation does not demonstrate a memory leak. It's normal for browser memory usage to fluctuate wildly, because the browser will generally not reclaim resources immediately, and in some cases will not reclaim resources until memory is nearly exhausted. Some browsers will also build up pools of resources for later re-use.

The only way to demonstrate a real memory leak is to demonstrate _memory exhaustion_: showing that the browser memory usage rises until all memory is exhausted and errors begin to occur. No other pattern of increasing memory usage - no matter how large - is considered evidence of a leak, because the browser may suddenly reclaim very large amounts of memory after memory usage rises to a certain trigger point. Memory exhaustion is the _only_ way to demonstrate a real memory leak.

Note that all debugging tools must be closed in order to demonstrate memory exhaustion because debugging tools may themselves consume large amounts of memory:

*   On the RPC tab of the SmartClient Developer Console, make sure that "Track RPCs" is **un**checked and then close the SmartClient Developer Console window.
*   If using Chrome's or Safari's developer tools, make sure that the developer tools are closed.
*   If using Firebug, close Firebug and restart Firefox, as Firebug may still be active even though closed.
*   If using Internet Explorer's Developer Tools, close Developer Tools and restart IE, as the Developer Tools may still be active even though closed.

To demonstrate memory exhaustion, you generally need to take whatever operation you suspect of leaking memory and cause it to be repeated thousands or hundreds of thousands of times - generally, by performing the same operation multiple times in a loop, or, for asynchronous operations like [DataSource](../classes/DataSource.md#class-datasource) saves, performing the operation again each time you receive notification of completion (via callbacks).

In Windows, you can speed up the process of demonstrating memory exhaustion by disabling paging of memory to disk, which causes Windows to use the physical memory of the system (RAM) only. To disable paging, go to Advanced System Settings, and in the "Virtual Memory" section of the "Performance" settings, uncheck the "Automatically manage paging file size for all drives" checkbox and select "No paging file" (this process may differ slightly on different versions of Windows). The system will need to be rebooted for these new settings to take effect.

Once paging is disabled, verify that you can still open the browser and load the application you intend to test. There needs to be ample physical memory available for the application to use. A rule of thumb is to have enough available memory for the browser's memory footprint to at least quadruple in size or at least 500 MB, which ever is greater. If the system does not have enough physical memory, one option is to re-enable paging, but limit the maximum size of the page file to 500 MB. Then begin the process of repeating the operation being tested for a memory leak.

If Windows shows a warning about low system memory, you have demonstrated memory exhaustion and therefore a memory leak. If you are working with a minimal, ready-to-run test case, you may have found a framework bug or a browser bug that SmartClient can work around. You should post your minimal test case to the [SmartClient forums](http://forums.smartclient.com/) for analysis by Isomorphic Support.

If you do not have a minimal test case and have simply shown that your application is leaking memory, consider the possible coding errors that could cause memory leaks (explained above), and work toward creating a minimal test case if you suspect a framework or browser bug is the underlying cause.

### See Also

- [Canvas.destroy](../classes/Canvas.md#method-canvasdestroy)
- [DrawItem.destroy](../classes/DrawItem.md#method-drawitemdestroy)
- [Class.destroy](../classes/Class.md#method-classdestroy)
- [ValuesManager](../classes/ValuesManager.md#class-valuesmanager)
- [DataSource.ID](../classes/DataSource.md#attr-datasourceid)

---
