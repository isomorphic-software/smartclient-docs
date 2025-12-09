# GraalJS Polyglot API for DMI

[← Back to API Index](../reference.md)

---

## KB Topic: GraalJS Polyglot API for DMI

### Description
#### Using GraalJS Polyglot API from DMI

The [Server Scripting](serverScript.md#kb-topic-server-scripting) documentation describes how to use JavaScript (via GraalJS or Nashorn) through the standard JSR223 ScriptEngine API. This approach is ideal for inline scripts in .ds.xml files and Velocity templates.

For more advanced use cases - such as loading complex JavaScript libraries, maintaining stateful JavaScript contexts across requests, or integrating JavaScript-based processing into your DMI logic - you can use GraalJS's Polyglot API directly. This provides finer control over the JavaScript execution environment.

#### Setup: Adding GraalJS to Your Project

To use GraalJS on a standard Oracle or OpenJDK JVM (not full GraalVM), add these Maven dependencies:

```
     <dependency>
         <groupId>org.graalvm.polyglot</groupId>
         <artifactId>polyglot</artifactId>
         <version>24.1.1</version>
     </dependency>
     <dependency>
         <groupId>org.graalvm.polyglot</groupId>
         <artifactId>js</artifactId>
         <version>24.1.1</version>
         <type>pom</type>
     </dependency>
 
```
Or download the standalone JARs from [https://www.graalvm.org/downloads/](https://www.graalvm.org/downloads/). SmartClient also ships GraalJS libraries in `WEB-INF/lib-graaljs/` which can be unzipped and added to your classpath.

#### Basic DMI Example: Calling JavaScript from Java

Here is a simple DMI class that uses GraalJS to execute JavaScript code:

```
 package com.mycompany.dmi;

 import org.graalvm.polyglot.*;
 import com.isomorphic.datasource.*;
 import java.util.Map;

 public class JavaScriptProcessor {

     // Reusable context for better performance (create once, reuse)
     private static final Engine engine = Engine.create();

     /**
      * DMI method that processes a record using JavaScript logic.
      * Called from a DataSource operationBinding.
      */
     public DSResponse processWithJS(DSRequest dsRequest) throws Exception {

         // Create a context with host access enabled (allows JS to call Java)
         try (Context context = Context.newBuilder("js")
                 .engine(engine)
                 .allowHostAccess(HostAccess.ALL)
                 .allowHostClassLookup(className -> true)
                 .build()) {

             // Get the record data from the request
             Map record = dsRequest.getValues();

             // Make the record available to JavaScript as 'record'
             context.getBindings("js").putMember("record", record);

             // Execute JavaScript that processes the record
             Value result = context.eval("js",
                 "// JavaScript code here\n" +
                 "var processed = {};\n" +
                 "processed.name = record.get('firstName') + ' ' + record.get('lastName');\n" +
                 "processed.nameLength = processed.name.length;\n" +
                 "processed;\n"  // Return the result
             );

             // Convert JavaScript result back to Java Map
             Map processedRecord = result.as(Map.class);

             // Return the processed data
             DSResponse response = new DSResponse();
             response.setData(processedRecord);
             return response;
         }
     }
 }
 
```

#### DataSource Configuration

Configure your DataSource to call this DMI:

```
     <DataSource ID="myDataSource">
         <fields>
             <field name="firstName" type="text"/>
             <field name="lastName" type="text"/>
         </fields>
         <operationBindings>
             <operationBinding operationType="custom" operationId="processJS">
                 <serverObject className="com.mycompany.dmi.JavaScriptProcessor"/>
                 <methodArguments>$dsRequest</methodArguments>
             </operationBinding>
         </operationBindings>
     </DataSource>
 
```

#### Loading External JavaScript Files

For more complex logic, load JavaScript from files:

```
 public class JavaScriptProcessor {

     private static final Engine engine = Engine.create();

     public DSResponse processWithExternalJS(DSRequest dsRequest) throws Exception {

         try (Context context = Context.newBuilder("js")
                 .engine(engine)
                 .allowHostAccess(HostAccess.ALL)
                 .allowHostClassLookup(className -> true)
                 .allowIO(IOAccess.ALL)  // Required to load files
                 .build()) {

             // Load a JavaScript file from the classpath or filesystem
             String scriptPath = "/path/to/my-script.js";
             Source source = Source.newBuilder("js", new File(scriptPath)).build();
             context.eval(source);

             // Call a function defined in the loaded script
             Value processFunc = context.getBindings("js").getMember("processRecord");
             Value result = processFunc.execute(dsRequest.getValues());

             DSResponse response = new DSResponse();
             response.setData(result.as(Map.class));
             return response;
         }
     }
 }
 
```

#### Performance Considerations

*   **Reuse the Engine:** Creating an `Engine` is expensive. Create it once (as a static field) and reuse it across contexts.
*   **Context Pooling:** For high-throughput scenarios, consider pooling `Context` objects rather than creating new ones per request.
*   **Warm-up:** GraalJS compiles JavaScript to optimized machine code over time. Initial calls may be slower than subsequent ones.

#### Security Notes

The example above uses `allowHostAccess(HostAccess.ALL)` which gives JavaScript full access to Java classes. For production use with untrusted scripts, consider:

*   Using `HostAccess.EXPLICIT` and annotating allowed methods with `@HostAccess.Export`
*   Restricting `allowHostClassLookup` to specific packages
*   Disabling `allowIO` if file access is not needed

For the JSR223-based approach that integrates with SmartClient's built-in scripting infrastructure, see [Server Scripting](serverScript.md#kb-topic-server-scripting).

---
