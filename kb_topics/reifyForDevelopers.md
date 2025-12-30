# Reify for Developers

[← Back to API Index](../reference.md)

---

## KB Topic: Reify for Developers

### Description
**What is Reify**

Reify is a cloud-based visual application builder in which users can build screens via drag-and-drop, create DataSources from sample data or using wizards, and visually define standard event handlers and multi-step workflows.

You can export a Reify project and continue development in an IDE, because an application built with Reify simply consists of standard Component XML screen definitions, DataSource definitions, and XML event handler and workflow declarations.

In fact, everything that Reify produces is standard, declarative usage of SmartClient, so if you are unfamiliar with a property that a Reify project uses, you can simply look it up in the documentation. We've also put a great deal of effort into ensuring that the XML declarations produced by Reify are concise and self-explanatory. Also, Reify never generates methods or other programmatic code, because there's no way generated programmatic code can ever be clean or clear. By keeping everything declarative, we ensure that everything Reify generates will be easy to understand and extend.

Because it's always possible to export your Reify projects and keep going in an IDE environment, you can start any kind of project with Reify - you don't have to limit your use of Reify to only projects that can be built completely in a visual tool.

**Reify Projects**

An exported Reify project consists of:

1.  a project file (_projectName_.proj.xml) which lists all the screens and DataSources involved in the project
2.  one or more screen files (_screenName_.ui.xml) which have [Component XML](componentXML.md#kb-topic-component-xml) screen definitions
3.  one or more DataSource files (_dataSourceId_.ds.xml) which have [DataSource](../classes/DataSource.md#class-datasource) definitions
4.  a launch .jsp that can start your project right away.

The launch file just contains a `<loadProject>` JSP tag which causes all screens and DataSources to be loaded, and the start screen to be created and drawn.

If all you want to do is deploy your application, all that's necessary is to provide real DataSources to replace the [MockDataSources](../classes/MockDataSource.md#class-mockdatasource) from the Reify project. Because the Reify project places MockDataSources into the special "mock" subdirectory, and DataSources are loaded from the first place they are found, you can replace your MockDataSources by just creating same-named DataSource descriptor files in the [DataSources directory configured for your project](../reference.md#kb-topic-serverproperties-file).

Replacement DataSources must have the same fields and field types. If all you want to do is use a SQL database, you can just:

1.  copy your MockDataSource files to the parent directory
2.  change the outer tag from MockDataSource to `<SQLDataSource>`
3.  use the [adminConsole](adminConsole.md#kb-topic-admin-console) tool to configure a connection to a SQL database, and create tables from the DataSources

.. and your project is now ready to deploy.

**Hybrid development style: mixing Reify projects and hand-coding**

It's easy to use Reify for just the simpler parts of a complex application. For example, the start screen of a complex application might need to be hand-coded, but from there, other screens might be Reify projects or hand-coded, in any mix. Even a hand-coded screen might use a Reify project for a pop-up dialog or wizard. All that's necessary to do this is to load the Reify project into your existing application, and use [RPCManager.createScreen](../classes/RPCManager.md#classmethod-rpcmanagercreatescreen) at the point where you want to introduce Reify-created screens.

Remember that while your Reify project is built and tested as a full-screen application, there's no requirement that it takes over the screen when embedded into a larger application. For example, say you have a hand-coded application where the main screen consists of a [SplitPane](../classes/SplitPane.md#class-splitpane) with a tree on the left, which controls what components are shown in the [detailPane](../classes/SplitPane.md#attr-splitpanedetailpane) on the right. You've loaded a Reify project with a screen called "leadDetails". If you wanted to place a Reify-created screen in _just the right pane_, you can just do this:

```
     mySplitPane.setDetailPane(isc.RPCManager.createScreen("leadDetails"));
 
```
Similarly, imagine you are building a modal window in Reify, such as a wizard or a pop-up dialog. There's no reason for the `Window` component itself to appear in the Reify project, since you can just do this:
```
    var myWindow = isc.Window.create({ 
            items : [ isc.RPCManager.createScreen("reifyScreenName") ],
            ... other properties ...
    });
 
```
Leaving the `Window` component out of the Reify project gives you a little more room to work in the editor, and may be a more natural split in your application. Alternatively, you may want the `Window` in the Reify project so that previewers see something closer to the actual appearance.

Either approach is fine; the key point is that in the Hybrid Development approach, you can place the boundary between your Reify screens and your custom code _anywhere you want_. You can use a Reify screen for the contents of a window, or a tab, or even just the _lower half_ of a tab, if there is a hand-coded component that needs to appear up top. This makes it possible to use Reify for a much greater proportion of your application than may at first be obvious.

**Hybrid Development: adding custom behavior while leaving Reify resources unchanged**

Ideally, leave the resources you import from your Reify project unchanged - that way, you can continue to modify them visually and collaboratively in the Reify tool, and re-import them into your IDE project at any time to pick up changes. Importing an updated Reify project into your IDE project is already simple, but we make it into just one step with special [Maven commands](reifyMaven.md#kb-topic-importing-from-reify).

Note that you can leave Reify resources unchanged, and yet still inject custom logic and custom components into the screen. For example:

1.  you can add event handlers to components in a loaded screen
    ```
     isc.RPCManager.createScreen("screenName", function (screen) {
       var mainGrid = screen.getByLocalID("mainGrid");
       isc.observe(mainGrid, "recordClick", "myApp.loadRelatedImages(record)");
     });
     
    ```
    
    **Note:** `addMethods()` would be another way to install a recordClick behavior, however using `[observe()](../classes/isc.md#staticmethod-iscobserve)` guarantees that you will not overwrite any behavior created in the Reify screen
    
2.  you can swap in custom subclasses for standard components. For example, say you have a custom subclass of `ListGrid` that you want to use everywhere in your application - you can use [CreateScreenSettings.classSubstitutions](../classes/CreateScreenSettings.md#attr-createscreensettingsclasssubstitutions) to do that:
    ```
     isc.RPCManager.createScreen("screenName", {
         classSubstitutions: { "ListGrid" : "MyCustomListGrid" }
     });
     
    ```
    .. alternatively, you can use [CreateScreenSettings.componentSubstitutions](../classes/CreateScreenSettings.md#attr-createscreensettingscomponentsubstitutions) to change the classes used for individual components by the component's ID:
    ```
     isc.RPCManager.createScreen("screenName", {
         componentSubstitutions : { 
             mainGrid : myCustomListGrid
         }
     });
     
    ```
    
3.  you can also inject components into the loaded screen, such as a custom component you've written
    ```
     screen.getByLocalID("mainLayout").addMember(customDisplayComponent);
     
    ```
    

Using the above techniques, you can keep large portions of even a complex application in declarative, Reify-editable files. This makes it much easier to make changes, and collaborate and iterate on possible designs.

**Uploading existing DataSources to Reify**

If you have existing DataSources in hand-coded applications, the quickest way to get them into Reify is to go to the Admin Console and do a CSV export. Export with the radio button set to "Reify format" to ensure both your field names and titles are written into the CSV. Then, within Reify, you can create a new DataSource from the CSV sample data.

If you give the DataSource you create in Reify the same ID as the real DataSource in your project, then when the Reify project is exported and added to an existing hand-coded project, the real DataSource will automatically take the place of the MockDataSource you create in Reify.

Note that Reify does not offer direct upload of existing .ds.xml files, because of the security implications of features such as [`<customSQL>`](#attr-operationbindingcustomsql) and [Server Scripting](serverScript.md#kb-topic-server-scripting). Even aside from security concerns, an existing .ds.xml can have dependencies on other parts of your environment, such as custom [SimpleTypes](../classes/SimpleType.md#class-simpletype), validators that invoke server Java code, or custom tags.

When you export to CSV and create a MockDataSource, Reify automatically determines field types, including distinguishing between "time", "date", and "datetime" fields, as well as between "int" and "float" fields, so the MockDataSource is a perfect stand-in for your real DataSource for design purposes.

Consider trimming the sample data down to 50-100 rows before creating the MockDataSource. Any additional data won't do anything other than slightly slow down the tool, as sample data in Reify is stored inside the .ds.xml file and not in a SQL database or other production-capable data store.

**Providing initial data to Reify screens**

Because the Reify-created portions of your application use the same DataSources as the rest of your application, they already have access to the same data. But what if there is some data that you want to pass to your Reify screen that isn't in a DataSource? For example, perhaps you have a variable that holds the current user name, and the Reify screen has an area that should say "Hello, _user_".

A simple way to handle that case is to simply reach into the Reify screen after you've created it, and populate components with the necessary data. For example:

```
 var myScreen = isc.RPCManager.createScreen("reifyScreenName");
 myScreen.getByLocalID("mainHeaderLabel").setContents("Hello " + userNameVariable);
 
```

However, what if you need to pass along information such as a record that is currently selected, where the Reify screen should load details related to this record? You could programmatically populate the components in the Reify screen with data, but this would mean that the Reify screen would have to be set up to _not_ populate itself with data, which would make it less capable and less useful for reviewers.

The recommended practice here is to _turn the data into a DataSource_. The natural way to build a Reify screen that needs to start with a specific selected record is simply to create a DataSource in the Reify project representing the selected record. You can fulfill the Reify project's need for data by creating a single-record, [clientOnly DataSource](../classes/DataSource.md#attr-datasourceclientonly), which the Reify project can fetch from when it draws.

This can be done with very little code, since you can use [DataSource.inheritsFrom](../classes/DataSource.md#attr-datasourceinheritsfrom) to avoid duplicating field definitions. For example, say you have a Reify screen that needs to load data related to a selected record from the "customer" DataSource. In the Reify project, a MockDataSource called "selectedCustomer" was created to represent the necessary data, and in your custom code, you've got a variable `currentCustomer` that has the Record for the currently selected customer. To make the data available to the Reify project, you can just do this:

```
 isc.DataSource.create({
     ID : "selectedCustomer",
     inheritsFrom : "customer",
     clientOnly:true,
     data : [ currentCustomer ]
 });
 isc.RPCManager.createScreen("reifyScreenName").draw();
 
```
Now the Reify screen can pull the data about the selected "customer" record from the "selectedCustomer" DataSource. If you have multiple Reify screens that need to start with a selected customer, you can standardize on the name "selectedCustomer" and just use `DataSource.setCacheData()` to update the data in the `selectedCustomer` client-only DataSource.

**Detecting that a Reify screen is done**

For many if not most scenarios of embedding Reify screens in a larger application, the user simply completes a task on the Reify-created screen and then navigates away, and may navigate back later and complete more tasks, so nothing special needs to be done. However, sometimes you need to know when a user has completed interacting with a Reify-created screen (such as a wizard), so that the containing application code can take the next step.

There are a few simple techniques for doing this:

*   watch for an event on some object in the Reify screen - for example, wait for the click event on a "Done" button
*   watch for Reify screen to hide itself, if that's what it does on completion. You can do this by using `observe()` on [Canvas.visibilityChanged](../classes/Canvas.md#method-canvasvisibilitychanged)
*   watch for a successful DataSource operation by using `observe()` on [DataSource.dataChanged](../classes/DataSource.md#method-datasourcedatachanged)
*   have the Reify screen write to a `clientOnly` DataSource when it completes. This is the same as the technique described above for providing initial data to a Reify screen, but in reverse. This is also useful if the Reify screen needs to pass data back to the main application, and you'd prefer not to retrieve that data by simply interrogating components in the Reify screen

**Best practices & long-term maintenance**

Once your exported Reify application has been integrated into an IDE-based project with custom code, you will need a process to coordinate on further changes made within Reify to try to avoid, or at least minimize, problems when new versions of the Reify project are pulled into the IDE-based project.

The boundary between the hand-written parts of your application and your Reify-created screens consists of:

1.  DataSources the Reify screen accesses
2.  component IDs that your custom code accesses in order to install event handlers, populate or retrieve data, or insert or replace components

For long-term maintenance, when you have a choice between integration techniques that use DataSources vs those that use component access, use DataSources where possible. DataSources are generally less likely to change, generally easier to reconcile when they do, and discrepancies are easier to detect. In fact, SmartClient provides tooling to detect those changes through Maven goals, Ant tasks, or a Java CLI.

By default, both [Maven](http://github.smartclient.com/isc-maven-plugin/reify-import-mojo.html) and [Ant](http://github.smartclient.com/isc-maven-plugin/apidocs/com/isomorphic/maven/mojo/reify/ImportTask.html) import utilities automatically check for common discrepancies on import, but this step may also be run independently at any time using [reify-validate](http://github.smartclient.com/isc-maven-plugin/reify-validate-mojo.html) goal or [ValidateTask](http://github.smartclient.com/isc-maven-plugin/apidocs/com/isomorphic/maven/mojo/reify/ImportTask.html) tasks, respectively. For Maven, that could be as simple as something like this:

```
 <plugin>
     <groupId>com.isomorphic</groupId>
     <artifactId>isc-maven-plugin</artifactId>
     <version>1.4.3</version>
     <configuration>
       <dataSourcesDir>WEB-INF/ds/classic-models</dataSourcesDir>
     </configuration>
     <dependencies>
        <dependency>
            <groupId>com.isomorphic.extras</groupId>
            <artifactId>isomorphic-m2pluginextras</artifactId>
            <version>\${smartclient.version}</version>
        </dependency>       
   </dependencies>
 </plugin> 
 
 mvn com.isomorphic:isc-maven-plugin:1.4.3:reify-validate
 
```
and for Ant:
```
 <target name="reify-validate" depends="reify-tasklibs">
     
     <taskdef name="reify-validate"
              classname="com.isomorphic.maven.mojo.reify.ValidateTask"
              classpathref="reify.classpath"/>
     <reify-validate datasourcesDir="WEB-INF/ds/classic-models" 
                     smartclientRuntimeDir="\${basedir}/war/isomorphic" />
 </target>   
 
 ant reify-validate
 
```

If, for any reason, one wanted access to the same feature outside of either Ant or Maven environments, a Java class is provided for invocation from command line, scripts, etc. Note that in this case, however, the classpath would need manual setup to include the isomorphic\_m2pluginextras JAR and [its dependencies](javaModuleDependencies.md#kb-topic-java-module-dependencies), and you'll need to provide the full path to your application resources. Assuming the required JARs could all be found at tools/reify/lib, that might look something like this:

```
 java -cp :tools/reify/lib/* com.isomorphic.tools.ReifyDataSourceValidator 
      -r /Users/you/dev/your-application/war/isomorphic
      -d /Users/you/dev/your-application/war/WEB-INF/ds/classic-models
      -m /Users/you/dev/your-application/war/WEB-INF/ds/mock
 
```

---
