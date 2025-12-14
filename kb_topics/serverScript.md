# Server Scripting

[← Back to API Index](../reference.md)

---

## KB Topic: Server Scripting

### Description
SmartClient allows you to embed "scriptlets" directly in your .ds.xml file to take care of simple business logic without having to create a separate file or class to hold the logic.

These scriptlets can be written in any language supported by the Java "JSR 223" standard, including Java itself, as well as languages such as Groovy, JavaScript, Velocity, Python, Ruby, Scala and Clojure.

Scriptlets are automatically recompiled when you change the .ds.xml file - just reload the page and the SmartClient Server Framework automatically notices the modified DataSource file and uses the new scriptlets.

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
 javax.servlet.http.*
 com.isomorphic.base.Config
 com.isomorphic.util.*
 com.isomorphic.datasource.*
 com.isomorphic.rpc.RPCManager
 
```
You can override these in [server.properties](server_properties.md#kb-topic-serverproperties-file) via the property `script.defaultImports`, which takes a comma- or space-separated list of packages or classes (like the above).

Dynamic languages such as Groovy or JavaScript allow you to place an import inside the script itself as well.

#### Available Languages

The Oracle JDK and JRE [include support for JavaScript scripting via the Nashorn engine](https://docs.oracle.com/javase/10/scripting/java-scripting-api.htm#JSJSG109).

For convenience, SmartClient also bundles a .jar providing Groovy support from [http://www.groovy-lang.org/](http://www.groovy-lang.org/), which uses the Apache license. We also include a .jar file providing Java language support (however see below for limitations). This implementation is based on the BSD-licensed Java.net implementation, but enhanced by Isomorphic to work around container-specific classloader issues that arise when running Java language scripting inside a servlet container and trying to reference common objects of the servlet API itself. See [sunNotice](sunNotice.md#kb-topic-suns-java-engine-implementation---notice-and-disclaimer) for licensing information.

There are **many** other languages available, sometimes with multiple implementations, and they are best found via web search.

**NOTE:** There is a known problem using SmartClient's built-in Java language scripting with Tomcat version 7.0.53 and newer (including Tomcat 8.x versions). The problem is a classloader issue for which there is no obvious workaround. For this reason, we recommend that you use Groovy if you wish to use Java as a scripting language: to a very large extent, Groovy is a superset of Java, so the great majority of scripted Java source will work unchanged if you just change the language definition from "java" to "groovy". There is no need to learn or use any of the Groovy language features - you are simply using Groovy as an evaluation engine for plain Java language script. Of course, if you want to use "real" Java, that is always available to you through the normal channels of [DMI](../classes/OperationBinding.md#attr-operationbindingserverobject) and [custom datasources](../classes/DataSource.md#attr-datasourceserverconstructor).

A full description of the differences between Groovy and Java is [here](http://groovy-lang.org/differences.html)

#### Standard Headers & Footers

You can define system-wide headers and footers for each language - code that is added before and after scriptlets wherever it is defined, and can set up variables or functions you use often. To define the location of header and footer files, set `script._languageName_.header` and `script._languageName_.footer` in server.properties. For example, these settings:

```
   script.groovy.header: $webRoot/shared/header.groovy
   script.groovy.footer: $webRoot/shared/footer.groovy
 
```
would add the Groovy fragments found in header.groovy and footer.groovy to beginning and end of every scriptlet that declares language="groovy" (or declares no language if the default engine is "groovy").

**NOTE**: most scripting engines are available under several language names. For example, the Rhino JavaScript engine registers both "javascript" and "ecmascript" as well as a few variations on letter case. When using the "language" attribute on script tags, the exact value supplied is used to look up header and footer files via server.properties. This means a language setting of "javascript" will find different header and footer files from a language of "JavaScript" even though both will execute via Rhino.

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

Scriptlets written in Java **must** use a `return` statement to return a result from the scriptlet. Scriptlets written in JavaScript `must not` use a `return` as Rhino will report this as an error - the JavaScript code is not executed in the scope of a function, and only functions can `return`.

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

### Related

- [DataSource.transformRawResponseScript](../classes/DataSource.md#attr-datasourcetransformrawresponsescript)
- [OperationBinding.transformRawResponseScript](../classes/OperationBinding.md#attr-operationbindingtransformrawresponsescript)

---
