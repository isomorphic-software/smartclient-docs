# Background Download

[← Back to API Index](../main.md)

---

## KB Topic: Background Download

### Description
Because all components of the framework are delivered to the browser as [cacheable](caching.md#kb-topic-caching) resources, users of your application typically need download the SmartClient runtime only once (until the cache expires or is purged).

Isomorphic recommends beginning that process as early in the user experience as possible, in a registration or login page for example, so that the runtime has already been downloaded by the time they reach your application and there is no perceived wait while the user loads the rich user interface.

Alternative implementations of this approach include loading the framework using `<script>` tags with the `defer` attribute, the [loadISC](loadISCTag.md#kb-topic-isomorphicloadisc) JSP tag with its `cacheOnly` attribute, or the [FileLoader.cache](../classes/FileLoader.md#classmethod-fileloadercache) JavaScript function.

To use FileLoader, add its script tag to your html and follow it with a request to cache framework resources. So from perhaps a login.html, registration.html, and/or index.html:

```
     <script>window.isomorphicDir = "./isomorphic/"; </script>
     <script src="./isomorphic/system/modules/ISC_FileLoader.js"></script>
     <script>
       isc.FileLoader.cache();
     </script>
 
```
Whenever your application is ready to draw the first component, you can load the previously cached framework and draw the component in its callback:
```
     isc.FileLoader.load(function() {
       isc.Label.create({contents: 'Hello World!'});
     });
 
```
You can even cause the component to be drawn in some existing DOM element, as outlined in the [Integration into Existing Applications](integrationIntoExistingApps.md#kb-topic-integrating-into-existing-apps) documentation topic:
```
     isc.FileLoader.load(function() {
       isc.Label.create({contents: 'Hello World!', htmlElement: 'greeting', matchElement: true});
     });
 
```
#### Loading DataSources
When you're loading the framework in the background, you'll also need to load your DataSources in the background, using the [DataSource.load](../classes/DataSource.md#classmethod-datasourceload) function, typically in the callback:
```
     isc.FileLoader.load(function() {
         isc.DataSource.load('User', function() {
             isc.ListGrid.create({dataSource: 'User'});
         });
     });
 
```

---
