# Server Scripting

[← Back to API Index](../reference.md)

---

## KB Topic: Server Scripting

### Description
SmartClient allows you to embed "scriptlets" directly in your .ds.xml and .app.xml files to take care of simple business logic without having to create a separate file or class to hold the logic.

These scriptlets can be written in any language supported by the Java "JSR 223" standard, including Java itself, as well as languages such as Groovy, JavaScript, Velocity, Python, Ruby, Scala and Clojure.

The primary use cases for server scripts are:

*   DMI scriptlet declared via [DataSource.script](../classes/DataSource.md#attr-datasourcescript). Like DMI logic declared via [ServerObject](../reference_2.md#object-serverobject), DMI scriptlets can be used to add business logic by modifying the DSRequest before it is executed, modifying the default DSResponse, or taking other, unrelated actions.
*   DMI scriplet declared via [OperationBinding.script](../classes/OperationBinding.md#attr-operationbindingscript), same as the above, but `operationBinding` specific and prioritized over the `DataSource.script` if both present.
*   validator scriptlets declared via [Validator.serverCondition](../classes/Validator.md#attr-validatorservercondition). Like a validator declared via [ServerObject](../reference_2.md#object-serverobject), a scriptlet validator defines whether data is valid by running arbitrary logic, then returning true or false.
*   scripted [VisibleMethod](../reference_2.md#object-visiblemethod) as part of [ServerObject.visibleMethods](../classes/ServerObject.md#attr-serverobjectvisiblemethods) declared in an [Application declaration file](applicationDeclaration.md#kb-topic-application-declaration-files).

For example `DataSource.script` below is executed before all DataSource operations adding session ID to the request helping to ensure that users can only read or write to the data they own (you can see this in action [here](https://www.smartclient.com/smartclient-latest/showcase/?id=scriptingUserSpecificData)):
```
 <DataSource ID="scripting_cartItem" ... >
     <script language="groovy">
         String sessionId = session.getId();
 
         if (DataSource.isAdd(dsRequest.getOperationType())) {
             dsRequest.setFieldValue("sessionId", sessionId);
         } else {
             dsRequest.setCriteriaValue("sessionId", sessionId);
         }
 
         return dsRequest.execute();
     </script>
     ...
 </DataSource>
 
```
Note that you can write Java code and execute it as Groovy script right away, so there's basically no learning curve here. Java code works immediately and Groovy-specific shortcuts can be picked up overtime.

Another example below shows [Validator.serverCondition](../classes/Validator.md#attr-validatorservercondition) scriplet checking submitted value against value fetched from different DataSource ensuring it does not exceed it (you can see this in action [here](https://www.smartclient.com/smartclient-latest/showcase/?id=inlineScriptValidation2)):

```
 <field name="quantity" type="integer">
     <validators>
          <validator type="serverCustom">
             <serverCondition language="javascript"><![CDATA[
                 value < dataSources.get("StockItem").fetchById(record.get("itemId")).get("quantity")
             ]]></serverCondition>
             <errorMessage>Not enough in stock</errorMessage>
         </validator>
     </validators>
 </field>
 
```
Note that general principles of [DataSource.operationBindings](../classes/DataSource.md#attr-datasourceoperationbindings) also apply, so you have the complete control over which operations end up being executed via scriplets. For example you can declare an `operationBinding` with no `operationId` to affect the default behavior of an operation. So if all update operations in a DataSource need to do a specific security check, you can just do:
```
 <operationBinding operationType="update">
     <script>
         // add a security check, update related records, etc
     </script>
 </operationBinding>
 
```
Scriptlets are automatically recompiled when you change the .ds.xml file - just reload the page and the SmartClient Server Framework automatically notices the modified DataSource file and uses the new scriptlets. Same applies to the scripts declared in .app.xml files.

Server Scripting is a great way to connect to an existing Java server API. You may have your existing server API and .ds.xml files that contain brief bits of scripts connecting DataSource operations to the existing API and that's it.

**Declaring Scriptlet Language**

You can set the default system-wide language in [server.properties](server_properties.md#kb-topic-serverproperties-file) by setting `script.defaultLanguage`:

```
     script.defaultLangauge: "groovy"
 
```
Alternatively, anywhere a scriptlet is allowed, you can use the "language" attribute to declare the language. For example:
```
    <operationBindings>
       <operationBinding operationType="add">
           <script language="groovy">
              ... Groovy code ...
           </script>
       </operationBinding>
    </operationBindings>
 
```
#### Error Reporting

If your scriptlet crashes, this is reported in the server-side log along with the line number of the crash.

```
      <!-- crash will be reported at line 1 -->
      <script>crash()</script>

      <!-- crash will be reported at line 2 -->
      <script>
          crash()
      </script>
 
```
It's common practice to use a CDATA tag so that XML-special characters such as < do not have to be quoted as &lt;. When doing this, be aware that the line numbering will still start **from the `<script>` tag**, not the CDATA tag. For example:
```
      <!-- crash will be reported at line 3 -->
      <script>
          <![CDATA[ 
             5 < crash()
          ]]>
      </script>

      <!-- crash will be reported at line 2 -->
      <script><![CDATA[ 
           5 < crash()
      ]]></script>
 
```

#### Java Imports

You can import Java libraries by placing a `<scriptImport>` tag immediately before a `<script>` or `<serverCondition>` tag, like so:

```
     <scriptImport>javax.servlet.http.*</scriptImport>
     <script language="groovy">
         String sessionId = session.getId();
         ...
 
```
There is also a system-wide set of default imports:
```
 java.util.*
 jakarta.servlet.http.*
 com.isomorphic.base.Config
 com.isomorphic.util.*
 com.isomorphic.datasource.*
 com.isomorphic.rpc.RPCManager
 
```
You can override these in [server.properties](server_properties.md#kb-topic-serverproperties-file) via the property `script.defaultImports`, which takes a comma- or space-separated list of packages or classes (like the above).

Dynamic languages such as Groovy or JavaScript allow you to place an import inside the script itself as well.

**NOTE:** If you are using Javascript as your scripting language, see the "Javascript" section below, and especially the discussion of GraalVM, for important caveats regarding Java imports

#### Available Languages

The Oracle JDK and JRE [include support for JavaScript scripting via the Nashorn engine](https://docs.oracle.com/javase/10/scripting/java-scripting-api.htm#JSJSG109). Note that Nashorn was removed from Oracle and OpenJDK JVMs as of Java 15. See the "JavaScript" section at the end of this article for details of the options available if you are using Java 15 or later.

For convenience, SmartClient also bundles a .jar providing Groovy support from [http://www.groovy-lang.org/](http://www.groovy-lang.org/), which uses the Apache license. We also include a .jar file providing Java language support (however see below for limitations). This implementation is based on the BSD-licensed Java.net implementation, but enhanced by Isomorphic to work around container-specific classloader issues that arise when running Java language scripting inside a servlet container and trying to reference common objects of the servlet API itself. See [sunNotice](sunNotice.md#kb-topic-suns-java-engine-implementation---notice-and-disclaimer) for licensing information.

There are **many** other languages available, sometimes with multiple implementations, and they are best found via web search. Making use of any available JSR223 language is as straightforward as dropping the applicable JAR file into your project and then using the name under which that language registers itself (from the language's documentation) as the `language` property of your script.

**NOTE:** There is a known problem using SmartClient's built-in Java language scripting with Tomcat version 7.0.53 and newer (including Tomcat 8.x versions). The problem is a classloader issue for which there is no obvious workaround. For this reason, we recommend that you use Groovy if you wish to use Java as a scripting language: to a very large extent, Groovy is a superset of Java, so the great majority of scripted Java source will work unchanged if you just change the language definition from "java" to "groovy". There is no need to learn or use any of the Groovy language features - you are simply using Groovy as an evaluation engine for plain Java language script. Of course, if you want to use "real" Java, that is always available to you through the normal channels of [DMI](../classes/OperationBinding.md#attr-operationbindingserverobject) and [custom datasources](../classes/DataSource.md#attr-datasourceserverconstructor).

A full description of the differences between Groovy and Java is [here](http://groovy-lang.org/differences.html)

#### Standard Headers & Footers

You can define system-wide headers and footers for each language - code that is added before and after scriptlets wherever it is defined, and can set up variables or functions you use often. To define the location of header and footer files, set `script._languageName_.header` and `script._languageName_.footer` in server.properties. For example, these settings:

```
   script.groovy.header: $webRoot/shared/header.groovy
   script.groovy.footer: $webRoot/shared/footer.groovy
 
```
would add the Groovy fragments found in header.groovy and footer.groovy to beginning and end of every scriptlet that declares language="groovy" (or declares no language if the default engine is "groovy").

**NOTE**: most scripting engines are available under several language names. For example, the Nashorn JavaScript engine registers both "javascript" and "ecmascript" as well as a few variations on letter case. When using the "language" attribute on script tags, the exact value supplied is used to look up header and footer files via server.properties. This means a language setting of "javascript" will find different header and footer files from a language of "JavaScript" even though both will execute via Nashorn.

#### Java scriptlets and the default script wrapper

Although it's not usually considered a "scripting language", using the Java language for scriplets has the advantage that developers do not need to understand two languages in order to modify server-side code. However, using Java for scripting presents special challenges, because unlike true scripting languages, in Java a piece of code cannot be compiled unless it forms a valid class definition.

For this reason, by default every Java scriplet has an implicit wrapper added around it which makes it into a class definition of a trivial class with one method, and your scriptlet code forms the body of that method, after a series of local variables have been set up to allow convenient access to context variables. The header and footer files you've defined, if any, appear before and after your scriptlet, still within the method body.

This makes Java viable as a scripting language despite its verbosity - if the actual business logic to be executed consists of just a few lines of Java, your overall scriptlet will be only that long instead of being forced to contain a complete class definition.

The automatic wrapping of Java code can be disabled by setting `script.java.useDefaultScriptWrapper` to false in server.properties. In this case any scriptlet must contain a valid class definition like the below - context variables need to be manually retrieved from the ScriptContext object instead of being automatically available as local variables, and the attribute "evalResult" is used to return data in lieu of using a `return` statement.

```
 class Temp {
     private static ScriptContext ctx;
     public static void setScriptContext(ScriptContext context) {
         ctx = context;
     }
     public static void main(String[] args) {
         String result = "Hello World!";
         ctx.setAttribute("evalResult", result, 
                          ScriptContext.ENGINE_SCOPE);
     }
 }
 
```
All scriptlets must also import javax.script.ScriptContext. For obvious reasons setting `useDefaultScriptWrapper` to false is not recommended.

#### Returning values and JavaScript

Scriptlets written in Java **must** use a `return` statement to return a result from the scriptlet. Scriptlets written in JavaScript **must not** use a `return` as Nashorn will report this as an error - the JavaScript code is not executed in the scope of a function, and only functions can `return`.

Instead, JavaScript scriptlets should simply end with a statement indicating the value they would like to return. For example:

```
     // if used as the last line, the scriptlet 
     // returns the result of dsRequest.execute();
     dsRequest.execute();

     // if you already have the value as a variable,
     // just end with the variable name plus semicolon
     var dsResponse = dsRequest.execute();
     dsResponse;

     // add a line like this to force returning null 
     // instead of the result of the previous line of code
     null;
 
```
Groovy makes the `return` statement optional, and like JavaScript, will take the value of the last statement as the returned value if there is no explicit `return`.

Other languages supported by JSR223 may have other special semantics for returning data - see their documentation for details.

#### Available context variables for scriptlets

Context variables that are available to a scriptlet are explained in the documentation for the particular property where a scriptlet may be declared, for example, [OperationBinding.script](../classes/OperationBinding.md#attr-operationbindingscript) and [Validator.serverCondition](../classes/Validator.md#attr-validatorservercondition).

In most JSR223 languages, context variables are available as ordinary local variables and you can simply refer to them directly in your scriptlet. This includes Java, so long as useDefaultScriptWrapper is left in its default setting (see above).

#### Caching

JSR223 script calls involve an overhead; the exact overhead depends on the language being used, including whether that language requires a compilation step, and the capability of the hardware. Our testing in this area shows a cost of between 10 and 100ms per call, running SmartClient Server on a VM hosted on a capable but not spectacular machine by the standards of early 2020's (AMD Ryzen 7 2700 CPU).

For this reason, SmartClient implements script caching for any JSR223 script language that supports pre-compilation (ie, implements the `javax.script.Compilable` interface). Pre-compiled scripts are cached per-DataSource, so if script performance is important to you, you should ensure you are using dataSource pooling (covered in [this overview](serverDataSourceImplementation.md#kb-topic-notes-on-server-side-datasource-implementations)). DataSource pooling is a good idea anyway, but it is especially important if you need script caching, because without pooling, DataSource instances are created from scratch each time they are needed, so any cached script will only be cached for the life of a server turnaround.

As you would expect, caching makes the second and subsequent calls to a given script significantly quicker. In-house, we test our script support with two JSR223 languages: JavaScript (the Nashorn engine built into the JVM in Java releases up to 14), and Groovy. Switching caching on makes JavaScript calls 5-6 times faster, and Groovy calls 50 or more times faster.

Script caching is on by default. You can switch it off system-wide with the following `server.properties` setting:

```
    scripting.cache.compilable.scripts: false
 
```

#### Relative Performance

Whether caching is on or off, script performance differs from language to language. Our automated tests show that, while JavaScript calls have a small fixed overhead (about 5ms per call, with caching switched on, on the hardware specs mentioned in the previous section), Groovy calls are **much** quicker: when measured with instrumented code using Java's `System.nanoTime()` API, cached Groovy scripts have an average invocation time of around 80 microseconds, or about one twelfth of a millisecond. This tiny overhead is because Groovy is a JVM language that compiles to the same bytecode as the equivalent Java, so we would expect similarly good performance from other JVM languages like [Kotlin](https://kotlinlang.org) or [JRuby](https://www.jruby.org), both of which also have a JSR223 implementation.

For this reason, we recommend using Groovy as a scripting language in cases where the best performance is required, such as "inner-loop" cases like [fieldValueScript](../classes/DataSourceField.md#attr-datasourcefieldfieldvaluescript)s (which are called for every field on which they are defined, for every record in a resultset). However, see the following section on Javascript for important extra information about this.

#### Javascript

In versions of Java up to JDK 14, there is a Javascript implmentation - Nashorn - built into the JVM. This was removed in version 15, but at the same time, OpenJDK made a standalone version of Nashorn available. Since this standalone version works without problems in pre-15 JDKs (ie, it does not clash with the built-in Nashorn), you can install it in your project without issues. However, note that it requires at least JDK 11, which is why we do not ship it as part of the product in this version. You can obtain the standalone Nashorn implementation here: [https://github.com/openjdk/nashorn](https://github.com/openjdk/nashorn)

An alternative to the standalone Nashorn implementation is to switch from the regular Oracle or OpenJDK JVM, to GraalVM, detailed below. And there are other options too: Mozilla Rhino is still maintained and does work with SmartClient's scripting feature (though it is slow and lacking in features compared to Nashorn); non-Oracle JVMs may implement other Javascript engines; and JSR223 is an open standard so there is nothing to stop people from creating their own ScriptEngine implementations based on whichever Javascript engine they favor. From a SmartClient server-scripting perspective, if a script is marked with a `language` of "javascript", "Javascript", JavaScript" or "ecmascript", we try to find an engine registered with any of those short names (ie, if the language is "JavaScript" but there is no ScriptEngine registered with that short name, we will also try "javascript", "Javascript" and "ecmascript" before giving up).

#### GraalVM
GraalVM is Oracle's "polyglot" VM, which has support for Javascript as a first-class language. You can use GraalVM instead of a regular JVM (the JVM core of it is OpenJDK), and access its Javascript support through a JSR223 interface (there are more direct ways to use Javascript in GraalVM, but this is how you use it with SmartClient's scripting feature). This approach works fine with SmartClient's scripting support, and moreover it is **much** faster than the Nashorn engine. In fact, it has the same tiny call overhead as Groovy - about 80 microseconds in local testing - and so is suitable for use in even the most intensive use cases where we previously have recommended that only Groovy should be used.

However, this very significant reduction in call overhead - from around 15ms per call in Nashorn in our local testing, to under 0.1ms in GraalJS - comes at the cost of reduced flexibility in importing Java classes. By default, SmartClient server scripts written in Javascript automatically import a number of useful or commonly-used Java packages - for example, `java.util.*`, `com.isomorphic.util.*` and `jakarta.servlet.http.*`. This ability to import whole packages is a Mozilla Rhino compatibility feature that is discouraged by the GraalVM team, and if you use it, call overhead times increase dramatically, to the point where there is no performance advantage over Nashorn.

For this reason, we support switching off Mozilla compatibility via a `server.properties` flag:

```
    script.javascript.useMozillaCompat: false
 
```
If you set that flag true, server scripts written in Javascript will:

*   Not load the special `nashorn:mozilla-compat.js` script (which, in GraalVM, has a small beneficial effect on call overhead times by itself)
*   Not use the Rhino-specific `importClass` and `importPackage` APIs. Instead, class-specific imports will be created as aliases using the native Nashorn (and GraalJS) technique, like this:
    ```
         var System = Java.type('java.lang.System')
     
    ```
    Wildcard package imports like `java.lang.*` will simply be skipped. Of course, depending on various factors, skipping wildcard imports may be too inconvenient to be practical in your use case. In that case there is currently no alternative other than to leave `mozillaCompat` set to true and live with the additional call overhead

At the time of writing, GraalVM is available based on OpenJDK 17, 21 and 23, though there are also older versions still downloadable based on JDK 11; if you use the OpenJDK 11 version, or you continue to deploy the standalone nashorn-core library mentioned above, this means you have both Nashorn and GraalJS available. In this case, there are conflicting registrations - a number of variations on "javascript", "js" and "ecmascript" are registered for both Nashorn and GraalVM. In our testing, the GraalVM registrations always win in this situation, but if you want to be absolutely sure of picking up a particular engine, specify lanaguage "nashorn" for Nashorn and "graal.js" for GraalJS. GraalVM homepage: [https://www.graalvm.org/](https://www.graalvm.org/)

It is also possible to implement GraalJS (the Javascript engine from GraalVM) directly on a regular Oracle or OpenJDK JVM (though note, in local testing we saw some but not all of the performance advantages of switching to the full GraalVM - call overheads are reduced to sub-millisecond, but do not get near the ~100 microsecond overhead that we saw with the full GraalVM). Implementing GraalJS on a regular JVM is largely a matter of just adding the applicable JAR files to your application, though by default, references to Java classes and objects will not work. This is a deliberate part of GraalVM's "secure by default" approach. It is possible to relax this by adding various security-related context flags, but SmartClient does not currently support that level of configuration. Instead, you will need to add the command-line flag `-Dpolyglot.js.nashorn-compat=true` to your servlet engine startup; this flag is an alternative way to relax Graal's default security lockdown. For further information, see [https://www.graalvm.org/latest/reference-manual/js/RunOnJDK](https://www.graalvm.org/latest/reference-manual/js/RunOnJDK) and [https://www.graalvm.org/latest/reference-manual/js/NashornMigrationGuide](https://www.graalvm.org/latest/reference-manual/js/NashornMigrationGuide)

### Related

- [DataSource.transformRequestScript](../classes/DataSource.md#attr-datasourcetransformrequestscript)
- [DataSource.transformRawResponseScript](../classes/DataSource.md#attr-datasourcetransformrawresponsescript)
- [DataSource.transformResponseScript](../classes/DataSource.md#attr-datasourcetransformresponsescript)
- [DataSourceField.fieldValueScript](../classes/DataSourceField.md#attr-datasourcefieldfieldvaluescript)
- [OperationBinding.transformRequestScript](../classes/OperationBinding.md#attr-operationbindingtransformrequestscript)
- [OperationBinding.transformRawResponseScript](../classes/OperationBinding.md#attr-operationbindingtransformrawresponsescript)
- [OperationBinding.transformResponseScript](../classes/OperationBinding.md#attr-operationbindingtransformresponsescript)

---
