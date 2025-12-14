# Spring 4 / Java Compatibility

[← Back to API Index](../reference.md)

---

## KB Topic: Spring 4 / Java Compatibility

### Description
The [Spring](https://spring.io/projects/spring-framework#learn) 4 framework integrated with SmartClient is no longer supported by Spring and is incompatible with [Java](https://www.oracle.com/java/technologies/downloads/) 16+, so you need to either use an older version of Java ([Java 8](https://www.oracle.com/java/technologies/javase/javase8u211-later-archive-downloads.html) or [Java 11 (LTS)](https://www.oracle.com/java/technologies/javase/jdk11-archive-downloads.html)), or not use Spring.

If you absolutely need to use Java 16+, you can remove Spring from the SmartClient server by removing all of the Spring JARs from your WEB-INF/lib server directory:

*   spring-beans-4.3.26.RELEASE.jar
*   spring-core-4.3.26.RELEASE.jar
*   spring-jdbc-4.3.26.RELEASE.jar
*   spring-tx-4.3.26.RELEASE.jar
*   spring-webmvc-4.3.26.RELEASE.jar
*   spring-aop-4.3.26.RELEASE.jar
*   spring-context-4.3.26.RELEASE.jar
*   spring-expression-4.3.26.RELEASE.jar
*   spring-orm-4.3.26.RELEASE.jar
*   spring-web-4.3.26.RELEASE.jar
*   isomorphic\_spring.jar
    
    and then removing the Spring configuration from your WEB-INF/web.xml:
    
    ```
     <!-- standard spring configuration -->
     <context-param>
         <param-name>contextConfigLocation</param-name>
         <param-value>/WEB-INF/applicationContext.xml</param-value>
     </context-param>    
     <listener>
         <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
     </listener>
    ```
    Note that Spring 5, which is compatible with JDK 16+, can be used in your application. You just can't use ${isc.DocUtils.linkForRef('group:springIntegration','SmartClient\\'s built-in Spring support')}, such as the "spring:" DMI target.

### See Also

- [springIntegration](springIntegration.md#kb-topic-integration-with-spring)

---
