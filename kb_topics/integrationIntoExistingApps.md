# Integrating into Existing Apps

[← Back to API Index](../main.md)

---

## KB Topic: Integrating into Existing Apps

### Description
SmartClient can be easily integrated into any existing web application, regardless of the technology used, because it's careful not to interfere with the functionality or appearance of content created by other frameworks.

SmartClient components can be adapted to your existing application's layout by using the [Canvas.htmlElement](../classes/Canvas.md#attr-canvashtmlelement) and [Canvas.matchElement](../classes/Canvas.md#attr-canvasmatchelement) APIs, for example, allowing them to be placed appropriately and respond automatically to DOM-level create, destroy, and resize events.

Using this strategy, replacing another table or list component with a SmartClient ListGrid can be as simple as [loading](backgroundDownload.md#kb-topic-background-download) the framework and creating the ListGrid:

```
   isc.FileLoader.load(function() {
       isc.DataSource.load('User', function() {
           isc.ListGrid.create({dataSource: 'User', htmlElement: 'userGrid', matchElement: true});
       });
   });
 
```
A screen or even an entire project could be imported from [Reify](reifyForDevelopers.md#kb-topic-reify-for-developers) and added in a similar fashion:
```
   const callback = (project, projects, rpcResponse) => {
       const screen = project.createStartScreen({
         htmlElement: 'userScreen'
       });
   };
   isc.FileLoader.load(function() {
     isc.Reify.loadProject('your-proj', callback, {userName: 'you', password: 'secret'});
   });
 
```
The [Angular](angularIntegration.md#kb-topic-angular-integration) documentation topic illustrates these points with a simple approach to integration of a ListGrid in that environment, but the same concepts apply to any existing web application, including those written in Angular, React, Vue, jQuery, Backbone, Svelte, etc.

---
