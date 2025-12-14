# Angular Integration

[← Back to API Index](../reference.md)

---

## KB Topic: Angular Integration

### Description
As with [other integrations](integrationIntoExistingApps.md#kb-topic-integrating-into-existing-apps), you can add SmartClient components to your Angular application by providing SmartClient with a DOM element created by Angular (or even the ID of a DOM element before it's been created).

All the same mechanisms for loading the framework apply, although Isomorphic recommends FileLoader's [cache](../classes/FileLoader.md#classmethod-fileloadercache) & [load](../classes/FileLoader.md#classmethod-fileloaderload) functions in most cases, where it's desirable to load the SmartClient runtime in the [background](backgroundDownload.md#kb-topic-background-download).

A simple way to facilitate that ability is to install SmartClient using Isomorphic [npm support](npmjs.md#kb-topic-npmjs-support), providing the location tag to point at a location that will be bundled with your app. The 'assets' directory is a standard location for such things, so from your project's root directory:

```
      npm install smartclient-eval --branch=13.0 --location=src/assets --yes
 
```
Next, use a script tag to load FileLoader itself, and ideally, follow it with a request to cache framework resources. So from perhaps a login.html, registration.html, and/or index.html:
```
     <script>window.isomorphicDir = "./assets/isomorphic/"; </script>
     <script src="./assets/isomorphic/system/modules/ISC_FileLoader.js"></script>
     <script>
       isc.FileLoader.cache();
     </script>
 
```
Now you're ready to build SmartClient components and use them in your Angular components. Here, we have an complete Angular Component, written in TypeScript, that hooks into the Angular Component Lifecycle and calls an imported JavaScript helper function at the appropriate event:
#### list.component.ts
```
 import {Component, AfterViewInit, ViewChild, ElementRef} from '@angular/core';

 import {drawCanvasOnElement} from '@app/_helpers/smartclient-framework';
 import {buildLayout} from './js/listComponent';

 @Component({
     template: `<div #layout style="width:auto; height:250px;"></div>`
 })
 export class ListComponent implements AfterViewInit {

     @ViewChild('layout', {static: true}) layoutElementRef: ElementRef;

     /*
      * When the Angular component creates the '#layout' element in the template,
      * provide it to the drawCanvasOnElement helper function.  Note that we do
      * not implement an ngOnDestroy function here to destroy the layout,
      * since SmartClient while detect the destruction of the nativeElement and in
      * turn destroy the component
      */
     ngAfterViewInit() {
         const ele = this.layoutElementRef.nativeElement;
         drawCanvasOnElement(buildLayout, ele);
     }
 }
 
```
This looks exactly like any other Angular component, but we import a few very simple JavaScript functions that do the heavy lifting.
#### ./js/listComponent.js
```
 export function buildLayout(element) {

   const ds = isc.DataSource.create({
     clientOnly: true,
     fields: [
       {name: 'id', type: 'text', primaryKey: true, canEdit: false, hidden: true},
       {name: 'title', type: 'text', required: true, valueMap: ['Mr', 'Mrs', 'Miss', 'Ms']},
       {name: 'firstName', type: 'text', required: true},
       {name: 'lastName', type: 'text', required: true},
       {name: 'email', type: 'text', required: true,
         validators: [
           {type: 'regexp', expression: '^([a-zA-Z0-9_.\\-+])+@(([a-zA-Z0-9\\-])+\\.)+[a-zA-Z0-9]{2,4}$'}
         ]
       },
       {name: 'role', type: 'text', required: true, valueMap: ['User', 'Admin']}
     ],
     cacheData: [{
       id: 1,
       title: 'Mr',
       firstName: 'Joe',
       lastName: 'Bloggs',
       email: 'joe@bloggs.com',
       role: 'User',
       password: 'joe123'
     }]
   });

   const grid = isc.ListGrid.create({
     dataSource: ds,
     autoFetchData: true,
     canEdit: true,
     canRemoveRecords: true
   });

   const button = isc.Button.create({
     title: 'Add User',
     autoFit: true,
     click: function() {
       grid.startEditingNew();
       return this.Super('click', arguments);
     }
   });

   /* position the layout on the provided element */
   return isc.VLayout.create({
     autoDraw: true,
     htmlElement: element,
     matchElement: true,
     members: [
       button,
       grid
     ],
     membersMargin: 10
   });
 }
 
```
This just creates a typical SmartClient Layout containing a databound ListGrid and a Button that manipulates the ListGrid, the same as any other SmartClient component creation. Note that when it's drawn, the layout will be placed in the DOM element created by the Angular component thanks to [Canvas.htmlElement](../classes/Canvas.md#attr-canvashtmlelement).

Finally, a little helper `drawCanvasOnElement` function that causes the SmartClient runtime to be loaded if it hasn't already, and provides the given element to the builder function when everything is ready.

#### @app/\_helpers/smartclient-framework.js
```
 /*
  * Load the SmartClient Runtime if it hasn't yet been, positioning a spinner placeholder
  * over the given element until the framework is available.  At that time, provide the
  * element to a 'builder' function, which will use it to create a component at the right place.
  */
 export function drawCanvasOnElement (builder, element) {

     isc.FileLoader.load(() => {
         builder(element);
     }, {target: element});
 }
 
```

---
