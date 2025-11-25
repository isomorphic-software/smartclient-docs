# Loading Optional Modules

[← Back to API Index](../main.md)

---

## KB Topic: Loading Optional Modules

### Description
_See the [SmartClient product page](https://www.smartclient.com/product/) for an overview of which optional modules are available with the various editions of SmartClient._

The SmartClient framework is loaded into the browser by specifying a set of JavaScript files to load. These may be explicitly included via simple ``<script src=...>`` tags, or by using the loadISC facility available on web servers supporting JSP.  
See [loadISCTag](loadISCTag.md#kb-topic-isomorphicloadisc) details on loading the core set of modules.

A SmartClient application may also make use of additional optional modules. These must also be explicitly loaded into your application's bootstrap page.

The table below describes how to load each module, either loading SmartClient through bare SCRIPT calls, or through the loadISC facility.

#### Java (JSP) backend

If you have a Java backend (JSP), invoke <isomorphic:loadISC> with the parameters indicated.

Note that if using [loadISCTag](loadISCTag.md#kb-topic-isomorphicloadisc), multiple optional modules can be included in a single tag - for example

```
     <isomorphic:loadISC includeModules="Charts,Analytics"/>
 
```
Refer to the [taglib documentation topic](../main.md#kb-topic-smartclient-jsp-tags) for usage.

#### Non-Java backend
To load optional modules with a Non-Java backend, add the specified `<SCRIPT>` block(s) at the end of your existing SmartClient `<SCRIPT>` loads in your bootstrap HTML file. Replace "../isomorphic/" with the value of window.isomorphicDir, as appropriate.

#### Installing module resources
Note that some optional modules are only available for specific editions of SmartClient.  
Additionally some optional modules may be purchased separately from the core framework and are made available via a separate download instead of being bundled with the SDK.

**Optional modules and Maven**  
Any optional modules not bundled with the core framework must of course be present in your webserver in order to be loaded.  
Developers using [Maven](mavenSupport.md#kb-topic-maven-support) can include the optional modules via `includeAnalytics`, `includeMessaging` arguments when [installing modules to the maven repository](http://github.smartclient.com/isc-maven-plugin/install-mojo.html). You can then configure configure your project POM to use the new dependency, for example:

```
    ....
    <!-- The SmartClient core -->
    <dependency>
        <groupId>com.isomorphic.smartclient.enterprise</groupId>
        <artifactId>smartclient-enterprise</artifactId>
        <version>${smartclient.version}</version>
    </dependency>
    <!-- Analytics optional module -->
    <dependency>
         <groupId>com.isomorphic.smartclient.enterprise</groupId>
         <artifactId>smartclient-analytics</artifactId>
         <version>${smartclient.version}</version>
    </dependency>
 
```

**Optional server functionality**  
Some optional modules may have server side functionality as well as client side functionality (notably [messaging](messaging.md#kb-topic-real-time-messaging)). In this case, if the module is provided as a separate download it will include any necessary `_.jar_` files. These should be installed into your Java Server in the standard way.

#### Modules

| ChartsRequired for [FacetChart](../classes/FacetChart.md#class-facetchart) and [FusionChart](../classes/FusionChart.md#class-fusionchart). Note that [FacetChart](../classes/FacetChart.md#class-facetchart) also requires the Drawing module to be loaded before this module. Note that [FusionChart](../classes/FusionChart.md#class-fusionchart) requires PluginBridges module be loaded before this module.JSP tag:<isomorphic:loadISC includeModules="Charts"/>HTML tag:`<SCRIPT SRC="../isomorphic/system/modules/ISC_Charts.js">``</SCRIPT>` |
|---|
| AIEnables AI for various components.JSP tag:<isomorphic:loadISC includeModules="AI"/>HTML tag:`<SCRIPT SRC="../isomorphic/system/modules/ISC_AI.js">``</SCRIPT>` |
| AnalyticsRequired for [CubeGrid](../classes/CubeGrid.md#class-cubegrid). Note that if charting is also required, the Charts module should be loaded before this one.JSP tag:<isomorphic:loadISC includeModules="Analytics"/>HTML tag:`<SCRIPT SRC="../isomorphic/system/modules/ISC_Analytics.js">``</SCRIPT>` |
| RealtimeMessaging (see [Messaging](messaging.md#kb-topic-real-time-messaging))JSP tag:<isomorphic:loadISC includeModules="RealtimeMessaging"/>HTML tag:`<SCRIPT SRC="../isomorphic/system/modules/ISC_RealtimeMessaging.js">``</SCRIPT>` |
| PluginBridgesRequired for all [BrowserPlugin](../main.md#class-browserplugin) derivatives (such as [Flashlet](../classes/Flashlet.md#class-flashlet)).JSP tag:<isomorphic:loadISC includeModules="PluginBridges"/>HTML tag:`<SCRIPT SRC="../isomorphic/system/modules/ISC_PluginBridges.js">``</SCRIPT>` |
| HistoryThis module provides synthetic browser history support via the [History](../main.md#object-history) class, and can be used independently. That is, you can use it on pages that don't load any other modules.JSP tag(s):<isomorphic:loadISC includeModules="History"/>HTML tag:`<SCRIPT SRC="../isomorphic/system/modules/ISC_History.js">``</SCRIPT>` |
| FileLoaderPart of the [Network Performance](networkPerformance.md#kb-topic-network-performance) subsystem. Note that unlike other optional modules the FileLoader can be loaded without loading the rest of the SmartClient modules. See [FileLoader](../main_2.md#object-fileloader) for more information on how this special class is used.JSP tag(s):<isomorphic:loadISC cacheOnly="true"/>or<isomorphic:loadISC deferLoad="true"/>HTML tag:`<SCRIPT SRC="../isomorphic/system/modules/ISC_FileLoader.js">``</SCRIPT>` |
| TourThis module contains the [Tour](../classes/Tour.md#class-tour) class, allowing developers to create interactive guided tours of an application's user interface. Note that [Tour](../classes/Tour.md#class-tour) also requires the Drawing module to be loaded before this module.JSP tag:<isomorphic:loadISC includeModules="Tour"/>HTML tag: `<SCRIPT SRC="../isomorphic/system/modules/ISC_Tour.js">``</SCRIPT>` |
| ToolsRequired for [Dashboards & Tools Framework](devTools.md#kb-topic-dashboards--tools-framework-overview). This module should always be included last in a group of optional modules.JSP tag:<isomorphic:loadISC includeModules="Tools"/>HTML tag:`<SCRIPT SRC="../isomorphic/system/modules/ISC_Tools.js">``</SCRIPT>`Note: Using these tools to edit hierarchies of SmartClient components and generate Component XML for them also requires the system schema to be loaded.JSP tag:`<script>`<isomorphic:loadSystemSchema />`</script>`HTML tag:`<SCRIPT SRC="../isomorphic/DataSourceLoader?dataSource=$systemSchema">``</SCRIPT>` |

---
