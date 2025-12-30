# Integration with Struts

[← Back to API Index](../reference.md)

---

## KB Topic: Integration with Struts

### Description
#### Please note that Apache Struts is deprecated and will be removed from Smartclient 13.0

**Overview of SmartClient integration with Struts and other popular server-side frameworks.**

Current and upcoming server-side frameworks solve a lot of problems endemic to the past generation of web applications. Piles of JSPs and Servlets have been replaced by MVC and other paradigms that enhance developer productivity. Unfortunately the end-user presentation remains vanilla HTML. SmartClient solves this problem by providing rich databindable components. SmartClient was designed to integrate cleanly with existing server-side frameworks. Because SmartClient components only require an HTML context to render, they can be used with any server-side frameworks that use HTML for presentation.

SmartClient provides a rich UI by doing more work on the client (browser) rather than sending every user action to the server for re-rendering. Instead of doing page transitions to redraw the whole page, SmartClient sends RPC (Remote Procedure Call) requests (or AJAX requests) to the server while the UI allows the user to continue interacting with the system. Current server-side frameworks, on the other hand are typically designed around page transitions - for example in Struts user actions are typically mapped to URLs that dispatch through a central servlet and ultimately return new HTML to be rendered by the browser. The problem with page transitions is that they destroy client-side state and introduce client-server latency (and generally use more bandwidth since HTML is sent over the wire rather than just data) - essentially destroying a large part of the Rich Internet Application (RIA) experience.

Fortunately, there's a way to get the best of both worlds - to leverage the power of your favorite server-side framework and combine it with the SmartClient UI. There are several approaches to integrating SmartClient into an existing framework:

**Plug-replacing HTML components with SmartClient components**

SmartClient components can be instructed to draw at page load time using by specifying `position: "relative"` at construction time. This enables you to replace any chunk of HTML with a SmartClient component - the new component simply inserts its HTML in the page flow during page load. This is the easiest integration option - you get a better UI with minimal work. The downside is that you don't get the full power of a rich client because most user actions will still trigger a page transition.

**Eliminating page transitions**

Most SmartClient components can accept new data (or even dynamically pre-fetch and expire data) without needing to be recreated. For example - let's say you want to draw a grid on a page. In a traditional server-side-rendered application the server would generate all of the html with "next 20 records" and "previous 20 records" buttons. When the user wants to see the next set of data, he clicks one of the buttons and the server replaces the entire page with a new grid that contains the next/previous 20 records. In a SmartClient application, you would create a databound ListGrid. Based on its configuration this grid will fetch the first N (say 20) records and display a scrollbar for the user to scroll through the data. When the user scrolls off the last cached record the ListGrid automatically sends an RPC to the server asking for the next 20 records. This RPC (fetch) is performed without destroying the page the user is currently looking at - it just happens seamlessly in the background. If the user now scrolls back to the first 20 records - they're already cached in the grid, so no fetch is performed. Of course, in a real world application, it's typical that a page has hundreds of components and in a server-side-only rendering all of them need to be rebuilt by the server and resent to the client when a piece of data in just one needs to be updated. SmartClient components can intelligently update just their data without the need to redraw the whole page.

The plug-replacement strategy listed above gives us a SmartClient component in place of a raw HTML rendering. Now we need to databind that component so that actions like scrolling a grid or validating a form don't cause a page transition. To do this, you need to set up a Struts Action that will handle **all** SmartClient `RPCRequest`s and `DSRequest`s. This is important, as requests need to be sent to the same URL to enable queuing to work. In your Action class, you simply need to invoke `RPCManager.processRequest()` to hook straight into the normal `DSRequest` processing flow.

The SDK contains a simple example of doing form validation without incurring a page transition. These examples also show how to populate e.g. field names using the struts-bean taglib and how to set validation errors using the standard Struts Validation plugin. Point your browser to [/examples/struts/forms](/examples/struts/forms) in the SmartClient SDK to take a look.

---
