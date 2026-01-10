# Server-Side JavaScript CLI

[← Back to API Index](../reference.md)

---

## KB Topic: Server-Side JavaScript CLI

### Description
SmartClient's server-side JavaScript modules can be executed from the command line for standalone processing, batch operations, or embedding in custom applications. This is separate from [Server Scripting](serverScript.md#kb-topic-server-scripting) which runs within the servlet container.

#### Execution Modes

Two command-line execution modes are available:

| Mode | Runtime | Use Case | Java Integration |
|---|---|---|---|
| Node.js | Node.js (v18+) | CLI tools, build scripts, standalone processing | None (pure JavaScript) |
| GraalJS Polyglot | GraalJS via Polyglot Context API | Custom Java applications embedding SmartClient JS | Full (runs inside JVM) |

#### Server Module Files

Server-side execution uses specially prepared module files that exclude browser-dependent code. These modules are located in `isomorphic/system/modules/`:

*   `ISC_Core_Server.js` - Core framework (language extensions, data structures, communications)
*   `ISC_DataBinding_Server.js` - DataSource, RPCManager, and data binding logic
*   `ISC_AI_Server.js` - AI module including AI integration classes

#### Runtime Detection

Code can detect which runtime is active using [Browser](../classes/Browser.md#class-browser) flags:

```
 if (isc.Browser.isNode) {
     // Running in Node.js
 } else if (isc.Browser.isPolyglot) {
     // Running in GraalJS Polyglot Context API
 } else if (isc.Browser.isGraalJS) {
     // Running in GraalJS JSR-223 (ScriptEngine)
 }

 // Unified check for any server-side JS environment
 if (isc.Browser.isServerJS) {
     // Running server-side (any of the above)
 }
 
```

#### GraalJS Integration

For Java applications embedding SmartClient JavaScript, two approaches are available:

*   **Polyglot Context API** - Provides finest control over the JavaScript execution environment. See [graalPolyglotDMI](graalPolyglotDMI.md#kb-topic-graaljs-polyglot-api-for-dmi) for detailed examples, required JARs, and setup instructions.
*   **JSR-223 ScriptEngine** - Standard Java Scripting API; simpler but less flexible. See [serverScript](serverScript.md#kb-topic-server-scripting) for configuration details.

#### JSEngineManager

SmartClient provides `JSEngineManager` for automatic engine detection. It detects available engines and selects the best option:

```
 EngineInfo info = JSEngineManager.detectEngines(getClass().getClassLoader());
 ScriptEngine engine = JSEngineManager.createEngine(getClass().getClassLoader());
 
```

**Engine Selection Priority:**

1.  GraalJS Polyglot mode (preferred - best Java interop and performance)
2.  GraalJS via JSR-223 ScriptEngine
3.  V8 via J2V8 (if available with platform-specific native libraries)
4.  Nashorn (OpenJDK standalone JAR for Java 15+, or Oracle built-in for Java 8-14)

#### Nashorn Compatibility

Scripts written for Oracle Nashorn can run on GraalJS with Nashorn compatibility shims. SmartClient automatically provides shims for common Nashorn constructs:

*   `java.lang.*`, `java.util.*` - Package shortcuts
*   `Java.type()` - Class loading (native to GraalJS)
*   `importClass()`, `importPackage()` - Legacy import functions

See [graalPolyglotDMI](graalPolyglotDMI.md#kb-topic-graaljs-polyglot-api-for-dmi) for using the Polyglot API from DMI within a servlet container, and [serverScript](serverScript.md#kb-topic-server-scripting) for using the JSR-223 ScriptEngine API for declarative scripts in .ds.xml files.

---
