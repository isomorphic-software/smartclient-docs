# Integrating Pre-Existing SmartClient Apps with React

[← Back to API Index](../reference.md)

---

## KB Topic: Integrating Pre-Existing SmartClient Apps with React

### Description
_**See [NPMJS](npmjs.md#kb-topic-npmjs-support) for how to install SmartClient in a React app, and [reactSupport](reactSupport.md#kb-topic-using-smartclient-with-react) if you are building a new application using SmartClient and React.**_

If you have a pre-existing, already-built SmartClient application, and you want to integrate it into a pre-existing, already-built React application, the fastest way is to import the ExternalPane class defined by SmartClient's React support, and use it to create your top-level widget by overriding the `buildPane()` method of ExternalPane with JS returning a new instance of your SmartClient UI.

For example:

```
 import React    from 'react';
 import ReactDOM from 'react-dom';
 import 'smartclient-eval/release';
 import 'smartclient-eval/skins/Tahoe';

 import { ExternalPane } from 'smartclient-eval/react';

 import '/MyGrid.js'; // load the SmartClient UI

 class MyPane extends ExternalPane {
     buildPane() {
         return isc.MyGrid.create({
             width: 500, height: 300,
             bodyProperties: {
                 backgroundColor: "#FFFFAA"
             }
         });
     }
  }

 ReactDOM.render(
     <MyPane/>,
     document.getElementById("targetElement")
 );
```
where `MyGrid.js` in this case contains the SmartClient UI classes:
```
 isc.defineClass("MyGrid", isc.ListGrid).addProperties({
     emptyMessage: "No commands have been loaded",

     defaultFields: [{
         name: "command", title: "Command"
     }, {
         name: "argument 1", title: "Argument 1"
     }, {
         name: "argument 2", title: "Argument 2"
     }]
 });
 
```
This will render the SmartClient UI you create into the DOM element in your React App with id `targetElement`

### See Also

- [reactSupport](reactSupport.md#kb-topic-using-smartclient-with-react)

---
