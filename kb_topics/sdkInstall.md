# Deploying the SmartClient SDK

[← Back to API Index](../main.md)

---

## KB Topic: Deploying the SmartClient SDK

### Description
Isomorphic currently recommends leveraging the [support for Maven](mavenSupport.md#kb-topic-maven-support), for those who are comfortable with it, as it dramatically simplifies initial installs, acquiring patched builds, and upgrading to new versions. Those not using Java might also consider using the built-in support for [Node Package Manager](npmjs.md#kb-topic-npmjs-support).

For those unable or unwilling to do so, however, this overview serves as a how-to for installing SmartClient into your web application. Evaluators are urged to use the SmartClient SDK with the embedded tomcat servlet engine during evaluation rather than pursue installation into an existing web application up front, however, reading this document and the related [server\\n integration](clientServerIntegration.md#kb-topic-client-server-integration) materials is recommended to get an overview.

SmartClient has two pieces - the client components that run in the browser and the server components that run in a J2SE-compatible container. You don't need to use a Java back-end to use SmartClient, but the SDK comes with some examples that assume the presence of the Java back-end and, for some examples, a SQL Database. If you will be using SmartClient with a Java back-end, see below for the list of J2SE application servers supported by the Java implementation of the SmartClient server.

The SDK contains two top-level directories: `smartclientSDK` and `smartclientRuntime`. The `smartclientSDK` directory contains the embedded servlet engine, embedded database, examples, and documentation. The `smartclientRuntime` directory contains just the client and server components of the SmartClient product - use the contents of this directory when deploying SmartClient into your application environment.

**Client integration**

To install the client-side portion of SmartClient, simply copy the `isomorphic` directory from the smartclientRuntime webroot to the webroot of your application. Having done this you can use SmartClient components on your pages regardless of the technologies used on your back-end and you can bind to server-side componentry backed by arbitrary technology - see the _Data Integration_ section of the [clientServerIntegration](clientServerIntegration.md#kb-topic-client-server-integration) section for more information.

**Server integration**

Note: Some of the instructions below ask you to copy files into the WEB-INF/classes folder. If you're using an IDE such as Eclipse that attempts to manage the WEB-INF/classes folder, we recommend that you copy these files to the src/ directory of your project (next to the top-level folder for your java namespace) such that your IDE auto-deploys them to the WEB-INF/classes folder. We have seen cases of tools like Eclipse periodically deleting files that are checked into to WEB-INF/classes directly.

*   Copy all files from the WEB-INF/lib directory of the smartclientRuntime to your WEB-INF/lib. The set of libs in the smartclientRuntime/WEB-INF/lib folder is a minimal set; smartclient**SDK**/WEB-INF/lib contains all other .jars you might need, including third-party libraries bundled for convenience. See [Java Module Dependencies](javaModuleDependencies.md#kb-topic-java-module-dependencies) for details of the .JAR files that comprise the SmartClient Server, and their dependencies on various third-party libraries. Generally, if there are conflicts with the versions of third-party libraries you want to use, you can use the versions you want - SmartClient has minimal dependencies on these libraries.
*   Copy the WEB-INF/classes/log4j.isc.config.xml from the smartclientRuntime to your WEB-INF/classes directory. This file contains the SmartClient server log configuration. See [serverLogging](serverLogging.md#kb-topic-server-logging) for information on server-side logging and how to configure it.
*   Copy the [WEB-INF/classes/server.properties](server_properties.md#kb-topic-serverproperties-file) from the smartclientRuntime to your WEB-INF/classes directory. This file contains settings for basic file locations such the location of webroot, the SmartClient SQL engine and DMI. The version under smartclientRuntime has a basic, secure configuration. See the version of [server.properties](server_properties.md#kb-topic-serverproperties-file) under the smartclientSDK directory for sample SQL and other settings.
*   Merge portions of the WEB-INF/web.xml into your application's web.xml; there are mandatory and optional servlets and filters to consider - see below.
*   **Power and Enterprise Editions only**. Copy the shared/ds/batchUpload.ds.xml file to the same location in your target webapp directory. This file is a utility DataSource that is used to provide the initial upload functionality of the [BatchUploader](../classes/BatchUploader.md#class-batchuploader) component - strictly speaking, you only need to perform this step if you intend to use that component.

See [Core and Optional SmartClient servlets](servletDetails.md#kb-topic-the-core-and-optional-smartclient-servlets) for details of additional changes you may need to make to your applications `web.xml` file. See [Java Module Dependencies](javaModuleDependencies.md#kb-topic-java-module-dependencies) for details of the .JAR files that comprise the SmartClient Server, and their dependencies on various third-party libraries.

**Multiple Applications / WARs**

To integrate the server portion of SmartClient, you need to follow the steps below for each application (WAR) that uses SmartClient. Note that, if installing into an environment that uses multiple WARs, installation of SmartClient JARs into a directory shared by multiple applications is not supported. Installation of a separate WAR with client-side SmartClient modules for maintaining cache coherence across applications using the same version of ISC is supported - contact Isomorphic support for more details on how to set that up.

**Troubleshooting**

This section covers some common problems with possible solutions. You may also need to refer to the documentation for your specific application server, web server, or database. If you experience any problems installing and configuring SmartClient in your environment, please post on the [SmartClient forums](http://forums.smartclient.com/) for assistance.

| Problem | Possible Causes | Solution |
|---|---|---|
| Browser displays a generic "page cannot be displayed" or "unable to locate the server" message. | Servlet engine not started. | Start your application server. |
| Missing/incorrect port for servlet engine in URL. | Check the startup messages, logs, or documentation for the servlet engine to determine what port it is using. |
| Host name is incorrect. | Check whether other pages on the host can be accessed. Try the base URL http://[host name]:[port number] to see whether the servlet engine or webserver is functioning. |
| Browser displays a 404 or other page/file not found error. | Incorrect URL. | Check for errors in the URL, including capitalization. |
| ClassNotFound or other Java Exceptions in the server log. | Missing JAR files | Verify every required .jar has been copied into the WEB-INF/lib directory of your deployment. Use [these docs](javaModuleDependencies.md#kb-topic-java-module-dependencies) to double-check. If in doubt, copy every available .jar, verify this is working, then trim off .jars you are definitely not using. |
| "isc" is not defined JS error | Incorrect URLs to SmartClient modules | Use View Source to look at SCRIPT includes (e.g. for ISC_Core.js), try those URLs directly in the browser to verify the files are correctly deployed |

**Caching Considerations**

When upgrading from one SmartClient release to the next, you want to make sure that the user picks up the new version on next access, but you also want to keep the ISC modules cacheable so they're not refetched on every access.

SmartClient deals with this problem by appending a version string as a query parameter to each module load directive. This is done by the <isomorphic:loadISC> and <isomorphic:loadModules> tags automatically. As long as you make sure that the file that contains these tags is non-cacheable, you will get the desired behavior.

**Supported J2SE/J2EE Containers**

Below is the list of J2SE/J2EE containers that have been tested to be compatible with this version of SmartClient. Installation in these containers is supported for deployment by Isomorphic. If your application server is not on this list, please contact us at the [SmartClient forums](http://forums.smartclient.com) to see if we can support your deployment. In general, the Java portion of ISC should work on servlet containers that comply with servlet specification version 2.3 and up and utilize a JVM no older than version 1.8. Older, currently supported versions require Java 1.6, but support for even older JVMs may be possible via special [contract with Isomorphic](https://www.smartclient.com/services/index.jsp#consulting).

Supported J2SE/J2EE Containers:

|  | Apache Tomcat ${Apache_Tomcat_versions} |  |
|---|---|---|
|  | Apache Geronimo ${Apache_Geronimo_versions} |  |
|  | Apache TomEE ${Apache_TomEE_versions} |  |
|  | Oracle WebLogic ${Oracle_WebLogic_versions} |  |
|  | Caucho Resin ${Caucho_Resin_versions} |  |
|  | IBM WebSphere ${IBM_WebSphere_versions} |  |
|  | IBM WebSphere Community Edition ${IBM_WebSphere_Community_Edition_versions} |  |
|  | JBoss ${JBoss_versions} |  |
|  | WildFly ${WildFly_versions} |  |
|  | Mortbay Jetty ${Mortbay_Jetty_versions} |  |
|  | Glassfish ${Glassfish_versions} |  |

---
