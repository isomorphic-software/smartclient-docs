# Server Framework Initialization

[← Back to API Index](../reference.md)

---

## KB Topic: Server Framework Initialization

### Description
The SmartClient Server framework must be initialized from its config files at startup time, before user code invokes _any_ framework functionality. If you are running standalone (ie, outside of a servlet container), you should call the static utility method `ISCInit.go()` early in your bootstrap code (eg, from the top of your `main()` method).

If you are running inside a servlet engine, install the following listener in your web.xml. Ideally this should be the first listener registered in web.xml because part of the init logic exports database connections configured via server.properties via JNDI for consumption by other frameworks (Spring, Hibernate, etc). See also below for other rationale related to Spring.

*   Install `InitListener`, which is a `ServletContextListener`:  
    ```
       <listener>
            <listener-class>com.isomorphic.base.InitListener</listener-class>
        </listener>
    ```
    

#### Interaction with Spring initialization
The Spring framework attempts to initialize itself in similar ways to the SmartClient framework, and similarly it wants its own initialization to be the very first thing that happens. This can cause problems in certain cases. For example, one known problem occurs when you define DataSource instances as Spring beans, and Spring gets to initialize itself first: it attempts to instantiate a instance of the bean, which ultimately calls into our framework code before the framework has been initialized.

The solution to this is to use the `InitListener`, and to ensure that it is declared in your `web.xml` file before the Spring `ContextLoaderListener`. The Servlet 2.3 spec states (SRV.10.3.3):

  _"During Web application execution, listeners are invoked in the order of their registration."_

Therefore, declaring the SmartClient listener before the Spring one ensures that things run in the correct order in Servlet 2.4-compatible containers, and in those Servlet 2.3 containers that enforce the rule of running listeners before initializing filters or servlets.

---
