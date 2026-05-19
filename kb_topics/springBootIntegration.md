# Integration with Spring Boot

[← Back to API Index](../reference.md)

---

## KB Topic: Integration with Spring Boot

### Description
_Note, this section is specifically about integrating with Spring Boot. If you are looking for information about integrating with the traditional Spring framework, read the [Integration with Spring](springIntegration.md#kb-topic-integration-with-spring) article_
#### Overview

[Spring Boot](https://spring.io/projects/spring-boot) is a popular technology for packaging entire webapps - including all config, all dependencies, and even the servlet engine itself - into a single standalone JAR file that can be executed with a simple "`java -jar`" command. SmartClient integrates with Spring Boot, and Isomorphic provides installer scripts that automate the creation of working Spring Boot starter projects. This article describes those scripts and how to use them.

#### Available starter artifacts

Whether you use the creation scripts mentioned below, or set up a project manually, the starter artifact you declare as a dependency in your `pom.xml` determines which server-side capabilities are included. The following starter artifacts are available:

**`smartclient-spring-boot-starter`** — the default starter, and the one used by the Hello World script. Includes SmartClient Server with its full SQL subsystem, making it the right choice for the majority of applications.

**`smartclient-spring-boot-starter-jpa-hibernate`** — extends the default starter with Isomorphic's JPA and Hibernate integration layers (the base starter is a transitive dependency, so you only need to declare this one). Use this if you want to use JPA or Hibernate in addition to SmartClient's built-in SQL subsystem. If you started from the Hello World app and subsequently decide you want JPA or Hibernate support, simply replace `smartclient-spring-boot-starter` with this artifact in your `pom.xml`.

**`smartclient-spring-boot-starter-no-storage`** — the core SmartClient Server with the SQL subsystem removed. Intended only for applications with entirely custom storage requirements, or for pure-client use cases where no server-side data operations are needed.

**`smartclient-spring-boot-starter-showcase`** — extends the default starter with JPA/Hibernate support and the complete set of Showcase example resources. This is what the Hello World script uses when you select the Showcase option. If you later want to strip the Showcase out of an app that was based on this starter, switch your dependency back to `smartclient-spring-boot-starter` , or `smartclient-spring-boot-starter-jpa-hibernate` if you still need JPA/Hibernate

#### Starter projects

Two categories of Spring Boot starter project are available:

**Hello World** — a minimal but complete project that demonstrates the full stack working correctly: a browser page containing a SmartClient [ListGrid](../classes/ListGrid_1.md#class-listgrid) populated with country data read from a SQL database. The installer script prompts for your SmartClient version, build date, license type and project coordinates, installs the required framework artifacts into your local Maven repository via the [isc-maven-plugin](https://github.smartclient.com/isc-maven-plugin), then generates the project, builds it with Maven, and optionally starts it. The generated project is placed as a new subdirectory of whatever directory you run the script from.

**SmartClient Showcase** — the complete Showcase application, containing hundreds of live examples covering data binding, grids, trees, forms, charts, drag-and-drop, AI integration, and much more. Because SmartClient is pure JavaScript, the entire Showcase can be packaged as static resources inside a Maven starter artifact (`smartclient-spring-boot-starter-showcase`); the installer script generates a project based on that starter rather than the default one, so no extra steps are needed beyond selecting it when prompted.

#### Prerequisites

All scripts require the following prerequisites to be in place before you run them. The scripts themselves will check for each of these and report a clear error if anything is missing:

*   **Java 17 or later**. The `java` executable must be on your `PATH`. Downloads are available from [Adoptium](https://adoptium.net/) and other providers
*   **Maven 3.9.2 or later**. The `mvn` executable must be on your `PATH`. Download from [maven.apache.org](https://maven.apache.org/download.cgi)
*   **SmartClient login credentials** in your Maven `settings.xml` file (`~/.m2/settings.xml` on Linux/macOS, `%USERPROFILE%\.m2\settings.xml` on Windows). See item \[2\] on the [Maven plugin configuration page](https://github.smartclient.com/isc-maven-plugin/examples/configuration.html) for the required `settings.xml` format. The scripts check for the presence of a `smartclient-developer` profile and warn if it is not found

#### Why custom installer scripts rather than Spring Initializr?

[Spring Initializr](https://start.spring.io) is the standard mechanism for bootstrapping new Spring Boot projects, but it is limited to artifacts published in the Spring and Maven Central ecosystems. SmartClient artifacts are bundled inside the SDK packages downloadable from the Isomorphic website and are not published to Maven Central; they must first be extracted and installed into your local `.m2` repository using the `isc-maven-plugin` — a step that Initializr has no knowledge of and cannot perform.

Beyond that initial installation step, there are further reasons why Initializr is not the right tool here. A SmartClient Spring Boot project must use Isomorphic's own `smartclient-spring-boot-starter-parent` as its Maven parent POM rather than Spring's `spring-boot-starter-parent`; Initializr always generates a project rooted at Spring's parent and there is no way to change this through the UI.

The installer scripts handle all of these steps end-to-end: they install the framework artifacts via the `isc-maven-plugin`, generate a correctly structured project with the right parent POM and all required configuration files, and build it with Maven in a single automated workflow.

Finally, this dependency on the `isc-maven-plugin` also means that **Maven is the only supported build tool**. We do not currently provide an equivalent plugin for Gradle or any other package manager, so projects must be Maven-based.

#### SmartClient Hello World starter

**Linux / macOS**

Download the script and make it executable, then run it:

```
   curl -O https://smartclient.com/spring-boot/create-smartclient-boot-app.sh
   chmod +x create-smartclient-boot-app.sh
   ./create-smartclient-boot-app.sh
```

**Windows**

Download the script from [https://smartclient.com/spring-boot/create-smartclient-boot-app.bat](https://smartclient.com/spring-boot/create-smartclient-boot-app.bat) and run it from a Command Prompt:

```
   create-smartclient-boot-app.bat
```

**What the script does**

The script will prompt you for the following information, with sensible defaults for each item:

*   **SmartClient version** — e.g. `15.0d`
*   **Build date** — a specific build date in `YYYY-MM-DD` format, or `latest` to use the most recently installed build
*   **License type** — `eval`, `pro`, `power`, or `enterprise`
*   **Project coordinates** — Maven group ID, artifact ID, version, Java package name, and a short project name used for the generated class files

After confirming your choices, the script installs the framework artifacts into your local Maven repository, generates all project files, runs `mvn clean package`, and offers to start the application for you. Once running, open `http://localhost:8080` in a browser to see the result.

**The SmartClient Showcase option**

Because SmartClient is pure JavaScript, the complete Showcase application — hundreds of live examples — can be bundled as static resources inside a Maven artifact. The `smartclient-spring-boot-starter-showcase` artifact does exactly this, and the Hello World script will generate a Showcase application as well as a minimal Hello World if you select `smartclient-spring-boot-starter-showcase` as the starter dependency when prompted. Once running, the Showcase is available at `http://localhost:8080/showcase.html`.

#### The demo database

Both of the starter projects — Hello World and Showcase — use an in-memory [HSQLDB](https://hsqldb.org/) database, populated on startup with Isomorphic's standard set of demo data. This is a deliberate choice: because a Spring Boot application runs from inside a JAR file, it cannot safely assume that a writable filesystem location exists at a predictable path, so a self-contained in-memory database is the most portable default. The trade-off is that any changes you make to the data are not persisted — the database is re-created fresh each time the application starts. Before doing any real development you should switch to a persistent database, as described in the _Project structure for further development_ section below.

#### Project structure for further development
Once the Hello World app is working, you can use it as a base for further development:

*   Remove the `spring.boot.import.demo.database: true` line from `server.properties` and instead add settings to configure access to a real database, as discussed in the [SQL database settings article](sqlSettings.md#kb-topic-sql-database-settings-in-serverproperties). For example, to connect to a local PostgreSQL database:
    ```
       sql.myDatabase.database.type: postgresql
       sql.myDatabase.driver.serverName: localhost
       sql.myDatabase.driver.portNumber: 5432
       sql.myDatabase.driver: org.postgresql.Driver
       sql.myDatabase.driver.databaseName: OrderProcessing
       sql.myDatabase.driver.name: PostgreSQL
       sql.myDatabase.driver.driverName: postgresql
       sql.myDatabase.interface.type: driverManager
       sql.myDatabase.driver.schema: public
       sql.myDatabase.driver.user: myDBUser
       sql.myDatabase.driver.password: myDBUserPassword
       sql.myDatabase.interface.credentialsInURL: true
    
       sql.defaultDatabase: myDatabase
     
    ```
    
*   Add your server-side Java logic under `src/main/java/`
*   Add uncompiled assets that should be looked up from the classpath (configuration files for Hibernate, Log4j, etc.) under `src/main/resources/` — that directory becomes the classpath root at runtime
*   Add your client-side assets under `src/main/resources/static/` — Spring Boot treats that directory specially, presenting it as the web root to the client side of your webapp. This is also the place to put non-compiled server-side assets that should be looked up from the webroot, such as `.ds.xml` files in a `shared/ds/` subdirectory. Ordinarily Spring Boot does not make the `static/` directory visible from the server side, but SmartClient adds this functionality because it is needed in order to maintain compatibility with regular, non-Boot SmartClient application structure

#### Spring Boot and SmartClient skins
In a Spring Boot app, the framework `skins/` directory - from which SmartClient reads all the CSS and media assets required to implement a skin (aka theme) such as Tahoe or Shiva - is by default hidden away in a nested JAR inside the app's fat JAR. We can still read skin assets in this scenario as long as we know the file name we want (which we usually do), but there is no reliable way to iterate over a directory's contents to discover the names of files. This means that SmartClient's [Skin Editor](skinEditor.md#kb-topic-skin-editor) - which tries to query the skins directory for a list of existing skins - does not work out of the box. To make it work, you must move the `skins/` directory out of the framework JAR and into a real filesystem location, and then change the `skinsDir` property in your `server.properties` file to point at the new location.

#### JPA and Hibernate

Because Spring Boot assets from starters end up bundled inside nested JAR files, we decided not to include default config files for JPA and Hibernate with `smartclient-spring-boot-starter-jpa-hibernate`, to avoid hidden, almost secret, settings that it may not be clear how to override. So before you can use one of these storage options you will need to provide config:

*   For Hibernate, provide a `hibernate.cfg.xml` file on the classpath (ie, in `src/main/resources/`). You can configure this however you like, but a minimal config that obtains database connections from the SQL [defaultDatabase](dbConfigTool.md#kb-topic-database-configuration) - which is the default approach we take with the regular, non-Spring Boot SDK, and also with the Spring Boot Showcase - would look similar to this:
    ```
       <?xml version='1.0' encoding='utf-8'?>
       <!DOCTYPE hibernate-configuration PUBLIC
            "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
            "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">
    
       <hibernate-configuration>
         <session-factory>
            <property name="connection.datasource">isomorphic/jdbc/defaultDatabase</property>
         </session-factory>
       </hibernate-configuration>
     
    ```
    
*   For JPA, provide a `persistence.xml` config file in a `META-INF` subdirectory off the classpath root (so, `src/main/resources/META-INF/persistence.xml`). Again, you can configure JPA however you like, but a minimal start point uses Hibernate as the ORM provider and the default SQL database as the connection source:
    ```
       <?xml version="1.0" encoding="UTF-8"?>
       <persistence xmlns="https://jakarta.ee/xml/ns/persistence"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                 xsi:schemaLocation="https://jakarta.ee/xml/ns/persistence/persistence_3_0.xsd"
                 version="3.0">
         <persistence-unit name="ds" transaction-type="RESOURCE_LOCAL">
           <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
           <class>com.mycompany.SomeJPABean</class>
           <!-- Additional bean mappings -->
           <properties>
             <property name="hibernate.connection.datasource" value="isomorphic/jdbc/defaultDatabase"/>
           </properties>
         </persistence-unit>
       </persistence>
     
    ```
    

#### The SmartClient servlets

SmartClient ships with a number of [servlets](servletDetails.md#kb-topic-the-core-and-optional-smartclient-servlets) providing server-side functionality. By default, the following servlets are mapped and available to your application, at the same URL as with the regular non-Boot framework

*   **IDACall** at `/isomorphic/IDACall/*`
*   **RESTHandler** at `/isomorphic/RESTHandler/*`
*   **HttpProxy** at `/isomorphic/HttpProxy`
*   **DataSourceLoader** at `/isomorphic/DataSourceLoader`
*   **ScreenLoaderServlet** at `/isomorphic/ScreenLoader`
*   **ProjectLoaderServlet** at `/isomorphic/ProjectLoader`

Additionally, the **FileDownload** servlet is mapped to the same URLs as in the regular, non-Boot framework, to provide compression and caching for framework code and skin assets. The `Init` servlet is not used; initialization logic is called from a Spring Boot Component, `SmartClientSpringBootServletContextInitializer`

**Removing and Customizing servlet mappings**

Changing SmartClient's default servlet mappings is a fairly common requirement

*   You may wish to remove an unused mapping - for example, if you have no intention of supporting REST requests, there is no need for `RESTHandler`
*   You may wish to override one of the SmartClient servlets with your own subclass - for example, customers sometimes use their own `IDACall` subclass to add things like custom request logging

However, Spring Boot places all configuration in code, so changing a framework servlet mapping is not just a case of changing a `web.xml` entry as it would be in a regular servlet container environment. Instead, you must do one of the following:

**To remove a framework servlet mapping:** Set the applicable property or properties from the list below to false in your Spring Boot `application.properties` or `application.yml` file:

*   smartclient.idacall-servlet.enabled - note, `IDACall` provides access to the SmartClient server framework and is thus required in any meaningful application that uses the server framework, unless you are accessing it purely via REST
*   smartclient.resthandler-servlet.enabled - if you do not need REST support
*   smartclient.datasourceloader-servlet.enabled - if you do not want to load DataSource definitions from the server (note, you nearly always DO want to load dataSources from the server; do not switch this servlet off unless you have a good reason)
*   smartclient.projectloader-servlet.enabled - if you do not need support for loading [Reify projects](#class-projects) into your application
*   smartclient.screenloader-servlet.enabled - if you do not need support for loading Reify screens into your application
*   smartclient.httpproxy-servlet.enabled - if you do not need [HTTP proxy support](../classes/RPCManager.md#classmethod-rpcmanagersendproxied)
*   smartclient.filedownload-servlet.enabled - if you do not want to use SmartClient's built-in support for serving framework assets compressed and with caching headers

**To customize a framework servlet mapping:** SmartClient's Spring Boot servlet configuration looks for Spring Beans with special names; if any of those beans exist, it will not map the corresponding base servlet. For example, to customize `IDACall`, create your own implementation (probably by extending the Isomorphic version), then create a Spring Bean to represent it and map it with a ServletRegistrationBean, like this:
```
   @Bean(name = "CustomIDACallServlet")
   public ServletRegistrationBean<MySuperIDACallSubclass> CustomIDACallServlet() {
      return new ServletRegistrationBean<>(new MySuperIDACallSubclass(), "/isomorphic/IDACall/*");
   }
 
```
The "special names" to use for your custom bean(s) to inhibit mapping for the base servlet(s) follow a predictable and fairly obvious pattern, and are as follows:

| Base servlet | Custom Spring Bean name |
|---|---|
| IDACall | CustomIDACallServlet |
| RESTHandler | CustomRESTHandlerServlet |
| DataSourceLoader | CustomDataSourceLoaderServlet |
| ProjectLoaderServlet | CustomProjectLoaderServlet |
| ScreenLoaderServlet | CustomScreenLoaderServlet |
| HttpProxy | CustomHttpProxyServlet |
| FileDownload | CustomFileDownloadServlet |

---
